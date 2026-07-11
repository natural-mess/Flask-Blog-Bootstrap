# Flask Blog Bootstrap

A Flask blog app styled with the Start Bootstrap Clean Blog theme.

The application loads blog posts from a remote JSON API and renders:
- A home page with post previews
- A post details page
- About and Contact pages

The Contact page now supports form submission and sends email through SMTP (Ethereal).

## Features

- Flask routing with a dynamic post page: `/post/<int:num>`
- Contact form with POST handling at `/contact`
- SMTP email sending using credentials from environment variables
- Jinja templates with shared header/footer includes
- Static assets served from `static/`
- Remote data fetching using `requests`

![Demo](demo/2026-07-10_19h35_01.gif)

## Project Structure

```text
Flask-Blog-Bootstrap/
├── main.py
├── blog_data.txt
├── templates/
│   ├── header.html
│   ├── footer.html
│   ├── index.html
│   ├── about.html
│   ├── contact.html
│   └── post.html
├── static/
│   ├── assets/
│   ├── css/
│   │   └── styles.css
│   └── js/
│       └── scripts.js
└── .env (local, not committed)
```

## Requirements

- Python 3.10+
- pip

Python packages:
- Flask
- requests
- python-dotenv

## Setup

### 1) Clone the repository

```bash
git clone <your-repo-url>
cd Flask-Blog-Bootstrap
```

### 2) Create and activate a virtual environment

Windows (PowerShell):

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

Windows (CMD):

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
pip install flask requests python-dotenv
```

### 4) Configure environment variables

Add these values to your environment (or to a `.env` file):

- `ETHEREAL_EMAIL`
- `ETHEREAL_PASSWORD`
- `ETHEREAL_HOST`

Example `.env`:

```env
ETHEREAL_EMAIL=your_ethereal_email
ETHEREAL_PASSWORD=your_ethereal_password
ETHEREAL_HOST=smtp.ethereal.email
```

Important:
- The current code loads env vars using an absolute path:
  `load_dotenv("D:/API/EnvironmentVariables/.env")`
- Update this path for your machine, or switch to `load_dotenv()` to load from the project root.

## Run the App

```bash
python main.py
```

Open in browser:
- http://127.0.0.1:5000/

## Routes

- `GET /` -> Home page with all posts
- `GET /about` -> About page
- `GET /contact` -> Contact page form
- `POST /contact` -> Sends contact message by email and shows success text
- `GET /post/<int:num>` -> Post details page (example: `/post/1`)

## Notes and Current Behavior

- Blog data source:
  `https://api.npoint.io/6b78c3badded7def110f`
- HTTPS requests currently use `verify=False` in `requests.get(...)`.
  This disables TLS certificate verification and is not recommended for production.
- Contact messages are currently sent to the configured Ethereal sender mailbox (self-delivery), not to the visitor-provided email.

## Troubleshooting

### Contact form submits but email is not sent

- Verify `ETHEREAL_EMAIL`, `ETHEREAL_PASSWORD`, and `ETHEREAL_HOST` are set correctly.
- Confirm the `.env` path in `load_dotenv(...)` exists on your machine.
- Ensure outbound SMTP on port `587` is allowed.

### Post page returns 404

- Check the post id in URL.
- If `/post/<num>` is greater than the available post count, the app returns `Post not found`.

## License

MIT. See `LICENSE`.
