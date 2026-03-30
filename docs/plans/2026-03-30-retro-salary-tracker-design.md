# Design Doc: Retro Salary Tracker (Super Mario Theme)

## OVERVIEW
A single-file static HTML application hosted on GitHub Pages that visualizes real-time earnings from a monthly salary. The UI features a Super Mario retro aesthetic (8-bit) with a question mark box dropping coins into a Mario pipe.

## USER EXPERIENCE (UX)
1. **INPUT**: User enters monthly gross salary (EUR) and **weekly working hours** (default 40).
2. **ACTION**: User clicks "START". 
   - A 'Power-up' sound plays.
   - Mario coin animation starts (falling from a yellow box into a green pipe).
   - Coin 'ding' sounds play periodically (togglable).
   - Real-time counters for **Gross** and **Net** euros increment up to cents.
3. **STOP**: User clicks "STOP".
   - Animation pauses.
   - Final earnings are displayed.
4. **MUTE**: User can toggle sound effects on/off.

## VISUAL DESIGN
- **Aesthetic**: Retro 8-bit pixel art.
- **Typography**: `Press Start 2P` (Google Fonts).
- **Color Palette**: 
  - Mario Yellow (#FFD700) for question box.
  - Mario Green (#43B047) for pipe.
  - High-contrast labels (White/Black).
- **Layout**: Center-aligned stage with a control panel at the bottom or top.
- **Components**:
  - `QuestionBox`: Animated 'jump' on coin drop.
  - `MarioPipe`: Static container for the 'pot'.
  - `CoinAnimation`: CSS/JS triggered sprite falling.
  - `StatBoard`: Dark 'retro-terminal' look for numbers.

## FUNCTIONAL SPECIFICATIONS
### 1. EARNINGS CALCULATION (DUTCH TAX 2024/2025)
- **Assumptions**: 
  - Weekly working hours input (e.g. 32, 36, 40).
  - Monthly gross salary input.
- **Gross Calculation**: 
  - Monthly hours = `(WeeklyHours * 52) / 12`.
  - Per-second rate = `(MonthlyGross / MonthlyHours) / 3600`.
- **Net Calculation**: 
  - Standard Dutch Box 1 brackets applied (simplified).
  - Algemene heffingskorting and Arbeidskorting included as rough estimates.
  - Netto factor is roughly `0.7` to `0.8` depending on income level.

### 2. AUDIO SYSTEM
- Uses Web Audio API or small base64/URL samples.
- **Sounds**:
  - `coin.mp3` (Mario Ding)
  - `start.mp3` (Level Start)
  - `stop.mp3` (Pipe Down)

### 3. PERSISTENCE
- LocalStorage saves the Gross Salary input for return visits.

## TECHNICAL ARCHITECTURE
- **Single File**: `index.html` contains all HTML, CSS, and JS.
- **Animations**: CSS `@keyframes` for the coin path; JS `setInterval` or `requestAnimationFrame` for logic.
- **Accessibility**: ARIA labels on buttons; high contrast ratios.

## ERROR HANDLING
- Validate salary input (must be numeric, positive).
- Handle browser autoplay policies for audio.
