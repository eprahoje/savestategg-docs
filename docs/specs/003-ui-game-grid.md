# Spec 003: UI Component - Game Grid

## Overview
Responsible for rendering a collection of `GameCard` components in a responsive grid layout.

## Layout Rules (Tailwind)
- Mobile: 2 columns.
- Tablet (md): 4 columns.
- Desktop (lg): 6 columns.
- Spacing: 1rem (gap-4).

## Props Contract
- `games`: Array of `Game` objects (Reference: Spec 001).