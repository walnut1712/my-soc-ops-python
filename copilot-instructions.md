# Copilot Instructions for Soc Ops

This document provides guidance for AI coding assistants working on the Soc Ops project.

## Project Overview

**Soc Ops** is a social bingo game designed for mixers and icebreaker events. Players find someone who matches each square and mark it off. The application uses:

- **Backend**: Python FastAPI with async Jinja2 templating
- **Frontend**: HTMX for dynamic interactions, vanilla JavaScript
- **Testing**: Pytest with 25+ comprehensive tests
- **Code Quality**: Ruff linting with type hints (Python 3.13+)

## Design Guide

### Design Philosophy

Soc Ops uses a **skeuomorphic, handcrafted aesthetic** inspired by paper cards, stickers, and chalkboards. This creates a warm, friendly, and tactile visual experience.

### Color Palette

**Core Colors:**

- **Cream**: `#fef9f3` - Primary background, warm and inviting
- **Paper White**: `#f5f1ed` - Secondary background, slightly darker
- **Tan**: `#e8dcc4` - Subtle accent, mid-tone
- **Kraft Brown**: `#8b7355` - Text and borders, earthy and grounded
- **Chalkboard**: `#2b2b2b` - Dark text and header backgrounds

**Sticker Colors (for buttons, highlights):**

- **Red**: `#ff4444` - Primary action color, energetic
- **Pink**: `#ff9fb2` - Secondary accent
- **Blue**: `#a8d8ff` - Tertiary accent
- **Green**: `#90ee90` - Additional accent
- **Purple**: `#d8bfd8` - Additional accent
- **Orange**: `#ffb347` - Additional accent

**Shadow Colors:**

- **Shadow Dark**: `#3a3a3a` - Dark shadow for 3D depth
- **Shadow Light**: `rgba(255, 255, 255, 0.3)` - Light inset shadow for highlights

### Typography

- **Handwritten Fonts**: `'Comic Sans MS'`, `'Segoe Print'`, `'Chalkboard SE'`
  - Creates playful, informal, human touch
  - Used for headings, buttons, interactive elements
- **Serif/Sans-serif Fallbacks**: System fonts for body text and accessibility
- **Text Effects**:
  - Headlines: Text shadow `2px 2px 4px rgba(0,0,0,0.3)` for depth
  - Chalkboard text: `1px 1px 0px rgba(0,0,0,0.5)` for carved effect

### Components

#### Buttons (`.btn-primary`)

- Background: Bright sticker color (red by default)
- Border: 3px solid chalkboard color
- Padding: 1rem 2rem with curved corners (1rem border-radius)
- Shadow: Dual shadow for 3D effect
  - Dark shadow: `4px 4px 0px var(--shadow-dark)`
  - Light inset: `6px 6px 12px var(--shadow-light)`
- On Hover: Lift effect with `translateY(-4px)`, enhanced shadow
- On Active: Subtle press effect with minimal lift, reduced shadow
- Font: Bold Comic Sans, 1.1rem size

#### Paper Cards (`.card-paper`)

- Background: Gradient from cream to paper-white
- Border: 2px dashed kraft-brown (torn paper effect)
- Padding: 1.5rem for breathing room
- Shadow: 5px 5px depth with dual shadow styling
- Transform: Subtle rotation (±1deg) for organic feel
- Border-radius: 1.25rem for rounded organic corners

#### Sticker Buttons (`.sticker-btn`)

- Same styling as `.btn-primary`
- Rotation variants available per color class
- Used for interactive elements throughout the game

#### Chalkboard Sections (`.chalkboard`)

- Background: Dark gradient (charcoal to blackboard)
- Border: 3px solid dark edge
- Text: Light gray on dark background
- List items: Checkmark/pencil icon prefix (`✎`)
- Box-shadow: Inset shadow for carved/recessed effect

### Effects & Animations

#### Shadows

- **3D Cards & Buttons**: `4px-8px 4px-8px 0px` dark shadow + `6px-12px 12px-20px` light shadow
- **Inset Effects**: `inset 0 0 10px rgba(0,0,0,0.5)` for depth
- **Paper Texture**: `repeating-linear-gradient` for crosshatch pattern overlay

#### Animations (Keyframes)

- **wobble**: ±2° rotation oscillation - used for celebratory elements
- **bounce-sticker**: Vertical bounce with subtle rotation - playful movement
- **slide-in-paper**: Entrance from left with rotation and fade
- **sticker-pop**: Scale and rotate pop animation for modals
- **wiggle**: Skew animation for attention-drawing
- **fade-in**: Simple opacity entrance

#### Paper Texture

- Applied globally via `repeating-linear-gradient`
- Creates subtle crosshatch pattern across backgrounds
- Enhances tactile, handcrafted feel

### Layout & Spacing

- **Padding**: Generous (1.5rem-2rem) for breathing room
- **Gaps**: 0.5rem (gap-2) between interactive elements
- **Containers**: Flex-based with centered content
- **Max-width**: Limited for comfortable reading and interaction

### Accessibility

- Maintain sufficient color contrast between text and background
- Buttons have clear focus states with enhanced shadows
- Animation is smooth but not excessive (0.3s-0.6s duration)
- Avoid animation on critical information—use only for delightful moments
- Use semantic HTML (button, a, h1-h6)

## Coding Conventions

### Python/FastAPI

- Type hints on all functions and methods
- Use `async`/`await` for route handlers
- Docstrings for complex logic
- 99-100 character line length (per ruff config)

### HTML/Templates

- Use Jinja2 for server-side rendering
- HTMX attributes for dynamic interactions (`hx-post`, `hx-swap`)
- Semantic HTML structure (landmarks, proper heading hierarchy)
- CSS classes follow BEM-like naming for clarity

### CSS

- Use CSS variables (defined in `:root`) for theming
- Group styles by component or functionality
- Comment sections: "/_ SECTION NAME _/" on their own lines
- Keyframes defined near animation utilities
- Responsive design with mobile-first approach

### Testing

- Write tests for all API endpoints
- Cover happy path and edge cases
- Use descriptive test function names
- Keep test fixtures minimal and reusable

## Implementation Priority

When extending the design:

1. **Maintain color consistency** - Use the defined palette exclusively
2. **Preserve handcrafted feel** - Prefer organic curves, shadows, and playful fonts
3. **Enhance tactile experience** - Use textures, shadows, and subtle animations
4. **Support accessibility** - Ensure interactive elements are clearly defined
5. **Keep it lightweight** - Minimize animations for core functionality, reserve bounce/wobble for celebrations

## Related Files

- Design system: [app/static/css/app.css](app/static/css/app.css)
- CSS utilities: [.github/instructions/css-utilities.instructions.md](.github/instructions/css-utilities.instructions.md)
- Frontend design skill: [.github/instructions/frontend-design.instructions.md](.github/instructions/frontend-design.instructions.md)
- Main template: [app/templates/base.html](app/templates/base.html)
- Game components: [app/templates/components/](app/templates/components/)
