# spaces-listener

Record and transcribe X/Twitter Spaces — live or replays. Zero API costs.

## Commands

```bash
# Audio only (recommended - fully automated)
spaces listen <url>

# Specify output directory
spaces listen <url> --output ~/Spaces

# Skip transcription
spaces listen <url> --no-transcribe

# Use larger Whisper model for better accuracy
spaces listen <url> --model medium
```

## Requirements

- **yt-dlp** — `brew install yt-dlp`
- **ffmpeg** — `brew install ffmpeg`  
- **whisper** — `brew install openai-whisper`

## What It Does

1. Downloads audio directly via yt-dlp (works for live + replay)
2. Transcribes locally with Whisper (no API key needed)
3. Saves audio + transcript to output directory

## Output

Files saved to `--output` dir (default: `~/Desktop`):
- `space_<username>_<date>.m4a` — audio file
- `space_<username>_<date>.txt` — transcript

## Whisper Models

| Model | Speed | Accuracy | Size |
|-------|-------|----------|------|
| tiny | Fastest | Basic | 39MB |
| base | Fast | Good | 142MB |
| small | Medium | Better | 466MB |
| medium | Slow | Great | 1.5GB |
| large | Slowest | Best | 2.9GB |

## Video Recording

For video clips of Spaces (showing the UI, speakers, waveforms), use one of these manual approaches:

**QuickTime Player (easiest):**
1. Set system audio output to your Multi-Output Device (with BlackHole)
2. File → New Screen Recording
3. Click dropdown next to record button, select "BlackHole 2ch" for audio
4. Record your screen while the Space plays

**OBS (most powerful):**
```bash
brew install --cask obs
```
Configure Desktop Audio to capture BlackHole.

**Why not automated?** macOS requires Screen Recording permission granted to a proper .app bundle. CLI tools (node, ffmpeg) running as background services can't easily get this permission.

## Examples

```bash
# Record a live Space (records until it ends or you Ctrl+C)
spaces listen "https://x.com/i/spaces/1ABC..."

# High-quality transcription for important content
spaces listen "https://x.com/i/spaces/1ABC..." --model large

# Save to organized folder
spaces listen "https://x.com/i/spaces/1ABC..." -o ~/Spaces/Tesla
```

## Notes

- Live Spaces record in real-time until they end
- Replays download at full speed
- All processing is local — no API costs, no rate limits
- First run downloads the Whisper model (~142MB for base)
