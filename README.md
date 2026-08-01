# Flask Blog Bootstrap

A Flask blog application built with Bootstrap styling, rich-text posts, user authentication, and comments.

## Features

- Blog posts with create, read, update, and delete workflows
- User registration, login, and logout
- Password hashing with Werkzeug
- Rich text editing for posts and comments via CKEditor
- Comment system tied to authenticated users
- Admin-only post management (admin is the user with `id == 1`)
- SQLAlchemy models for posts, users, and comments

## Tech Stack

- Flask
- Bootstrap-Flask
- Flask-SQLAlchemy / SQLAlchemy 2
- Flask-Login
- Flask-WTF / WTForms
- Flask-CKEditor
- python-dotenv

## Project Structure

```text
Flask-Blog-Bootstrap/
├── main.py
├── forms.py
├── requirements.txt
├── blog_data.txt
├── instance/
├── static/
│   ├── assets/
│   ├── css/
│   └── js/
└── templates/
        ├── about.html
        ├── contact.html
        ├── footer.html
        ├── header.html
        ├── index.html
        ├── login.html
        ├── make-post.html
        ├── post.html
        └── register.html
```

## Requirements

- Python 3.10+
- pip

## Setup

### 1) Clone the repository

```bash
git clone <your-repo-url>
cd Flask-Blog-Bootstrap
```

### 2) Create and activate a virtual environment

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Windows CMD:

```bat
python -m venv .venv
.venv\Scripts\activate.bat
```

macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3) Install dependencies

```bash
pip install -r requirements.txt
```

### 4) Configure environment variables

Set at least these values before running the app:

- `FLASK_KEY` (required)
- `DB_URI` (optional, defaults to `sqlite:///posts.db`)

Example:

```env
FLASK_KEY=replace_with_a_long_random_secret
DB_URI=sqlite:///posts.db
```

Note: `main.py` currently calls `load_dotenv("D:/API/EnvironmentVariables/.env")`. If that file does not exist on your machine, define the variables in your shell or update this path.

## Run the App

```bash
python main.py
```

Default URL:

- http://127.0.0.1:5000/

The app creates database tables automatically on startup with `db.create_all()`.

## Data Model

- `User`
    - `id`, `email`, `password`, `name`
    - one-to-many with `BlogPost`
    - one-to-many with `Comment`
- `BlogPost`
    - `id`, `title`, `subtitle`, `date`, `body`, `img_url`, `author_id`
    - many-to-one with `User`
    - one-to-many with `Comment`
- `Comment`
    - `id`, `text`, `author_id`, `post_id`
    - many-to-one with `User`
    - many-to-one with `BlogPost`

## Routes

- `GET /` - List all posts
- `GET|POST /register` - Register a new user
- `GET|POST /login` - Log in
- `GET /logout` - Log out
- `GET|POST /post/<int:post_id>` - View a post and submit comments
- `GET|POST /new-post` - Create a post (admin only)
- `GET|POST /edit-post/<int:post_id>` - Edit a post (admin only)
- `GET /delete/<int:post_id>` - Delete a post (admin only)
- `GET /about` - About page
- `GET /contact` - Contact page

## Notes

- Admin access is hard-coded to the first registered user (`current_user.id == 1`).
- The app currently runs with `debug=False`.
- `FLASK_KEY` must be set or form/session features may fail.

## Troubleshooting

### Import errors

Reinstall dependencies:

```bash
pip install -r requirements.txt
```

### App fails on startup with missing secret key behavior

Make sure `FLASK_KEY` is set in your environment.

### Database seems empty

- Confirm `DB_URI` points where you expect.
- Restart the app to ensure tables are created.

## License

MIT. See LICENSE.
