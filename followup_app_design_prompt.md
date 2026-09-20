# Siyaram CRM Follow-up App Design Prompt

Design and implement the next Siyaram CRM experience inside the existing React and Android application.

## Product Shape

The app is a fast, mobile-first real-estate CRM for daily follow-up work. Use the Siyaram monochrome liquid-glass visual language described below. Do not bring back blue, violet, gold, or amber branding. Keep the interface practical, touch-friendly, and optimized for repeated sales actions.

## Primary Navigation

Use a floating glass bottom navigation bar with five destinations:

1. **Aaj**
   - Daily command center.
   - Show a large count of today's actionable work.
   - Show a clear `Shuru karo` action.
   - Show the next calls, visits, messages, reviews, and overdue follow-ups.
   - Allow one-tap opening of the relevant client, project, or follow-up.

2. **Projects**
   - Show every project as a scannable card.
   - Display project name, status, location, client count, next milestone, and active follow-up count.
   - Open Project Detail/Edit.
   - Keep project link, documents, floor maps, contacts, features, milestones, recordings, and delete confirmation working.

3. **Leads**
   - Show lead/client list with search, status filters, colour chips, phone actions, and next follow-up state.
   - Open Client Profile on selection.
   - Keep Excel import available from this area.
   - Client Profile must support edit, follow-up, call, WhatsApp, recording, activity timeline, and confirmed delete.

4. **Visit**
   - Use the existing follow-up and site-visit workflow.
   - Group work by today, upcoming, overdue, calls, WhatsApp, meetings, and reviews.
   - Make the next action obvious and one tap away.

5. **Refer**
   - Use the existing tags/labels system as the referral and categorisation workspace unless a dedicated referral data model is introduced.
   - Keep colour labels, filtering, client/project association, and bulk actions functional.

## Opening From The Top

Keep these controls accessible from the top area:

- **Post-call card**: open as a bottom sheet after a call. It must support call outcome, notes, next action, next follow-up date, channel, and optional voice recording. Saving must create/update the correct communication log, client follow-up, and client next-follow-up fields.
- **Settings**: open from the top settings action. Preserve colour/accent names, follow-up day defaults, notification time, theme, offline mode, backup export/import, and restore behaviour.

## Excel Import Contract

The import flow must be deterministic and must not guess:

- `Name`, `Client`, or `Buyer Name` maps to Client Name.
- `Mob`, `Mobile`, `Phone`, or `Contact` maps to Mobile Number.
- Remove `+91`, country prefixes, spaces, brackets, hyphens, and a leading zero.
- Normalize valid Indian mobile numbers to exactly 10 digits.
- Detect duplicate mobiles within the file and against existing clients.
- Existing mobile numbers update the existing profile; never create a second profile.
- New mobiles create a new client profile.
- Link a project only when the project match is unambiguous.
- Mark unknown or ambiguous project values as `Needs Review`.
- Create follow-up records from valid follow-up data.
- Show a summary containing Total Records, New, Existing, Duplicates, Missing Data, and Needs Review.

## Safety And Data Integrity

- Client delete requires a confirmation dialog and must remove client-project links, follow-ups, communication logs, recordings, and stale references safely.
- Project delete requires a confirmation dialog and must clean client links, project recordings, follow-up references, communication references, documents, floor maps, contacts, features, and milestones safely.
- Do not hide errors with an error boundary. Fix root causes.
- Never use Reset Data as a workaround.
- Preserve backup/restore compatibility.
- Preserve calling, notification, recording, project, document, and follow-up functionality.

## Performance Requirements

- Do not parse localStorage on every render.
- Keep initial storage reads lazy and persistence effect-based.
- Memoize expensive dashboard, client, project, and follow-up calculations when safe.
- Avoid recalculating the complete client list for unrelated state changes.
- Keep Excel parsing asynchronous so the UI remains responsive.
- Avoid unnecessary provider-wide rerenders and repeated state updates.
- Keep large lists touch responsive.

## React Correctness

- Every hook must execute in the same order on every render.
- Never place hooks below loading, missing-record, or modal early returns.
- Validate Client Profile, Client List, Dashboard, Project Detail, import modal, and settings for hook-order violations.
- Do not suppress React errors. Test the actual route transitions: list -> profile -> refresh -> back -> project -> profile.

## Visual Direction

- Support exactly three appearance modes: `Light`, `Dark`, and `Phone`.
- `Phone` follows the operating system colour-scheme setting automatically.
- Expose the three choices in Settings as a clear Light / Dark / Phone control.
- Use a 500 ms soft colour transition when the appearance mode changes.
- The application shell uses only white, black, and grey tones. Do not use blue, violet, green, amber, orange, or other accent colours for decoration, navigation, backgrounds, borders, buttons, or active states.
- Colour is reserved for lead status meaning only: status dots, lead avatars, status chips, and pipeline bars may use semantic status colours.
- Red is reserved exclusively for Danger, forgotten/overdue leads, errors, destructive warnings, and red lead status. Never use red as a general accent.
- Status colours must communicate state rather than decorate the interface. Keep their labels and contrast accessible in both Light and Dark modes.
- Use floating glass navigation with readable active states and badges.
- Keep cards compact and scannable on mobile.
- Use icons inside icon actions and tooltips for unfamiliar icons.
- Keep destructive actions visually clear but not easy to trigger accidentally.
- Maintain responsive layouts for Android phone, tablet, and desktop.
- Do not introduce blue/purple or gold/amber branding, generic dashboard filler, or decorative UI that competes with the daily work queue.

### 6.2 Button Design Options

Choose exactly one button treatment for the product. The default is **Option 1: Crystal**.

| Option | Name | Key characteristic | Best for |
| --- | --- | --- | --- |
| 1 | **Crystal** | Solid black/white button with a thin, bright neutral edge. | Clearest reading and strongest Android reliability. **Default.** |
| 2 | **Mist** | More blurred glass, larger rounded corners, and soft grey contrast. | The calmest, quietest interface. |
| 3 | **Glass button** | Translucent glass button with a subtle light reflection along the edge. | The most Apple-like treatment; slightly lighter on Android. |

Button option rules:

- Keep button text and icons black, white, or grey only.
- Do not use a coloured glow, coloured border, or coloured active fill.
- Keep destructive buttons red only when they represent a destructive action.
- Keep the selected option consistent across bottom navigation, primary actions, cards, dialogs, and sheets.

### 6.3 Crystal Colour Tokens

Option 1 is the default. Use these exact values for the Crystal treatment:

| Token | Light | Dark |
| --- | --- | --- |
| Background | `#F7F7F8` | `#000000` |
| Text | `#0A0A0A` | `#FFFFFF` |
| Secondary text | `#6B6B70` | `#9A9AA0` |
| Button | `#0A0A0A` with white text | `#FFFFFF` with black text |
| Glass fill | White at 55% opacity | White at 8% opacity |
| Success tick | `#1D9E75` | `#5DCAA5` |

Use these exact neutral tokens for borders and supporting surfaces:

- `--ink: #0A0A0A`
- `--paper: #FFFFFF`
- `--background-light: #F7F7F8`
- `--background-dark: #000000`
- `--secondary-light: #6B6B70`
- `--secondary-dark: #9A9AA0`
- `--glass-light: rgba(255, 255, 255, 0.55)`
- `--glass-dark: rgba(255, 255, 255, 0.08)`
- `--success-light: #1D9E75`
- `--success-dark: #5DCAA5`
- `--danger: #C62828`

Lead status colours are semantic exceptions and may be defined separately for dot, avatar, chip, and pipeline-bar states. Red must use `--danger` and remain reserved for forgotten/overdue, error, danger, and red lead status.

## Verification Checklist

1. `npm install`
2. `npm run lint`
3. `npm run build:android`
4. Validate Android source and generated assets.
5. Check React hook order on Client Profile, Client List, Dashboard, and Project Detail.
6. Verify client delete confirmation and data cleanup.
7. Verify project delete confirmation and data cleanup.
8. Verify Excel import normalization, deduplication, update/create, project matching, and summary.
9. Verify profile creation/update and follow-up creation.
10. Check obvious rerender and localStorage performance issues.
11. Rebuild `siyaram-crm-final-source-2026-09-20.zip` because the GitHub workflow builds from that archive.
12. Commit and push the updated archive to `main`.
