# 🎧 spaces-listener

Record and transcribe X/Twitter Spaces — live or replays.

**Zero API costs.** Everything runs locally on your Mac.

## Features

- 📥 **Audio recording** — Direct download via yt-dlp (fast, small files)
- 🎬 **Video recording** — Screen capture with BlackHole audio routing
- 📝 **Auto-transcription** — Local Whisper (no API key needed)
- ⏺️ **Live Spaces** — Record in real-time as they happen
- 🔄 **Replays** — Download at full speed

## Installation

### Prerequisites

```bash
brew install yt-dlp ffmpeg openai-whisper

# For video mode (optional)
brew install blackhole-2ch
```

### Install the skill

```bash
# Clone to your skills directory
git clone https://github.com/jamescowie/spaces-listener.git ~/clawd/skills/spaces-listener

# Add to PATH (add to your .zshrc)
export PATH="$HOME/clawd/skills/spaces-listener/scripts:$PATH"
```

## Usage

### Basic (audio only)

```bash
spaces listen "https://x.com/i/spaces/1ABC..."
```

### With video

```bash
spaces listen "https://x.com/i/spaces/1ABC..." --video
```

### Options

| Flag | Description |
|------|-------------|
| `--video` | Record screen + audio (requires BlackHole) |
| `--output`, `-o` | Output directory (default: ~/Desktop) |
| `--model` | Whisper model: tiny/base/small/medium/large |
| `--no-transcribe` | Skip transcription |

### Examples

```bash
# Record a live Space
spaces listen "https://x.com/i/spaces/1ABC..."

# High-quality transcription
spaces listen "https://x.com/i/spaces/1ABC..." --model large

# Save to specific folder
spaces listen "https://x.com/i/spaces/1ABC..." -o ~/Spaces

# Video mode for clips
spaces listen "https://x.com/i/spaces/1ABC..." --video
```

## Output

Files saved to output directory:
- `space_<username>_<date>.m4a` — Audio
- `space_<username>_<date>.txt` — Transcript
- `space_<username>_<date>.mp4` — Video (if --video)

## Video Mode Setup

For video recording with audio:

1. Install BlackHole: `brew install blackhole-2ch`
2. Open **Audio MIDI Setup**
3. Create **Multi-Output Device** with:
   - Your speakers/headphones
   - BlackHole 2ch
4. Set Multi-Output as system output
5. Now `spaces listen --video` captures both screen and audio

## How It Works

### Audio Mode (default)
1. yt-dlp extracts the HLS stream directly
2. Saves as .m4a (no transcoding needed)
3. Whisper transcribes locally

### Video Mode
1. Opens Space URL in browser
2. ffmpeg captures screen + BlackHole audio
3. Extracts audio track for transcription
4. Whisper transcribes locally

## License

MIT
