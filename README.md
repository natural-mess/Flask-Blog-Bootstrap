# Flask Blog Bootstrap

A Flask blog application styled with the Start Bootstrap Clean Blog theme. The current version uses SQLite for storage and includes create, read, update, and delete post flows through server-side routes.

![Demo](demo/2026-07-10_19h35_01.gif)

## Features

- SQLite-backed blog posts with SQLAlchemy
- Create, edit, view, and delete post routes
- Flask-WTF forms with validation
- Rich text post editing with CKEditor
- HTML sanitization for post bodies using Bleach
- Bootstrap 5 integration through `Bootstrap-Flask`
- Contact form with SMTP email sending through Ethereal credentials
- Shared Jinja templates for layout and page sections

## Tech Stack

- Flask
- Bootstrap-Flask
- Flask-SQLAlchemy
- SQLAlchemy 2
- Flask-WTF and WTForms
- Flask-CKEditor
- Bleach
- python-dotenv

## Project Structure

```text
Flask-Blog-Bootstrap/
├── main.py
├── requirements.txt
├── blog_data.txt
├── demo/
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
    ├── make-post.html
    └── post.html
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

### 4) Configure email environment variables

The contact form sends email using these environment variables:

- `ETHEREAL_EMAIL`
- `ETHEREAL_PASSWORD`
- `ETHEREAL_HOST`

The current code loads them from:

```text
D:/API/EnvironmentVariables/.env
```

Example `.env` contents:

```env
ETHEREAL_EMAIL=your_ethereal_email
ETHEREAL_PASSWORD=your_ethereal_password
ETHEREAL_HOST=smtp.ethereal.email
```

## Run the App

```bash
python main.py
```

Open the app at:

- http://127.0.0.1:5003/

The database tables are created automatically on startup. The app is configured to use:

```text
sqlite:///posts.db
```

## Routes

- `GET /` - List all blog posts
- `GET /post/<int:post_id>` - View a single post
- `GET /new-post` - Show the create post form
- `POST /new-post` - Create a new post
- `GET /edit-post/<int:post_id>` - Show the edit form for a post
- `POST /edit-post/<int:post_id>` - Update an existing post
- `GET /delete-post/<int:post_id>` - Delete a post
- `GET /about` - About page
- `GET /contact` - Contact page
- `POST /contact` - Send a contact email and show a success message

## Notes

- Post content is sanitized before saving to the database.
- The editor allows formatted content, but only a limited set of safe HTML tags and attributes are preserved.
- Contact emails are sent through Ethereal SMTP and currently deliver back to the configured sender mailbox.
- The application currently runs in debug mode on port `5003`.
- The Flask `SECRET_KEY` is defined directly in `main.py`. For real deployments, move it to an environment variable.

## Troubleshooting

### `ModuleNotFoundError` or import failures

Install dependencies again:

```bash
pip install -r requirements.txt
```

### Database or post data does not appear

- Start the app once so `db.create_all()` can create the tables.
- Verify the SQLite database file is being created in the Flask instance path used by your local environment.

## License

MIT. See `LICENSE`.
