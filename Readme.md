# InnovaSpectrix Website Documentation

This document outlines the architecture, foundational integrations, and critical modifications made to the **InnovaSpectrix** website. It serves as a reference for current maintainers and future developers to ensure smooth onboarding, preserve architectural decisions, and prevent regressions during updates.

---

# 🛠 Tech Stack & Rationale

## Frontend
- **HTML5, CSS3, Vanilla JavaScript**
- Heavy frameworks (React, Vue, etc.) were intentionally avoided to maintain ultra‑fast load times, high performance, and zero dependency overhead.

## Styling
- Custom CSS built around a **Glassmorphism Design System** using `backdrop-filter`.
- Global CSS Variables (`:root`) manage color palettes for easy global theming or future dark/light mode support.

## Hosting
- **GitHub Pages (Static Hosting)**
- Chosen for reliability, cost efficiency, and automated deployment without server management.

## Email Service
- **Zoho Mail** — `info@innovaspectrix.com`
- Acts as the primary professional inbox for client and partner communication.

## Form Handling Backend
- **FormSubmit.co (AJAX Integration)**
- Bridges static frontend forms with email delivery without requiring a backend server.

---

# 🚀 Recent Core Modifications & Fixes

## 1. Mobile Optimization & Critical Security Script Fix

### Hamburger Menu
- Custom JavaScript hamburger menu for viewports `max-width: 900px`.
- Uses absolute positioning and CSS transitions for smooth navigation animation without affecting layout flow.

### Responsive Grids
- `.products-grid`, `.app-grid`, `.team-grid` now collapse into single-column layouts on smaller screens.
- Prevents horizontal scrolling and improves readability.

### CRITICAL BUG FIX — Mobile Layout Thrashing
- A previous "Protect Source Code" script applied `blur(12px)` during window resize events.
- Mobile browsers trigger resize events while scrolling due to address bar behavior.
- Result: layout thrashing, UI glitches, and freezes.
- **Action Taken:** Script permanently removed.
- Basic right-click and F12 listeners remain for casual scraping deterrence.

---

## 2. UI / UX Enhancements

### Multi‑Layered Background System
The visual depth is created using three layers:

1. **Base Layer** — `image_50621f.jpg` fixed background image.
2. **Interactive Layer** — Animated HTML5 canvas (`#bg-canvas`) with floating particles.
3. **Overlay Layer** — `body::before` dark overlay (`rgba(5, 13, 26, 0.82)`) to ensure text contrast.

### Ergonomic Floating Controls
- WhatsApp, Phone Call, and "Scroll to Top" grouped in `.floating-wrapper`.
- Positioned bottom‑right to respect left‑to‑right reading patterns and avoid blocking content.

### Glassmorphism Contrast Improvements
- Darkened `rgba` backgrounds on content cards.
- Enhanced frosted-glass effect with `backdrop-filter: blur(12px)`.
- Improves typography clarity over neon backgrounds.

---

## 3. Team Structure Update

The Team section is divided into two CSS grid blocks:

### Core Team
- 4-column grid
- Includes CEO & Founder **Dr. M. Valliammai**, R&D Directors, and Sales roles.

### Scientific Advisory Board
- 2-column centered grid
- Includes **Dr. P. Chandrakumar** and **Dr. N. Vinodhkumar**.
- Dedicated advisor section increases academic credibility.

---

# ✉️ Contact Form Integration (FormSubmit)

Since GitHub Pages only serves static files and does not support PHP or Node.js, **FormSubmit.co** is used to capture form submissions and forward them to Zoho Mail.

## AJAX-Based Submission Flow

Standard HTML form submission redirects users to a generic external page. To preserve UX:

- JavaScript intercepts the submit event.
- `FormData` is converted into JSON.
- A background `fetch POST` request is sent.
- UI feedback includes:
  - Button disabled during submission
  - "Sending... → Inquiry Sent ✓" animation
  - Form reset after completion

---

## Anti-Spam Setup (Critical)

Publishing raw email addresses in frontend code exposes them to spambots. Use FormSubmit's **Random String Proxy**.

### Setup Workflow

1. In `index.html`, locate:
```
fetch('https://formsubmit.co/ajax/info@innovaspectrix.com', ...)
```

2. Submit the first test form.
3. FormSubmit sends an **Activation Email** to Zoho inbox.
4. After activation, a unique Random String is generated.

### Developer Action
Replace the email with the Random String:
```
fetch('https://formsubmit.co/ajax/a1b2c3d4e5f6g7h8i9j0', ...)
```

This hides the real email address while keeping functionality intact.

---

# 🔮 Notes for Future Upgrades & Migrations

## Moving to Backend Hosting (Hostinger / cPanel)

If migrated from GitHub Pages to a backend-capable host:

- Remove FormSubmit.co dependency.
- Rename `index.html` → `index.php`.
- Implement secure server-side form processing using PHP `mail()`.
- Improves privacy and long-term reliability.

---

## Asset Management & Image Updates

- Current background image: `image_50621f.jpg` located in root directory.
- If assets are moved (e.g., `/assets/images/`), update the `background-image: url('...')` path inside the root CSS block.
- Incorrect paths will cause fallback dark background to display alone.

---

# ✅ Maintainer Notes

- Preserve the lightweight architecture philosophy (no heavy JS frameworks unless absolutely required).
- Maintain accessibility and mobile stability when adding scripts.
- Avoid dimension-based resize logic that affects layout rendering.

---

**End of Documentation**

