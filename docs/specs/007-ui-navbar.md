# Spec 007: UI Component - Navbar

## Overview
A responsive, global top navigation bar providing access to primary platform sections, catalog search with real-time suggestions, quick log functionality, and user profile management.

## Visual & Layout Rules (Tailwind)
- **Container:** Fixed or sticky top bar (`sticky top-0 z-40 w-full`), backdrop blur with semi-transparent dark background (`bg-neutral-950/80 backdrop-blur-md border-b border-neutral-800`).
- **Inner Content:** Centered container with max-width matching the platform grid (`max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between gap-4`).
- **Brand (Left):**
  - SaveStateGG logo with retro badge or clean typography, linking to `/`.
  - Primary navigation links (`Games` -> `/games`, `Lists` -> `/lists`).
  - Active route highlighting (`text-white font-medium`) vs inactive links (`text-neutral-400 hover:text-white transition-colors`).
- **Search Bar (Center/Center-Right):**
  - Search input box with dark background (`bg-neutral-900 border border-neutral-800 rounded-lg px-3 py-1.5 text-sm text-white placeholder-neutral-500 focus:outline-none focus:ring-2 focus:ring-green-500`).
  - Leading magnifying glass icon (`Search` from Lucide).
  - Trailing keyboard shortcut indicator badge (`/` or `⌘K` / `Ctrl+K`).
  - Floating autocomplete dropdown (`bg-neutral-900 border border-neutral-800 rounded-lg shadow-2xl overflow-hidden mt-1`) presenting:
    - Game thumbnail cover (aspect ratio 3:4 or square thumbnail).
    - Game title and release year.
    - Keyboard arrow navigation (`ArrowUp` / `ArrowDown`) with highlighted item.
    - Footer row: *"Press Enter to see all results for '{query}'"*.
- **Actions & Profile (Right):**
  - **Quick Action (+ Log Button):** Prominent solid accent button (`bg-green-500 hover:bg-green-400 text-neutral-950 font-semibold px-3.5 py-1.5 rounded-md text-sm transition-colors flex items-center gap-1.5`).
  - **User Profile Area:**
    - If authenticated: Circular avatar with dropdown menu containing links to *Profile*, *Backlog*, *Lists*, and *Sign Out*.
    - If unauthenticated: Ghost button *Sign In* / *Join*.

## Interaction & Behavior
1. **Real-time Autocomplete:**
   - Triggers when user types >= 2 characters with 250ms debounce.
   - Selecting an item navigates directly to `/games/[id]`.
   - Submitting the search form (pressing `Enter` without an autocomplete selection) redirects to `/search?q={query}`.
2. **Quick Log Workflow (Letterboxd Pattern):**
   - Clicking `+ Log` opens a two-step modal:
     - **Step 1:** Focused search field (*"Which game did you play?"*) with quick results.
     - **Step 2:** Selecting a game transitions into the standard `LogModal` (Spec 006) with the selected game title pre-populated, enabling rating, review notes, and date confirmation.
3. **Keyboard Shortcuts:**
   - Pressing `/` or `Ctrl+K` / `Cmd+K` anywhere on the page focuses the search input.
   - Pressing `Escape` closes active dropdowns, search results, or menus.
4. **Mobile Adaptations (< 768px):**
   - Topbar displays Logo, Search toggle button, and Mobile Hamburger menu toggle.
   - Tapping the search icon opens a full-screen search overlay with auto-focused input.
   - Hamburger menu reveals navigation links (`Games`, `Lists`), the `+ Log` button, and profile options.

## Props Contract
- `currentUser?: { id: string; username: string; avatarUrl?: string } | null`
- `activePath?: string`
- `onSearch?: (query: string) => void`
- `onLogGame?: (gameTitle: string) => void`

## Acceptance Criteria
- Must render brand logo linking to `/`.
- Search field must support keyboard shortcut (`/` and `Ctrl+K` / `Cmd+K`) and dismiss with `Escape`.
- Autocomplete dropdown must show game thumbnail, title, and release year.
- `+ Log` action must allow searching and opening the `LogModal` without requiring the user to be on that game's page first.
- Mobile layout must collapse smoothly into search toggle and hamburger menu without horizontal overflow.
