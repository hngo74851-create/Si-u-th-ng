# CODEX MASTER PROMPT — SIEU THI DANG LUCKY GAME WEBSITE

You are a senior full-stack web developer. Build a complete, modern, secure, and production-ready lucky game website for **Sieu Thi Dang — Shop Dang Gi Cung Co**.

The website must include a customer-facing page, a separate admin dashboard, a lucky wheel, a random prize draw game, customer verification codes, prize management, audio settings, and permanent cloud database storage.

## 1. Project Requirements

- Inspect the existing project before making changes.
- If no project exists, initialize a new application.
- Implement fully functional features, not just static mockups.
- Write clean, maintainable, well-structured code.
- Test the application and fix errors before finishing.
- Use Vietnamese for all customer-facing website text.
- Use English for source code, variable names, comments, and technical documentation.

## 2. Recommended Technology Stack

Use:
- Next.js with TypeScript.
- Tailwind CSS for responsive styling.
- Supabase for cloud database, authentication, and file storage.
- Server-side API routes or server actions for all sensitive operations.
- Environment variables for private credentials.

Do not use browser localStorage as the primary database. Do not expose administrator passwords, service-role keys, or private credentials in frontend code.

## 3. Visual Design and User Experience

Create a premium, modern, playful Gen Z design inspired by transparent glassmorphism and the iPhone interface.

Requirements:
- Smooth animations and polished transitions.
- Beautiful gradients, glass panels, rounded cards, and modern typography.
- Clear Vietnamese labels and easy-to-use buttons.
- Responsive layouts for Android phones, iPhones, tablets, laptops, and desktop computers.
- Fast loading and accessible controls.
- A circular shop logo that administrators can upload or replace.
- Never invent a real shop logo if the original logo has not been provided.

Make the website feel like a professional mini-game platform rather than an ordinary business website.

## 4. Customer Registration and Verification

Before playing, customers must enter:
- Their full name.
- A four-digit customer code issued by the administrator.

The server must validate the code against the database.

Requirements:
- Codes must be exactly four digits, including leading zeros.
- Administrators can create, edit, disable, and manage customer codes.
- Prevent duplicate active codes.
- Reject invalid, disabled, or previously used codes.
- Never allow customers to create their own valid codes.
- Do not rely on frontend-only validation.

## 5. Game A — Lucky Wheel

Create an animated spinning wheel with a prominent **SPIN NOW** button.

Features:
- Realistic spinning animation.
- Smooth deceleration and accurate final positioning.
- Tick-tick-tick sound while spinning.
- A clear prize announcement displayed above the wheel or prominently over the wheel area, never hidden below it.
- Celebratory animations for winning outcomes.
- Disable repeated clicks while a spin is processing.
- Prevent users from changing the outcome by modifying browser JavaScript.

The server must select the result. The wheel animation must visually match the server-confirmed result.

## 6. Game B — Lucky Draw

Create a separate random draw game featuring an attractive lucky-draw box or draw bag.

Features:
- A **DRAW NOW** button.
- An animated ticket-drawing effect.
- A prominent result announcement.
- Optional celebration effects and sounds.
- A responsive layout consistent with the lucky wheel.

Both games must share the same customer-code system. A customer who has already played either game must not be able to play the other game with the same code.

## 7. Prize List and Winning Configuration

Display the following six prize slots:

1. Better Luck Next Time
2. Better Luck Next Time
3. Better Luck Next Time
4. Win 5,000 VND
5. Free Shipping
6. Choose a Gift Worth Less Than 20,000 VND

Preserve all six slots in the visual prize configuration.

The administrator must be able to:
- Enable or disable individual prizes.
- Configure winning weights.
- Edit prize names.
- Upload prize images.
- Configure prize limits where appropriate.
- Save all changes permanently to the database.

Default configuration should prioritize the three “Better Luck Next Time” slots. Only prizes explicitly enabled by the administrator should be eligible to win.

The 5,000 VND prize, free shipping, and gift under 20,000 VND must be configurable.

Important:
- Select and validate the result on the server.
- Store the confirmed result in the database.
- Do not trust a prize result submitted by the browser.
- Never allow the frontend to override the winning result.
- Validate prize availability and limits before confirming a win.

## 8. Separate Admin Dashboard

Create a separate administrator page at `/admin`.

The dashboard must require secure authentication. Do not hardcode an administrator password in frontend JavaScript or commit credentials to the repository.

Security requirements:
- Ask the administrator to authenticate whenever they open a new admin session.
- Do not persist an admin login indefinitely across visits.
- Configure appropriate session expiration and secure logout behavior.
- Use secure, server-side authentication and authorization.
- Protect all administrative API endpoints.

### A. Customer Management

Allow administrators to:
- Add customers.
- Enter customer names.
- Generate unique four-digit codes.
- Edit customer information and codes.
- Disable or reactivate codes.
- Search customers.
- View used and unused codes.
- View each customer's game history.

Ensure that code changes are validated and recorded in the audit log.

### B. Game History

Display:
- Customer name.
- Customer code, masked when full visibility is unnecessary.
- Game type.
- Confirmed prize.
- Play date and time.
- Game status.

Include:
- Search and filtering.
- Sorting.
- Pagination.
- CSV export.

Store history permanently until an authorized administrator deletes it.

### C. Prize Management

Allow administrators to:
- Add, edit, and remove prizes.
- Change prize names and images.
- Enable or disable prizes.
- Adjust winning weights.
- Configure prize limits.
- Save changes to the cloud database.

### D. Logo, Images, and Audio

Allow administrators to:
- Upload or replace the circular shop logo.
- Upload backgrounds and prize images.
- Upload MP3 files for spinning, drawing, and winning sounds.
- Preview sounds before saving.
- Enable or disable individual sound effects.
- Replace uploaded files without editing source code.

### E. Shop Settings

Provide settings for:
- Shop name.
- Shop tagline: “Shop Dang Gi Cung Co”.
- Game availability.
- Prize configuration.
- Audio settings.
- Logo and visual assets.
- Customer-code rules.

Include a gear icon for accessing settings.

## 9. Audio and Vietnamese Announcements

Audio behavior:
- Play ticking sounds while the wheel spins.
- Play appropriate sounds when the wheel stops or a draw finishes.
- Support natural Vietnamese voice announcements for winning prizes.
- Never play a default English voice announcement.
- Prevent duplicate or overlapping announcements.
- Allow administrators to upload custom Vietnamese MP3 announcements.
- If no announcement audio exists, display the result visually without generating an English announcement.
- Respect browser autoplay restrictions.

## 10. Security and Anti-Cheating

This section is mandatory.

Implement:
- Server-side customer-code validation.
- Server-side prize selection.
- Server-side authorization for every admin operation.
- Database-level access policies.
- Rate limiting for code validation and game requests.
- Protection against brute-force attempts.
- Input validation and sanitization.
- Secure handling of uploaded files.
- Audit logs for important administrative actions.

A customer code must be usable for only one successful game across the entire website.

Use an atomic database transaction, database function, or equivalent concurrency-safe operation to claim the code and record the game result. Two simultaneous requests using the same code must never create two successful plays.

Do not rely on:
- Hidden buttons.
- Hidden admin URLs.
- Client-side password checks.
- Client-side prize selection.
- localStorage flags.
- Frontend-only used-code tracking.

Do not expose private customer data to other customers.

## 11. Cloud Database and Permanent Storage

Design database tables for:
- Customers and customer codes.
- Code usage status.
- Game sessions and results.
- Prize definitions and winning weights.
- Shop settings.
- Uploaded assets.
- Administrator accounts and audit logs.

Requirements:
- Persist data across page refreshes, browsers, and devices.
- Use appropriate database indexes and constraints.
- Apply least-privilege access policies.
- Protect private information.
- Support reliable backup and recovery procedures.
- Make configuration changes available across devices.
- Never claim data is permanently stored unless the cloud database is actually configured.

## 12. Deployment and URLs

Create these routes:
- Customer website: `/`
- Admin dashboard: `/admin`

Prepare the project for deployment on Vercel with Supabase.

Provide:
- Database schema and migration files.
- A safe `.env.example` containing placeholders only.
- Setup instructions.
- Deployment instructions.
- Environment variable configuration.
- Instructions for creating the first administrator securely.

Do not claim the website is publicly accessible until it has actually been deployed and verified.

## 13. Testing Requirements

Test the following cases:

1. A valid unused customer code can play.
2. An invalid code is rejected.
3. A used code cannot play again.
4. A code used for the wheel cannot be used for the draw game.
5. Concurrent requests using the same code cannot create multiple valid plays.
6. The recorded prize matches the animation and announcement.
7. Prize configuration persists after refreshing the page.
8. Uploaded logos and sounds remain available across devices.
9. Unauthenticated users cannot access administrative operations.
10. Customers cannot read or modify private customer data.
11. The website works on mobile and desktop.
12. No private passwords or secret API keys appear in frontend bundles.

Fix discovered issues before reporting completion.

## 14. Final Deliverables

Provide:
- Complete source code.
- Clear project structure.
- Database schema and migrations.
- `.env.example`.
- Installation and local development instructions.
- Secure administrator setup instructions.
- Deployment instructions for Vercel and Supabase.
- Automated tests for important security and game logic.
- A list of completed features and actual test results.
- Instructions for backup, recovery, and maintenance.

Start by inspecting the current project. Then implement the complete application, run the tests, fix errors, and prepare it for deployment.

Do not stop after writing a plan. Do not provide only sample code. Build the actual working project and clearly identify any external setup that still requires my action.