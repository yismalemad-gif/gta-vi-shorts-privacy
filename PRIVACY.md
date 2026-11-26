# Privacy Policy — GTA VI Shorts Production System

Version: 1.0
Status: Approved for publication

## Who operates this application
This is a private application run by its operator on their own Windows computer. It is not
offered to the public. Contact: yismalemad@gmail.com.

## YouTube API Services
This application uses YouTube API Services. By using it you agree to be bound by the
YouTube Terms of Service: https://www.youtube.com/t/terms

Google's handling of data is described in the Google Privacy Policy:
https://policies.google.com/privacy

## What data is processed
- **Data from YouTube API Services:** public video and channel information such as video
  IDs, channel IDs, uploads playlist IDs, titles, descriptions, channel names, thumbnails,
  publication dates, durations, upload/privacy/live-broadcast status, licence, and public
  view/like counts.
- **Information you enter:** search terms, notes, labels, workflow status, permission
  decisions and descriptions of permission evidence, and creator handles.
- **Local operational logs and backups:** API request/quota logs (endpoint, timestamp,
  HTTP status, error reason, attempt count, and sanitized request context such as search
  terms or creator selectors), workflow change history, and local database backups in
  `data/backups/`.

The application uses an API key only. It does not ask you to sign in with Google, does not
access any Google account and does not store authorization tokens.

## Where data is stored and who receives it
- All data is stored only in a local SQLite database on the operator's computer.
- Requests to YouTube API Services send search terms, video/channel/playlist IDs,
  creator handles, a standard `User-Agent` header, and the API key to Google. Nothing
  else is sent anywhere; no data is sold or shared.

## How long data is kept
- **YouTube API data** (video snapshots, YouTube video/channel link records, and
  discovery associations) is refreshed or deleted within 28 days of the last successful
  check (below the 30-day limit in the YouTube API Services Developer Policies).
- If a video or channel can no longer be confirmed through the API, its YouTube-derived
  identifiers, API data, and discovery associations are removed. Your own workflow
  records (status, permission decisions, sanitized notes/labels/evidence, and creator
  entries) remain after best-effort removal of YouTube-derived text.
- Expired YouTube data is never displayed.
- **Local workflow records and operational logs** (workflow event history and `quota_log`
  entries) are not removed by the 28-day API-data purge and remain on the operator's
  computer until deleted by the operator.
- **Database backups** in `data/backups/` are point-in-time copies of the SQLite database
  (taken before migrations, restores, or large purges) and contain any YouTube API data
  present when the backup was created. Maintenance and startup runs (`python -m
  shorts.maintenance purge`, `python -m shorts.db`, and API commands) automatically
  attempt to purge expired YouTube API data from backup files using the same 28-day
  retention rules (upgrading legacy v1 backups and cleaning them in place when needed). A
  `pre-purge` safety backup created during a large purge is preserved for that single run
  and cleaned on the next run. If a backup file is corrupt or inaccessible during cleanup,
  a warning is logged and it should be deleted manually. Restored current-version backups
  are purged immediately on restore, whereas older restored backups are migrated and
  purged before display on the next startup.

## How to delete data
- Run `python -m shorts.maintenance purge` to remove expired (>28 days) YouTube data immediately.
- Delete the `data/` folder to remove all stored data, including backups.

## Changes
A new version of this policy must be accepted again before the application uses the
YouTube API.
