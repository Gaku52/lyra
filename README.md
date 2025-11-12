# Lyra (ライラ)

<div align="center">

🎵 **Instant music genre detection from audio**

*Listen. Discover. Understand.*

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/license-MIT-green.svg)](LICENSE)

</div>

---

## 🌟 What is Lyra?

**Lyra** is a music genre detection application that identifies genres from live audio input in real-time.

Unlike Shazam (which matches songs to a database), Lyra **analyzes acoustic features** to classify genres - meaning it works with:
- Unknown songs
- Original compositions
- Remixes
- Live performances
- Any audio playing near your microphone

Named after the ancient Greek lyre (竪琴), Lyra represents the essence of music itself.

---

## ✨ Core Concept

### The Problem
- "What genre is this song?" - No easy way to find out
- Artist/metadata not always available
- Need to understand music characteristics

### The Solution
**One button. One answer.**

```
1. Press button
2. Play audio (5-10 seconds)
3. Get genre instantly
```

That's it. No complexity. No friction.

---

## 🎯 Vision

> **Simple is better than complex.**

Lyra aims to be:
- The simplest way to identify music genres
- A learning tool for understanding music characteristics
- A reference tool for music producers and DJs
- Accessible to everyone, everywhere

---

## 🚀 Planned Features

### Phase 1: MVP (Current Focus)
- [x] Project setup
- [ ] Audio input from microphone
- [ ] Genre classification (8-10 basic genres)
- [ ] Simple CLI interface
- [ ] Model training with GTZAN dataset

**Target Genres (Phase 1):**
- Rock
- Pop
- Jazz
- Hip-Hop
- Electronic/EDM
- Classical
- Blues
- Metal
- Reggae
- Country

### Phase 2: Web Application
- [ ] FastAPI backend
- [ ] Next.js frontend
- [ ] Simple, beautiful UI
- [ ] Confidence percentage display
- [ ] Deploy to production

### Phase 3: Advanced Features
- [ ] Sub-genre classification (Acid Techno, Minimal, etc.)
- [ ] Custom dataset for electronic music
- [ ] History tracking (optional)
- [ ] Acoustic feature visualization

---

## 🛠 Tech Stack

### Backend (Python)
- **Audio Processing**: librosa, sounddevice, numpy
- **Machine Learning**: scikit-learn (or PyTorch for deep learning)
- **API**: FastAPI, uvicorn

### Frontend
- **Framework**: Next.js + TypeScript
- **Audio**: Web Audio API

### Data
- **Initial**: GTZAN Dataset
- **Future**: Custom datasets for sub-genres

---

## 🎨 Design Philosophy

### Simplicity First
- One button operation
- No account required
- No complex settings
- Instant results

### Beautiful Experience
- Inspired by the ancient lyre
- Poetic, not mechanical
- Music is emotion, not just data

---

## 📖 Development Progress

Development starts: **Friday, November 15, 2024**

Current Status: **Planning & Setup** ✅

---

## 🌍 Target Users

1. **Music Producers/DTM Artists**: Reference analysis, genre checking for own compositions
2. **DJs/Curators**: Library organization, playlist creation
3. **Music Enthusiasts**: Learning about genres, discovering new music
4. **Educators**: Teaching music theory and genre characteristics

---

## 📝 License

MIT License - See [LICENSE](LICENSE) for details

---

## 👨‍💻 Author

**Gaku** (Gaku52)
- Learning Python through this project
- Passionate about music and technology
- Committed to building useful, beautiful tools

---

## 🎵 The Name

**Lyra (ライラ)** comes from:
- The ancient Greek lyre (竪琴) - one of the oldest musical instruments
- The constellation Lyra - home to Vega, one of the brightest stars
- Symbolizes the essence and soul of music

> "Let Lyra reveal the truth of music."

---

*This project is in active development. Star ⭐ this repo to follow progress!*
