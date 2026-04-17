# Spec 006: UI Component - Log Modal

## Overview
A modal interface allowing users to log a game session, write a text review, and assign a star rating.

## Layout Rules (Tailwind)
- **Backdrop:** Fixed overlay, semi-transparent black (`bg-black/80`) with a blur effect.
- **Container:** Centered modal box, dark gray background (`bg-neutral-900`), rounded corners, border (`border-neutral-800`), max-width `md`.
- **Content:**
  - Header with the Game Title and a Close (X) button.
  - Date input (`type="date"`).
  - Textarea for the review (min-height 3 lines).
  - `StarRating` component integration.
- **Actions:** 'Cancel' (ghost button) and 'Save' (primary solid button).

## Props Contract
- `gameTitle`: string
- `isOpen`: boolean
- `onClose`: function