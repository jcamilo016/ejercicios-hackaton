---
colors:
  primary: "#1A73E8"
  secondary: "#34A853"
  surface: "#FFFFFF"
  background: "#F8F9FA"
  text-primary: "#202124"
  text-secondary: "#5F6368"
  error: "#D93025"
typography:
  font-family-heading: "Inter, sans-serif"
  font-family-body: "Inter, sans-serif"
  scale: [12, 14, 16, 20, 24, 32, 40, 48]
  line-height-body: 1.6
  line-height-heading: 1.2
spacing:
  base: 8
  scale: [4, 8, 12, 16, 24, 32, 48, 64, 96]
border-radius:
  small: 4
  medium: 8
  large: 16
  pill: 9999
---

# Design System — MyApp

## Philosophy

Clean, functional interface. No excessive decoration. Clear visual hierarchy through size and typographic weight, not color. Color is reserved for actions and states.

## Components

### Buttons

- **Primary**: background `primary`, white text, border-radius `medium`, padding 12px 24px
- **Secondary**: transparent background, 1px `primary` border, `primary` text
- **Ghost**: no background, no border, `primary` text, hover with `background` fill

States: hover darkens 10%, disabled opacity 0.5, focus ring 2px offset.

### Cards

Background `surface`, border-radius `large`, padding 24px, subtle shadow (0 1px 3px rgba(0,0,0,0.1)). No visible border. Hover elevates shadow.

## Constraints

- Never use gradients on backgrounds
- Maximum 2 typographic weights per page (regular + bold)
- Do not use outline on inputs — use border that changes color on focus
- Icons: stroke only, never filled
