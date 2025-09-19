# Kitchen Automation - Daylight Behavior Issue & Fix

## The Problem

With your current light level at **53 lux**, the automation should be **blocking** the lights from turning on during the day, but you mentioned the lights are still on.

## Current Logic Analysis

Looking at your original flow:
```
Light Level Check:
- halt_if: "15"
- halt_if_compare: "gt" 
- This means: IF illuminance > 15 lux → HALT (don't turn on lights)
```

**At 53 lux (which is > 15 lux), the automation should be halting and NOT turning on lights.**

## Possible Reasons Lights Are Still On

1. **Manual Override Active**: Someone pressed a dimmer button, activating manual override
2. **Automation Disabled**: Hold gesture disabled the automation system
3. **Lights Already On**: Lights were turned on before motion detection
4. **Logic Error**: The halt condition might be inverted or not working properly

## The Fix

I recommend updating your light level threshold and adding better logging:

### Option 1: Increase Threshold (Recommended)
Change from 15 lux to 25 lux threshold:
- **< 25 lux**: Turn on lights (darker conditions)
- **≥ 25 lux**: Don't turn on lights (sufficient daylight)

### Option 2: Add Logging to Debug
Add logging nodes to see exactly what's happening:
- Log when motion is detected
- Log current light level
- Log why automation is blocked/proceeding

## Quick Fix for Your Current Flow

1. **Check Manual Override Status**:
   - Look at your Node-RED debug panel
   - Check if you see "manual override active" messages

2. **Check Current Light State**:
   - Are the lights physically on right now?
   - Did someone turn them on manually?

3. **Reset the System**:
   - Hold the OFF button on your dimmer (should enable automation)
   - Wait 45 minutes for any manual override to clear

## Recommended Settings

For a kitchen with 53 lux daylight:
```javascript
THRESHOLDS: {
    LIGHT_SENSOR_LUX: 30  // Increased from 15 to 30
}
```

This means:
- **< 30 lux**: Lights turn on (cloudy days, early morning, late afternoon)
- **≥ 30 lux**: Lights stay off (bright daylight - your current 53 lux situation)

## Debug Steps

1. **Check the debug panel** for recent messages
2. **Look for these specific messages**:
   - "Motion detected - Automation: true, Override: false"
   - "Motion automation blocked: manual override active"
   - "Motion blocked - too bright for daytime automation"

3. **If you see manual override messages**:
   - Hold OFF button on dimmer to re-enable automation
   - Or wait 45 minutes for automatic reset

The key issue is likely that either:
- Manual override is active (from previous dimmer use)
- The lights were already on from before
- The threshold needs adjustment for your lighting conditions

Would you like me to create a corrected flow file with the 25-30 lux threshold and better logging?
