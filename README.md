# Twilio Audio Host

A simple static web host for audio files used with Twilio's telephony services.

## Overview

This repository hosts audio files that can be used with Twilio for various purposes such as:

- Hold music during calls
- IVR (Interactive Voice Response) prompts
- Call waiting music
- Custom audio messages

## Files

- `index.html` - Simple directory listing of available audio files
- `audio.wav` - Hold music audio file (20.6 MB)

## Usage

### Deploy to GitHub Pages

1. Go to your repository settings
2. Navigate to **Pages** section
3. Under **Source**, select `main` branch
4. Click **Save**
5. Your audio files will be available at: `https://utkarsh-blandlabs.github.io/twilio-audio/`

### Use with Twilio

Once deployed, reference the audio file URL in your Twilio applications:

**TwiML Example:**

```xml
<Response>
    <Play>https://utkarsh-blandlabs.github.io/twilio-audio/audio.wav</Play>
</Response>
```

**Twilio Node.js SDK Example:**

```javascript
const VoiceResponse = require('twilio').twiml.VoiceResponse;

const response = new VoiceResponse();
response.play('https://utkarsh-blandlabs.github.io/twilio-audio/audio.wav');

console.log(response.toString());
```

## Supported Audio Formats

Twilio supports the following audio formats:

- WAV (uncompressed, PCM)
- MP3
- GSM
- μ-law (MuLaw)
- Other formats (see [Twilio docs](https://www.twilio.com/docs/voice/twiml/play#audio-file-formats))

## Adding New Audio Files

### For Large Files (> 10 MB)

This repository uses **Git LFS** (Large File Storage) for audio files:

```bash
# Install Git LFS (one-time setup)
brew install git-lfs  # macOS
# or
apt-get install git-lfs  # Ubuntu/Debian

# Initialize Git LFS in the repo
git lfs install

# Track audio files with LFS
git lfs track "*.wav"
git lfs track "*.mp3"

# Add and commit your audio files
git add .gitattributes
git add your-audio-file.wav
git commit -m "Add new audio file"
git push
```

### For Small Files (< 10 MB)

```bash
git add your-audio-file.mp3
git commit -m "Add new audio file"
git push
```

## Local Development

Simply open `index.html` in your browser to view the file listing:

```bash
open index.html
# or
python3 -m http.server 8000  # Then visit http://localhost:8000
```

## Troubleshooting

### Push Failed - File Too Large

If you get an error like `RPC failed; HTTP 400` when pushing, your audio file is too large for GitHub without Git LFS.

**Solution:** Use Git LFS (see "Adding New Audio Files" section above)

### Audio Not Playing in Twilio

- Ensure the file URL is publicly accessible
- Check that the audio format is supported by Twilio
- Verify the file isn't corrupted by testing it locally
- Make sure GitHub Pages is enabled and deployed

## Best Practices

1. **Optimize Audio Files**: Use compressed formats (MP3) when possible to reduce file size
2. **Sample Rate**: Twilio recommends 8kHz or 16kHz sample rate for voice applications
3. **Bit Rate**: 64 kbps or lower is usually sufficient for hold music
4. **Duration**: Keep files reasonably short to avoid long uploads and downloads

## License

This project is for internal use at Bland Labs.

## Contact

For questions or issues, contact the Bland Labs development team.
