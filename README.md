# Events Project

A Django web application for listing and browsing events, each with a title, description, date, and poster image. Events are displayed on a single home page with an optional date filter, and images are served from a local media directory.

## Overview

The project consists of a Django site configuration (`events/`) and one app, `event_list/`, which holds all of the application logic:

- **`event_list.models.Event`** — the core model, with fields for `title`, `description`, `image` (uploaded to `media/event_list/images/`), and `date`.
- **`event_list.views.home`** — renders the event list, collects the distinct set of event dates for a filter dropdown, and filters events by `selected_date` when provided via a GET query parameter.
- **`event_list.admin`** — registers `Event` with the Django admin so events can be created/edited/deleted from `/admin/`.
- **Templates** — `home.html` (extends `base.html`) renders a Bootstrap-style grid of event cards with poster images, titles, descriptions, and dates, plus a date picker form for filtering.

## Key Features

- Event listing with title, description, date, and poster image for each event
- Image uploads via Django's `ImageField`, served from the `media/` folder
- Date-based filtering of events through a dropdown/date-picker on the home page
- Django admin interface for managing events (add/edit/delete)
- SQLite database for local development/storage

## Tech Stack

- **Python / Django 5.0.6**
- **SQLite** (default `db.sqlite3` database)
- **Bootstrap** (grid layout/styling in templates) and **jQuery UI datepicker** (used in `home.html`)
- Django's built-in `ImageField` for media/image handling (requires Pillow)

## Project Structure

```
events_project/
├── events/            # Django project config (settings, urls, wsgi, asgi)
├── event_list/        # Main app: models, views, admin, templates, static, migrations
├── media/             # Uploaded event images
├── db.sqlite3         # SQLite database
└── manage.py
```

## Setup Instructions

1. **Install dependencies** (no `requirements.txt` is present in this project, so install directly):
   ```
   pip install django pillow
   ```

2. **Apply database migrations:**
   ```
   python manage.py migrate
   ```

3. **(Optional) Create an admin user** to manage events via the Django admin:
   ```
   python manage.py createsuperuser
   ```

4. **Run the development server:**
   ```
   python manage.py runserver
   ```

5. Visit `http://127.0.0.1:8000/` to view the event list, or `http://127.0.0.1:8000/admin/` to manage events.

## Notes

- `DEBUG = True` and a development `SECRET_KEY` are set in `events/settings.py` — these should be changed before any production deployment.
- Uploaded event images are stored under `media/event_list/images/` and served via Django's static file helper for `MEDIA_URL` during development.
