# Devin Bots — always-on code automation pipeline for cloudpc-console

Stack: Go backend + React + a Playwright worker fleet
Repo: github.com/KingLingo/cloudpc-console

The Bot is the orchestrator, not a suggestion box:

- watches the issue stream — new `bug` label triggers a Devin session that
  reproduces and opens a PR
- nightly coverage scan → fans out parallel Devins on the 3 lowest modules
- CI failures on open PRs spawn fix sessions automatically
- keeps queue state (in flight / merged / blocked) so parallel sessions
  never collide on the same files

Retry policy: one retry with CI logs attached, hard stop on second failure,
escalates to me in the daily digest. Anything touching billing/auth/prod
never auto-merges.

Daily report lands in our Telegram group (Gotify + TG):

  [Devin Bot] ✅ PR #142 merged — fix: idempotency on /refresh webhook
  Files: 3 changed | Tests: 2 added | Coverage: filecenter 44%→52%

A human doing this is just cron with extra steps — that's what the Bot is for.
