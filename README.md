# 🎬 ClipsAI Web Container

A complete containerized solution for AI-powered video processing with transcription, clip finding, and intelligent resizing.

## 🚀 Quick Start

### Option 1: Docker Compose (Recommended)
```bash
git clone https://github.com/jyoung2000/clipsai-web-container.git
cd clipsai-web-container
docker-compose up --build
```

### Option 2: Docker
```bash
docker build -t clipsai-web .
docker run -p 8501:8501 clipsai-web
```

### Option 3: Local Development
```bash
# Install system dependencies
sudo apt-get install ffmpeg libmagic1  # Ubuntu/Debian
brew install ffmpeg libmagic           # macOS

# Install Python dependencies
pip install -r requirements.txt
pip install whisperx@git+https://github.com/m-bain/whisperx.git
pip install git+https://github.com/ClipsAI/clipsai.git

# Run Streamlit app
streamlit run app.py

# OR run the enhanced web server
python web_server.py
```

## 🌐 Access

Once running, open your browser to:
- **Streamlit Interface**: http://localhost:8501
- **Enhanced Web Server**: http://localhost:8501 (if using web_server.py)

## ✨ Features

### 🎯 Core Functionality
- **Video Upload**: Drag & drop or click to upload MP4, AVI, MOV, MKV, FLV, WMV
- **Transcription**: WhisperX integration with 5 model sizes (tiny → large-v2)
- **Clip Finding**: AI-powered segment detection using TextTiling algorithm
- **Speaker Diarization**: Pyannote integration for speaker identification
- **Video Trimming**: Precise segment extraction
- **Video Resizing**: Multiple aspect ratios (16:9, 9:16, 1:1, 4:3, custom)
- **Download**: Get processed videos instantly

### 🎨 User Experience
- **Professional UI**: Modern dark theme with gradients and animations
- **Step-by-Step Workflow**: Clear progression from upload to download
- **Real-time Progress**: Loading animations and status updates
- **Error Handling**: Comprehensive error messages and recovery
- **Responsive Design**: Works on desktop, tablet, and mobile

### 🛠️ Technical Features
- **Containerized**: Full Docker support for easy deployment
- **API Endpoints**: RESTful API for programmatic access
- **Session Management**: Persistent state across interactions
- **File Management**: Automatic cleanup of temporary files
- **Testing Suite**: Comprehensive test coverage

## 🔧 Configuration

### Required Setup
1. **Hugging Face Token**: Get from [HF Settings](https://huggingface.co/settings/tokens)
2. **Pyannote License**: Accept at [Pyannote HF](https://huggingface.co/pyannote/speaker-diarization-3.0)

### Model Selection
- **tiny**: Fastest, least accurate (~1GB VRAM)
- **base**: Good balance (recommended, ~1GB VRAM)
- **small**: Better accuracy (~2GB VRAM)
- **medium**: High accuracy (~5GB VRAM)
- **large-v2**: Best accuracy (~10GB VRAM)

### Clip Settings
- **Min Duration**: 5-60 seconds
- **Max Duration**: 60-1800 seconds
- **Aspect Ratios**: Multiple presets + custom

## 📊 API Endpoints

```bash
# Check status
GET /api/status

# Upload video
POST /api/upload

# Transcribe video
POST /api/transcribe

# Find clips
POST /api/find_clips

# Process video
POST /api/process
```

## 🧪 Testing

Run the test suite:
```bash
python test_app.py
```

Test individual endpoints:
```bash
# Test transcription
curl -X POST http://localhost:8501/api/transcribe

# Test clip finding
curl -X POST http://localhost:8501/api/find_clips

# Test processing
curl -X POST -H "Content-Type: application/json" \
  -d '{"operation":"trim_and_resize"}' \
  http://localhost:8501/api/process
```

## 🔒 Security & Privacy

- **Local Processing**: All computation happens on your machine
- **No Data Upload**: Videos never leave your environment
- **Temporary Files**: Automatically cleaned up
- **Token Security**: HF tokens handled securely

## 🚨 Troubleshooting

### Common Issues

1. **Container won't start**
   ```bash
   docker logs clipsai-web
   ```

2. **Out of memory**
   - Use smaller Whisper models
   - Increase container memory limits
   - Process shorter video segments

3. **Slow processing**
   - Enable GPU support in Docker
   - Use appropriate model size for your hardware
   - Check available system resources

## 📈 Performance

### Expected Processing Times
- **Transcription**: 1-2x video length (base model)
- **Clip Finding**: 10-30 seconds
- **Video Trimming**: 5-15 seconds
- **Video Resizing**: 2-5x clip length (includes diarization)

### Resource Requirements
- **RAM**: 2-16GB depending on model size
- **GPU**: Optional but significantly faster
- **Storage**: ~2x original video size for temporary files

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests
5. Submit a pull request

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

## 🙏 Acknowledgments

- [ClipsAI](https://github.com/ClipsAI/clipsai) - Core video processing library
- [WhisperX](https://github.com/m-bain/whisperx) - Enhanced Whisper transcription
- [Pyannote](https://github.com/pyannote/pyannote-audio) - Speaker diarization
- [Streamlit](https://streamlit.io/) - Web framework

---

**🎬 Transform your videos with the power of AI!**

*Generated with [Claude Code](https://claude.ai/code)*