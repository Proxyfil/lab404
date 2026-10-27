# syntax=docker/dockerfile:1

FROM dhi.io/python:3.14-dev AS build

WORKDIR /app

COPY requirements.txt .

RUN python -m venv /opt/venv \
    && /opt/venv/bin/pip install --no-cache-dir -r requirements.txt

COPY . .


FROM dhi.io/python:3.14

WORKDIR /app

COPY --from=build /opt/venv /opt/venv
COPY --from=build /app .

ENV PATH="/opt/venv/bin:$PATH"

EXPOSE 8080

USER 65532:65532

CMD [
  "opentelemetry-instrument",
  "gunicorn",
  "--bind=0.0.0.0:8080",
  "--access-logfile=-",
  "app:app"
]