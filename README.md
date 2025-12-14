# HR
version: '3.8'
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: hr
      POSTGRES_USER: hruser
      POSTGRES_PASSWORD: hrpass
    volumes:
      - db_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  backend:
    build: ./backend
    env_file: ./backend/.env
    ports:
      - "8000:8000"
    depends_on:
      - db

  frontend:
    build: ./frontend
    env_file: ./frontend/.env
    ports:
      - "3000:3000"
    depends_on:
      - backend

volumes:
  db_data:
