# My Expense Control

**Personal Expense Tracking & Unnecessary Spending Control App**

**My Expense Control** is a mobile-first, offline-ready Progressive Web App (PWA) designed exclusively for recording personal expenses in INR (`₹`) and curbing impulsive, avoidable spending. All financial records remain 100% private inside local IndexedDB storage on your device.

> **Expense-Only By Design:** This application intentionally excludes income, salary, revenue, profit, invoicing, and business accounting features.

---

## Project Folder Structure

```text
├── index.html                        # App entry HTML + PWA meta tags
├── public/
│   ├── icon.svg                      # Maskable vector PWA icon
│   ├── manifest.webmanifest          # Android home-screen PWA manifest
│   └── sw.js                         # Offline-first caching Service Worker
└── src/
    ├── main.tsx                      # React root & Service Worker registration
    ├── App.tsx                       # App shell, navigation, modals, theme sync
    ├── index.css                     # Tailwind CSS v4 + dark mode & mobile utilities
    ├── types/
    │   └── expense.ts                # Strict TypeScript models (Expense, Category, Backup, etc.)
    ├── constants/
    │   └── defaults.ts               # 16 default categories, payment methods, Hinglish hints
    ├── db/
    │   └── database.ts               # Dexie.js IndexedDB store, CRUD, backup validation & merge
    ├── utils/
    │   ├── formatters.ts             # INR formatting, Asia/Kolkata timezone math, CSV export
    │   └── analytics.ts              # Budget math, alerts, Expense Control & Month-End analytics
    └── components/
        ├── DashboardView.tsx         # Home summary, budgets, alerts, trends, recurring banner
        ├── ExpenseControlView.tsx    # Unnecessary spending control, streaks, savings simulator
        ├── AddExpenseView.tsx        # Fast entry, voice entry confirmation, inline category add
        ├── HistoryView.tsx           # Search, filters, sorting, daily/monthly subtotals, CSV
        ├── ReportsView.tsx           # Month-end analysis, MoM change, 5-point summary, exports
        ├── RecurringManagerModal.tsx # Recurring templates (confirm/skip when due)
        ├── SettingsView.tsx          # Budgets, category manager, JSON backup/restore, clear data
        ├── Charts.tsx                # Interactive daily, 6-month, and donut SVG charts
        ├── CategoryIcon.tsx          # Category icon badge renderer
        └── ConfirmDialog.tsx         # Confirmation modal for destructive actions
```

---

## Installation & Startup Instructions

1. **Install dependencies:**
   ```bash
   npm install
   ```
2. **Start local development server:**
   ```bash
   npm run dev
   ```
3. **Create a production static build:**
   ```bash
   npm run build
   ```
4. **Preview the production build locally:**
   ```bash
   npm run preview
   ```
   Deploy the generated `dist/` directory to any static host (Netlify, Vercel, Cloudflare Pages, GitHub Pages, or local server).

---

## Installing the PWA on Android

1. Open the deployed HTTPS URL in **Google Chrome** on your Android phone.
2. Tap **Install** in the top bar (if prompted), or tap Chrome's top-right menu (`⋮`) and select **Install app** / **Add to Home screen**.
3. Open **My Expense Control** from your Android home screen. After the first load, the Service Worker caches the application shell so it works completely offline.

---

## Exporting & Restoring Backups

- **Export Backup:** Open **Settings → Local Backup & Recovery (JSON)** and tap **Export Full JSON Backup**. Save the downloaded `.json` file safely.
- **Restore Backup:** Tap **Import JSON Backup File** and choose a backup file. The app validates the schema and displays a preview of total records, new unique records, and duplicates before modifying your database:
  - **Merge:** Keeps existing local records and imports only non-duplicate expenses.
  - **Replace All Existing Data:** Overwrites local storage after explicit confirmation.
- **Important Local Storage Notice:** Data is stored strictly on your device in IndexedDB and is **not** automatically uploaded to Google Drive or any server. Clearing browser site data or uninstalling without a saved JSON backup will erase local records.

---

## Verification & Testing Checklist

- [x] Add multiple expenses with decimal INR amounts (`₹1,250.50`) and prevent `<= 0` or duplicate rapid taps.
- [x] Refresh the page and confirm IndexedDB persistence.
- [x] Edit and delete expenses (with delete confirmation dialog).
- [x] Verify daily subtotals, today's total, and monthly totals in `Asia/Kolkata`.
- [x] Verify monthly budget remaining, overspending display, daily allowance, and category-wise budget alerts.
- [x] Verify Necessary vs. Unnecessary vs. Want calculations and 1-tap reclassification.
- [x] Verify month/year boundary transitions (`Dec ↔ Jan`, leap-year February).
- [x] Export and re-import JSON backup (Merge duplicate skipping + Replace confirmation).
- [x] Reject malformed JSON or non-positive backup records safely.
- [x] Export CSV reports from History and Reports.
- [x] Verify zero-expense months and unconfigured budget states without `NaN`/`Infinity`.
