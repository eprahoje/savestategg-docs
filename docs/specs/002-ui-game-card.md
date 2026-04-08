# Spec 002: UI Component - Game Card

## Overview
Displays summarized game information within the Homepage grid.

## Visual Elements
- Cover (Image): Aspect ratio 3:4.
- Title (Text): Truncated to 1 line if too long.
- Rating (Badge): Circle or label showing the score (e.g., 85).
- Overlay: Hover effect that highlights the card.

## Props Contract
- `game`: `Game` object (Reference: Spec 001).