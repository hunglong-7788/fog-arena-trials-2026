# FOG Arena Trials — FSC x Flame

Standalone esports/"Liên Quân"-themed Club Day minigame by FSC x Flame, FSchool Quy Nhơn. This is an original fan-made activity, unaffiliated with the game publisher.

## Feature set

- Six different challenge formats in a single short run (roughly 60 seconds):
  1. IQ Rush — 4-option quiz about team play and basic mechanics.
  2. Draft Room — composition and role selection.
  3. Shotcall — macro and objective decisions.
  4. Vision Memory — 4-symbol sequence recall after 2.7 seconds.
  5. Reaction Check — visually identify the golden target.
  6. Smite Clash — timing a moving indicator at a server-verified moment.
- Server-authoritative scoring through a Supabase Edge Function; never trust a client-submitted total.
- Separate Arena Trials best-by-codename leaderboard and operator event screen, Supabase Broadcast with polling fallback.
- No sign-in and no personally identifying student information requested.
- Practice offline if backend unavailable; practice scores never appear in the live leaderboard.
- Responsive and keyboard accessible. Reduced-motion CSS preference honored.

## Run locally

Serve the directory on HTTP, e.g. `python -m http.server 8080` and open `http://localhost:8080`.

## Deploy

1. Create a **new** Vercel project (do not overwrite FSC x Flame club portal or FOG Glitch Raid).
2. Upload the contents of this folder as static site files, or push them to a new GitHub repository and connect it to Vercel.
3. Set framework to **Other** (static), root directory to folder root; deploy.
4. Check API `https://sjwyrtgyuwqhhkpcsbuj.supabase.co/functions/v1/arena-trials?action=leaderboard` for `{ok:true}` and run end-to-end tests on mobile and PC before advertising the QR.
5. Print/share the deployment URL as a QR for Booth 2.

## Backend environment and release gate

The current API (`arena-trials`) and prefixed tables (`public.arena_v1_sessions`, `public.arena_v1_control`) have been deployed to the user's **existing Supabase non-production project** `sjwyrtgyuwqhhkpcsbuj`. No tables in the separate club Production project were modified. This backend is useful for demo/preview only unless user agrees to an event-dedicated production backend. Project remains under the account owner's control. Edge Function name and table prefix must be reserved solely for Arena Trials.

- RLS enabled and public table access revoked; Edge Function uses an injected service-role credential to compute scores server-side.
- Server-issued tasks carry secret answers only in protected database rows. Browser sends selected choices, not scores.
- One answer per stage enforced using conditional database update; session replay rejected.
- Device/IP hashed and subject to basic 30-minute request caps; this is abuse mitigation, not perfect anti-cheat. There is no strong identity without participant verification.
- Public Edge Function is intentionally `verify_jwt=false` to allow anonymous play; only supports `start`, `answer`, and read-only `leaderboard` actions. No public admin mutations.
- Nickname uniqueness is not verified; for prize awards, staff should independently confirm winners and retain a paper/booth backup.
- Supabase Broadcast shares *refresh signals only*; public leaderboard API returns nicknames, scores and timestamps, no device hash or secret answers.
- Deployment of this source to a new Vercel site still requires a project creation/upload action; current Vercel connector returned HTTP 403 on create project. Treat the package as a release candidate until full QA on deployed URLs.

## Copyright

The artwork and code are original. No copyrighted hero portraits, official logos, audio or assets included. The theme is an unofficial club activity about the broad play style and teamwork of Liên Quân Mobile (Arena of Valor).
