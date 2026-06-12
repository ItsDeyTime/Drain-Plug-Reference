# Drain Plug Reference

A single-page, client-side automotive reference tool for drain plug torque specs, vehicle service data, and related maintenance notes. The application runs entirely in the browser and uses Supabase for authentication, session management, and shared custom entries.

---

## Overview

This project is a lightweight, fast reference system designed for quick lookup of vehicle drain plug torque specifications and related service information. It includes search, filtering, suggestion workflows, and admin-style editing features — all within a single `index.html` file.

Despite being a single-page application, it implements secure session handling, persistent login state, and remote data synchronization via Supabase.

---

## Key Features

### Secure Client-Side Architecture
- Removed inline `onclick` handlers to eliminate XSS risks
- Uses event delegation with `data-*` attributes for all interactive actions
- Proper HTML escaping based on context
- Safer string handling in dynamic UI generation

---

### Authentication & Session Management
- Supabase authentication integration
- Sessions stored in `localStorage`
- Automatic token refresh (1 minute before expiration)
- Automatic retry of failed requests after refresh
- Clean logout clears all session data

---

### Data Entry & Validation
- Year input normalization (handles en/em dashes and spacing)
- Strict validation for:
  - YYYY
  - YYYY-YYYY
- Rejects invalid years with user feedback instead of silently storing bad data

---

### UI / UX Improvements
- Login modal improvements:
  - Close button added
  - Click-outside-to-close behavior
  - Escape key support
  - Prevents stale deferred actions after cancellation
- Fixed missing `.modal-hint` styling
- Improved feedback messaging and state handling

---

### Data Handling Enhancements
- Torque values:
  - Displays "N/A — see notes" for valid zero-torque cases (e.g., EVs / plastic pan designs)
  - Allows 0 as a valid input for admin entries
- Suggestion system:
  - Fixed ID comparison issues for consistent status updates
- Custom entries now properly persist to Supabase instead of local-only storage

---

## Architecture Notes

- Fully client-side single-page application (`index.html`)
- Uses Supabase for:
  - Authentication
  - Suggestions table
  - Custom entry storage
- No backend server required

---

## Known Limitations / Design Decisions

- Vehicle dataset is intentionally untouched when correctness cannot be verified (e.g., questionable entries like “Scion iC”)
- Part numbers / SAP numbers are not editable via client:
  - Requires Supabase schema changes
- RLS (Row Level Security) policies should be reviewed:
  - Suggestion reads are anonymous in the current implementation
  - Write restrictions should be validated server-side

---

## Tech Stack

- HTML / CSS / Vanilla JavaScript
- Supabase (Auth + Database)
- LocalStorage (session persistence)

---

## Notes for Maintainers

This project prioritizes:
- correctness over guesswork in automotive data
- client-side safety (no inline JS execution patterns)
- resilience of session handling in unstable network conditions

---

## Future Improvements (Suggested)

- Split into modular JS files for maintainability
- Add server-side validation layer (or Edge Functions in Supabase)
- Expand schema for part numbers / SAP data
- Optional offline caching layer for field use

---

## License

Internal / private use unless otherwise specified.
