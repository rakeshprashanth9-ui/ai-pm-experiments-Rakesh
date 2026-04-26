# Product Requirement Document: Dark Theme Toggle for Memory Game

## 1. Purpose
Enable a dark theme option for the Memory Game so players can choose a lower-light visual style. This improves usability for evening play, accessibility, and personal preference.

## 2. Scope
- Add a persistent light/dark theme toggle UI control
- Apply dark theme colors across the entire game page
- Preserve current game state while switching themes
- Store user preference in `localStorage`
- Support keyboard and assistive technology

## 3. Background
The game is currently a single-page HTML/CSS/JS app using CSS custom properties in `:root`. This makes theme switching straightforward by updating variables and applying a theme class.

## 4. User Stories
- As a player, I want to switch to a dark theme so the game is easier to play at night.
- As a returning player, I want the game to remember my theme preference so I don’t have to switch it every time.
- As an accessibility user, I want the theme toggle to be keyboard operable and screen-reader friendly.

## 5. Requirements

### 5.1 Functional
- Add a visibly labeled toggle control: `Dark Theme` / `Dark Mode`
- Clicking the toggle switches between light and dark themes
- The theme toggle should be placed in the controls area or header for easy access
- The selected theme should persist across browser reloads using `localStorage`
- On page load, apply saved theme, or default to light theme if no preference exists
- If no saved preference exists, optionally initialize based on `prefers-color-scheme`

### 5.2 Visual Design
- Light theme remains the existing default appearance
- Dark theme must include:
  - Dark background for `body`, content cards, controls, and modal
  - Light text color and accessible contrast
  - Card front/back color adjustments to remain readable
  - Button and focus-state styling consistent with dark palette
- Ensure all UI components (grid, controls, modal, best scores) adapt to the theme

### 5.3 Accessibility
- The toggle must be reachable by keyboard
- Use ARIA attributes such as `aria-pressed`, `role="switch"`, or equivalent
- Provide a visible focus indicator
- Maintain text contrast ratios in both themes
- Preserve all existing keyboard/game controls

### 5.4 Technical
- Use CSS custom properties for both themes
- Implement theme switching by toggling a class on `document.documentElement` or `body`
- Example:
  - `body.dark-theme { --background-color: #121212; ... }`
- Avoid page reload when switching theme
- Do not change existing game logic or reset the timer/moves counter

## 6. Acceptance Criteria

### 6.1 Behavior
- [ ] A theme toggle appears in the UI
- [ ] Clicking it switches the page to dark theme
- [ ] Clicking again returns to light theme
- [ ] Theme selection persists after refresh
- [ ] Default loads as light theme when no preference exists
- [ ] Theme switch does not interfere with gameplay or reset progress

### 6.2 Visual
- [ ] Dark theme background is dark and consistent
- [ ] Text, buttons, cards, modal, and controls are legible
- [ ] Dark theme uses accessible contrast ratios
- [ ] All UI elements adapt correctly to theme changes

### 6.3 Accessibility
- [ ] The toggle is keyboard operable
- [ ] Screen readers announce the toggle state
- [ ] Focus state is visible on the toggle control
- [ ] Existing keyboard navigation remains intact

## 7. Implementation Notes
- Update CSS in `memory-game.html` using theme variables:
  - `--background-color`
  - `--text-color`
  - `--card-back`
  - `--card-front`
  - `--primary-color`
  - `--success-color`
- Add a toggle button near the game controls:
  - `<button id="theme-toggle" aria-pressed="false">Dark Mode</button>`
- Add JS logic:
  - `const themeToggle = document.getElementById('theme-toggle')`
  - `const savedTheme = localStorage.getItem('theme')`
  - `document.documentElement.classList.toggle('dark-theme', savedTheme === 'dark')`
  - `themeToggle.addEventListener('click', ...)`

## 8. Testing
- Validate theme toggle toggles styles without reloading
- Confirm `localStorage` stores `theme=dark` or `theme=light`
- Verify on page refresh the theme is restored
- Test on desktop and mobile viewport widths
- Run keyboard-only navigation and screen reader state checks
- Check visual contrast with a tool like Chrome DevTools Lighthouse or Axe

## 9. Success Metrics
- Dark theme is accessible and visually consistent
- Theme persists correctly across sessions
- No regressions in game functionality
- Players can toggle without losing game progress
