# spaces-listener

Record and transcribe X/Twitter Spaces — live or replays. Zero API costs.

## Commands

```bash
# Start recording (runs in background until Space ends)
spaces listen <url>

# Check recording status
spaces status

# Stop recording
spaces stop

# Transcribe an existing audio file
spaces transcribe ~/Desktop/space.m4a

# Options
spaces listen <url> --output ~/Spaces
spaces listen <url> --model medium
spaces listen <url> --no-transcribe
```

## Requirements

- **yt-dlp** — `brew install yt-dlp`
- **ffmpeg** — `brew install ffmpeg`  
- **whisper** — `brew install openai-whisper`

## How It Works

1. `spaces listen` starts recording in the background using `nohup`
2. Recording continues until the Space ends (or you run `spaces stop`)
3. You can close your terminal — recording persists
4. When done, run `spaces transcribe <file>` to generate transcript

## Output

Files saved to `--output` dir (default: `~/Desktop`):
- `space_<username>_<date>.m4a` — audio file
- `space_<username>_<date>.log` — download progress log
- `space_<username>_<date>.txt` — transcript (after transcribing)

## Whisper Models

| Model | Speed | Accuracy | Size |
|-------|-------|----------|------|
| tiny | Fastest | Basic | 39MB |
| base | Fast | Good | 142MB |
| small | Medium | Better | 466MB |
| medium | Slow | Great | 1.5GB |
| large | Slowest | Best | 2.9GB |

## Video Recording

For video clips of Spaces, use QuickTime Player with BlackHole audio routing.
See the README for setup instructions.

## Examples

```bash
# Record a live Space (background, persists until Space ends)
spaces listen "https://x.com/i/spaces/1ABC..."

# Check if recording is still going
spaces status

# Stop early if needed
spaces stop

# Transcribe when done
spaces transcribe ~/Desktop/space_username_2026-01-28.m4a --model large
```
