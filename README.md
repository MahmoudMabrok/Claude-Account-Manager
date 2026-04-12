# Claude Account Manager

<div align="center">

Manage multiple Claude CLI accounts on the same machine.

ادارة عدة حسابات Claude CLI على نفس الجهاز.

<br>

[English](#english) | [العربية](#العربية)

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

- Simple web UI to add and remove accounts
- Each account gets a dedicated command (`claude-<name>`)
- Login status indicator for each account
- Bilingual interface (Arabic / English)
- Zero interference between accounts

### Requirements

- [Node.js](https://nodejs.org/) (v18+)
- [Claude CLI](https://docs.anthropic.com/en/docs/claude-code) installed globally

### Installation

```bash
git clone https://github.com/noor1yasser9/Claude-Account-Manager.git
cd Claude-Account-Manager
npm install
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

- واجهة ويب بسيطة لإضافة وحذف الحسابات
- كل حساب له أمر خاص (`claude-<name>`)
- مؤشر حالة تسجيل الدخول لكل حساب
- واجهة ثنائية اللغة (عربي / إنجليزي)
- لا تداخل بين الحسابات أبداً

### المتطلبات

- [Node.js](https://nodejs.org/) (v18+)
- [Claude CLI](https://docs.anthropic.com/en/docs/claude-code) مثبّت

### التثبيت

```bash
git clone https://github.com/noor1yasser9/Claude-Account-Manager.git
cd Claude-Account-Manager
npm install
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
