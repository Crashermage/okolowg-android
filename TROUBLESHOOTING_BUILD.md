# Build Configuration Troubleshooting

## Problem: Limited Build Options in Android Studio

### Check These Steps:

#### 1. Verify Project Structure
**Expected modules:**
- `ui` (application) - Main app you can run
- `tunnel` (library) - Supporting library

**How to check:**
- Look at the Project panel on the left
- You should see both `ui` and `tunnel` folders

#### 2. Set Correct Run Configuration
**Step-by-step:**
1. Look at the top toolbar dropdown (next to the green play button)
2. It should show `ui` as an option
3. If you see `<No Configurations>` or only see `tunnel`:
   - Click the dropdown → "Edit Configurations..."
   - Click the "+" button → "Android App"
   - Name: `ui`
   - Module: `ui`
   - Click "OK"

#### 3. Check Build Variants Panel
**To open Build Variants:**
- **View** → **Tool Windows** → **Build Variants**
- OR click "Build Variants" tab (usually bottom-left)

**You should see:**
```
Module: ui
Build Variant: debug (dropdown with debug/release/googleplay)

Module: tunnel  
Build Variant: debug (dropdown with debug/release)
```

#### 4. Gradle Sync Issues
If you see sync errors:
1. **File** → **Sync Project with Gradle Files**
2. Wait for sync to complete
3. Check for any red error messages in "Build" panel

#### 5. SDK/NDK Configuration
This project requires:
- **Android SDK** (auto-configured by Android Studio)
- **NDK** (for native code compilation)

**To install NDK:**
1. **Tools** → **SDK Manager**
2. **SDK Tools** tab
3. Check "NDK (Side by side)"
4. Click "Apply"

## Quick Test:

1. **Select `ui` in run configuration dropdown**
2. **Click green play button**
3. **Choose an emulator or connected device**

## Expected Build Process:

1. **First build takes 5-10 minutes** (compiling native code)
2. **You should see:** "BUILD SUCCESSFUL" in Build panel
3. **App launches** on device/emulator with AmneziaWG interface

## Common Error Solutions:

### "No module selected"
- **Solution:** Select `ui` module in run configuration

### "SDK not found"
- **Solution:** Android Studio should auto-configure this. If not:
  - **File** → **Project Structure** → **SDK Location**

### "NDK not found" 
- **Solution:** Install NDK via SDK Manager (see step 5 above)

### "Submodule errors"
- **Solution:** 
  ```bash
  git submodule update --init --recursive
  ```

### "Gradle sync failed"
- **Solution:**
  1. **File** → **Invalidate Caches and Restart**
  2. Delete `.gradle` folder in project root
  3. **File** → **Sync Project with Gradle Files**

## Still Having Issues?

1. **Check Android Studio version** (2023.3+ recommended)
2. **Check available disk space** (need 2-3GB for dependencies)
3. **Try creating new AVD** (Android Virtual Device) if emulator issues
4. **Check internet connection** for downloading dependencies

## Success Indicators:

✅ `ui` appears in run configuration dropdown  
✅ Build Variants panel shows debug/release options  
✅ Green play button is enabled  
✅ No red errors in Build panel after sync  
✅ Project builds without errors