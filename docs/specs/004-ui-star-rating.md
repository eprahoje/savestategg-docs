# Spec 004: UI Component - Star Rating

## Overview
A reusable component for the 0-5 stars rating system, mirroring the Letterboxd interaction model.

## Layout Rules
- Displays 5 star icons.
- Supports half-stars (e.g., 3.5, 4.5).
- Two modes: `readonly` (for displaying existing ratings) and `interactive` (for logging a new rating with hover effects).
- Color: Use a distinct accent color (e.g., Tailwind's `text-green-500` to match the reference).

## Props Contract
- `rating`: number (0 to 5)
- `isReadOnly`: boolean (default: true)
- `onRatingChange`: function (optional, returns the new rating number)