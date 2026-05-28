# MediFlow

MediFlow is a Next.js medicine reminder and adherence dashboard. It helps users create a local account, manage medicine schedules, track taken/missed/skipped doses, monitor stock levels, view adherence charts, check openFDA drug information, and send reminder emails through EmailJS.

## Features

- Landing page with feature highlights, sign in, sign up, and light/dark theme support.
- Local account creation and sign in using `localStorage`, `sessionStorage`, and `bcryptjs` password hashing.
- Protected dashboard and settings pages through a client-side auth guard.
- Medicine management with dose times, frequency, dosage, notes, color tags, stock thresholds, refill dates, critical medicine flags, and archive/delete actions.
- Dose history tracking with taken, missed, and skipped states.
- Automatic missed-dose marking for past scheduled doses.
- Overdose protection based on each medicine's saved dose interval.
- Adherence charts powered by Recharts.
- Drag-and-drop medicine ordering and bulk delete.
- JSON backup import/export and CSV dose-history export.
- openFDA medicine suggestions, drug details, and interaction checks.
- Email reminder queue, escalation reminders, snooze links, daily/weekly summary support, and EmailJS test email configuration.
- Global settings for stock thresholds, dose interval defaults, notification recipients, quiet hours, and EmailJS credentials.

## Tech Stack

- Next.js 16
- React 18
- TypeScript
- Tailwind CSS
- Framer Motion
- Lucide React
- Recharts
- EmailJS
- bcryptjs

## Getting Started

Install dependencies:

```bash
npm install
```

Create a local environment file:

```bash
cp .env.example .env.local
```

Fill in EmailJS values if you want email reminders to work:

```env
NEXT_PUBLIC_EMAILJS_SERVICE_ID=your_service_id
NEXT_PUBLIC_EMAILJS_TEMPLATE_ID=your_template_id
NEXT_PUBLIC_EMAILJS_PUBLIC_KEY=your_public_key
```

Start the development server:

```bash
npm run dev
```

Open the app at `http://localhost:3000`.

## Scripts

```bash
npm run dev
```

Runs the app in development mode.

```bash
npm run build
```

Builds the production app.

```bash
npm run start
```

Starts the production server after a build.

```bash
npm run lint
```

Runs the Next.js lint command configured in `package.json`.

## Project Structure

```text
src/
  app/
    page.tsx              Landing page
    dashboard/page.tsx    Main medicine dashboard
    settings/page.tsx     Reminder and account settings
    signup/page.tsx       Account setup page
    layout.tsx            Root layout and metadata
    globals.css           Tailwind and global styles
  components/
    auth-guard.tsx        Client-side route protection
    auth-section.tsx      Sign-in form
    signup-form.tsx       Sign-up form
    hero.tsx              Landing hero
    features.tsx          Feature list
    landing-nav.tsx       Landing navigation
    theme-toggle.tsx      Light/dark mode control
    footer.tsx            Landing footer
  lib/
    auth.ts               Local auth/session helpers
    mediflow-db.ts        Local database, medicine, history, email, and import/export helpers
    mock-data.ts          Older mock medicine/adherence data
```

## Data Storage

This app is currently browser-only. User accounts, sessions, medicine data, history, settings, email queue items, and backups are stored in browser storage.

Important keys include:

- `mediflow_auth_user`
- `mediflow_session`
- `mediflow_db`
- `mediflow_db_backup`
- `mediflow_theme`

Because there is no backend database, data is tied to the current browser profile unless exported and imported manually.

## Email Reminders

Email reminders use EmailJS from the browser. Configure the public EmailJS values in `.env.local` or enter them on the settings page.

The EmailJS template should accept these variables:

```text
to_email
subject
message_html
```

## Medical Data Notice

MediFlow can show medicine information and possible interaction text from openFDA, but it is not a medical device and should not replace advice from a licensed healthcare professional.

## Notes

- The app seeds sample medicines on first load.
- Authentication and persistence are client-side only.
- The current `.gitignore` ignores `node_modules`; generated Next.js output such as `.next` should usually also be ignored before committing.
