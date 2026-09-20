# Stage A Builder File: Visuals And GlassKit

Use with `followup_app_design_prompt.md`.

## Default Visuals

- Button preset: Crystal.
- Theme preset: Phone follows the device by default.
- Shell: white, black, and grey only.
- Lead status colours are semantic and always include written labels.
- Use three stable grey/silver background orbs.
- Use 14 dp edge padding, 10 dp card gap, 48 dp minimum touch targets, native phone font, Regular and SemiBold only, and no text below 12 sp.

## Effects

GlassKit presets are Minimal, Standard, and Full. Standard is the default. Reduce motion disables all effects. Pause loops when the screen is off or the app is backgrounded. If the phone lags, reduce blur first, then disable effects.

## Required Disclosure

The builder must state whether real backdrop blur was implemented with a free library and version, or whether translucent-card fallback was used and why.
