# OpenCode for Android

Run [OpenCode](https://opencode.ai) — the open source AI coding agent — on your Android phone via Termux and proot-distro.

## Prerequisites

- Android 8+ (recommended)
- At least 4GB RAM
- [Termux](https://f-droid.org/repo/com.termux_118.apk) from F-Droid (**not** the Play Store version — it's outdated)

---

## Step 1: Install Termux

1. Download Termux from [F-Droid](https://f-droid.org/repo/com.termux_118.apk)
2. Install the APK and open Termux
3. Run updates:

```bash
pkg update && pkg upgrade -y
```

> **Note:** If you get a "repository is under maintenance" error, enable the default repos:
> ```bash
> termux-change-repo
> ```

## Step 2: Install proot-distro & Ubuntu

```bash
pkg install proot-distro -y
proot-distro install ubuntu
```

## Step 3: Login to Ubuntu

```bash
proot-distro login ubuntu
```

Once inside Ubuntu, update packages:

```bash
apt update && apt upgrade -y
```

---

## Step 4: Install OpenCode CLI

### Inside Ubuntu, install Node.js 20+:

```bash
apt install -y curl
curl -fsSL https://deb.nodesource.com/setup_20.x | bash -
apt install -y nodejs
```

Verify:

```bash
node --version   # should be 20.x or higher
```

### Install OpenCode globally via npm:

```bash
npm install -g opencode-ai@latest
```

Verify:

```bash
opencode --version
```

### Or use the install script (alternative):

```bash
curl -fsSL https://opencode.ai/install | bash
```

---

## Step 5: Run OpenCode

```bash
opencode
```

On first launch it will create the `.opencode` directory and SQLite database. You can configure your preferred LLM provider by setting environment variables before running:

```bash
export ANTHROPIC_API_KEY="your-key"
export OPENAI_API_KEY="your-key"
# or just use the built-in free models
opencode
```

---

## Tips for Android

- **Keep Termux alive:** Use `termux-wake-lock` to prevent the process from being killed.
- **Increase swap:** If OpenCode runs out of memory, add a swap file in Termux:
  ```bash
  pkg install swap
  swapon /sdcard/swapfile
  ```
- **External keyboard:** OpenCode works best with a Bluetooth keyboard or Hacker's Keyboard app.
- **Persist proot-distro:** Every time you open Termux, run `proot-distro login ubuntu` and then `opencode` from your project directory.

---

## Credits

- **[anomalyco](https://github.com/anomalyco/opencode)** — The original creator and maintainer of [OpenCode](https://opencode.ai), the open source AI coding agent.
- [**Minaty001**](https://github.com/Minaty001) — For the Android adaptation guide and testing OpenCode on mobile devices.

---

## License

This guide is for educational purposes. OpenCode itself is MIT-licensed — see the [official repository](https://github.com/anomalyco/opencode).
