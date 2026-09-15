# HTML to APK Builder

Automatically convert your HTML files into Android APK apps using GitHub Actions!

## 🎯 How It Works

1. **Edit `index.html`** - Customize your web app however you want
2. **Push to GitHub** - Every time you push changes to the main branch
3. **Automatic Build** - GitHub Actions automatically builds your APK
4. **Download APK** - Get your APK from Artifacts in Actions

## 🚀 Quick Start - MANUAL SETUP (If Workflow Not Running)

If you don't see a build in Actions, **copy this and manually create the workflow**:

### Step 1: Create Workflow File
1. Go to your repo: https://github.com/overvortex/html-to-apk-builder
2. Click **Code** tab
3. Click **Add file** → **Create new file**
4. Type: `.github/workflows/build-apk.yml`
5. **Paste this code** (see below)
6. Click **Commit changes**

### Step 2: Copy & Paste This Workflow Code:

```yaml
name: Build APK from HTML

on:
  push:
    branches:
      - main
    paths:
      - 'index.html'

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v3
      
      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install Apache Cordova
        run: |
          sudo npm install -g cordova
      
      - name: Create Cordova project
        run: |
          cordova create app com.htmltoapp.app "Joke App"
          cd app
          cordova platform add android
      
      - name: Copy HTML file
        run: |
          cp index.html app/www/index.html
      
      - name: Set up Android SDK
        uses: android-actions/setup-android@v2
      
      - name: Build APK
        run: |
          cd app
          cordova build android --release
      
      - name: Upload APK
        uses: actions/upload-artifact@v3
        with:
          name: app-release
          path: app/platforms/android/app/build/outputs/apk/release/*.apk
```

### Step 3: Trigger the Build
1. Make any small edit to `index.html` (add a space, anything)
2. Commit and push
3. Go to **Actions** tab
4. You should see **"Build APK from HTML"** running!
5. Wait 5-10 minutes for it to complete
6. When done, scroll down to **Artifacts** section
7. Download **app-release** → the APK file!

## 📱 Install on Android Phone

1. Transfer the APK file to your phone
2. Settings → Security → Enable **"Unknown sources"** or **"Install unknown apps"**
3. Open the APK file
4. Tap **Install**
5. Done! Your app is installed! 🎉

## ✅ What's in Your App Now

Your **Random Joke Generator** has:
- 🎭 3 joke categories (General, Programming, Knock-Knock)
- 📡 Real jokes from **JokeAPI** (free API)
- 📱 Share jokes with friends
- 🎨 Beautiful purple UI with smooth animations

## 🔄 Update Your App

Every time you:
1. Edit `index.html`
2. Commit and push to `main`
3. GitHub Actions automatically builds a new APK!

Just download the latest artifact and install it on your phone.

## 📝 Example Edits You Can Make

```html
<!-- Change the title -->
<h1>My Cool App</h1>

<!-- Add new buttons -->
<button onclick="doSomething()">Click Me!</button>

<!-- Add custom JavaScript -->
<script>
  function doSomething() {
    alert('Hello from my app!');
  }
</script>
```

## 🐛 Troubleshooting

**No build appearing?**
- Make sure you created the `.github/workflows/build-apk.yml` file correctly
- Try making a small edit to `index.html` and pushing again

**Build fails?**
- Click on the failed workflow in Actions
- Scroll down to see error logs
- Most common: Java/Android SDK issues (not your fault, GitHub's runner)

**APK won't install?**
- Enable "Unknown sources" in phone settings
- Make sure you have enough storage
- Try uninstalling the old version first

---

**Need help?** Check your Actions tab for detailed logs!

🎉 Have fun building!
