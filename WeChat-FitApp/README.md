# 💪 FitApp - WeChat Mini-Program Fitness Trainer

A comprehensive offline fitness training application for WeChat Mini-Programs with support for 6 languages, fuzzy search, favorites, custom workout plans, and real-time timer.

## ✨ Core Features

### 1. Exercise Browser & Search
- 🏋️ Browse by body parts (Chest, Back, Shoulders, Arms, Core, Legs)
- 🔍 Fuzzy search engine (typo-tolerant) using Levenshtein distance algorithm
- 🏷️ Multi-dimensional filtering (body part, equipment, muscle)
- 📊 1,324+ exercise database from exercises-dataset

### 2. Favorites Management
- ⭐ One-click favoriting
- 💾 Local persistent storage
- 📋 Favorites list management

### 3. Custom Workout Plans
- 🎯 Create personalized training plans
- ➕ Freely select exercises
- ⚙️ Adjust sets, reps, weight, rest time
- 💪 Flexible workout design

### 4. Real-Time Timer
- ⏱️ Precise timing (second-level)
- 📍 Set/rep tracking
- 🔊 Completion reminders (optional)
- 📊 Automatic data recording

### 5. Multi-Language Support (6 Languages)
- 🇬🇧 English
- 🇨🇳 中文 (Chinese)
- 🇷🇺 Русский (Russian)  
- 🇯🇵 日本語 (Japanese)
- 🇰🇷 한국어 (Korean)
- 🇪🇸 Español (Spanish)

## 📁 Project Structure

```
WeChat-FitApp/
├── app.json              # App config
├── app.js                # Global logic
├── app.wxss              # Global styles
├── utils/
│   ├── i18n.js          # Multi-language (6 languages)
│   ├── search.js        # Fuzzy search engine
│   └── db.js            # Local database manager
├── pages/
│   ├── index/           # Home/Browse exercises
│   ├── search/          # Search & Filter
│   ├── plan/            # Workout Plans
│   ├── favorites/       # Favorites
│   ├── settings/        # Settings
│   ├── exercise-detail/ # Exercise Details
│   ├── training/        # Training (Coming soon)
│   └── history/         # History (Coming soon)
└── data/
    └── exercises.json   # Exercise dataset (1,324 exercises)
```

## 🚀 Quick Start

### 1. Download WeChat Developer Tools
https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html

### 2. Clone Repository & Open in DevTools
```bash
git clone https://github.com/MiaYang001/exercises-dataset.git
cd exercises-dataset/WeChat-FitApp
```

### 3. Open in WeChat Developer Tools
- File → Open → Select `WeChat-FitApp` folder
- Use test AppID if needed
- Click "Preview" or scan QR code with WeChat

## 🔍 Search Algorithm

Based on **Levenshtein Distance** for fuzzy matching:

```javascript
Search Weights:
1. Exact name match: 10
2. Name similarity (>0.6): 5
3. Body part match: 3
4. Target muscle match: 2
5. Equipment match: 2
```

**Examples:**
- Search "bench" → finds "Barbell Bench Press"
- Search "curl" → finds "Dumbbell Curl", "Barbell Curl"
- Search "chest" → finds all chest exercises

## 💾 Local Storage

### Favorites
```javascript
wx.setStorageSync('favorites', [
  {
    id: "0001",
    name: "Barbell Bench Press",
    body_part: "chest",
    equipment: "barbell",
    target: "pectorals",
    addedAt: "2024-01-15T10:30:00Z"
  }
])
```

### Plans
```javascript
wx.setStorageSync('plans', [
  {
    id: "plan_xxx",
    name: "Upper Body",
    exercises: [
      {
        id: "0001",
        name: "Barbell Bench Press",
        sets: 4,
        reps: 8,
        weight: 80,
        rest: 120
      }
    ]
  }
])
```

### History
```javascript
wx.setStorageSync('history', [
  {
    id: "record_xxx",
    planId: "plan_xxx",
    duration: 1800,  // seconds
    exercises: [...],
    date: "2024-01-15T10:30:00Z"
  }
])
```

## 🎨 Theme Colors

```css
/* Primary Colors */
--primary-color: #1E90FF;      /* Dodger Blue */
--primary-dark: #1873CC;        /* Dark Blue */
--success-color: #52C41A;       /* Green */
--warning-color: #FAAD14;       /* Orange */
--danger-color: #F5222D;        /* Red */

/* Text Colors */
--text-primary: #262626;        /* Primary text */
--text-secondary: #8C8C8C;      /* Secondary text */

/* Background Colors */
--bg-primary: #FFFFFF;          /* Primary background */
--bg-secondary: #F5F5F5;        /* Secondary background */
```

## 📊 Data Statistics

- **Total Exercises**: 1,324
- **Supported Languages**: 6
- **Max Package Size**: 20MB (WeChat limit)
- **Local Storage**: Unlimited
- **Offline Support**: ✅ Full offline capability

## ⚙️ API Reference

### Search Module (`utils/search.js`)
```javascript
fuzzySearch(exercises, query, language = 'en')
filterByBodyPart(exercises, bodyPart)
filterByEquipment(exercises, equipment)
search(exercises, query, filters = {}, language = 'en')
```

### Database Module (`utils/db.js`)
```javascript
// Favorites
getFavorites()
addFavorite(exercise)
removeFavorite(exerciseId)
isFavorite(exerciseId)

// Plans
getPlans()
createPlan(plan)
updatePlan(planId, updates)
deletePlan(planId)
getPlan(planId)
addExerciseToPlan(planId, exercise, sets, reps, weight, rest)
removeExerciseFromPlan(planId, exerciseId)

// History
getHistory()
addHistoryRecord(record)

// Config
getUserConfig()
updateUserConfig(config)
```

### i18n Module (`utils/i18n.js`)
```javascript
t(key, language = 'en')
// Supported languages: 'en', 'zh', 'ru', 'ja', 'ko', 'es'
```

## 🔧 Development

### Adding New Exercises
Edit `data/exercises.json`:
```json
{
  "id": "0004",
  "name": "Squat",
  "body_part": "upper legs",
  "equipment": "barbell",
  "target": "glutes",
  "instructions": {
    "en": "Stand with feet shoulder-width apart...",
    "zh": "双脚分开与肩同宽站立..."
  }
}
```

### Adding New Language
1. Edit `utils/i18n.js`
2. Add new language code and translations to `translations` object
3. Update `settings.js` language list

### Customize Search Weights
Edit `utils/search.js` line with score assignments

## ❓ FAQ

**Q: Why no GIF animations?**
A: GIFs are not included due to copyright issues. You can:
- Get them from [ExerciseDB official](https://oss.exercisedb.dev)
- Use other open-source video resources
- Add video display in `exercise-detail.wxml`

**Q: Can it work offline?**
A: Yes! All data is stored locally. No internet needed after first download.

**Q: How to add more exercises?**
A: Edit `data/exercises.json` and follow the existing format.

**Q: How to change theme colors?**
A: Edit `app.wxss` CSS variables.

## 🏗️ Roadmap

- [x] Exercise browsing & search
- [x] Multi-language support (6 languages)
- [x] Favorites management
- [x] Custom workout plans
- [ ] Real-time training timer
- [ ] Training history & analytics
- [ ] GIF animation support
- [ ] Social sharing
- [ ] Cloud sync (optional)

## 📄 License

Based on [exercises-dataset](https://github.com/hasaneyldrm/exercises-dataset) which uses the same license terms.

## 🙏 Credits

- **Data Source**: [exercises-dataset](https://github.com/hasaneyldrm/exercises-dataset)
- **Original Data**: [ExerciseDB](https://oss.exercisedb.dev)
- **Framework**: WeChat Mini-Program API
- **Developer**: MiaYang001

## 📞 Support

For issues, suggestions, or contributions, please:
- Open an [Issue](https://github.com/MiaYang001/exercises-dataset/issues)
- Submit a [Pull Request](https://github.com/MiaYang001/exercises-dataset/pulls)
- Contact via GitHub

---

**Version**: 1.0.0  
**Last Updated**: 2024-01  
**WeChat DevTools**: v1.06+  
**iOS**: 6.5.0+  
**Android**: All versions  

**🎉 Happy Training! 💪**
