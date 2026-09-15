# HTML to APK Builder

Automatically convert your HTML files into Android APK apps using GitHub Actions!

## 🎯 How It Works

1. **Edit `index.html`** - Customize your web app however you want
2. **Push to GitHub** - Every time you push changes to the main branch
3. **Automatic Build** - GitHub Actions automatically builds your APK
4. **Download APK** - Get your APK from the Releases section

## 🚀 Getting Started

### Prerequisites
- GitHub account
- This repository

### Setup

1. The workflow is already configured in `.github/workflows/build-apk.yml`
2. Just edit `index.html` with your custom HTML/CSS/JavaScript
3. Push your changes to the `main` branch
4. The build will start automatically

### Monitoring Builds

1. Go to your repository
2. Click on **Actions** tab
3. You'll see "Build APK from HTML" workflow running
4. Once complete, go to **Releases** to download your APK

## 📝 Customizing Your App

### Edit the HTML
Simply modify `index.html` to add:
- Custom HTML markup
- CSS styling
- JavaScript functionality
- Images and media

### App Configuration
Edit `cordova-config.xml` to change:
- App name
- App ID (`com.htmltoapp.app`)
- Author information
- Permissions

## 📱 Features

- ✅ Responsive design support
- ✅ Full JavaScript support
- ✅ Local storage access
- ✅ Camera and device features (with Cordova plugins)
- ✅ Automatic versioning

## 🔧 Adding Cordova Plugins

To add functionality like camera, geolocation, etc., modify the workflow:

```yaml
- name: Add plugins
  run: |
    cd app
    cordova plugin add cordova-plugin-camera
    cordova plugin add cordova-plugin-geolocation
```

## 📦 Release Management

Each successful build creates a new Release with:
- Build number
- APK file ready to download
- Automatic tagging

## 🐛 Troubleshooting

**Build fails?**
- Check the Actions tab for error logs
- Make sure your HTML is valid
- Check `cordova-config.xml` for syntax errors

**APK won't install?**
- Make sure to enable "Unknown sources" in Android settings
- The APK is signed with a debug key (fine for testing)

## 📄 License

Your app, your rules!

---

Happy coding! 🎉
