# 💪 Workout Tracker PWA

A modern, feature-rich progressive web app for tracking gym workouts with progress charts, offline support, and customizable training schedules.

## ✨ Features

- **📱 Progressive Web App** - Install to home screen (iOS, Android, desktop)
- **📊 Progress Tracking** - Visual charts for weight progression
- **🎯 3-Day Split Routine** - Pre-configured with machine-based exercises
- **🌓 Dark/Light Mode** - Choose your preferred theme
- **🎨 Accent Colors** - Customize with Blue, Green, Purple, or Orange
- **⏱️ Session Timer** - Track workout duration and exercise-specific times
- **🔄 Restart Mode** - Deload weeks for returning from breaks
- **💾 Offline Support** - Works completely without internet
- **⚡ Zero Dependencies** - Single HTML file, no build process

## 🚀 Quick Start

### Option 1: Direct Browser
1. Open `index.html` in any modern web browser
2. Bookmark it or add to home screen
3. Start logging workouts!

### Option 2: Deploy Online
See [DEPLOYMENT.md](DEPLOYMENT.md) for instructions on:
- GitHub Pages (free)
- Netlify (free)
- Vercel
- Self-hosted servers

## 📋 Default Workout Schedule

**Day 1 — Horizontal Push/Pull**
- Chest Press Machine (3×8)
- Seated Cable Row (3×8)
- Chest-Supported Row (3×8)
- Pec Deck Fly (3×12)
- Reverse Pec Deck (3×12)
- Tricep Pushdown (3×12)

**Day 2 — Legs**
- Leg Press (3×8)
- Leg Extension (3×12)
- Lying Hamstring Curl (3×12)
- Bulgarian Split Squats (3×10)
- Standing Calf Raise (3×15)
- Hyperextension (3×10)

**Day 3 — Vertical Push/Pull**
- Lat Pulldown (3×8)
- Smith Machine OHP (3×8)
- Straight Arm Pulldown (3×12)
- Lateral Raise Machine (3×12)
- Face Pulls (3×15)

## 💻 How to Use

### Logging a Workout
1. Select a workout day (Day 1, 2, or 3)
2. Enter weight and reps for each set
3. Use the timer to track exercise duration
4. Complete the workout

### Viewing Progress
1. Go to **📊 Progress** tab
2. Select an exercise from dropdown
3. View weight progression over time

### Restart Mode (Deload Weeks)
Perfect when returning after 2+ weeks off:
1. Tap **🔄 Restart Mode**
2. Choose Week 1 or Week 2
3. App reduces sets to 2 and reminds you to use lighter weight
4. After 2 weeks, switch back to Normal mode

## 🔒 Privacy & Data

✅ **Your data stays on your device**
- All workouts saved in browser localStorage
- No cloud sync or accounts needed
- No ads, tracking, or analytics
- No internet required after first load

**Backup your data:**
Open DevTools (F12) → Application → Local Storage → Copy these keys:
- `workoutTrackerState`
- `workoutSchedule`
- `workoutSessions`

## 📱 Installation

### Mobile (iOS/Android)
1. Open app in browser
2. Tap **Share** → **Add to Home Screen**
3. Name it and install

### Desktop (Chrome/Edge)
1. Click install icon in address bar
2. Confirm installation

## 🛠️ Technical Details

- **Single File**: Everything in one HTML file (~30KB)
- **No Build Process**: Open and run immediately
- **Works Offline**: Service Worker for offline PWA features
- **LocalStorage**: All data persists locally
- **Responsive Design**: Mobile, tablet, and desktop optimized

## 📊 Browser Support

| Browser | Support | Install |
|---------|---------|---------|
| Chrome/Edge | ✅ | ✅ |
| Firefox | ✅ | ❌ |
| Safari (iOS) | ✅ | ✅ |
| Safari (Mac) | ✅ | ❌ |

## 🔗 GitHub Setup

### Clone the Repository
```bash
git clone https://github.com/yourusername/workout-tracker.git
cd workout-tracker
```

### Push to Your Repository
```bash
git remote add origin https://github.com/yourusername/workout-tracker.git
git branch -M main
git push -u origin main
```

### Enable GitHub Pages
1. Go to Settings → Pages
2. Select "main" branch as source
3. Your app is live at: `https://yourusername.github.io/workout-tracker/`

## 📝 Customize the Routine

Edit the `getDefaultSchedule()` function in `index.html` to modify exercises, sets, or reps.

Example:
```javascript
{ id: 'squat', name: 'Barbell Squat', sets: 4, reps: 5, type: 'compound' }
```

## 🚀 Deployment

### GitHub Pages (Easiest)
```bash
git push origin main
```
Live at: `https://yourusername.github.io/workout-tracker/`

### Netlify (Alternative)
```bash
# Install Netlify CLI
npm i -g netlify-cli

# Deploy
netlify deploy --prod --dir .
```

### Self-Hosted
1. Upload `index.html` to your web server
2. Enable HTTPS (required for PWA)
3. Done!

See [DEPLOYMENT.md](DEPLOYMENT.md) for detailed instructions.

## 🤝 Contributing

Contributions welcome! Please:
1. Fork the repository
2. Create a feature branch
3. Make changes
4. Submit a pull request

## 📄 License

MIT License - See [LICENSE](LICENSE) file

## 💡 Future Features

- [ ] Cloud backup & sync
- [ ] Multiple workout splits
- [ ] CSV export
- [ ] AI form feedback
- [ ] Wearable integration
- [ ] Social sharing

## 🐛 Issues & Feedback

Found a bug? Have ideas?
- Open an issue on GitHub
- Email: your.email@example.com

## 🙏 Support

- ⭐ Star the repository
- 📢 Share with your gym friends
- 🐛 Report bugs
- 💡 Suggest features

---

**Made with 💪 for fitness enthusiasts**

v1.0.0 | April 2025
