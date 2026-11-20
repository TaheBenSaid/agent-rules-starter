# Ledgerline

## Project

Internal service that imports bank statements and categorizes transactions. Python 3.12,
FastAPI, SQLAlchemy 2, Postgres, Celery workers for imports. Dependencies managed with uv.

## Commands

- Install: `uv sync`
- Run API: `uv run uvicorn ledgerline.main:app --reload`
- Run worker: `uv run celery -A ledgerline.worker worker -l info`
- Test: `uv run pytest`
- Test one file: `uv run pytest tests/test_categorize.py`
- Lint: `uv run ruff check .`
- Format: `uv run ruff format .`
- Type check: `uv run mypy src`
- New migration: `uv run alembic revision --autogenerate -m "<short message>"`

## Architecture

- `src/ledgerline/api/`: FastAPI routers, one file per resource.
- `src/ledgerline/services/`: business logic. Routers call services.
- `src/ledgerline/models/`: SQLAlchemy models.
- `src/ledgerline/schemas/`: Pydantic request and response models.
- `src/ledgerline/tasks/`: Celery tasks. Keep them thin, call services.
- `migrations/versions/`: Alembic migrations, generated.
- `tests/fixtures/`: sample statement files. Fake data only.

## Rules

Do:

- Type hint every function. `mypy` runs in strict mode.
- Use Pydantic models for every request and response body.
- Store money as `Decimal` or integer cents. Never `float`.
- Use `structlog` from `ledgerline.log`, not `print`.
- Make Celery tasks safe to run twice.

Don't:

- Put SQL or ORM queries in routers.
- Edit a migration that's already merged. Write a new one.
- Add a dependency with `pip install`. Use `uv add`, and ask first.
- Catch `Exception` without logging and re-raising.

## Style

- snake_case for files, functions and variables. PascalCase for classes.
- Ruff handles formatting and import order. Don't hand-format.
- Docstrings only on public service functions, and only when the name isn't enough.

## Before you finish

1. `uv run ruff check .` passes.
2. `uv run mypy src` passes.
3. `uv run pytest` passes.
4. If you changed a model, a new Alembic migration exists and you read it.
5. List the files you changed.

## Never

- Commit `.env`, real bank files, or anything with real account numbers.
- Run `alembic upgrade` against anything but the local database.
- Touch `infra/` or `docker-compose.prod.yml`.
- Force push or push to `main`.
