# Description
Vibe coded startpage

<img width="1290" height="742" alt="image" src="https://github.com/user-attachments/assets/5a5026fb-ea88-4d43-93e4-42566902eaba" />

## Functionality
- Typing shortcuts on the terminal takes you to that site.

# Pipeline
1. Extract the requirements using Qwen Studio and an Image of reference
2. Iterate on Google AI Studio (Gemini 3.8 FLash) until I got the desired result.

# Initial Qwen prompt
> Extract the requirements for a startpage (pure html, css and js) like the one in the image. Make sure to use a black/red color palette and to feature the weather and hour.
<img width="1913" height="918" alt="image" src="https://github.com/user-attachments/assets/f8519ecd-e6a3-4a4c-a588-8531d2f0d329" />

# Qwen Response

Build a personal browser startpage as a single self-contained HTML file (inline CSS and JS, no external frameworks or libraries). The page must be fully functional when opened directly in a browser.

## COLOR PALETTE (strict)
- Background: #0a0a0a (near-black) with optional dark gradient overlay
- Panel backgrounds: rgba(15, 15, 15, 0.88)
- Primary text: #e8e8e8
- Accent color: #cc0000 (red) — used for borders, hover states, clock colons, logo segment
- Secondary/labels: #888888
- Links hover: #ff3333
- Panel borders: 1px solid rgba(204, 0, 0, 0.25) with a 3px solid #cc0000 left accent bar

## LAYOUT
Use CSS Grid with 3 columns (1fr 2fr 1fr) and multiple rows, ~12px gap.
Panels have: padding 20px, border-radius 3px, backdrop-filter: blur(4px).
Make it responsive: stack panels vertically below 768px.

## PANELS

1. HOMEPAGE (top-left)
   - Title "HOMEPAGE" centered, uppercase, letter-spacing 4px
   - Large circular ring logo drawn with SVG or CSS conic-gradient, with one red segment (~15% of the ring)

2. SEARCH (top-center)
   - Title "SEARCH"
   - Full-width input, dark bg, red border on focus
   - On Enter, redirect to https://www.google.com/search?q=QUERY

3. MAIN / TERMINAL (top-right)
   - Title "Main"
   - Monospace text:
     Welcome Cel51
     Cel51@homepage:~$ █
   - Blinking cursor animation on the block character

4. GREETING + TIME + DATE + WEATHER (middle-left, one panel or stacked)
   - Dynamic greeting based on hour: GOOD MORNING / AFTERNOON / EVENING / NIGHT
   - Username "CEL51" in red below greeting
   - Label "TIME" → live 24h clock HH : MM : SS updating every second, red colons
   - Label "DATE" → DD . MM . YYYY
   - Label "WEATHER" → fetch from Open-Meteo API (no key needed):
     https://api.open-meteo.com/v1/forecast?latitude=LAT&longitude=LON&current_weather=true
     Use browser Geolocation API; fallback to latitude=46.95, longitude=7.45 (Bern, CH).
     Display: temperature (°C), weather condition text, and a Unicode weather icon (️ ☁️ 🌧️ ️ ⛅).
     Map WMO weather codes to icons/text. Refresh every 10 minutes.
     Show "Weather unavailable" on error.

5. BOOKMARKS (center, largest panel)
   - Title "BOOKMARKS"
   - 3-column sub-grid of categories, each with abbreviation (gray, monospace) + name (white link):
     WORK: cpnv→cpnv, gh→github, gm→gmail, bb→bitbucket
     SOCIAL: wa→whatsapp, hang→hangouts, fb→facebook, twi→twitter
     DOWNLOAD: tpb→thepiratebay, t411→T411
     REDDIT: fp→Frontpage, lol→LoL, 4ch→4chan, mh→Monster Hunter, ph→Programmer Humor
     4CHAN: b→/b/, wg→/wg/, g→/g/
     OTHERS: hgl→hugelol, hdl→hiddenlol
   - All links open in new tab, turn red on hover.

6. NEWS / LINKS (bottom-right)
   - Three uppercase links: "20MIN HI-TECH", "INTERNET IS BEAUTIFUL", "LISTEN TO THIS"
   - Letter-spaced, red on hover

## TYPOGRAPHY
- Titles: system sans-serif, uppercase, letter-spacing 4px, ~14px
- Clock: monospace (Courier New / Fira Code), ~32px, bold
- Bookmarks: abbreviations monospace 11px gray, names sans-serif 13px

## BACKGROUND
Use a dark CSS radial gradient as background (no external image needed):
background: radial-gradient(ellipse at center, #1a0505 0%, #0a0a0a 70%);

## OUTPUT
Return ONLY the complete HTML file. No explanations, no markdown wrappers around the code — just the raw <!DOCTYPE html> document ready to save as index.html and open in a browser.

# Initial Gemini prompt

Build a personal browser startpage as a single self-contained HTML file (inline CSS and JS, no external frameworks or libraries). The page must be fully functional when opened directly in a browser.
COLOR PALETTE (strict)
Background: #0a0a0a (near-black) with optional dark gradient overlay
Panel backgrounds: rgba(15, 15, 15, 0.88)
Primary text: #e8e8e8
Accent color: #cc0000 (red) — used for borders, hover states, clock colons, logo segment
Secondary/labels: #888888
Links hover: #ff3333
Panel borders: 1px solid rgba(204, 0, 0, 0.25) with a 3px solid #cc0000 left accent bar
LAYOUT
Use CSS Grid with 3 columns (1fr 2fr 1fr) and multiple rows, ~12px gap.
Panels have: padding 20px, border-radius 3px, backdrop-filter: blur(4px).
Make it responsive: stack panels vertically below 768px.
PANELS
HOMEPAGE (top-left)
Title "HOMEPAGE" centered, uppercase, letter-spacing 4px
Large circular ring logo drawn with SVG or CSS conic-gradient, with one red segment (~15% of the ring)
SEARCH (top-center)
Title "SEARCH"
Full-width input, dark bg, red border on focus
On Enter, redirect to https://www.google.com/search?q=QUERY
MAIN / TERMINAL (top-right)
Title "Main"
Monospace text:
Welcome Cel51
Cel51@homepage:~$ █
Blinking cursor animation on the block character
GREETING + TIME + DATE + WEATHER (middle-left, one panel or stacked)
Dynamic greeting based on hour: GOOD MORNING / AFTERNOON / EVENING / NIGHT
Username "CEL51" in red below greeting
Label "TIME" → live 24h clock HH : MM : SS updating every second, red colons
Label "DATE" → DD . MM . YYYY
Label "WEATHER" → fetch from Open-Meteo API (no key needed):
https://api.open-meteo.com/v1/forecast?latitude=LAT&longitude=LON&current_weather=true
Use browser Geolocation API; fallback to latitude=46.95, longitude=7.45 (Bern, CH).
Display: temperature (°C), weather condition text, and a Unicode weather icon (️ ☁️ 🌧️ ️ ⛅).
Map WMO weather codes to icons/text. Refresh every 10 minutes.
Show "Weather unavailable" on error.
BOOKMARKS (center, largest panel)
Title "BOOKMARKS"
3-column sub-grid of categories, each with abbreviation (gray, monospace) + name (white link):
WORK: gh→github, gm→gmail
SOCIAL: wa→whatsapp
All links open in new tab, turn red on hover.
NEWS / LINKS (bottom-right)
Three uppercase links: "20MIN HI-TECH", "INTERNET IS BEAUTIFUL", "LISTEN TO THIS"
Letter-spaced, red on hover
TYPOGRAPHY
Titles: system sans-serif, uppercase, letter-spacing 4px, ~14px
Clock: monospace (Courier New / Fira Code), ~32px, bold
Bookmarks: abbreviations monospace 11px gray, names sans-serif 13px
BACKGROUND
Use a dark CSS radial gradient as background (no external image needed):
background: radial-gradient(ellipse at center, #1a0505 0%, #0a0a0a 70%);
OUTPUT
Return ONLY the complete HTML file. No explanations, no markdown wrappers around the code — just the raw <!DOCTYPE html> document ready to save as index.html and open in a browser.

