# Ollama Downloader (Linux AppImage)

A single-file Linux desktop app for downloading Ollama models in chunks, with resume support and a built-in GUI.

**Author:** Raveuk
**Distribution:** `Ollama_Downloader-x86_64.AppImage` (~12 MB)
**Platform:** Linux x86_64

---

## What it does

`Ollama_Downloader-x86_64.AppImage` is a self-contained desktop application that downloads Ollama models (e.g. `llama3:8b`, `qwen2.5:14b`) directly from the Ollama registry, with features designed for slow or unstable connections:

- **Chunked downloads** — splits each model blob into smaller pieces (default 1 GB, configurable) so a dropped connection only loses a single chunk
- **Parallel transfers** — up to 8 concurrent connections per model
- **Resume support** — interrupt at any time and continue from where you left off
- **SHA256 verification** — every chunk and final blob is integrity-checked
- **GUI + CLI** — double-click to launch the GUI, or pass subcommands on the command line
- **Model management** — list local models, verify, re-assemble, or clean up partial downloads from inside the app
- **IPv6 preference** — optional, often faster on dual-stack networks
- **3-day free trial** built in, no signup required

---

## Requirements

- Linux x86_64, glibc-based distro (Ubuntu 22.04+, Debian 12+, Fedora 36+, or newer)
- A working GPU driver (NVIDIA, AMD, Intel, or Mesa software fallback)
- An X11 or XWayland display

On minimal installs you may need:

```bash
sudo apt install libgl1 libx11-6 libxcb1 libxau6 libxdmcp6
```

---

## How to launch it

1. Download `Ollama_Downloader-x86_64.AppImage` from the [Releases](https://github.com/raveuk/Ollama-Model-downloader/releases) page.
2. Make it executable:
   ```bash
   chmod +x Ollama_Downloader-x86_64.AppImage
   ```
3. Run it:
   ```bash
   # No arguments → launches the GUI
   ./Ollama_Downloader-x86_64.AppImage

   # Or pass a CLI subcommand
   ./Ollama_Downloader-x86_64.AppImage list
   ./Ollama_Downloader-x86_64.AppImage pull llama3:8b
   ```

Double-clicking the AppImage from your file manager opens the GUI directly.

### If no window appears

Fyne (the GUI toolkit) needs a working OpenGL context. As a quick test, force software rendering:

```bash
LIBGL_ALWAYS_SOFTWARE=1 ./Ollama_Downloader-x86_64.AppImage
```

If that works, your GPU driver stack needs attention (often a mismatched NVIDIA kernel module / userland version).

---

## Using the GUI

When launched, the app opens with three tabs:

### 1. Download tab
- **Model Name** — type the model identifier, e.g. `llama3:8b`, `qwen2.5:14b`, `mistral:latest`
- **Output Dir** — where finished models are written (defaults to your Ollama models directory)
- **Temp Dir** — where in-progress chunks live until assembly
- **Chunk** — chunk size (100 MB / 250 MB / 500 MB / 1 GB / 2 GB)
- **Threads** — number of parallel connections (1–8)
- **Pull Model** — start the download
- **Cancel** — stop the current download (progress is preserved for resume)
- A live status line shows percentage, downloaded / total size, current speed, ETA, and a scrolling log

### 2. Models tab
Lists local and partially-downloaded models with size and status. Per-row actions:
- **Refresh** — rescan disk
- **Resume** — continue an incomplete download
- **Verify** — re-check SHA256 of a finished model
- **Assemble** — reassemble from completed chunks
- **Clean** / **Clean All** — remove partial downloads

### 3. License tab
- Shows current license status and your **Machine ID**
- **Start Free Trial (3 days)** — one-click activation, no email required
- **Activate License** — paste the key and email you received after purchase
- **Deactivate License** — remove the license from this machine

---

## Using the CLI

The same AppImage works as a command-line tool. All flags can be combined.

```bash
# Pull a model
./Ollama_Downloader-x86_64.AppImage pull llama3:8b

# Pull with custom chunk size and 8 parallel connections
./Ollama_Downloader-x86_64.AppImage pull llama3:8b -c 250MB -p 8

# Pull preferring IPv6
./Ollama_Downloader-x86_64.AppImage pull llama3:8b --ipv6

# Resume an interrupted download
./Ollama_Downloader-x86_64.AppImage resume llama3:8b

# Resume everything that was incomplete
./Ollama_Downloader-x86_64.AppImage resume --all

# List models (local + incomplete)
./Ollama_Downloader-x86_64.AppImage list

# Verify integrity
./Ollama_Downloader-x86_64.AppImage verify llama3:8b

# Clean partial downloads
./Ollama_Downloader-x86_64.AppImage clean --all
```

### Command reference

| Command | Description |
|---------|-------------|
| `pull <model>` | Download a model |
| `resume [model]` | Resume an interrupted download (or `--all`) |
| `list` | List local and incomplete models |
| `verify <model>` | Re-verify SHA256 of a model |
| `clean` | Remove partial downloads |
| `gui` | Force-launch the GUI |
| `license trial` | Start the 3-day free trial |
| `license info` | Show your Machine ID |
| `license activate` | Activate a purchased license |
| `license status` | Show current license state |
| `license deactivate` | Remove the license from this machine |

### Pull flags

| Flag | Description | Default |
|------|-------------|---------|
| `-c, --chunk-size` | Chunk size (e.g. `100MB`, `1GB`) | `1GB` |
| `-p, --parallel` | Parallel connections | `4` |
| `-o, --output` | Output directory | Ollama models dir |
| `-t, --temp-dir` | Temp dir for chunks | `~/.ollama-dl-temp` |
| `--ipv6` | Prefer IPv6 connections | off |
| `--no-verify` | Skip SHA256 verification | off |
| `--no-progress` | Disable progress bar | off |

---

## License & activation key

The app runs with a **3-day free trial** out of the box (one trial per machine). After that, a license key is required to keep downloading.

### Pricing

| Plan | Price | Duration |
|------|-------|----------|
| 1 Year | **$10.99** | 365 days |

### How to request an activation key

1. **Get your Machine ID.** In the app, open the **License** tab — your Machine ID is shown there. From the CLI:
   ```bash
   ./Ollama_Downloader-x86_64.AppImage license info
   ```
2. **Send payment** of **$10.99** via PayPal to **`raveuk@live.co.uk`**.
3. **Email** [`raveuk@live.co.uk`](mailto:raveuk@live.co.uk) with:
   - Your **Machine ID**
   - The **email address** you want the license tied to
   - Your **PayPal transaction reference**
4. Your license key will be sent back by email, typically within **30 minutes to 12 hours**.
5. Check your **junk / spam folder** if it does not arrive.

> **Important:** the key is generated once and tied to your Machine ID. Keep it safe — it cannot be regenerated. If you reinstall your OS or change major hardware, your Machine ID may change and a new key will be required.

### Activating

**In the GUI:** open the **License** tab → paste your key and email → click **Activate License**.

**On the CLI:**
```bash
./Ollama_Downloader-x86_64.AppImage license activate
# Enter your license key when prompted
# Enter the email used for purchase
```

Verify it worked:
```bash
./Ollama_Downloader-x86_64.AppImage license status
```

---

## Troubleshooting

**Download timing out on a slow connection** — use smaller chunks:
```bash
./Ollama_Downloader-x86_64.AppImage pull llama3:8b -c 100MB
```

**Slow speeds** — try IPv6 and more parallel connections:
```bash
./Ollama_Downloader-x86_64.AppImage pull llama3:8b --ipv6 -p 8
```

**Resume after a crash or reboot** — progress is saved automatically:
```bash
./Ollama_Downloader-x86_64.AppImage resume --all
```

**Trial already used** — each machine gets one trial. Purchase a license to continue.

**GUI won't open** — see the OpenGL note above; try `LIBGL_ALWAYS_SOFTWARE=1`.

---

## License

Proprietary software. A valid license key is required for use beyond the 3-day trial.

Copyright © 2026 Raveuk. All rights reserved.
