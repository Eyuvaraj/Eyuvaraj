# Meloverse

**Repository:** [Meloverse](https://github.com/Eyuvaraj/Meloverse)

## One-line summary
Solo academic Flask project (IIT Madras "MAD1" coursework, per README: "MAD1 Project") — a music streaming web app with user accounts, creator profiles, playlists, following, likes, and an admin panel with matplotlib-generated usage charts.

## Technology Stack
Flask, Flask-SQLAlchemy, SQLAlchemy, Flask-Login, Flask-RESTful, Jinja2, Bootstrap 5, jQuery, Plyr.js, matplotlib, and SQLite.

## Architecture
Not classic MVC folders (no `views/`, `controllers/` split cleanly) but a comparable layered structure: `application/models.py` (all SQLAlchemy models), three Flask **Blueprints** in `application/app_controllers/` (`auth.py`, `admin.py`, `users.py`) acting as controllers, and Jinja templates under `templates/{admin,creator,user}/` as the view layer. `app.py` wires blueprints together via `create_app()` and registers one Flask-RESTful resource (`SongAPI`). No separate `services/` or `repositories/` layer — DB queries live directly inside route handlers, including raw SQL `UPDATE` statements for counter increments.

## Key Features
- User signup/login/logout with Flask-Login sessions (`application/app_controllers/auth.py`).
- Playlist create/edit/delete and track-add via `Playlist`/`User_Playlist` join model (`users.py:224-333`, route `/meloverse/u/<user>/my_playlists`).
- "Creator" role users can publish singles/albums, edit tracks, and post announcements (`users.py:601-781`, `creator_center/<user>/*` routes) — a user becomes a creator via a separate `Creator` profile record (`creator_signup`, `users.py:128`), not a `Users.role` value.
- Follow/unfollow creators, like/dislike tracks, albums, playlists, announcements — several small stats tables (`Track_likes_stats`, `Album_likes_stats`, `whois_Followeing_who`, etc.).
- Admin dashboard with counts, top creators, and 7-day trending tracks/albums computed from a `usage_timeline` table (`admin.py:58-123`); admin user-role management (grant/revoke admin, `admin.py:126-152`); admin can generate matplotlib PNGs of usage stats on demand (`admin.py:304-386`, run in a background thread).
- One JSON API endpoint, `GET /song`, returning song/user/creator data (`application/api.py`).

## Scale and Scope
Built as a solo academic project over approximately five and a half months, with 30 routes across three Flask blueprints and 14 SQLAlchemy models.

## Key Highlights
- Built a Flask music-streaming app with SQLAlchemy-backed playlists, creator profiles, and follow/like features, using Flask-Login for session auth across 30 routes.
- Designed a 14-table SQLAlchemy schema (tracks, albums, playlists, follows, per-entity like/dislike stats) supporting a multi-role user/creator/admin content model.
- Implemented an admin analytics dashboard computing 7-day trending tracks and albums from a usage-event log, rendered as matplotlib charts on demand.
- Served uploaded audio through Flask with a Jinja and Bootstrap 5 frontend and Plyr.js playback controls.
