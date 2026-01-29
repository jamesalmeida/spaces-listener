# spaces-listener

Record and transcribe X/Twitter Spaces — live or replays.

## Commands

```bash
# Audio only (fast, uses yt-dlp direct)
spaces listen <url>

# With video (screen records browser + BlackHole audio)
spaces listen <url> --video

# Specify output directory
spaces listen <url> --output ~/Desktop

# Skip transcription
spaces listen <url> --no-transcribe

# Use larger Whisper model for better accuracy
spaces listen <url> --model medium
```

## Requirements

- **yt-dlp** — `brew install yt-dlp`
- **ffmpeg** — `brew install ffmpeg`
- **whisper** — `brew install openai-whisper`
- **BlackHole** (video mode only) — `brew install blackhole-2ch`

## What It Does

1. **Audio mode** (default):
   - Downloads audio directly via yt-dlp
   - Fast, works for live and replay Spaces
   - Small file sizes (~1MB/min)

2. **Video mode** (`--video`):
   - Opens Space in browser
   - Records screen + system audio via BlackHole
   - Captures visual UI, speaker indicators, comments
   - Good for social media clips

3. **Transcription**:
   - Runs Whisper locally (no API key needed)
   - Creates `.txt` transcript alongside audio
   - Models: tiny, base (default), small, medium, large

## Output

Files are saved to `--output` dir (default: `~/Desktop`):
- `space_<username>_<date>.m4a` — audio file
- `space_<username>_<date>.txt` — transcript
- `space_<username>_<date>.mp4` — video (if --video)

## Examples

```bash
# Record a live Space
spaces listen "https://x.com/i/spaces/1ABC..."

# Record with video for clips
spaces listen "https://x.com/i/spaces/1ABC..." --video

# High-quality transcription
spaces listen "https://x.com/i/spaces/1ABC..." --model large
```

## Notes

- Live Spaces record in real-time until they end (or you Ctrl+C)
- Replays download at full speed
- Video mode requires BlackHole audio routing configured
- Transcription runs locally — no API costs, no rate limits
