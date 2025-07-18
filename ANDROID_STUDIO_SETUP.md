# AmneziaWG Android - Android Studio Setup Guide

This guide will help you set up the AmneziaWG Android project in Android Studio.

## Prerequisites

1. **Android Studio** (Latest stable version recommended)
2. **Android SDK** (will be installed automatically by Android Studio)
3. **Git** (for submodule management)

## Project Setup Instructions

### 1. Open the Project in Android Studio

1. Launch Android Studio
2. Choose "Open an Existing Project" or "File → Open"
3. Navigate to this project folder and select it
4. Click "OK"

### 2. SDK Configuration

Android Studio should automatically:
- Detect that this is an Android project
- Configure the Android SDK location in `local.properties`
- Download any missing SDK components

If you see SDK-related errors:
1. Go to **File → Project Structure → SDK Location**
2. Ensure the Android SDK Location is set (usually auto-detected)
3. Click "Apply" and "OK"

### 3. Gradle Sync

After opening the project:
1. Android Studio will automatically start a Gradle sync
2. If it doesn't, click the "Sync Now" banner or **File → Sync Project with Gradle Files**
3. Wait for the sync to complete (this may take a few minutes for the first time)

### 4. Build the Project

1. Go to **Build → Make Project** (or press Ctrl+F9 / Cmd+F9)
2. Ensure there are no build errors

### 5. Run the App

1. Connect an Android device or start an Android emulator
2. Select the "ui" module in the run configuration dropdown
3. Click the "Run" button (green play icon) or press Shift+F10

## Project Structure

This is a multi-module Android project:
- **`tunnel/`** - Core AmneziaWG tunnel functionality (Java/JNI)
- **`ui/`** - Android UI application (Kotlin)

## Common Issues and Solutions

### "SDK location not found" Error
- **Solution**: Open the project in Android Studio, which will automatically configure the SDK location

### "Submodule not found" Errors
- **Solution**: The submodules are already initialized. If you encounter issues, run:
  ```bash
  git submodule update --init --recursive
  ```

### Build Errors Related to NDK
- **Solution**: Install the NDK through Android Studio:
  1. Go to **Tools → SDK Manager**
  2. Click the "SDK Tools" tab
  3. Check "NDK (Side by side)" and click "Apply"

### Gradle Sync Issues
- **Solution**: Try these steps:
  1. **File → Invalidate Caches and Restart**
  2. Delete `.gradle` folder in project root
  3. **File → Sync Project with Gradle Files**

## Building APK

To build a release APK:
1. Go to **Build → Generate Signed Bundle / APK**
2. Choose "APK"
3. Create or select a keystore for signing
4. Choose "release" build variant
5. Click "Finish"

## Development Notes

- This project includes native code (Go/C) via JNI
- First build may take longer due to native compilation
- Make sure you have sufficient disk space (2-3GB) for all dependencies

## Need Help?

If you encounter any issues:
1. Check the official [Android Developer documentation](https://developer.android.com/studio)
2. Review the project's original [README.md](./README.md)
3. Check the [AmneziaWG repository](https://github.com/amnezia-vpn/amneziawg-android) for updates

## Success!

If everything is set up correctly, you should be able to:
- Build the project without errors
- Run the app on a device/emulator
- See the AmneziaWG Android UI interface