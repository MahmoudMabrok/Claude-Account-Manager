# Claude Account Manager

<div align="center">

Manage multiple Claude CLI accounts on the same machine.

ادارة عدة حسابات Claude CLI على نفس الجهاز.

<br>

[English](#english) | [العربية](#العربية)

<br>

[![Watch Demo](https://img.shields.io/badge/Watch_Demo-Video-c4a35a?style=for-the-badge&logo=youtube)](https://github.com/noor1yasser9/Claude-Account-Manager/releases/download/v1.0.0/demo.mp4)

</div>

---

## English

### The Problem

Claude CLI supports only one active session at a time with no official way to switch between accounts.

### The Solution

A local web app (`localhost:3737`) that creates **isolated commands** for each account using the `CLAUDE_CONFIG_DIR` environment variable. Each account gets its own config directory and a dedicated terminal command.

```
claude-noor  → logs in with Noor's account
claude-work  → logs in with Work account
claude-test  → logs in with Test account
```

No symlinks, no file copying, no session conflicts. Each account is **fully isolated**.

### Features

- Each account gets a dedicated command (`claude-<name>`)
- Account details: user name, email, organization, plan, model
- Per-account model selection (Opus / Sonnet / Haiku)
- Rename, lock/unlock, and color-code accounts
- Export/import accounts as JSON
- Auto-detect PATH issues with one-click fix
- Dark / Light theme
- Bilingual interface (Arabic / English)
- Auto-refresh login status every 30s
- Fully configurable via `.env`

### Requirements

- [Node.js](https://nodejs.org/) (v18+)
- [Claude CLI](https://docs.anthropic.com/en/docs/claude-code) installed globally

### Installation

```bash
git clone https://github.com/noor1yasser9/Claude-Account-Manager.git
cd Claude-Account-Manager
npm install
cp .env.example .env  # optional: customize settings
```

### Usage

```bash
npm start
```

Open **http://localhost:3737** in your browser.

#### Add an Account

1. Enter an account name (e.g. `noor`) in the web UI
2. Click **Add**
3. Run `claude-noor` in your terminal
4. Log in when prompted — the session is saved automatically

#### Use an Account

Just type the command in any terminal:

```bash
claude-noor    # opens Claude with Noor's session
claude-work    # opens Claude with Work's session
```

Each command is independent. You can run multiple accounts simultaneously in different terminal windows.

### Configuration

Copy `.env.example` to `.env` and customize:

| Variable | Description | Default |
|----------|-------------|---------|
| `PORT` | Server port | `3737` |
| `HOST` | Server host | `localhost` |
| `ACCOUNTS_DIR` | Accounts storage path | `~/.claude-accounts` |
| `BIN_DIR` | Commands directory | `/usr/local/bin` (auto-detected) |
| `DEFAULT_LANG` | Default language (`ar` / `en`) | `ar` |
| `DEFAULT_THEME` | Default theme (`dark` / `light`) | `dark` |
| `AUTO_REFRESH_INTERVAL` | Status refresh interval (ms) | `30000` |
| `DEFAULT_MODEL` | Default model for new accounts | _(empty)_ |

### How It Works

```
~/.claude-accounts/
├── noor/          # Noor's isolated config (CLAUDE_CONFIG_DIR)
├── work/          # Work's isolated config
└── accounts.json  # Account registry

/usr/local/bin/
├── claude-noor    # → exec env CLAUDE_CONFIG_DIR=~/.claude-accounts/noor claude "$@"
└── claude-work    # → exec env CLAUDE_CONFIG_DIR=~/.claude-accounts/work claude "$@"
```

The generated scripts are one-liners that set `CLAUDE_CONFIG_DIR` before launching Claude CLI. This is a native environment variable supported by Claude CLI.

---

## العربية

### المشكلة

Claude CLI يدعم جلسة حساب واحد فقط في نفس الوقت، ولا توجد طريقة رسمية للتبديل بين حسابات متعددة.

### الحل

تطبيق ويب محلي (`localhost:3737`) ينشئ **أوامر معزولة** لكل حساب باستخدام متغير البيئة `CLAUDE_CONFIG_DIR`. كل حساب ياخذ مجلد إعدادات خاص فيه وأمر مستقل في الترمنال.

```
claude-noor  ← يدخل بحساب نور
claude-work  ← يدخل بحساب العمل
claude-test  ← يدخل بحساب التجربة
```

بدون symlinks، بدون نسخ ملفات، بدون تعارض جلسات. كل حساب **معزول تماماً**.

### المميزات

- كل حساب له أمر خاص (`claude-<name>`)
- عرض تفاصيل الحساب: اسم المستخدم، الإيميل، المنظمة، الباقة، الموديل
- إعدادات موديل لكل حساب (Opus / Sonnet / Haiku)
- إعادة تسمية، قفل/فتح، وتلوين الحسابات
- تصدير واستيراد الحسابات كـ JSON
- كشف مشاكل الـ PATH تلقائياً مع إصلاح بضغطة واحدة
- وضع داكن / فاتح
- واجهة ثنائية اللغة (عربي / إنجليزي)
- تحديث تلقائي لحالة الدخول كل 30 ثانية
- إعدادات كاملة عبر `.env`

### المتطلبات

- [Node.js](https://nodejs.org/) (v18+)
- [Claude CLI](https://docs.anthropic.com/en/docs/claude-code) مثبّت

### التثبيت

```bash
git clone https://github.com/noor1yasser9/Claude-Account-Manager.git
cd Claude-Account-Manager
npm install
cp .env.example .env  # اختياري: تخصيص الإعدادات
```

### التشغيل

```bash
npm start
```

افتح **http://localhost:3737** في المتصفح.

#### إضافة حساب

1. اكتب اسم الحساب (مثلاً `noor`) في الواجهة
2. اضغط **إضافة**
3. شغّل `claude-noor` في الترمنال
4. سجّل دخول — الجلسة تنحفظ تلقائياً

#### استخدام الحساب

اكتب الأمر في أي ترمنال:

```bash
claude-noor    # يفتح Claude بجلسة نور
claude-work    # يفتح Claude بجلسة العمل
```

كل أمر مستقل. تقدر تشغّل عدة حسابات في نفس الوقت في نوافذ ترمنال مختلفة.

### الإعدادات

انسخ `.env.example` إلى `.env` وعدّل:

| المتغير | الوصف | القيمة الافتراضية |
|---------|-------|------------------|
| `PORT` | بورت السيرفر | `3737` |
| `HOST` | عنوان السيرفر | `localhost` |
| `ACCOUNTS_DIR` | مسار حفظ الحسابات | `~/.claude-accounts` |
| `BIN_DIR` | مسار الأوامر | `/usr/local/bin` (يُكتشف تلقائياً) |
| `DEFAULT_LANG` | اللغة الافتراضية (`ar` / `en`) | `ar` |
| `DEFAULT_THEME` | الثيم الافتراضي (`dark` / `light`) | `dark` |
| `AUTO_REFRESH_INTERVAL` | فترة تحديث الحالة (مللي ثانية) | `30000` |
| `DEFAULT_MODEL` | الموديل الافتراضي للحسابات الجديدة | _(فاضي)_ |

### آلية العمل

```
~/.claude-accounts/
├── noor/          # إعدادات نور المعزولة (CLAUDE_CONFIG_DIR)
├── work/          # إعدادات العمل المعزولة
└── accounts.json  # سجل الحسابات

/usr/local/bin/
├── claude-noor    # → exec env CLAUDE_CONFIG_DIR=~/.claude-accounts/noor claude "$@"
└── claude-work    # → exec env CLAUDE_CONFIG_DIR=~/.claude-accounts/work claude "$@"
```

السكريبتات المولّدة سطر واحد فقط — تضبط `CLAUDE_CONFIG_DIR` قبل تشغيل Claude CLI. هذا متغير بيئة رسمي مدعوم من Claude CLI.

---

## License

MIT
