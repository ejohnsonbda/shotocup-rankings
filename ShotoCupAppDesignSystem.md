# Shoto Cup App Design System

This document outlines the design tokens, component patterns, and architectural conventions used in the Tatami Floor Mapper app. This system is designed to create a premium, "designer-app" aesthetic with a deep dark mode, glassmorphism, and high-contrast vibrant accents. Use these guidelines to replicate this look and feel across other Shoto Cup applications.

---

## 1. Core Design Tokens

The foundation of the design system relies on a strict set of CSS custom properties (variables) defined at the `:root` level.

### Colors

| Token | Hex / RGBA | Usage |
|---|---|---|
| `--bg` | `#080810` | The deep, dark foundational background colour. |
| `--surface-1` | `rgba(14, 14, 22, 0.96)` | Primary card backgrounds (glassmorphism base). |
| `--surface-2` | `rgba(20, 20, 32, 0.92)` | Secondary nested surfaces. |
| `--surface-3` | `#0d0d18` | Solid dark surfaces (inputs, inner boards, stat cards). |
| `--border` | `rgba(255, 255, 255, 0.07)` | Subtle borders for cards and dividers. |
| `--border-hover` | `rgba(255, 255, 255, 0.14)` | Highlighted borders on hover states. |
| `--text` | `#f0f0ff` | Primary white text with a slight cool tint. |
| `--text-2` | `#9898b8` | Secondary muted text (descriptions, labels). |
| `--text-3` | `#5a5a7a` | Tertiary text (placeholders, hints, disabled states). |
| `--accent` | `#e03030` | Primary brand red. |
| `--accent-glow` | `rgba(224, 48, 48, 0.22)` | Soft red glow for shadows and highlights. |
| `--accent-2` | `#3060e8` | Secondary brand blue. |
| `--accent-2-glow` | `rgba(48, 96, 232, 0.18)` | Soft blue glow. |
| `--green` | `#22c55e` | Success states and positive stats. |
| `--amber` | `#f59e0b` | Warning states. |

### Typography

- **Font Family:** `'Inter', system-ui, sans-serif`
- **Weights:** 300 (Light), 400 (Regular), 500 (Medium), 600 (SemiBold), 700 (Bold), 800 (ExtraBold), 900 (Black).
- **Scale & Hierarchy:**
  - **Hero Title:** `clamp(3rem, 7vw, 6.2rem)`, Weight: 900, Tracking: `-0.04em`.
  - **App Title (H1):** `clamp(2.2rem, 3.5vw, 3.4rem)`, Weight: 900, Tracking: `-0.03em`.
  - **Card Titles:** `1.05rem`, Weight: 800, Tracking: `-0.01em`.
  - **Labels / Eyebrows:** `0.72rem - 0.82rem`, Weight: 700, Tracking: `0.08em - 0.14em`, Uppercase.

### Geometry & Shadows

| Token | Value | Usage |
|---|---|---|
| `--radius-xl` | `28px` | Main application cards. |
| `--radius-lg` | `20px` | Inner panels and boards. |
| `--radius-md` | `14px` | Inputs, buttons, and stat cards. |
| `--radius-sm` | `10px` | Small buttons, icons, and grid cells. |
| `--shadow-card` | `0 24px 64px rgba(0,0,0,0.55), 0 2px 0 rgba(255,255,255,0.04) inset` | Deep drop shadow with a subtle top inner highlight for glassmorphism. |
| `--shadow-btn` | `0 4px 20px rgba(0,0,0,0.4)` | Standard button shadow. |
| `--transition` | `0.18s cubic-bezier(0.4,0,0.2,1)` | Snappy, modern animation curve for all hover states. |

---

## 2. Layout Patterns

### Background System
The app uses a layered background approach to create depth:
1. **Solid Base:** `--bg` (`#080810`).
2. **Mesh Gradients:** Fixed radial gradients (`.bg-mesh`) in red, blue, and white placed at the corners and centre to create soft ambient lighting.
3. **Grid Overlay:** A subtle fixed CSS grid pattern (`.bg-grid`) using linear gradients and masked with a radial gradient so it fades out at the edges.

### Hero Section (`.hero`)
- **Full Bleed:** Minimum height of `88vh`.
- **Background Image:** Absolute positioned image with `cover` sizing and a slow scale animation (`transform: scale(1.04)` to `scale(1)`).
- **Overlays:** A diagonal gradient overlay combining navy and dark red, topped with a subtle SVG noise texture (`opacity: 0.35`).
- **Fade:** A bottom linear gradient (`.hero-fade`) transitioning from transparent to `--bg` to blend seamlessly into the app section.

### App Grid (`.main-grid`)
- A responsive CSS grid.
- **Desktop:** Two columns: `380px minmax(0, 1fr)`.
- **Tablet/Mobile:** Stacks into a single column (`1fr`) at `1024px` and below.

---

## 3. UI Components

### Glassmorphism Cards (`.card`)
The primary container for tools and content.
- **Background:** `--surface-1` with `backdrop-filter: blur(16px)`.
- **Border:** `1px solid var(--border)`.
- **Border Radius:** `--radius-xl`.
- **Shadow:** `--shadow-card`.
- **Structure:** Divided into `.card-header` (with bottom border) and `.card-body`.

### Form Fields
- **Container:** `.field` wrapper with a `.field-label` (uppercase, tracked out text).
- **Inputs & Selects:**
  - Background: `--surface-3`.
  - Padding: `12px 14px`.
  - Border Radius: `--radius-md`.
  - **Focus State:** Red border (`rgba(224,48,48,0.5)`), a soft red box-shadow ring, and a slightly darker background (`rgba(14,14,22,0.98)`).
- **Suffixes:** Absolute positioned text (e.g., "mats", "R", "C") inside an `.input-wrap`.

### Buttons
Buttons use a shared geometric foundation with distinct visual styles.

| Style | Class | Appearance |
|---|---|---|
| **Primary** | `.btn-primary` | Red diagonal gradient (`#e03030` to `#b81c1c`), white text, red drop shadow. Lifts on hover. |
| **Secondary (Blue)** | `.btn-blue` | Blue diagonal gradient (`#3060e8` to `#1a3fb0`), white text, blue drop shadow. Lifts on hover. |
| **Ghost** | `.btn-ghost` | Transparent background, subtle white border, muted text. On hover: white text, slightly visible background. |
| **PDF Export** | `.btn-pdf` | Tinted red background (`rgba(224,48,48,0.08)`), red border, red text. Used for secondary prominent actions. |

### Badges & Pills
- **Eyebrow Pill:** Used in the hero (`.hero-eyebrow`). Pill-shaped, blurred background, uppercase text, featuring a pulsing CSS dot.
- **Status Badge:** Used in toolbars (`.toolbar-badge`). Small pill with a green or red static/pulsing dot to indicate system state.

### Stat Cards (`.stat-card`)
Used to display data points in a grid (`.stats-grid`).
- **Background:** `--surface-3`.
- **Border Radius:** `--radius-md`.
- **Typography:** `.stat-label` (uppercase, muted) and `.stat-value` (large, bold, white).
- **Value Accents:** Values can take modifier classes like `.accent` (red), `.blue`, or `.green` to highlight specific data types.

---

## 4. Architectural Conventions

1. **Vanilla HTML/CSS/JS:** The system is built without heavy frameworks to ensure maximum performance and portability. It relies on modern CSS features (Grid, Flexbox, Custom Properties, Clamp).
2. **Iconography:** The system relies heavily on native emojis (e.g., 🗺, ⚡, 🖌, 💡) or inline SVGs (for the PDF button) rather than external icon libraries, keeping the payload light.
3. **State Management:** A simple global `state` object in JavaScript manages the app's data (e.g., `unit`, `selectedColor`, `cells`), driving UI updates via dedicated render functions (`renderGrid()`, `renderStats()`).
4. **PDF Generation:** Utilises `jsPDF` for native PDF construction and `html2canvas` for capturing complex DOM elements (like the layout grid) as images.

---

*End of Design System Documentation.*
