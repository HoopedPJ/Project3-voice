# Voice Assistant PWA

An offline-first Progressive Web App (PWA) voice assistant built with Next.js, TypeScript, and local AI models. Features real-time speech-to-text, OpenAI chat completion, and text-to-speech synthesis.

## Features

- 🎤 **Voice Recording**: High-quality audio capture with noise suppression
- 🧠 **Local STT**: Whisper.cpp running in Web Worker for offline transcription
- 💬 **AI Chat**: OpenAI GPT-4 integration for intelligent responses
- 🔊 **Local TTS**: Coqui-style TTS model for speech synthesis
- 📱 **PWA**: Offline-first with service worker caching
- ⚡ **Performance**: Sub-1.2s response time target with detailed metrics
- 🎯 **Real-time**: Streaming audio processing and playback

## Tech Stack

- **Frontend**: Next.js 14, TypeScript, Tailwind CSS, shadcn/ui
- **Audio**: MediaRecorder API, Web Audio API, AudioWorklet
- **AI Models**: Whisper.cpp (WASM), Coqui TTS (ONNX), OpenAI GPT-4
- **Workers**: Web Workers for heavy processing
- **PWA**: Service Worker, Web App Manifest

## Setup Instructions

### 1. Clone and Install

\`\`\`bash
git clone <repository-url>
cd voice-assistant-pwa
npm install
\`\`\`

### 2. Environment Variables

Create \`.env.local\` file:

\`\`\`env
OPENAI_API_KEY=your_openai_api_key_here
\`\`\`

### 3. WASM Files Setup

You need to provide the following files in the \`public\` directory:

#### Whisper WASM Files
- \`public/wasm/whisper.wasm\` - Whisper model compiled to WASM
- \`public/wasm/whisper.js\` - Whisper JavaScript bindings

**Download from**: [whisper.cpp releases](https://github.com/ggerganov/whisper.cpp/releases)

#### TTS Model Files
- \`public/models/tts-model.onnx\` - Coqui TTS model in ONNX format
- \`public/models/tts-config.json\` - Model configuration

**Example TTS config**:
\`\`\`json
{
  "sample_rate": 22050,
  "hop_length": 256,
  "win_length": 1024,
  "n_mel_channels": 80,
  "n_speakers": 1,
  "languages": ["en"]
}
\`\`\`

### 4. Development

\`\`\`bash
npm run dev
\`\`\`

Visit \`http://localhost:3000\`

### 5. Production Build

\`\`\`bash
npm run build
npm start
\`\`\`

## File Structure

\`\`\`
├── app/
│   ├── api/chat/route.ts          # OpenAI chat endpoint
│   ├── layout.tsx                 # Root layout with PWA meta
│   └── page.tsx                   # Main voice assistant interface
├── components/
│   ├── mic-button.tsx             # Recording toggle button
│   ├── transcript-display.tsx     # Speech/response display
│   ├── audio-playback.tsx         # TTS audio player
│   └── performance-metrics.tsx    # Latency monitoring
├── public/
│   ├── sw.js                      # Service worker
│   ├── manifest.json              # PWA manifest
│   ├── workers/
│   │   ├── whisperWorker.js       # STT processing
│   │   └── ttsWorker.js           # TTS synthesis
│   ├── wasm/                      # Whisper WASM files
│   └── models/                    # TTS model files
└── .env.local                     # Environment variables
\`\`\`

## Usage

1. **Grant Permissions**: Allow microphone access when prompted
2. **Start Recording**: Tap the microphone button to begin recording
3. **Speak**: Say your message clearly
4. **Stop Recording**: Tap the button again to stop and process
5. **Listen**: The AI response will be automatically played back

## Performance Monitoring

The app tracks and displays:
- **STT Time**: Speech-to-text processing duration
- **LLM Time**: OpenAI API response time
- **TTS Time**: Text-to-speech synthesis duration
- **Total Time**: End-to-end response time

Target: < 1200ms total response time

## PWA Features

- **Offline Support**: Core functionality works without internet
- **Installable**: Add to home screen on mobile devices
- **Background Sync**: Queue requests when offline
- **Caching**: WASM files and models cached for offline use

## Browser Compatibility

- **Chrome/Edge**: Full support
- **Firefox**: Partial support (no AudioWorklet)
- **Safari**: Limited support (no service worker modules)
- **Mobile**: iOS Safari 14.5+, Chrome Mobile 90+

## Troubleshooting

### Audio Issues
- Ensure HTTPS (required for microphone access)
- Check browser permissions
- Verify audio codec support

### WASM Loading
- Confirm WASM files are in correct paths
- Check CORS headers for WASM files
- Verify file sizes (models can be large)

### Performance
- Monitor network conditions
- Check console for timing logs
- Optimize model sizes if needed

## Development Notes

### Mock Implementation
The current implementation includes mock STT/TTS for demonstration. To use real models:

1. Replace \`whisperWorker.js\` with actual Whisper.cpp integration
2. Replace \`ttsWorker.js\` with real TTS model inference
3. Provide actual WASM and model files

### Security
- API keys are server-side only
- CORS configured for WASM files
- Content Security Policy headers set

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## License

MIT License - see LICENSE file for details
