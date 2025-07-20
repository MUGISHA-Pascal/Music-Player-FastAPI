# Music Player FastAPI

A backend API for a music player application built with FastAPI, SQLAlchemy, and PostgreSQL. It supports user authentication, song upload, listing, and favoriting, with media storage via Cloudinary.

## Features
- User signup and login with JWT authentication
- Upload songs and thumbnails (stored on Cloudinary)
- List all songs
- Favorite/unfavorite songs
- List user's favorite songs

## Project Structure
```
main.py                # FastAPI app entry point
routes/                # API route definitions (auth, song)
models/                # SQLAlchemy ORM models (User, Song, Favorite)
pydantic_schemas/      # Pydantic schemas for request validation
middleware/            # Custom authentication middleware
```

## Requirements
- Python 3.8+
- PostgreSQL
- Cloudinary account (for media storage)

### Python Dependencies
- fastapi
- uvicorn
- sqlalchemy
- psycopg2-binary
- bcrypt
- pyjwt
- pydantic
- cloudinary

Install with:
```bash
pip install fastapi uvicorn sqlalchemy psycopg2-binary bcrypt pyjwt pydantic cloudinary
```

## Setup
1. **Clone the repository**
2. **Create and activate a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate
   ```
3. **Install dependencies** (see above)
4. **Configure PostgreSQL**
   - Create a database named `fluttermusicapp`.
   - Update the `DATABASE_URL` in `database.py` if needed:
     ```python
     DATABASE_URL = 'postgresql://postgres:postgres@localhost:5432/fluttermusicapp'
     ```
5. **Configure Cloudinary**
   - Update credentials in `routes/song.py`:
     ```python
     cloudinary.config(
         cloud_name="<your_cloud_name>",
         api_key="<your_api_key>",
         api_secret="<your_api_secret>",
         secure=True
     )
     ```
6. **Run the application**
   ```bash
   uvicorn main:app --reload
   ```

## API Endpoints

### Auth
- `POST /auth/signup` — Register a new user
- `POST /auth/login` — Login and receive JWT token
- `GET /auth/` — Get current user info (requires `x-auth-token` header)

### Songs
- `POST /song/upload` — Upload a new song (multipart/form-data, requires auth)
- `GET /song/list` — List all songs (requires auth)
- `POST /song/favorite` — Favorite/unfavorite a song (requires auth)
- `GET /song/list/favorites` — List user's favorite songs (requires auth)

## Environment Variables
- `DATABASE_URL` (in `database.py`)
- Cloudinary credentials (in `routes/song.py`)

## Notes
- The `venv/` directory is git-ignored.
- All endpoints requiring authentication expect a JWT token in the `x-auth-token` header.

## License
MIT 