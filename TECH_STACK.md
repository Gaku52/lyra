# Lyra - Technology Stack & Infrastructure

**Project**: Lyra - Music Genre Detection
**Last Updated**: 2024-11-13
**Status**: Design Phase

---

## Overview

Lyra will be developed in three phases:
1. **Phase 1**: Python CLI (1-2 months)
2. **Phase 2**: Web Application (1-2 months)
3. **Phase 3**: iOS Native App (2-3 months) - **Target: App Store Release**

---

## Phase 1: CLI Development (Month 1-2)

### Technology Stack

**Language:**
- Python 3.10

**Package Manager:**
- Poetry

**Core Libraries:**
```toml
[tool.poetry.dependencies]
python = "^3.10"
librosa = "^0.10.0"           # Audio feature extraction
sounddevice = "^0.4.6"        # Microphone input
scikit-learn = "^1.3.0"       # Machine learning (Random Forest)
numpy = "^1.24.0"             # Numerical computation
scipy = "^1.10.0"             # Scientific computation
soundfile = "^0.12.0"         # Audio file I/O
joblib = "^1.3.0"             # Model serialization
tqdm = "^4.65.0"              # Progress bars
colorama = "^0.4.6"           # Terminal colors
```

**Development Tools:**
```toml
[tool.poetry.dev-dependencies]
black = "^23.0.0"             # Code formatter
ruff = "^0.1.0"               # Linter
pytest = "^7.4.0"             # Testing framework
pytest-cov = "^4.1.0"         # Code coverage
```

### Features

- Audio capture from microphone (5-10 seconds)
- Feature extraction (MFCCs, Spectral features, Tempo, etc.)
- Genre classification (10 main genres)
- CLI interface with progress indicators

### Cost

**$0** (Local development only)

---

## Phase 2: Web Application (Month 3-4)

### Architecture

```
┌─────────────────────────────────┐
│  User (Browser)                 │
└─────────────────────────────────┘
              ↓
┌─────────────────────────────────┐
│  Frontend (Vercel)              │
│  - Next.js 14 (App Router)      │
│  - TypeScript                   │
│  - Tailwind CSS                 │
└─────────────────────────────────┘
              ↓ REST API
┌─────────────────────────────────┐
│  Backend (Railway/GCP)          │
│  - FastAPI                      │
│  - Python 3.10                  │
│  - ML Model (scikit-learn)      │
└─────────────────────────────────┘
```

### Frontend

**Framework:** Next.js 14
**Language:** TypeScript
**Styling:** Tailwind CSS
**Audio:** Web Audio API

**Key Features:**
- One-button operation
- Real-time audio capture
- Clean, minimal UI
- Responsive design

**Deployment:** Vercel
**Cost:** $0 (Hobby plan)

---

### Backend

**Framework:** FastAPI
**Language:** Python 3.10
**ML:** scikit-learn (Random Forest)

**Dependencies:**
```python
fastapi = "^0.104.0"
uvicorn = "^0.24.0"
pydantic = "^2.0.0"
python-multipart = "^0.0.6"
librosa = "^0.10.0"
scikit-learn = "^1.3.0"
numpy = "^1.24.0"
```

**API Endpoints:**
```
POST /api/analyze
- Input: Audio file (multipart/form-data)
- Output: { "genre": "Acid Techno", "confidence": 0.92 }
```

**Deployment Options:**

#### Option A: Railway (Recommended for MVP)
- **Cost:** $0-15/month
- **Setup:** Git push auto-deploy
- **Features:** Built-in PostgreSQL, logs, metrics
- **Capacity:** Up to 1,000 users/month

#### Option B: GCP Cloud Run (For Growth)
- **Cost:** $0-20/month (with free tier)
- **Setup:** Docker container
- **Features:** Auto-scaling, pay-per-use
- **Capacity:** Up to 10,000 users/month

---

### Database

**Phase 2 MVP:**
- Railway PostgreSQL (included with backend)
- Store user analytics (optional)

**Phase 3 Growth:**
- Option to migrate to GCP Cloud SQL
- Cost: $10-30/month

---

### Storage

**GCS (Google Cloud Storage)**
- ML models (50-200MB)
- Dataset backup (optional)
- Cost: $0-2/month (5GB free tier)

---

### Cost Summary (Phase 2)

| Service | Cost/Month | Notes |
|---------|-----------|-------|
| **Vercel** (Frontend) | $0 | Free Hobby plan |
| **Railway** (Backend) | $0-15 | Free $5 credit, then usage-based |
| **Total** | **$0-15** | **~¥0-2,250** |

**Expected Costs by User Count:**
- 0-100 users: $0/month
- 100-500 users: $3-8/month
- 500-1,000 users: $8-15/month

---

## Phase 3: iOS Application (Month 5-7)

**Target: App Store Release in 2-3 months after Web launch**

### Architecture

```
┌─────────────────────────────────┐
│  iOS App (Swift/SwiftUI)        │
│  - Audio Capture (AVFoundation) │
│  - UI (SwiftUI)                 │
│  - ML Inference                 │
└─────────────────────────────────┘
        ↓ (Option A or B)

Option A: On-Device ML
┌─────────────────────────────────┐
│  Core ML Model                  │
│  (Converted from scikit-learn)  │
└─────────────────────────────────┘

Option B: API-Based
┌─────────────────────────────────┐
│  Backend API (FastAPI on GCP)   │
│  ML Model (Python)              │
└─────────────────────────────────┘
```

### Technology Stack

**Language:** Swift 5.9+
**UI Framework:** SwiftUI
**Audio:** AVFoundation
**ML:** Core ML (for on-device) or URLSession (for API)

**Key Features:**
- Native iOS interface
- Microphone permission handling
- Real-time audio capture
- Smooth animations
- Offline capability (if using Core ML)

### Development Approach

#### Recommended: Hybrid Approach

**Phase 3A (Month 5-6): API-Based iOS App**
```swift
iOS App (Swift)
   ↓
Python Backend API (FastAPI)
   ↓
ML Model (scikit-learn)
```

**Advantages:**
- Faster development (use existing API)
- Easy model updates (server-side)
- Consistent with Web version

**Phase 3B (Month 7+): Add Core ML Support**
```swift
iOS App (Swift)
   ↓
Core ML Model (converted from Python)
   ↓
On-device inference (offline capability)
```

**Advantages:**
- Offline functionality
- Lower latency
- No server costs per inference
- Better privacy

---

### iOS Cost Structure

**Development:**
- Apple Developer Program: $99/year (¥15,000/year)
- Xcode: Free
- TestFlight: Free

**Backend (if using API approach):**
- Same as Phase 2 Web costs
- GCP Cloud Run: $0-20/month

**Total:** $99/year + $0-20/month backend

---

## Cost Projection (All Phases)

### Year 1 Breakdown

| Phase | Duration | Monthly Cost | Total Cost |
|-------|----------|--------------|------------|
| **Phase 1** (CLI) | 2 months | $0 | $0 |
| **Phase 2** (Web MVP) | 2 months | $0-5 | $0-10 |
| **Phase 2** (Web Growth) | 6 months | $5-15 | $30-90 |
| **Phase 3** (iOS Dev) | 2 months | $5-15 + $99 | $10-30 + $99 |
| **Year 1 Total** | 12 months | - | **$139-229** |

**In Japanese Yen: ¥21,000-34,000/year (~¥1,750-2,850/month)**

---

### Monthly Budget: $20 (~¥3,000)

**What $20/month covers:**

| User Count | Infrastructure Cost | Covered? |
|-----------|-------------------|----------|
| 0-1,000 | $0-10 | ✅ Yes |
| 1,000-10,000 | $10-18 | ✅ Yes |
| 10,000-30,000 | $18-56 | ⚠️ Needs revenue |

**Conclusion:** $20/month is sufficient for the first 10,000 users.

---

## Deployment Strategy

### Phase 2: Web Application

**Frontend (Vercel):**
```bash
# Automatic deployment
git push origin main
→ Vercel auto-deploys
```

**Backend (Railway):**
```bash
# Automatic deployment
git push origin main
→ Railway auto-deploys
```

**Custom Domain:**
- Frontend: lyra.yourdomain.com
- Backend: api.lyra.yourdomain.com

---

### Phase 3: iOS Application

**Development:**
```
1. Develop in Xcode
2. Test with Simulator
3. TestFlight beta testing
4. App Store submission
```

**App Store Submission Checklist:**
- [ ] App icon (1024x1024)
- [ ] Screenshots (all device sizes)
- [ ] App description (English + Japanese)
- [ ] Privacy policy
- [ ] Microphone usage description
- [ ] Terms of service (if needed)

**Timeline:**
- Development: 6-8 weeks
- TestFlight beta: 1-2 weeks
- App Review: 1-2 weeks
- **Total: 2-3 months**

---

## Technology Migration Path

### Upgrading ML Model (Future)

**From scikit-learn to PyTorch:**

When to upgrade:
- Need higher accuracy (80%+ → 90%+)
- Need to support more subgenres
- Have collected sufficient training data

**Migration:**
```python
# Current: scikit-learn Random Forest
model = RandomForestClassifier()

# Future: PyTorch CNN
model = torch.nn.Sequential(
    Conv2d(...),
    MaxPool2d(...),
    Dense(...),
)
```

**Cost Impact:** Minimal (same infrastructure)

---

### Scaling Strategy

**When to scale:**

| Metric | Trigger | Action |
|--------|---------|--------|
| **Users** | > 10,000/month | Migrate to GCP Cloud Run |
| **Requests** | > 500,000/month | Add load balancing |
| **Model Size** | > 500MB | Use CDN for model delivery |
| **Accuracy** | < 70% | Collect more data, upgrade model |

---

## Development Environment

### Required Tools

**For All Phases:**
- Git
- Python 3.10
- Poetry
- VS Code (recommended)

**For Phase 2 (Web):**
- Node.js 18+
- npm/yarn
- Railway CLI (optional)
- GCP CLI (for Cloud Run)

**For Phase 3 (iOS):**
- macOS (required)
- Xcode 15+
- Swift 5.9+
- iOS Simulator
- Apple Developer Account ($99/year)

---

## Risk Mitigation

### Technical Risks

**Risk 1: Low ML Accuracy**
- Mitigation: Start with proven GTZAN dataset
- Fallback: Use pre-trained models from research

**Risk 2: High Server Costs**
- Mitigation: Start with Railway (cheap)
- Fallback: Optimize model size, add caching

**Risk 3: iOS App Rejection**
- Mitigation: Follow Apple guidelines strictly
- Fallback: Detailed privacy policy, clear mic usage

**Risk 4: Development Delay**
- Mitigation: Phased approach, MVP first
- Fallback: Skip iOS, focus on Web

---

## Success Metrics

### Phase 1 (CLI)
- ✅ Can classify 10 genres
- ✅ Accuracy ≥ 70%
- ✅ Inference time < 3 seconds

### Phase 2 (Web)
- ✅ Deployed to production
- ✅ 100+ users
- ✅ Positive user feedback
- ✅ Monthly cost < $20

### Phase 3 (iOS)
- ✅ App Store approval
- ✅ 1,000+ downloads in first month
- ✅ 4+ star rating
- ✅ Featured testimonials

---

## Timeline

### Detailed Roadmap

**Month 1-2: Phase 1 (CLI)**
- Week 1-2: Setup, dataset acquisition
- Week 3-4: Feature extraction implementation
- Week 5-6: Model training and evaluation
- Week 7-8: CLI interface and testing

**Month 3-4: Phase 2 (Web)**
- Week 9-10: FastAPI backend
- Week 11-12: Next.js frontend
- Week 13-14: Integration and testing
- Week 15-16: Deployment and optimization

**Month 5-7: Phase 3 (iOS)**
- Week 17-20: Swift/SwiftUI development
- Week 21-22: API integration
- Week 23-24: TestFlight beta
- Week 25-26: App Store submission

**Target: iOS App Store release by Month 7**

---

## Conclusion

### Confirmed Technology Stack

**Backend:** Python 3.10 + FastAPI
**Frontend:** Next.js 14 + TypeScript
**Mobile:** Swift + SwiftUI (iOS native)
**ML:** scikit-learn → PyTorch (future)
**Deploy:** Vercel (Frontend) + Railway/GCP (Backend)
**Budget:** $20/month (~¥3,000/month)

**Timeline:** 7 months to iOS App Store release

**Risk:** Low - Phased approach, proven technologies

**ROI:** High - Python + iOS skills, portfolio, potential revenue

---

*This is a living document and will be updated as the project progresses.*
