# CMake Build Error Fix Guide

## Problem: CXX1429 Error - Cannot find source file

### Error Description:
```
CMake Error at CMakeLists.txt:11 (add_executable):
  Cannot find source file: amneziawg-tools/src/wg-quick/android.c
```

## Root Cause:
This error occurs due to:
1. **Corrupted CMake cache** - Old build configurations interfering
2. **macOS-specific make path issues** - `${ANDROID_HOST_PREBUILTS}/bin/make` not properly resolved

## ✅ Fix Applied:

### 1. Cleaned Build Cache
- Removed `.cxx` directories
- Removed `tunnel/build` directory  
- Cleaned Gradle cache

### 2. Fixed CMakeLists.txt
**Changed:**
```cmake
COMMAND "${ANDROID_HOST_PREBUILTS}/bin/make"
```
**To:**
```cmake
COMMAND make
```

This uses the system's make command instead of relying on Android toolchain variables that might not be properly set on macOS.

## 🔧 Manual Steps (if needed):

### If you still get CMake errors:

1. **Clean Everything:**
   ```bash
   cd /path/to/your/project
   rm -rf tunnel/build
   rm -rf tunnel/.cxx
   rm -rf .gradle/caches
   ```

2. **In Android Studio:**
   - **File** → **Invalidate Caches and Restart**
   - Wait for restart
   - **File** → **Sync Project with Gradle Files**

3. **Force Clean Build:**
   - **Build** → **Clean Project**
   - **Build** → **Rebuild Project**

### If CMakeLists.txt was reverted:
```bash
# Restore the fix
sed -i.bak 's/"${ANDROID_HOST_PREBUILTS}\/bin\/make"/make/g' tunnel/tools/CMakeLists.txt
```

## ✅ Verification:

After applying the fix, you should see:
- No more "Cannot find source file" errors
- CMake configuration completes successfully
- Build progresses to native compilation stage

## Expected Build Process:

1. **Gradle Sync** (30-60 seconds)
2. **CMake Configuration** (1-2 minutes) 
3. **Native Compilation** (3-5 minutes)
   - Building libwg.so
   - Building libwg-quick.so  
   - Building libwg-go.so (Go components)
4. **APK Assembly** (1-2 minutes)

**Total first build time: 5-10 minutes**

## Still Having Issues?

### Check Prerequisites:
- ✅ **NDK installed** (Tools → SDK Manager → SDK Tools → NDK)
- ✅ **CMake installed** (Should be automatic with NDK)
- ✅ **Make available** (`which make` should return a path)
- ✅ **Go installed** (for libwg-go.so compilation)

### macOS-Specific:
- Install Xcode Command Line Tools: `xcode-select --install`  
- Install Homebrew make if needed: `brew install make`

### Verify Submodules:
```bash
git submodule status
# Should show:
# [commit] tunnel/tools/amneziawg-tools (version)
# [commit] tunnel/tools/elf-cleaner (version)
```

## Success Indicators:

✅ CMake configures without errors  
✅ Native libraries compile successfully  
✅ Build completes with "BUILD SUCCESSFUL"  
✅ APK can be generated and installed

The fix has been applied to your project and should resolve the build issues!