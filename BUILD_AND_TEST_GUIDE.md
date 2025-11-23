# UI Refactoring - Build & Test Guide

## Quick Start Guide

### Step 1: Build the Project
```bash
./gradlew clean build
```

### Step 2: Run on Device/Emulator
```bash
./gradlew installDebug
```

## What Was Changed

### New Components
- **WaterCupView.kt** - Premium 3D water cup with animations

### Enhanced Components
- **GlassCard.kt** - Multi-layer glassmorphism with shadows
- **AnimationUtils.kt** - Premium spring and fade animations
- **Bottom Navigation** - Floating pill design with blur

### Dialog Changes
Both dialogs now feature:
- Premium glassmorphism styling
- Refined typography
- Better button styling
- Smooth animations on open/close

### Functionality Added
- **Reminder Interval Settings** - Users can now:
  - Select from predefined intervals (15, 30, 60, 90 min)
  - Set custom intervals (10-1440 minutes)
  - Changes apply immediately to reminders

## Testing Scenarios

### 1. Water Cup Animation
1. Open Home fragment
2. See water cup instead of wave
3. Click quick add buttons (250ml, 500ml, 750ml)
4. Water should fill smoothly
5. Water surface should wave

### 2. Dialog Styling
1. Click "Set Goal" button in Profile
2. Dialog should appear with glassmorphic background
3. Input field should have refined borders
4. Buttons should have proper styling
5. Same for "Add Water" dialog

### 3. Reminder Interval
1. Go to Profile fragment
2. Find "Reminder Interval" setting
3. Click on it
4. Dialog appears with options:
   - 15 minutes
   - 30 minutes
   - 60 minutes
   - 90 minutes
   - Custom input
5. Select or enter custom value
6. Value should update

### 4. Bottom Navigation
1. Check that bottom nav has:
   - Floating appearance (margins on sides)
   - Rounded corners (pill shape)
   - Smooth icon transitions
   - No harsh edges

### 5. Animations
1. Opening fragments should slide in
2. Cards should scale and fade
3. FAB should scale in
4. Water cup should animate smoothly
5. No janky or stuttering animations

## Known Considerations

### Platform Compatibility
- **Android 12+ (S)**: Full blur effects on dialogs
- **Android 11-**: Graceful fallback without blur
- **All**: Glassmorphism effects work on all API levels

### Performance
- Used ValueAnimator for smooth 60fps animations
- Custom canvas drawing for WaterCupView (no layout inflation)
- Efficient layer-based approach for bottom nav
- Reused animation utilities to avoid code duplication

### Visual Consistency
- All colors defined in colors.xml
- Consistent corner radii (14-24dp)
- Unified typography throughout
- Consistent spacing and padding

## Troubleshooting

### If Water Cup doesn't animate:
- Check if WaterCupView is in fragment_home.xml
- Verify setProgress() is called from updateProgress()
- Check logcat for inflation errors

### If Dialogs look plain:
- Verify GlassCard component is used
- Check if layout XML has correct root element
- Ensure colors.xml has all required colors

### If Bottom Nav doesn't look right:
- Verify bottom_nav_background.xml uses layer-list
- Check activity_main.xml has 12dp margins
- Ensure elevation is set (12dp)

### If Reminders don't work:
- Verify intervalContainer has correct ID
- Check if setOnClickListener is attached
- Verify UserPreferences.setReminderInterval() is called
- Check WorkManager permissions in manifest

## Next Steps (Optional Enhancements)

1. **True Gaussian Blur**
   - Implement RenderScript-based blur
   - Add to all dialogs for consistency

2. **Dynamic Colors**
   - Read wallpaper colors
   - Adapt glassmorphism palette

3. **More Animations**
   - Add parallax on scroll
   - Implement swipe gestures
   - Add haptic feedback

4. **Advanced Effects**
   - Implement glass morphism with shader
   - Add more interactive elements
   - Create premium micro-interactions

## Verification Checklist

- [ ] Project builds without errors
- [ ] APK installs successfully
- [ ] All fragments load without crashes
- [ ] Water cup displays and animates
- [ ] Dialogs show glassmorphic styling
- [ ] Bottom nav has floating pill appearance
- [ ] Reminder interval dialog works
- [ ] All buttons are clickable
- [ ] Animations play smoothly
- [ ] No console errors
- [ ] App doesn't crash on orientation change
- [ ] Dark mode (if applicable) works

## Command Reference

```bash
# Clean and build
./gradlew clean build

# Build and install debug APK
./gradlew installDebug

# Run specific activity
adb shell am start -n com.hydration.tracker/.ui.MainActivity

# View logs
adb logcat | grep "hydration\|WaterCupView\|GlassCard"

# Run tests
./gradlew test

# Create release build
./gradlew assembleRelease
```

## Support

For issues or questions about the refactoring:
1. Check the UI_REFACTORING_SUMMARY.md for complete change list
2. Review individual file changes
3. Check logcat for specific errors
4. Verify all string resources are defined
5. Ensure colors.xml has all required colors

