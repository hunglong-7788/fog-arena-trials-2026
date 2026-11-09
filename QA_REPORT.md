# QA / Release Gate — 2026-11-09

## Verified

- Browser JavaScript syntax: `node --check app.js` PASS.
- Responsive renders at desktop 1440×1000 and phone 390×844: PASS visual inspection.
- Client-side offline fallback: PASS.
- Simulated complete 6-stage Playwright run: IQ Rush → Draft Room → Shotcall → Vision Memory → Reaction Check → Smite Clash: PASS, no page errors.
- Result screen → leaderboard → fullscreen-capable BTC page navigation: PASS in automated UI simulation.
- Supabase Edge Function deployed: `arena-trials`, version 3, `ACTIVE`.
- Live read-only health check: HTTP endpoint returns `{ok:true, top:[], isOpen:true, totalRuns:0, totalFinishers:0}` before test plays.
- Supabase arena tables RLS enabled; public policies absent by design, public table access revoked; current game session count 0.
- Production club portal project/database unchanged.

## Not verified / release blockers

- Vercel `create_project` returned **403 forbidden** for a new project, even though linked team/project read works. This file package is not yet deployed to a new live URL.
- No end-to-end POST `start`→`answer`→`finish` test has run through the live Edge Function, so server write and public ranking publishing are not yet validated from real devices.
- No real multi-device concurrent test or cross-device Broadcast verification.
- No offline-to-online reconnection test on a real event Wi-Fi network.
- The API currently lives in the user's Supabase non-production project (isolated tables). Before using for a heavily attended live event, move/approve a dedicated production data store and verify quotas, backups and concurrency.
- Anti-cheat mitigates simple client-submitted score edits. No-login mode cannot absolutely prevent deliberate automation, impersonation or repeated identities. BTC must manually validate winners.

## Release status

**PREVIEW / TEST CANDIDATE — NOT PRODUCTION LIVE.**
