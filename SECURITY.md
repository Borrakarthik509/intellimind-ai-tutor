# Security Policy

## Dual Supabase Architecture

INTELLMIND utilizes a dual Supabase project architecture:
1. **Auth DB**: Handles authentication and login logging.
2. **Data DB**: Handles application data such as chat summaries and study plans.

### Critical Rule Regarding Secrets
- **Backend**: Uses the `service_role` key (or a highly privileged key) for `Auth DB` to bypass Row Level Security (RLS) for backend administration like verifying JWTs via `auth.get_user()`.
- **Frontend**: Must **never** contain a `service_role` key. The `frontend/login/js/env.js` file contains `sb_publishable_...` keys, which are safe for client-side use. Never place a backend `service_role` key in any frontend configuration file.

## Authorization Pattern (`verify_student_roll`)

We employ the `verify_student_roll` pattern to enforce strict data isolation. 
- The system extracts the email prefix (before the `@`) from the validated JWT and compares it to the `student_roll` provided in API calls. 
- This prevents horizontal privilege escalation (e.g., Student A cannot access or modify Student B's data by simply swapping the roll number in the request body).

## Anti-Inspection Shield (`security.js`)

The frontend includes an anti-inspection script (`shared/js/security.js`) that blocks right-clicking, standard DevTools shortcuts, and view-source commands. 
- **Note:** This is purely a UX deterrent to prevent casual inspection or scraping by students. It is **not** a true security layer. Real security is handled entirely server-side via JWT validation and role checks.

## Reporting a Vulnerability

If you discover any security vulnerabilities in the platform, please do not disclose them publicly.
Instead, email the vulnerability details to: **karthik.borra524@gmail.com**. We will aim to acknowledge and patch the issue as quickly as possible.

## Secret Rotation Procedure

If secrets (such as the `.env` file) are accidentally exposed or committed to version control, follow these steps immediately:
1. **Supabase**: Go to your Supabase Project Dashboard → Project Settings → API → Click **Roll keys** for both the Auth DB and Data DB projects.
2. **Gemini AI**: Go to Google Cloud Console → APIs & Services → Credentials → Delete the compromised API key and create a new one.
3. Update your backend `.env` file with the newly generated keys.
