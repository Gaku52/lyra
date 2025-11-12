# Lyra - Technical Specification

## Project Overview

**Project Name**: Lyra (ライラ)
**Type**: Music Genre Detection Application
**Primary Language**: Python
**Target Platform**: Web (CLI initially)

---

## Problem Statement

Users want to identify music genres from audio without:
- Requiring song metadata
- Relying on database matching (like Shazam)
- Complex setup or operations

**Solution**: Real-time acoustic analysis for instant genre classification.

---

## Target Users & Use Cases

### 1. Music Producers/DTM Artists
- **Use Case**: Analyze reference tracks to understand genre characteristics
- **Use Case**: Verify genre classification of their own compositions
- **Value**: Objective genre feedback during production

### 2. DJs & Music Curators
- **Use Case**: Automatically organize large music libraries
- **Use Case**: Discover genre patterns in playlists
- **Value**: Efficient library management

### 3. Music Enthusiasts
- **Use Case**: Learn about different music genres
- **Use Case**: Identify unknown tracks playing in cafes, stores, etc.
- **Value**: Music education and discovery

---

## Core Requirements

### Functional Requirements

#### MVP (Phase 1)
1. **Audio Input**
   - Capture audio from system microphone
   - Duration: 5-10 seconds
   - Sample rate: 22050 Hz (standard for music analysis)

2. **Genre Classification**
   - Classify into 8-10 broad genres
   - Display single most likely genre
   - Show confidence percentage

3. **User Interface**
   - CLI interface (Python script)
   - Single command execution
   - Clear result display

#### Phase 2
4. **Web Application**
   - REST API backend (FastAPI)
   - Web frontend (Next.js)
   - One-button operation
   - Real-time audio capture via browser

5. **Enhanced Display**
   - Visual feedback during listening
   - Smooth result animation
   - Confidence meter

#### Phase 3
6. **Advanced Features**
   - Sub-genre classification
   - History tracking (optional)
   - Acoustic feature visualization
   - Multiple genre suggestions with probabilities

### Non-Functional Requirements

1. **Performance**
   - Analysis time: < 3 seconds after audio capture
   - Total operation: < 15 seconds from button press to result

2. **Accuracy**
   - Target: 70%+ accuracy on test set (Phase 1)
   - Target: 80%+ accuracy (Phase 2+)

3. **Usability**
   - Zero learning curve
   - No manual required
   - Works on first try

4. **Simplicity**
   - No account registration
   - No complex settings
   - Single button operation

---

## Technical Architecture

### Phase 1: CLI Application

```
┌─────────────────────────────────────┐
│         User (Terminal)             │
└─────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────┐
│         lyra.py (Main)              │
│  - Audio capture                    │
│  - Feature extraction               │
│  - Model inference                  │
│  - Result display                   │
└─────────────────────────────────────┘
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
┌──────────────┐    ┌──────────────┐
│   librosa    │    │ scikit-learn │
│  (Features)  │    │   (Model)    │
└──────────────┘    └──────────────┘
```

### Phase 2: Web Application

```
┌─────────────────────────────────────┐
│      Browser (Next.js)              │
│  - Web Audio API                    │
│  - Simple UI                        │
└─────────────────────────────────────┘
                  │
                  ▼ (HTTP/REST)
┌─────────────────────────────────────┐
│      FastAPI Backend                │
│  - Audio processing endpoint        │
│  - Feature extraction               │
│  - Model inference                  │
└─────────────────────────────────────┘
                  │
        ┌─────────┴─────────┐
        ▼                   ▼
┌──────────────┐    ┌──────────────┐
│   librosa    │    │ Trained Model│
│  (Features)  │    │   (.pkl)     │
└──────────────┘    └──────────────┘
```

---

## Data & Models

### Dataset

#### Phase 1: GTZAN Genre Collection
- **Size**: 1000 audio tracks (100 per genre)
- **Duration**: 30 seconds each
- **Genres**: 10 genres (blues, classical, country, disco, hiphop, jazz, metal, pop, reggae, rock)
- **Format**: WAV, 22050 Hz
- **License**: Public research dataset

**Alternative**: FMA (Free Music Archive) - larger, more diverse

#### Phase 2+: Custom Dataset
- **Focus**: Electronic music sub-genres
- **Sources**:
  - YouTube (with proper attribution)
  - Free Music Archive
  - Bandcamp free tracks
  - Own collection (personal use only)
- **Target**: 100+ tracks per sub-genre

### Feature Extraction

**Acoustic Features** (via librosa):
1. **MFCCs** (Mel-Frequency Cepstral Coefficients)
   - 13-20 coefficients
   - Captures timbral texture

2. **Spectral Features**
   - Spectral centroid (brightness)
   - Spectral rolloff (shape)
   - Spectral bandwidth

3. **Rhythm Features**
   - Tempo (BPM)
   - Beat strength

4. **Chroma Features**
   - Pitch class distribution
   - Harmonic content

5. **Zero Crossing Rate**
   - Noise vs. pitch content

### Machine Learning Models

#### Phase 1: Traditional ML
**Model**: Random Forest Classifier
- Fast training
- Good interpretability
- Works well with small datasets

**Alternatives**: SVM, Gradient Boosting

#### Phase 2: Deep Learning (if needed)
**Model**: CNN (Convolutional Neural Network)
- Input: Mel-spectrogram (2D image)
- Architecture: VGG-like or ResNet
- Better accuracy for complex patterns

---

## User Experience Flow

### MVP (CLI)

```
$ python lyra.py

🎵 Lyra - Music Genre Detector
================================

Press ENTER to start listening...

[User presses ENTER]

🎧 Listening... (10 seconds)
████████████████████ 100%

🔍 Analyzing...

✨ Genre: Electronic/EDM
   Confidence: 87%

Press ENTER to analyze again, or Ctrl+C to exit.
```

### Phase 2 (Web)

**Initial State:**
```
┌─────────────────────────────────┐
│                                 │
│        🎵 Lyra                  │
│                                 │
│     [  Detect Genre  ]          │  ← Single button
│                                 │
└─────────────────────────────────┘
```

**Listening State:**
```
┌─────────────────────────────────┐
│                                 │
│    🎧 Listening...              │
│    ████████░░░░░░░ 60%          │  ← Progress
│                                 │
└─────────────────────────────────┘
```

**Result State:**
```
┌─────────────────────────────────┐
│                                 │
│    🎸 Electronic / EDM          │  ← Large, clear
│       87% confident             │  ← Smaller
│                                 │
│    [  Listen Again  ]           │
│                                 │
└─────────────────────────────────┘
```

---

## Genre Taxonomy

### Phase 1: Broad Genres (8-10)
1. Rock
2. Pop
3. Jazz
4. Hip-Hop
5. Electronic / EDM
6. Classical
7. Blues
8. Metal
9. Reggae
10. Country

### Phase 2: Electronic Sub-genres
- Techno
- House
- Drum & Bass
- Dubstep
- Trance
- Ambient

### Phase 3: Techno Sub-genres
- Acid Techno (target!)
- Minimal Techno
- Detroit Techno
- Industrial Techno
- Deep Techno

---

## Development Roadmap

### Week 1-2: MVP Development
- [x] Project setup & specification
- [ ] Environment setup (Python, libraries)
- [ ] Dataset acquisition (GTZAN)
- [ ] Feature extraction implementation
- [ ] Model training & evaluation
- [ ] CLI interface

### Week 3-4: Web Application
- [ ] FastAPI backend
- [ ] Audio processing endpoint
- [ ] Next.js frontend setup
- [ ] UI implementation
- [ ] Integration & testing

### Week 5+: Enhancement
- [ ] Deploy to production
- [ ] Collect user feedback
- [ ] Sub-genre dataset collection
- [ ] Model improvement
- [ ] Feature additions (based on usage)

---

## Technical Constraints

### Audio Processing
- **Minimum audio length**: 5 seconds (shorter = less accurate)
- **Maximum audio length**: 30 seconds (longer = unnecessary)
- **Audio quality**: Works best with clear audio, minimal background noise

### Model Performance
- **File size**: Model should be < 100MB for web deployment
- **Inference time**: < 3 seconds on modern hardware

### Browser Compatibility
- **Chrome**: Full support (Web Audio API)
- **Firefox**: Full support
- **Safari**: Full support (with WebKit quirks)
- **Mobile**: Supported, but microphone permissions required

---

## Success Metrics

### MVP Stage
- ✅ Application runs without errors
- ✅ Can classify 8-10 genres
- ✅ Accuracy ≥ 70% on test set
- ✅ User can operate without instructions

### Public Release
- 🎯 10+ users per week
- 🎯 Positive feedback from DTM/DJ community
- 🎯 Accuracy ≥ 80%
- 🎯 Mentioned on social media (Reddit, Twitter)

### Long-term
- 🎯 100+ users per week
- 🎯 Can classify sub-genres (including Acid Techno)
- 🎯 Accuracy ≥ 85%
- 🎯 Featured in music production communities

---

## Risks & Mitigation

### Risk 1: Low Accuracy
**Mitigation**:
- Start with proven GTZAN dataset
- Use established feature extraction methods
- Iterate on model architecture

### Risk 2: Poor User Experience
**Mitigation**:
- Keep it simple (one button)
- Test with real users early
- Prioritize speed over features

### Risk 3: Dataset Copyright Issues
**Mitigation**:
- Use public/research datasets
- For custom data, use Creative Commons licensed music
- Personal use only during development

### Risk 4: Web Audio API Complexity
**Mitigation**:
- Start with CLI to prove core functionality
- Research Web Audio API thoroughly
- Have fallback plan (file upload instead of live capture)

---

## Future Possibilities

### Advanced Features (Post-Launch)
- Multi-genre detection (e.g., "Rock with Electronic elements")
- Mood/emotion detection
- BPM and key detection
- Similar artist recommendations
- API for third-party integration

### Monetization (If Successful)
- Freemium model (basic free, advanced features paid)
- API access for developers
- White-label for music platforms
- Educational content/courses

---

## Appendix

### Technology Stack Summary

**Core:**
- Python 3.9+
- librosa 0.10+
- scikit-learn 1.3+
- numpy, scipy

**Web (Phase 2):**
- FastAPI 0.104+
- Next.js 14+
- TypeScript
- Tailwind CSS

**Development:**
- Git & GitHub
- pytest (testing)
- black (code formatting)
- Jupyter (experimentation)

**Deployment:**
- Vercel (frontend)
- Railway/Render (backend)
- Or: Single server with Docker

---

*This specification is a living document and will evolve as development progresses.*
