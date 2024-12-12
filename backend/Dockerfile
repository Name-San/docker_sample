FROM python:3.13.1-slim AS builder

WORKDIR /app

COPY pyproject.toml requirements.txt ./
RUN pip wheel --no-cache-dir --no-deps --wheel-dir wheels -r requirements.txt

FROM python:3.13-slim AS runner

COPY --from=builder /app/wheels /wheels
RUN pip install --no-cache /wheels/* && rm -rf /wheels

EXPOSE 8000

CMD ["uvicorn", "mysite.main:app", "--host", "0.0.0.0", "--port", "8000"]