# ollama-dl

A command-line tool for downloading Ollama models in configurable chunks with resume support.

**Author:** Raveuk
**Version:** 1.1.0
**Created:** March 2026

## Features

- **Chunked Downloads** - Download large models in 1GB chunks (configurable)
- **Parallel Downloads** - Up to 8 concurrent connections
- **Resume Support** - Interrupt and resume downloads anytime
- **Progress Display** - See overall and per-thread progress
- **Integrity Verification** - SHA256 verification of all downloads
- **IPv6 Support** - Optional IPv6 preference for faster speeds
- **Free Trial** - 3-day free trial, no credit card required
- **Cross-Platform** - Windows and Linux (x64 & ARM64)

## Installation

### Windows

1. Download `ollama-dl.exe`
2. Run from command prompt or PowerShell

### Linux

```bash
# For x64 (most desktops/servers)
chmod +x ollama-dl-linux-amd64
./ollama-dl-linux-amd64

# For ARM64 (Raspberry Pi 4, etc.)
chmod +x ollama-dl-linux-arm64
./ollama-dl-linux-arm64

# Optional: Install system-wide
sudo mv ollama-dl-linux-amd64 /usr/local/bin/ollama-dl
```

### Available Downloads

| Platform | File |
|----------|------|
| Windows x64 | `ollama-dl.exe` |
| Linux x64 | `ollama-dl-linux-amd64` |
| Linux ARM64 | `ollama-dl-linux-arm64` |

After downloading, start a free trial or activate your license (see below)

## Free Trial

Try ollama-dl free for 3 days! No credit card required.

```bash
ollama-dl license trial
```

The trial:
- Lasts 3 days from activation
- Full functionality, no limitations
- One trial per machine

## License Activation

After the trial, a valid license is required to download models.

### Pricing

| Plan | Price | Duration |
|------|-------|----------|
| 1 Year | $10 | 365 days |

Purchase:

Download the tool and run from the command prompt
type ollama-dl license info
$10.99 a Year
Send payment to using paypal to raveuk@live.co.uk with Machine ID any instruction
Email me at raveuk@live.co.uk with your details
License will be sent within 30mins to 12hrs to your email
Check your junks mails
Code will be sent only once and can't be generated



### Get Your Machine ID

```bash
ollama-dl license info
```

This displays your unique Machine ID needed for license purchase.

### Activate License

```bash
ollama-dl license activate
```

Enter your license key and email when prompted.

### Check License Status

```bash
ollama-dl license status
```

### Deactivate License

```bash
ollama-dl license deactivate
```

## Usage

### Download a Model

```bash
# Download with defaults (1GB chunks, 4 parallel connections)
ollama-dl pull llama3:8b

# Download with smaller chunks
ollama-dl pull llama3:8b -c 100MB

# Download with more parallel connections
ollama-dl pull llama3:8b -p 8

# Download with IPv6 preference
ollama-dl pull llama3:8b --ipv6

# Download to custom directory
ollama-dl pull llama3:8b -o ./models
```

### Resume Interrupted Download

```bash
# Resume a specific model
ollama-dl resume llama3:8b

# Resume all incomplete downloads
ollama-dl resume --all
```

### List Models

```bash
# List local and incomplete downloads
ollama-dl list

# List only local models
ollama-dl list -l

# List only incomplete downloads
ollama-dl list -i
```

### Verify Model Integrity

```bash
ollama-dl verify llama3:8b
```

### Clean Partial Downloads

```bash
# Show what would be cleaned
ollama-dl clean

# Clean all partial downloads
ollama-dl clean --all

# Clean specific model
ollama-dl clean -m llama3:8b

# Force clean without confirmation
ollama-dl clean --all --force
```

## Command Reference

| Command | Description |
|---------|-------------|
| `pull <model>` | Download a model |
| `resume [model]` | Resume interrupted downloads |
| `list` | List models |
| `verify <model>` | Verify model integrity |
| `clean` | Remove partial downloads |
| `license trial` | Start free 3-day trial |
| `license info` | Show machine ID & trial status |
| `license activate` | Activate license |
| `license status` | Check license status |
| `license deactivate` | Remove license |

## Global Flags

| Flag | Description |
|------|-------------|
| `-o, --output` | Output directory |
| `-t, --temp-dir` | Temp directory for chunks |
| `-q, --quiet` | Suppress output |
| `-v, --verbose` | Verbose output |
| `--ipv6` | Prefer IPv6 connections |

## Pull Flags

| Flag | Description | Default |
|------|-------------|---------|
| `-c, --chunk-size` | Chunk size (e.g., 100MB, 1GB) | 1GB |
| `-p, --parallel` | Parallel connections | 4 |
| `--no-progress` | Disable progress bar | false |
| `--no-verify` | Skip SHA256 verification | false |
| `--simple` | Single-line progress (Git Bash compatible) | false |

## Progress Display

During download, you'll see multi-line progress with per-thread details:

```
Downloading sha256:30e51a7cb1cf... ██████████░░░░░░░░░░░░░░░░░░░░ 35.2% (18.3/52.0 GB) 80.9 MB/s ETA: 4m58s
  Threads: 4 active
    Chunk   5: [========-------]  42.3% 156.2 KB/s
    Chunk   6: [=====----------]  28.1% 145.8 KB/s
    Chunk   7: [==-------------]  15.6% 138.4 KB/s
    Chunk   8: [---------------]   3.2% 141.2 KB/s
```

The number of thread lines shown matches your `-p` setting (e.g., `-p 8` shows 8 threads).

### Simple Mode (Git Bash)

If using Git Bash and the display is scrolling, use `--simple` for single-line progress:

```bash
ollama-dl pull llama3:8b --simple
```

Output:
```
Downloading sha256:30e... ████████░░░░░░░░░░░░ 40.0% (19.3/48.2 GB) 80.9 MB/s ETA: 5m58s [4 threads]
```

## Troubleshooting

### Download Timeout

If downloads timeout on slow connections, try smaller chunks:
```bash
ollama-dl pull model:tag -c 100MB
```

### Slow Speeds

Try IPv6 or increase parallel connections:
```bash
ollama-dl pull model:tag --ipv6 -p 8
```

### Resume After Interruption

Progress is saved automatically. Just run:
```bash
ollama-dl resume
```

### Trial Already Used

Each machine can only use the trial once. If your trial has expired, purchase a license to continue using ollama-dl.

### Progress Display Issues (Git Bash)

If the progress display is scrolling/repeating in Git Bash, use the `--simple` flag:
```bash
ollama-dl pull model:tag --simple
```

PowerShell and Windows Terminal work correctly with the default multi-line display.

## License

This is proprietary software. A valid license is required for use.

Copyright (c) 2026 Raveuk. All rights reserved.


