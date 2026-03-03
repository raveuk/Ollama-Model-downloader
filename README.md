# ollama-dl

A command-line tool for downloading Ollama models in configurable chunks with resume support.

**Author:** Raveuk
**Version:** 1.0.0
**Created:** March 2026

Purchase: 
1. Download the tool and run from the command prompt
2. type ollama-dl license info
3. **$10.99 a Year**
4. Send payment to using paypal to raveuk@live.co.uk with **Machine ID** any instruction
5. Email me at **raveuk@live.co.uk** with your details
6. License will be sent within 30mins to 12hrs to your email
7. Check your junks mails
8. Code will be sent only once and can't be generated


## Features

- **Chunked Downloads** - Download large models in 1GB chunks (configurable)
- **Parallel Downloads** - Up to 8 concurrent connections
- **Resume Support** - Interrupt and resume downloads anytime
- **Progress Display** - See overall and per-thread progress
- **Integrity Verification** - SHA256 verification of all downloads
- **IPv6 Support** - Optional IPv6 preference for faster speeds

## Installation

1. Download `ollama-dl.exe` to your desired location
2. Activate your license (see License Activation below)

## License Activation

This software requires a valid license to download models.

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
| `license info` | Show machine ID |
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

## Progress Display

During download, you'll see:

```
┌─ Downloading sha256:30e51a7cb1cf...
│ ██████████████████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  35.2% (18.3/52.0 GB) 582.0 kB/s ETA: 16h5m
├─ Active threads: 4
│   Chunk   5: [========>           ]  42.3% 156.2 kB/s
│   Chunk   6: [=====>              ]  28.1% 145.8 kB/s
│   Chunk   7: [==>                 ]  15.6% 138.4 kB/s
│   Chunk   8: [>                   ]   3.2% 141.2 kB/s
└─────────────────────────────────────────────────────────────────
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

## License

This is proprietary software. A valid license is required for use.

Copyright (c) 2026 Raveuk. All rights reserved.


