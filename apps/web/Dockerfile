# syntax=docker/dockerfile:1

FROM dhi.io/python:3.14-dev@sha256:42fb1e613a3fd86e85c30f1b054536ba642c455123d6b4bcbd796aa49de4e46b AS build

WORKDIR /app

COPY requirements.txt .

RUN python -m venv /opt/venv \
    && /opt/venv/bin/pip install --no-cache-dir --require-hashes -r requirements.txt

COPY . .


FROM dhi.io/python:3.14@sha256:aa13af4b3777149bbf18dc6fe392c5ab9eb097d39715d57f4bacde537b6e0e26

WORKDIR /app

COPY --from=build /opt/venv /opt/venv
COPY --from=build /app .

ENV PATH="/opt/venv/bin:$PATH"

EXPOSE 8080

USER 65532:65532

CMD ["opentelemetry-instrument", "gunicorn", "--bind=0.0.0.0:8080", "--access-logfile=-", "app:app"]