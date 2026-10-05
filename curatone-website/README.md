# CURATONE MUSIC ACADEMY – Phase 1
`npm install && npm run dev` → http://localhost:3000 · `npm run build` for production.
- Content & media paths: `lib/site.ts` (swap files in `public/images`, `public/videos`).
- AI: `app/api/ai/route.ts` calls Gemini using `GEMINI_API_KEY` from `.env.local`; academy facts live in `lib/knowledge.ts` (add confirmed fees/schedules there).
- Backend: `lib/services/enquiries.ts` (currently opens email; swap for Supabase/Firebase). 
- Instagram/WhatsApp are set in `site.social`; set the real domain in `site.url`.

## Portal (Supabase)
1. Create a free project at supabase.com. 2. SQL Editor: run `supabase/schema.sql`.
3. Copy `.env.example` to `.env.local` and fill URL + anon key (Project Settings > API).
4. Authentication > Users: add your account, then run the `update profiles set role='admin'...` line at the end of the schema file.
5. Add teachers/parents/students as Auth users, then set teacher roles (`update profiles set role='teacher' ...`; students: `'student'`).
6. In /staff (admin) add students, link parent/student accounts by email; teachers add comments, achievements, certificates.
Security: roles are stored in Postgres and enforced by Row Level Security (parents/students only read their linked children). Sign-ups default to `parent`; only admins change roles. Disable public sign-ups in Supabase Auth settings.
Not built yet: certificate PDF downloads, password-reset page, attendance history.
