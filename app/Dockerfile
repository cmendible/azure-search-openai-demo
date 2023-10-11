FROM node:16.20.2-bullseye AS builder
RUN mkdir /backend
WORKDIR /frontend
COPY ./frontend/ ./
RUN npm install;npm run build

FROM python:3.11.1-slim-buster
WORKDIR /app
COPY ./backend/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY ./backend .
COPY --from=builder ./backend/static ./static
EXPOSE 50505
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "50505"]
