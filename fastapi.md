# FastAPI — Complete Notes

> Every major FastAPI concept, each with an explanation, 2–3 examples and interview questions.
> Covers routing, Pydantic v2, dependency injection, databases (SQLAlchemy 2.0 + Alembic), auth (OAuth2 + JWT), middleware, background jobs, WebSockets, testing, performance, deployment and production best practices.
> Read `python.md` first for async/await, type hints, decorators and context managers.

---

## Table of Contents

1. [What is FastAPI](#1-what-is-fastapi)
2. [Setup & First App](#2-setup--first-app)
3. [Path Operations & HTTP Methods](#3-path-operations--http-methods)
4. [Path Parameters](#4-path-parameters)
5. [Query Parameters](#5-query-parameters)
6. [Request Body with Pydantic](#6-request-body-with-pydantic)
7. [Pydantic v2 Deep Dive](#7-pydantic-v2-deep-dive)
8. [Response Models & Status Codes](#8-response-models--status-codes)
9. [Headers, Cookies, Forms & File Uploads](#9-headers-cookies-forms--file-uploads)
10. [Error Handling](#10-error-handling)
11. [Dependency Injection](#11-dependency-injection)
12. [APIRouter & Project Structure](#12-apirouter--project-structure)
13. [async def vs def](#13-async-def-vs-def)
14. [Settings & Configuration](#14-settings--configuration)
15. [Databases: SQLAlchemy 2.0](#15-databases-sqlalchemy-20)
16. [Async SQLAlchemy](#16-async-sqlalchemy)
17. [Migrations with Alembic](#17-migrations-with-alembic)
18. [Other Databases: SQLModel & MongoDB (Beanie)](#18-other-databases-sqlmodel--mongodb-beanie)
19. [Authentication: OAuth2 + JWT](#19-authentication-oauth2--jwt)
20. [Authorization: Roles, Scopes, Ownership](#20-authorization-roles-scopes-ownership)
21. [Multi-Tenancy & API Versioning](#21-multi-tenancy--api-versioning)
22. [Middleware & CORS](#22-middleware--cors)
23. [Lifespan Events (startup/shutdown)](#23-lifespan-events)
24. [Background Tasks & Job Queues](#24-background-tasks--job-queues)
25. [Task Queues in Depth: Celery & ARQ](#25-task-queues-in-depth-celery--arq)
26. [WebSockets & Streaming](#26-websockets--streaming)
27. [Server-Sent Events & Streaming Answers in FastAPI](#27-server-sent-events--streaming-answers-in-fastapi)
28. [Pagination, Filtering & Sorting](#28-pagination-filtering--sorting)
29. [Caching & Rate Limiting](#29-caching--rate-limiting)
30. [Calling External APIs (httpx)](#30-calling-external-apis)
31. [Integrations: Webhooks, Payments, Email & S3 Uploads](#31-integrations-webhooks-payments-email--s3-uploads)
32. [Testing FastAPI](#32-testing-fastapi)
33. [OpenAPI Docs Customization](#33-openapi-docs-customization)
34. [Logging, Monitoring & Request IDs](#34-logging-monitoring--request-ids)
35. [Observability Hands-On in FastAPI (Metrics, Tracing, Error Tracking)](#35-observability-hands-on-in-fastapi-metrics-tracing-error-tracking)
36. [Security Best Practices](#36-security-best-practices)
37. [OWASP API Top 10 in FastAPI](#37-owasp-api-top-10-in-fastapi)
38. [Performance](#38-performance)
39. [Deployment: Uvicorn, Gunicorn, Docker](#39-deployment)
40. [Complete CRUD Example (layered)](#40-complete-crud-example)
41. [Production Checklist & Best Practices](#41-production-checklist)
42. [FastAPI vs Flask vs Django vs Express](#42-fastapi-vs-flask-vs-django-vs-express)
43. [Most Asked Interview Questions](#43-most-asked-interview-questions)

---

## 1. What is FastAPI

**FastAPI** is a modern, high-performance Python web framework for building APIs, based on **standard Python type hints**.

Built on:
- **Starlette** — the ASGI web toolkit (routing, middleware, WebSockets, requests/responses).
- **Pydantic** — data validation & serialization using type hints.

Key features:
- **Fast**: one of the fastest Python frameworks (async, ASGI, Pydantic core in Rust).
- **Type hints drive everything**: validation, conversion, serialization, editor autocomplete, docs.
- **Automatic interactive docs**: Swagger UI at `/docs`, ReDoc at `/redoc`, OpenAPI schema at `/openapi.json`.
- **Dependency Injection** system built in.
- **async/await** first-class (but sync functions work too).
- Standards-based: OpenAPI, JSON Schema, OAuth2.

### WSGI vs ASGI

| WSGI (Flask, Django classic) | ASGI (FastAPI, Starlette, Django async) |
|---|---|
| Synchronous, one request per worker thread | Asynchronous, many concurrent requests per worker |
| No native WebSockets | WebSockets, HTTP/2, long-lived connections |
| Servers: Gunicorn, uWSGI | Servers: Uvicorn, Hypercorn, Granian |

**Interview Qs**
- Why FastAPI? → Speed, automatic validation & docs from type hints, DI, async support, great developer experience.
- What are Starlette and Pydantic's roles? (above)
- WSGI vs ASGI? (table)

---

## 2. Setup & First App

```bash
mkdir api && cd api
python3 -m venv .venv && source .venv/bin/activate   # isolated environment (see python.md: Installing Packages)
pip install "fastapi[standard]"                      # includes uvicorn, the fastapi CLI, httpx, etc.

# or with uv (faster, manages the venv for you)
uv init api && cd api && uv add "fastapi[standard]"
```

```python
# main.py
from fastapi import FastAPI

app = FastAPI(title="Todo API", version="1.0.0")

@app.get("/")
def root():
    return {"message": "Hello FastAPI"}      # dicts/lists/Pydantic models → JSON automatically

@app.get("/health")
async def health():
    return {"status": "ok"}
```

```bash
fastapi dev main.py            # dev server with auto-reload → http://127.0.0.1:8000
fastapi run main.py            # production mode
uvicorn main:app --reload      # classic way (module:variable)
```

Open `http://127.0.0.1:8000/docs` → interactive Swagger UI where you can try every endpoint.

---

## 3. Path Operations & HTTP Methods

A **path operation** = path + HTTP method + function. The decorator registers the route.

```python
@app.get("/items")            # read (list)
@app.get("/items/{id}")       # read one
@app.post("/items")           # create
@app.put("/items/{id}")       # replace
@app.patch("/items/{id}")     # partial update
@app.delete("/items/{id}")    # delete
@app.options(...), @app.head(...)
@app.api_route("/ping", methods=["GET", "POST"])
```

### Example — in-memory CRUD

```python
from fastapi import FastAPI, HTTPException, status
from pydantic import BaseModel

app = FastAPI()

class TodoIn(BaseModel):
    title: str
    done: bool = False

class Todo(TodoIn):
    id: int

todos: dict[int, Todo] = {}
next_id = 1

@app.get("/todos")
def list_todos() -> list[Todo]:
    return list(todos.values())

@app.post("/todos", status_code=status.HTTP_201_CREATED)
def create_todo(data: TodoIn) -> Todo:
    global next_id
    todo = Todo(id=next_id, **data.model_dump())
    todos[next_id] = todo
    next_id += 1
    return todo

@app.get("/todos/{todo_id}")
def get_todo(todo_id: int) -> Todo:
    if todo_id not in todos:
        raise HTTPException(status_code=404, detail="Todo not found")
    return todos[todo_id]

@app.delete("/todos/{todo_id}", status_code=status.HTTP_204_NO_CONTENT)
def delete_todo(todo_id: int) -> None:
    if todos.pop(todo_id, None) is None:
        raise HTTPException(status_code=404, detail="Todo not found")
```

### Route order matters

Routes are matched **in the order they're declared**.

```python
@app.get("/users/me")          # must come BEFORE /users/{user_id}
def me(): ...

@app.get("/users/{user_id}")
def get_user(user_id: int): ...
# If reversed, "/users/me" would try to parse "me" as an int → 422
```

---

## 4. Path Parameters

Values embedded in the URL path. The type hint makes FastAPI **validate and convert** automatically.

```python
@app.get("/users/{user_id}")
def get_user(user_id: int):          # "/users/42" → 42 (int); "/users/abc" → 422 error
    return {"user_id": user_id}
```

### Example — Enum for fixed values

```python
from enum import StrEnum

class Category(StrEnum):
    electronics = "electronics"
    books = "books"

@app.get("/products/{category}")
def by_category(category: Category):
    return {"category": category.value}   # only allowed values; shown as a dropdown in /docs
```

### Example — validation with Path & Annotated

```python
from typing import Annotated
from fastapi import Path

@app.get("/orders/{order_id}")
def get_order(order_id: Annotated[int, Path(gt=0, le=1_000_000, description="The order ID")]):
    return {"order_id": order_id}

@app.get("/files/{file_path:path}")      # path converter: captures slashes
def read_file(file_path: str):
    return {"file_path": file_path}      # /files/a/b/c.txt → "a/b/c.txt"
```

`Annotated[type, metadata]` is the recommended style — the type stays a normal type, and metadata (validation, dependencies) is attached separately.

---

## 5. Query Parameters

Function parameters that are **not** in the path are treated as **query parameters** (`?key=value`).

```python
@app.get("/products")
def list_products(skip: int = 0, limit: int = 20, q: str | None = None, in_stock: bool = False):
    # /products?skip=20&limit=10&q=phone&in_stock=true
    return {"skip": skip, "limit": limit, "q": q, "in_stock": in_stock}
```

- Default value → optional. No default → **required**.
- `bool` accepts `true/false/1/0/yes/no/on/off`.

### Validation with Query

```python
from fastapi import Query

@app.get("/search")
def search(
    q: Annotated[str, Query(min_length=2, max_length=50, pattern=r"^[\w\s-]+$")],
    page: Annotated[int, Query(ge=1)] = 1,
    size: Annotated[int, Query(ge=1, le=100)] = 20,
    tags: Annotated[list[str], Query()] = [],        # ?tags=a&tags=b → ["a", "b"]
    sort: Annotated[str, Query(alias="sort-by")] = "created_at",  # ?sort-by=price
):
    return {"q": q, "page": page, "size": size, "tags": tags, "sort": sort}
```

### Query parameter models (group many params)

```python
from pydantic import BaseModel, Field
from typing import Literal

class ProductFilters(BaseModel):
    model_config = {"extra": "forbid"}          # reject unknown query params
    q: str | None = None
    min_price: float | None = Field(None, ge=0)
    max_price: float | None = Field(None, ge=0)
    sort: Literal["price", "-price", "newest"] = "newest"
    page: int = Field(1, ge=1)
    size: int = Field(20, ge=1, le=100)

@app.get("/products")
def list_products(filters: Annotated[ProductFilters, Query()]):
    return filters
```

---

## 6. Request Body with Pydantic

A parameter typed as a **Pydantic model** is read from the **JSON body**.

```python
from pydantic import BaseModel, EmailStr, Field

class UserCreate(BaseModel):
    name: str = Field(min_length=2, max_length=50)
    email: EmailStr                               # needs `email-validator` (included in fastapi[standard])
    age: int | None = Field(default=None, ge=13, le=120)
    tags: list[str] = []

@app.post("/users", status_code=201)
def create_user(user: UserCreate):
    # user is already validated & typed
    return {"created": user.name, "email": user.email}
```

Invalid body → automatic **422 Unprocessable Entity** with details:

```json
{
  "detail": [
    { "type": "string_too_short", "loc": ["body", "name"], "msg": "String should have at least 2 characters", "input": "A" },
    { "type": "value_error", "loc": ["body", "email"], "msg": "value is not a valid email address..." }
  ]
}
```

### Mixing path, query and body

```python
@app.put("/items/{item_id}")
def update_item(item_id: int, item: ItemUpdate, notify: bool = False):
    # item_id → path, item → body, notify → query
    ...
```

### Multiple bodies & Body()

```python
from fastapi import Body

@app.post("/orders")
def create_order(
    order: OrderIn,
    customer: CustomerIn,
    priority: Annotated[int, Body(ge=1, le=5)] = 3,
):
    # expects {"order": {...}, "customer": {...}, "priority": 3}
    ...

@app.post("/notes")
def create_note(note: Annotated[NoteIn, Body(embed=True)]):
    # expects {"note": {...}} instead of the model fields at the top level
    ...
```

---

## 7. Pydantic v2 Deep Dive

Pydantic validates data using type hints and converts ("coerces") input to the declared types. v2's core is written in Rust (much faster than v1).

### Models & fields

```python
from datetime import datetime
from decimal import Decimal
from typing import Annotated, Literal
from pydantic import BaseModel, Field, EmailStr, HttpUrl, ConfigDict, SecretStr

class Address(BaseModel):
    city: str
    pincode: Annotated[str, Field(pattern=r"^\d{6}$")]

class User(BaseModel):
    model_config = ConfigDict(
        str_strip_whitespace=True,     # trim strings
        extra="forbid",                # error on unknown fields (catches typos & mass-assignment)
        frozen=False,
    )

    id: int
    name: str = Field(min_length=2, max_length=50, examples=["Rohit"])
    email: EmailStr
    website: HttpUrl | None = None
    password: SecretStr                # hidden in repr/logs
    role: Literal["user", "admin"] = "user"
    balance: Decimal = Decimal("0.00")
    address: Address | None = None     # nested model
    tags: list[str] = Field(default_factory=list)
    created_at: datetime = Field(default_factory=datetime.now)

u = User(id="1", name="  Rohit ", email="r@x.com", password="secret")
u.id            # 1 (string "1" coerced to int in the default "lax" mode)
u.name          # "Rohit" (stripped)
u.password      # SecretStr('**********')
u.password.get_secret_value()   # "secret"
```

### Validation & serialization methods (v2 names)

```python
User.model_validate({"id": 1, ...})         # dict → model (validates)
User.model_validate_json('{"id": 1, ...}')  # JSON string → model (fast)
u.model_dump()                              # model → dict
u.model_dump(exclude={"password"}, exclude_none=True, by_alias=True)
u.model_dump(mode="json")                   # JSON-safe types (datetime → str, Decimal → str)
u.model_dump_json(indent=2)                 # → JSON string
u.model_copy(update={"name": "New"})        # copy with changes
User.model_json_schema()                    # JSON Schema (used for OpenAPI)
```

| v1 | v2 |
|---|---|
| `.dict()` | `.model_dump()` |
| `.json()` | `.model_dump_json()` |
| `parse_obj()` | `model_validate()` |
| `class Config: orm_mode = True` | `model_config = ConfigDict(from_attributes=True)` |
| `@validator` | `@field_validator` |
| `@root_validator` | `@model_validator` |

### Custom validators

```python
from pydantic import field_validator, model_validator
from typing import Self

class SignUp(BaseModel):
    username: str
    password: str
    confirm_password: str

    @field_validator("username")
    @classmethod
    def username_alphanumeric(cls, v: str) -> str:
        if not v.isalnum():
            raise ValueError("must be alphanumeric")
        return v.lower()                      # validators can also transform

    @field_validator("password")
    @classmethod
    def strong_password(cls, v: str) -> str:
        if len(v) < 8 or not any(c.isdigit() for c in v) or not any(c.isupper() for c in v):
            raise ValueError("min 8 chars, with a digit and an uppercase letter")
        return v

    @model_validator(mode="after")            # cross-field validation
    def passwords_match(self) -> Self:
        if self.password != self.confirm_password:
            raise ValueError("passwords do not match")
        return self
```

### Reusable annotated types

```python
from pydantic import AfterValidator, BeforeValidator

def validate_phone(v: str) -> str:
    digits = "".join(c for c in v if c.isdigit())
    if len(digits) != 10:
        raise ValueError("phone must have 10 digits")
    return digits

IndianPhone = Annotated[str, AfterValidator(validate_phone)]
PositiveInt = Annotated[int, Field(gt=0)]
LowerStr = Annotated[str, BeforeValidator(lambda v: v.lower() if isinstance(v, str) else v)]

class Contact(BaseModel):
    phone: IndianPhone
    age: PositiveInt
    handle: LowerStr
```

### Computed fields, aliases, strict mode

```python
from pydantic import computed_field, AliasChoices

class CartItem(BaseModel):
    price: Decimal
    qty: int

    @computed_field                     # included in model_dump & the response
    @property
    def subtotal(self) -> Decimal:
        return self.price * self.qty

class ExternalUser(BaseModel):
    model_config = ConfigDict(populate_by_name=True)
    user_id: int = Field(alias="userId")          # accept camelCase JSON, use snake_case in Python
    full_name: str = Field(validation_alias=AliasChoices("fullName", "name"))

ExternalUser.model_validate({"userId": 1, "fullName": "A"})

class StrictModel(BaseModel):
    model_config = ConfigDict(strict=True)        # no coercion: "1" is NOT accepted for int
    count: int
```

### camelCase API automatically

```python
from pydantic.alias_generators import to_camel

class CamelModel(BaseModel):
    model_config = ConfigDict(alias_generator=to_camel, populate_by_name=True)

class OrderOut(CamelModel):
    order_id: int
    created_at: datetime
# FastAPI responses use aliases by default → {"orderId": 1, "createdAt": "..."}
```

### Discriminated unions

```python
class CardPayment(BaseModel):
    method: Literal["card"]
    card_last4: str

class UpiPayment(BaseModel):
    method: Literal["upi"]
    vpa: str

class PaymentRequest(BaseModel):
    amount: Decimal
    payment: Annotated[CardPayment | UpiPayment, Field(discriminator="method")]

PaymentRequest.model_validate({"amount": "99", "payment": {"method": "upi", "vpa": "a@okbank"}})
```

### ORM mode (from_attributes)

```python
class UserOut(BaseModel):
    model_config = ConfigDict(from_attributes=True)   # read from object attributes (SQLAlchemy models)
    id: int
    email: str

UserOut.model_validate(db_user)   # works on an ORM object
```

**Interview Qs**
- What does Pydantic do in FastAPI? → Validates requests, serializes responses, generates JSON Schema for docs.
- `field_validator` vs `model_validator`?
- Lax vs strict mode?
- How to hide fields like passwords in responses? → Separate output models / `response_model`, `exclude`, `SecretStr`.

---

## 8. Response Models & Status Codes

**Always define what your API returns.** A response model:
- **filters** output to only declared fields (e.g. never leak `hashed_password`),
- **validates** & serializes output,
- **documents** the response in OpenAPI.

### Example 1 — separate input / output / DB schemas (the standard pattern)

```python
class UserBase(BaseModel):
    email: EmailStr
    name: str

class UserCreate(UserBase):          # input
    password: str

class UserUpdate(BaseModel):         # partial input (PATCH)
    email: EmailStr | None = None
    name: str | None = None

class UserOut(UserBase):             # output — no password
    model_config = ConfigDict(from_attributes=True)
    id: int
    created_at: datetime

@app.post("/users", response_model=UserOut, status_code=201)
def create_user(data: UserCreate, db: DbSession):
    user = User(email=data.email, name=data.name, hashed_password=hash_password(data.password))
    db.add(user); db.commit(); db.refresh(user)
    return user                       # ORM object → filtered through UserOut

# Return type annotation works too (and is type-checked):
@app.get("/users/{user_id}")
def get_user(user_id: int, db: DbSession) -> UserOut:
    ...
```

### Example 2 — PATCH with exclude_unset

```python
@app.patch("/users/{user_id}", response_model=UserOut)
def update_user(user_id: int, data: UserUpdate, db: DbSession):
    user = db.get(User, user_id)
    if not user:
        raise HTTPException(404, "User not found")
    for field, value in data.model_dump(exclude_unset=True).items():   # only fields the client sent
        setattr(user, field, value)
    db.commit(); db.refresh(user)
    return user
```

`exclude_unset=True` distinguishes "not sent" from "sent as null".

### Example 3 — response options & other response classes

```python
@app.get("/users", response_model=list[UserOut], response_model_exclude_none=True)

from fastapi.responses import JSONResponse, HTMLResponse, PlainTextResponse, RedirectResponse, FileResponse, StreamingResponse, Response

@app.get("/legacy")
def legacy():
    return RedirectResponse("/new", status_code=301)

@app.get("/report.pdf")
def report():
    return FileResponse("reports/latest.pdf", media_type="application/pdf", filename="report.pdf")

@app.get("/custom")
def custom():
    return JSONResponse(content={"ok": True}, status_code=202, headers={"X-Job-Id": "123"})

@app.get("/page", response_class=HTMLResponse)
def page():
    return "<h1>Hello</h1>"
```

When you return a `Response` directly, FastAPI skips `response_model` validation — you're in full control.

### Status codes

```python
from fastapi import status

@app.post("/items", status_code=status.HTTP_201_CREATED)
@app.delete("/items/{id}", status_code=status.HTTP_204_NO_CONTENT)

# Dynamic status
from fastapi import Response
@app.put("/items/{id}")
def upsert(id: int, item: ItemIn, response: Response):
    if id not in db:
        response.status_code = 201
    ...
```

Common: 200 OK, 201 Created, 202 Accepted, 204 No Content, 400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 409 Conflict, 422 Validation Error, 429 Too Many Requests, 500 Server Error, 503 Unavailable.

---

## 9. Headers, Cookies, Forms & File Uploads

### Headers & cookies

```python
from fastapi import Header, Cookie, Response

@app.get("/whoami")
def whoami(
    user_agent: Annotated[str | None, Header()] = None,      # reads "User-Agent" (underscores → hyphens)
    x_request_id: Annotated[str | None, Header()] = None,
    session_id: Annotated[str | None, Cookie()] = None,
):
    return {"ua": user_agent, "request_id": x_request_id, "session": session_id}

@app.post("/login")
def login(response: Response):
    response.set_cookie(
        key="session_id", value="abc123",
        httponly=True, secure=True, samesite="lax", max_age=60 * 60 * 24,
    )
    response.headers["X-Custom"] = "value"
    return {"ok": True}

@app.post("/logout")
def logout(response: Response):
    response.delete_cookie("session_id")
    return {"ok": True}
```

### Form data (HTML forms, OAuth2 login)

```python
from fastapi import Form

@app.post("/contact")
def contact(name: Annotated[str, Form()], message: Annotated[str, Form(max_length=1000)]):
    return {"name": name}
```

### File uploads

```python
from fastapi import UploadFile, File
import aiofiles, uuid
from pathlib import Path

ALLOWED = {"image/jpeg", "image/png", "image/webp"}
MAX_SIZE = 5 * 1024 * 1024
UPLOAD_DIR = Path("uploads")

@app.post("/avatar")
async def upload_avatar(file: UploadFile):
    if file.content_type not in ALLOWED:
        raise HTTPException(415, "Only JPEG/PNG/WebP images allowed")

    ext = Path(file.filename or "").suffix.lower()
    dest = UPLOAD_DIR / f"{uuid.uuid4()}{ext}"          # never trust the client's filename
    size = 0
    async with aiofiles.open(dest, "wb") as out:
        while chunk := await file.read(1024 * 1024):   # stream in 1MB chunks
            size += len(chunk)
            if size > MAX_SIZE:
                await out.close(); dest.unlink(missing_ok=True)
                raise HTTPException(413, "File too large (max 5MB)")
            await out.write(chunk)
    return {"filename": dest.name, "size": size}

@app.post("/gallery")
async def upload_many(files: list[UploadFile], album: Annotated[str, Form()]):
    return {"album": album, "count": len(files)}
```

`UploadFile` is spooled to disk for large files (doesn't load everything into memory). In production, upload to object storage (S3) — ideally via **pre-signed URLs** so files go directly from client to storage.

---

## 10. Error Handling

### HTTPException

```python
from fastapi import HTTPException

@app.get("/items/{item_id}")
def get_item(item_id: int):
    item = db.get(item_id)
    if item is None:
        raise HTTPException(
            status_code=404,
            detail="Item not found",
            headers={"X-Error": "item-missing"},
        )
    return item
```

### Custom exceptions + global handlers (recommended pattern)

Keep business logic free of HTTP details: raise **domain exceptions** in services, map them to HTTP responses in one place.

```python
# errors.py
class AppError(Exception):
    status_code = 500
    code = "INTERNAL_ERROR"
    def __init__(self, message: str, details: dict | None = None):
        super().__init__(message)
        self.message = message
        self.details = details or {}

class NotFoundError(AppError):
    status_code = 404
    code = "NOT_FOUND"

class ConflictError(AppError):
    status_code = 409
    code = "CONFLICT"

class PermissionDenied(AppError):
    status_code = 403
    code = "FORBIDDEN"

# main.py
from fastapi import Request
from fastapi.responses import JSONResponse
from fastapi.exceptions import RequestValidationError
import logging

logger = logging.getLogger(__name__)

@app.exception_handler(AppError)
async def app_error_handler(request: Request, exc: AppError):
    return JSONResponse(
        status_code=exc.status_code,
        content={"error": {"code": exc.code, "message": exc.message, "details": exc.details}},
    )

@app.exception_handler(RequestValidationError)
async def validation_handler(request: Request, exc: RequestValidationError):
    return JSONResponse(
        status_code=422,
        content={"error": {
            "code": "VALIDATION_ERROR",
            "message": "Invalid request",
            "details": [{"field": ".".join(map(str, e["loc"][1:])), "message": e["msg"]} for e in exc.errors()],
        }},
    )

@app.exception_handler(Exception)
async def unhandled_handler(request: Request, exc: Exception):
    logger.exception("Unhandled error on %s %s", request.method, request.url.path)
    return JSONResponse(status_code=500, content={"error": {"code": "INTERNAL_ERROR", "message": "Something went wrong"}})

# services/users.py
def get_user_or_404(db, user_id: int) -> User:
    user = db.get(User, user_id)
    if not user:
        raise NotFoundError(f"User {user_id} not found")
    return user
```

Benefits: consistent error format for the frontend, no stack traces leaked, services reusable outside HTTP (CLI, workers).

**Interview Qs**
- 422 vs 400? → 422 = FastAPI's automatic validation error; 400 = a generic bad request you raise yourself.
- How do you return a consistent error format? → Custom exception classes + `@app.exception_handler`.

---

## 11. Dependency Injection

`Depends()` declares that a path operation **needs** something (DB session, current user, settings, pagination params, services). FastAPI calls the dependency, caches it **per request**, and injects the result. Dependencies can depend on other dependencies (a graph).

Why DI: reuse, separation of concerns, easy testing (override dependencies), cleanup handled automatically.

### Example 1 — reusable common parameters

```python
from fastapi import Depends

def pagination(page: int = Query(1, ge=1), size: int = Query(20, ge=1, le=100)) -> dict:
    return {"offset": (page - 1) * size, "limit": size}

Pagination = Annotated[dict, Depends(pagination)]      # type alias → reuse everywhere

@app.get("/products")
def list_products(p: Pagination):
    return {"offset": p["offset"], "limit": p["limit"]}

@app.get("/orders")
def list_orders(p: Pagination): ...
```

### Example 2 — dependencies with `yield` (setup + teardown): DB session

```python
from sqlalchemy.orm import Session

def get_db():
    db = SessionLocal()
    try:
        yield db                 # injected into the route
    except Exception:
        db.rollback()            # undo partial work if the handler raised
        raise
    finally:
        db.close()               # always runs (cleanup)

# Commit explicitly in the service/route (db.commit()) BEFORE returning, so a failed
# commit becomes an error response instead of a "200 OK" for data that wasn't saved.

DbSession = Annotated[Session, Depends(get_db)]

@app.get("/users/{user_id}")
def get_user(user_id: int, db: DbSession):
    return db.get(User, user_id)
```

### Example 3 — dependency chain: token → current user → admin

```python
from fastapi.security import OAuth2PasswordBearer

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="/auth/token")

def get_current_user(token: Annotated[str, Depends(oauth2_scheme)], db: DbSession) -> User:
    payload = decode_token(token)                   # raises 401 if invalid
    user = db.get(User, int(payload["sub"]))
    if not user or not user.is_active:
        raise HTTPException(401, "Invalid credentials", headers={"WWW-Authenticate": "Bearer"})
    return user

CurrentUser = Annotated[User, Depends(get_current_user)]

def require_admin(user: CurrentUser) -> User:
    if user.role != "admin":
        raise HTTPException(403, "Admins only")
    return user

AdminUser = Annotated[User, Depends(require_admin)]

@app.get("/me")
def me(user: CurrentUser): return user

@app.delete("/users/{user_id}")
def delete_user(user_id: int, admin: AdminUser, db: DbSession): ...
```

### Class-based & parameterized dependencies

```python
class RoleChecker:
    def __init__(self, *allowed: str):
        self.allowed = allowed
    def __call__(self, user: CurrentUser) -> User:     # instance is callable → usable in Depends
        if user.role not in self.allowed:
            raise HTTPException(403, "Insufficient permissions")
        return user

@app.post("/articles", dependencies=[Depends(RoleChecker("editor", "admin"))])
def publish_article(...): ...
```

### Service layer injection

```python
class UserService:
    def __init__(self, db: DbSession):
        self.db = db
    def get(self, user_id: int) -> User:
        user = self.db.get(User, user_id)
        if not user:
            raise NotFoundError(f"User {user_id} not found")
        return user

@app.get("/users/{user_id}", response_model=UserOut)
def read_user(user_id: int, service: Annotated[UserService, Depends()]):   # Depends() with no arg → uses the type
    return service.get(user_id)
```

### Router-level & global dependencies

```python
router = APIRouter(prefix="/admin", dependencies=[Depends(require_admin)])   # all admin routes protected
app = FastAPI(dependencies=[Depends(verify_api_key)])                       # every route
```

### Caching per request

If two dependencies both depend on `get_db`, it's called **once** per request and the same session is shared. Use `Depends(get_db, use_cache=False)` to opt out.

### Overriding in tests

```python
app.dependency_overrides[get_db] = get_test_db
app.dependency_overrides[get_current_user] = lambda: User(id=1, role="admin")
```

**Interview Qs**
- What is DI in FastAPI and why use it?
- How do `yield` dependencies work? → Code before `yield` runs before the handler, code after runs after (cleanup).
- How do you protect all routes in a router? → `APIRouter(dependencies=[...])`.
- How do you mock dependencies in tests? → `app.dependency_overrides`.

---

## 12. APIRouter & Project Structure

Split the app into routers (like Express routers / Flask blueprints).

```python
# app/api/routes/users.py
from fastapi import APIRouter

router = APIRouter(prefix="/users", tags=["users"])

@router.get("/", response_model=list[UserOut])
def list_users(db: DbSession, p: Pagination): ...

@router.post("/", response_model=UserOut, status_code=201)
def create_user(data: UserCreate, service: Annotated[UserService, Depends()]): ...

# app/main.py
from app.api.routes import users, auth, orders

app = FastAPI()
app.include_router(auth.router)
app.include_router(users.router, prefix="/api/v1")
app.include_router(orders.router, prefix="/api/v1", dependencies=[Depends(get_current_user)])
```

### Recommended structure (layered)

```
app/
├── main.py                # create app, include routers, middleware, handlers, lifespan
├── core/
│   ├── config.py          # Settings (pydantic-settings)
│   ├── security.py        # hashing, JWT
│   ├── logging.py
│   └── errors.py          # AppError hierarchy + handlers
├── db/
│   ├── base.py            # DeclarativeBase
│   └── session.py         # engine, SessionLocal, get_db
├── models/                # SQLAlchemy ORM models
│   └── user.py
├── schemas/               # Pydantic models (request/response)
│   └── user.py
├── repositories/          # DB queries only
│   └── user_repo.py
├── services/              # business logic (no HTTP stuff)
│   └── user_service.py
├── api/
│   ├── deps.py            # shared dependencies (DbSession, CurrentUser, Pagination)
│   └── routes/
│       ├── auth.py
│       └── users.py
└── workers/               # background jobs
tests/
alembic/
pyproject.toml
Dockerfile
```

Flow: **route** (HTTP: parse/validate, status codes) → **service** (business rules) → **repository** (SQL) → **model** (DB table). Schemas (Pydantic) at the edges.

For large apps, group by **feature/domain** instead: `app/users/{router,schemas,models,service}.py`.

---

## 13. async def vs def

FastAPI supports both:

| You write | FastAPI runs it | Use when |
|---|---|---|
| `async def` | Directly on the event loop | You `await` async libraries (httpx.AsyncClient, asyncpg, async SQLAlchemy, redis.asyncio) |
| `def` | In a **threadpool** (so it doesn't block the loop) | You use **blocking** libraries (requests, sync SQLAlchemy, psycopg2, boto3) or CPU-light sync code |

### The #1 FastAPI performance bug

```python
import time, requests

@app.get("/bad")
async def bad():
    time.sleep(2)                         # ❌ blocks the whole event loop — ALL requests freeze
    return requests.get(URL).json()       # ❌ blocking HTTP inside async def

@app.get("/ok-sync")
def ok_sync():                            # ✅ plain def → runs in threadpool
    time.sleep(2)
    return requests.get(URL).json()

@app.get("/good-async")
async def good_async():                   # ✅ truly async
    await asyncio.sleep(2)
    async with httpx.AsyncClient() as client:
        r = await client.get(URL)
    return r.json()

@app.get("/mixed")
async def mixed():
    data = await fetch_async()
    result = await run_in_threadpool(blocking_sdk_call, data)   # from starlette.concurrency
    # or: await asyncio.to_thread(blocking_sdk_call, data)
    return result
```

**Rules**
- Inside `async def`: never call blocking I/O or `time.sleep`.
- If unsure / using sync libraries → use `def`.
- CPU-heavy work (image processing, ML inference, big reports) → offload to a process pool or a task queue (Celery/ARQ), not the request.
- Dependencies follow the same rule (can be `def` or `async def`).

**Interview Qs**
- When should a FastAPI endpoint be `async def` vs `def`?
- What happens if you use `requests` inside `async def`? → Blocks the event loop; throughput collapses.

---

## 14. Settings & Configuration

```python
# app/core/config.py
from functools import lru_cache
from pydantic import PostgresDsn, SecretStr, AnyHttpUrl
from pydantic_settings import BaseSettings, SettingsConfigDict

class Settings(BaseSettings):
    model_config = SettingsConfigDict(env_file=".env", env_file_encoding="utf-8", extra="ignore")

    app_name: str = "My API"
    environment: str = "development"
    debug: bool = False
    database_url: PostgresDsn
    redis_url: str = "redis://localhost:6379/0"
    jwt_secret: SecretStr
    jwt_algorithm: str = "HS256"
    access_token_expire_minutes: int = 15
    cors_origins: list[AnyHttpUrl] = []          # JSON list in env: CORS_ORIGINS='["https://app.com"]'

@lru_cache                                       # read env once
def get_settings() -> Settings:
    return Settings()

SettingsDep = Annotated[Settings, Depends(get_settings)]

@app.get("/info")
def info(settings: SettingsDep):
    return {"app": settings.app_name, "env": settings.environment}
```

- Env vars are validated at startup → missing/invalid config fails fast.
- `SecretStr` prevents secrets from appearing in logs.
- Using a dependency makes it easy to override settings in tests.

---

## 15. Databases: SQLAlchemy 2.0

**SQLAlchemy** is the standard Python ORM. Version 2.0 uses typed `Mapped[...]` models and the `select()` API.

### Setup

```python
# app/db/session.py
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker, DeclarativeBase

engine = create_engine(
    str(settings.database_url),         # postgresql+psycopg://user:pass@localhost:5432/app
    pool_size=10, max_overflow=20,      # connection pool
    pool_pre_ping=True,                 # drop dead connections
)
SessionLocal = sessionmaker(bind=engine, autoflush=False, expire_on_commit=False)

class Base(DeclarativeBase):
    pass
```

### Models

```python
# app/models/user.py
from datetime import datetime
from sqlalchemy import String, ForeignKey, func, Index
from sqlalchemy.orm import Mapped, mapped_column, relationship

class User(Base):
    __tablename__ = "users"

    id: Mapped[int] = mapped_column(primary_key=True)
    email: Mapped[str] = mapped_column(String(255), unique=True, index=True)
    name: Mapped[str] = mapped_column(String(100))
    hashed_password: Mapped[str]
    role: Mapped[str] = mapped_column(default="user")
    is_active: Mapped[bool] = mapped_column(default=True)
    created_at: Mapped[datetime] = mapped_column(server_default=func.now())

    posts: Mapped[list["Post"]] = relationship(back_populates="author", cascade="all, delete-orphan")

class Post(Base):
    __tablename__ = "posts"
    id: Mapped[int] = mapped_column(primary_key=True)
    title: Mapped[str] = mapped_column(String(200))
    body: Mapped[str | None]                          # nullable because of `| None`
    author_id: Mapped[int] = mapped_column(ForeignKey("users.id", ondelete="CASCADE"), index=True)
    author: Mapped[User] = relationship(back_populates="posts")
```

### CRUD with the 2.0 API

```python
from sqlalchemy import select, update, delete, func
from sqlalchemy.orm import selectinload

# Create
user = User(email="r@x.com", name="Rohit", hashed_password=hash_password("pw"))
db.add(user)
db.commit()
db.refresh(user)                                       # load generated id/defaults

# Read
db.get(User, 1)                                        # by primary key
db.scalar(select(User).where(User.email == "r@x.com")) # one or None
users = db.scalars(
    select(User)
    .where(User.is_active, User.name.ilike("%ro%"))
    .order_by(User.created_at.desc())
    .offset(0).limit(20)
).all()
total = db.scalar(select(func.count()).select_from(User))

# Avoid N+1: eager-load relationships
users_with_posts = db.scalars(select(User).options(selectinload(User.posts))).all()

# Joins & aggregates
rows = db.execute(
    select(User.name, func.count(Post.id).label("post_count"))
    .join(Post, isouter=True)
    .group_by(User.id)
    .having(func.count(Post.id) > 2)
).all()

# Update
user.name = "New Name"; db.commit()
db.execute(update(User).where(User.last_login < cutoff).values(is_active=False)); db.commit()

# Delete
db.delete(user); db.commit()
db.execute(delete(Post).where(Post.author_id == 1)); db.commit()
```

### Transactions

```python
with SessionLocal() as db, db.begin():         # commits on success, rolls back on exception
    sender = db.get(Account, 1, with_for_update=True)    # row lock (SELECT ... FOR UPDATE)
    receiver = db.get(Account, 2, with_for_update=True)
    if sender.balance < 100:
        raise ValueError("insufficient funds")
    sender.balance -= 100
    receiver.balance += 100
```

### Repository pattern

```python
class UserRepository:
    def __init__(self, db: Session):
        self.db = db
    def get_by_email(self, email: str) -> User | None:
        return self.db.scalar(select(User).where(User.email == email))
    def create(self, **fields) -> User:
        user = User(**fields)
        self.db.add(user)
        self.db.flush()          # get id without committing (service decides when to commit)
        return user
    def list(self, offset: int, limit: int) -> list[User]:
        return list(self.db.scalars(select(User).offset(offset).limit(limit)))
```

**SQLModel** (by FastAPI's author) combines SQLAlchemy models + Pydantic models in one class — handy for small apps. For MongoDB use **Beanie** (async ODM) or **Motor**.

---

## 16. Async SQLAlchemy

For fully async apps (`async def` routes), use async drivers (`asyncpg`) and `AsyncSession`.

```python
# app/db/session.py
from sqlalchemy.ext.asyncio import create_async_engine, async_sessionmaker, AsyncSession

engine = create_async_engine(
    "postgresql+asyncpg://user:pass@localhost/app",
    pool_size=10, max_overflow=20, pool_pre_ping=True,
)
AsyncSessionLocal = async_sessionmaker(engine, expire_on_commit=False)

async def get_db():
    async with AsyncSessionLocal() as session:
        yield session

AsyncDb = Annotated[AsyncSession, Depends(get_db)]

@app.get("/users/{user_id}", response_model=UserOut)
async def get_user(user_id: int, db: AsyncDb):
    user = await db.get(User, user_id)
    if not user:
        raise NotFoundError(f"User {user_id} not found")
    return user

@app.get("/users", response_model=list[UserOut])
async def list_users(db: AsyncDb, p: Pagination):
    result = await db.scalars(select(User).offset(p["offset"]).limit(p["limit"]))
    return result.all()

@app.post("/users", response_model=UserOut, status_code=201)
async def create_user(data: UserCreate, db: AsyncDb):
    user = User(**data.model_dump(exclude={"password"}), hashed_password=hash_password(data.password))
    db.add(user)
    try:
        await db.commit()
    except IntegrityError:
        await db.rollback()
        raise ConflictError("Email already registered")
    await db.refresh(user)
    return user
```

Async gotcha: **lazy loading doesn't work** in async (accessing `user.posts` triggers I/O without `await` → error). Always eager-load with `selectinload`/`joinedload`.

---

## 17. Migrations with Alembic

**Migrations** version-control your DB schema changes. Never use `Base.metadata.create_all()` in production.

```bash
uv add alembic
alembic init -t async alembic       # or `alembic init alembic` for sync
```

```python
# alembic/env.py (key lines)
from app.core.config import get_settings
from app.db.base import Base
import app.models                    # import all models so autogenerate sees them

config.set_main_option("sqlalchemy.url", str(get_settings().database_url))
target_metadata = Base.metadata
```

```bash
alembic revision --autogenerate -m "create users and posts"   # generates a migration file — REVIEW IT
alembic upgrade head                                          # apply
alembic downgrade -1                                          # roll back one
alembic history; alembic current
```

```python
# alembic/versions/xxxx_add_phone_to_users.py
def upgrade() -> None:
    op.add_column("users", sa.Column("phone", sa.String(15), nullable=True))
    op.create_index("ix_users_phone", "users", ["phone"])

def downgrade() -> None:
    op.drop_index("ix_users_phone", table_name="users")
    op.drop_column("users", "phone")
```

Best practices: review autogenerated migrations, keep them small, make changes **backwards compatible** (expand → migrate data → contract), run migrations in CI/deploy step before starting new app versions.

---

## 18. Other Databases: SQLModel & MongoDB (Beanie)

### SQLModel — one class for the table and the schema

**SQLModel** (by FastAPI's author) builds on **SQLAlchemy + Pydantic**: a class can be both a database table and a validation/serialization model, which removes duplication in small/medium apps.

The recommended pattern still uses **separate models per purpose**, but shares fields through inheritance:

```python
from sqlmodel import SQLModel, Field, Session, create_engine, select
from fastapi import FastAPI, Depends, HTTPException, Query
from typing import Annotated

# Shared fields
class HeroBase(SQLModel):
    name: str = Field(index=True, min_length=1, max_length=100)
    age: int | None = Field(default=None, ge=0)

# Table model (table=True → SQLAlchemy table)
class Hero(HeroBase, table=True):
    id: int | None = Field(default=None, primary_key=True)
    secret_name: str                                  # stored, never returned

# API schemas (plain Pydantic models)
class HeroCreate(HeroBase):
    secret_name: str

class HeroPublic(HeroBase):
    id: int

class HeroUpdate(SQLModel):
    name: str | None = None
    age: int | None = None

engine = create_engine("sqlite:///heroes.db", connect_args={"check_same_thread": False})

def get_session():
    with Session(engine) as session:
        yield session

SessionDep = Annotated[Session, Depends(get_session)]
app = FastAPI()

@app.post("/heroes", response_model=HeroPublic, status_code=201)
def create_hero(data: HeroCreate, session: SessionDep):
    hero = Hero.model_validate(data)                  # validate & convert to the table model
    session.add(hero)
    session.commit()
    session.refresh(hero)
    return hero                                       # secret_name filtered out by HeroPublic

@app.get("/heroes", response_model=list[HeroPublic])
def list_heroes(session: SessionDep, offset: int = 0, limit: Annotated[int, Query(le=100)] = 20):
    return session.exec(select(Hero).offset(offset).limit(limit)).all()

@app.patch("/heroes/{hero_id}", response_model=HeroPublic)
def update_hero(hero_id: int, data: HeroUpdate, session: SessionDep):
    hero = session.get(Hero, hero_id)
    if not hero:
        raise HTTPException(404, "Hero not found")
    hero.sqlmodel_update(data.model_dump(exclude_unset=True))   # only fields the client sent
    session.add(hero)
    session.commit()
    session.refresh(hero)
    return hero
```

**SQLModel vs SQLAlchemy + Pydantic**

| SQLModel | SQLAlchemy 2.0 + separate Pydantic schemas |
|---|---|
| Less code, shared fields via inheritance | More explicit, full SQLAlchemy power |
| Great for small/medium apps & prototypes | Better for large/complex domains, advanced queries |
| Still uses SQLAlchemy underneath (and Alembic for migrations) | The industry standard, most docs/examples |

Either way: use Alembic migrations, never `SQLModel.metadata.create_all()` in production.

---

### MongoDB with Beanie (async ODM)

**Beanie** is an async ODM for MongoDB built on **Pydantic** — documents are Pydantic models, so they plug straight into FastAPI. (The older **Motor** driver is being replaced by PyMongo's native async client; recent Beanie versions support it — check the versions you install.)

```python
from contextlib import asynccontextmanager
from datetime import datetime, UTC
from typing import Annotated
from beanie import Document, Indexed, PydanticObjectId, init_beanie
from pydantic import BaseModel, Field
from pymongo import AsyncMongoClient, ASCENDING, DESCENDING, IndexModel

class Address(BaseModel):                      # embedded document
    city: str
    pincode: str

class Product(Document):
    name: str
    sku: Annotated[str, Indexed(unique=True)]
    price_paise: int = Field(gt=0)
    tags: list[str] = []
    address: Address | None = None
    created_at: datetime = Field(default_factory=lambda: datetime.now(UTC))

    class Settings:
        name = "products"                      # collection name
        indexes = [IndexModel([("tags", ASCENDING), ("created_at", DESCENDING)])]

class ProductCreate(BaseModel):
    name: str
    sku: str
    price_paise: int = Field(gt=0)
    tags: list[str] = []

@asynccontextmanager
async def lifespan(app):
    client = AsyncMongoClient(settings.mongo_url)
    await init_beanie(database=client["shop"], document_models=[Product])   # also creates indexes
    yield
    await client.close()

app = FastAPI(lifespan=lifespan)

@app.post("/products", response_model=Product, status_code=201)
async def create_product(data: ProductCreate):
    return await Product(**data.model_dump()).insert()

@app.get("/products/{product_id}", response_model=Product)
async def get_product(product_id: PydanticObjectId):          # validates the ObjectId format → 422 if invalid
    product = await Product.get(product_id)
    if not product:
        raise HTTPException(404, "Product not found")
    return product

@app.get("/products", response_model=list[Product])
async def search_products(tag: str | None = None, max_price: int | None = None, skip: int = 0, limit: int = 20):
    query = Product.find()
    if tag:
        query = query.find(Product.tags == tag)
    if max_price is not None:
        query = query.find(Product.price_paise <= max_price)
    return await query.sort(-Product.created_at).skip(skip).limit(min(limit, 100)).to_list()

@app.patch("/products/{product_id}/price")
async def update_price(product_id: PydanticObjectId, price_paise: int):
    product = await Product.get(product_id)
    if not product:
        raise HTTPException(404, "Product not found")
    await product.set({Product.price_paise: price_paise})   # atomic $set
    return {"ok": True}
```

MongoDB + FastAPI tips:
- Define **indexes** in `Settings` for every query pattern; add unique indexes for natural keys (SKU, email).
- Return **response models** that hide internal fields; convert `ObjectId` to string (`PydanticObjectId` does it).
- Embed data read together (addresses, line items); reference data that grows unbounded or is shared.
- Use **transactions** (replica set required) only when multiple documents must change atomically.
- Cursor-based pagination (`_id > last_id`) for large collections instead of big `skip` values.

**SQL or MongoDB for a FastAPI app?** Default to **Postgres** (relations, transactions, reporting); choose MongoDB when data is document-shaped, schemas vary a lot, and access patterns are known.

### Interview Qs

1. What is SQLModel and how does it relate to SQLAlchemy and Pydantic?
2. Why still keep separate Create/Public/Update models with SQLModel?
3. How do you integrate MongoDB with FastAPI? What is Beanie?
4. How do you validate MongoDB ObjectIds in path parameters?
5. Embedding vs referencing in MongoDB?

---

## 19. Authentication: OAuth2 + JWT

The standard FastAPI setup: **OAuth2 Password flow** with **JWT bearer tokens**, passwords hashed with **Argon2/bcrypt**.

```bash
uv add pyjwt "pwdlib[argon2]"      # (older tutorials use python-jose + passlib)
```

### Security helpers

```python
# app/core/security.py
from datetime import datetime, timedelta, UTC
import jwt
from pwdlib import PasswordHash

password_hash = PasswordHash.recommended()        # Argon2

def hash_password(plain: str) -> str:
    return password_hash.hash(plain)

def verify_password(plain: str, hashed: str) -> bool:
    return password_hash.verify(plain, hashed)

def create_access_token(subject: str, role: str, expires_minutes: int = 15) -> str:
    now = datetime.now(UTC)
    payload = {"sub": subject, "role": role, "iat": now, "exp": now + timedelta(minutes=expires_minutes), "type": "access"}
    return jwt.encode(payload, settings.jwt_secret.get_secret_value(), algorithm=settings.jwt_algorithm)

def decode_token(token: str) -> dict:
    try:
        return jwt.decode(token, settings.jwt_secret.get_secret_value(), algorithms=[settings.jwt_algorithm])
    except jwt.ExpiredSignatureError:
        raise HTTPException(401, "Token expired", headers={"WWW-Authenticate": "Bearer"})
    except jwt.InvalidTokenError:
        raise HTTPException(401, "Invalid token", headers={"WWW-Authenticate": "Bearer"})
```

Always pass `algorithms=[...]` explicitly when decoding (prevents algorithm-confusion attacks).

### Login endpoint & protected routes

```python
from fastapi.security import OAuth2PasswordBearer, OAuth2PasswordRequestForm

oauth2_scheme = OAuth2PasswordBearer(tokenUrl="/auth/token")   # enables the "Authorize" button in /docs

class Token(BaseModel):
    access_token: str
    token_type: str = "bearer"

@router.post("/auth/token", response_model=Token)
def login(form: Annotated[OAuth2PasswordRequestForm, Depends()], db: DbSession):
    user = db.scalar(select(User).where(User.email == form.username))   # OAuth2 form uses "username"
    if not user or not verify_password(form.password, user.hashed_password):
        raise HTTPException(401, "Incorrect email or password", headers={"WWW-Authenticate": "Bearer"})
    return Token(access_token=create_access_token(str(user.id), user.role))

def get_current_user(token: Annotated[str, Depends(oauth2_scheme)], db: DbSession) -> User:
    payload = decode_token(token)
    if payload.get("type") != "access":
        raise HTTPException(401, "Invalid token type")
    user = db.get(User, int(payload["sub"]))
    if user is None or not user.is_active:
        raise HTTPException(401, "User not found or inactive")
    return user

CurrentUser = Annotated[User, Depends(get_current_user)]

@router.get("/users/me", response_model=UserOut)
def read_me(user: CurrentUser):
    return user
```

To avoid **timing-based user enumeration**, run a dummy password verify even when the user doesn't exist.

### Register

```python
@router.post("/auth/register", response_model=UserOut, status_code=201)
def register(data: UserCreate, db: DbSession):
    if db.scalar(select(User).where(User.email == data.email)):
        raise HTTPException(409, "Email already registered")
    user = User(email=data.email, name=data.name, hashed_password=hash_password(data.password))
    db.add(user); db.commit(); db.refresh(user)
    return user
```

### Refresh tokens (HttpOnly cookie)

```python
@router.post("/auth/login")
def login_cookie(form: Annotated[OAuth2PasswordRequestForm, Depends()], response: Response, db: DbSession):
    user = authenticate(db, form.username, form.password)
    refresh = create_refresh_token(str(user.id), token_version=user.token_version)   # e.g. 7 days, type="refresh"
    response.set_cookie("refresh_token", refresh, httponly=True, secure=True, samesite="strict",
                        path="/auth/refresh", max_age=7 * 24 * 3600)
    return {"access_token": create_access_token(str(user.id), user.role), "token_type": "bearer"}

@router.post("/auth/refresh")
def refresh(response: Response, db: DbSession, refresh_token: Annotated[str | None, Cookie()] = None):
    if not refresh_token:
        raise HTTPException(401, "Missing refresh token")
    payload = decode_token(refresh_token)
    user = db.get(User, int(payload["sub"]))
    if not user or payload.get("type") != "refresh" or payload.get("ver") != user.token_version:
        raise HTTPException(401, "Refresh token revoked")
    # rotate: issue a new refresh token too
    ...
```

Logout-everywhere: increment `user.token_version` → all old refresh tokens become invalid.

### API keys (service-to-service)

```python
from fastapi.security import APIKeyHeader
import secrets

api_key_header = APIKeyHeader(name="X-API-Key")

def verify_api_key(key: Annotated[str, Depends(api_key_header)]):
    if not secrets.compare_digest(key, settings.internal_api_key.get_secret_value()):   # constant-time compare
        raise HTTPException(403, "Invalid API key")
```

---

## 20. Authorization: Roles, Scopes, Ownership

```python
# Role-based
def require_roles(*roles: str):
    def checker(user: CurrentUser) -> User:
        if user.role not in roles:
            raise HTTPException(403, "Insufficient permissions")
        return user
    return checker

@router.delete("/users/{user_id}", status_code=204, dependencies=[Depends(require_roles("admin"))])
def delete_user(user_id: int, db: DbSession): ...

# Ownership (prevents IDOR — accessing someone else's resource by changing the ID)
@router.patch("/posts/{post_id}", response_model=PostOut)
def update_post(post_id: int, data: PostUpdate, user: CurrentUser, db: DbSession):
    post = db.get(Post, post_id)
    if not post:
        raise HTTPException(404, "Post not found")
    if post.author_id != user.id and user.role != "admin":
        raise HTTPException(403, "Not your post")        # or 404 to hide existence
    for k, v in data.model_dump(exclude_unset=True).items():
        setattr(post, k, v)
    db.commit(); db.refresh(post)
    return post
```

OAuth2 **scopes** (`Security(get_current_user, scopes=["items:write"])` + `SecurityScopes`) are available for fine-grained permissions shown in the docs.

**Rule**: every route that touches user data must check both authentication (who) and authorization (allowed?). Filter queries by the owner: `select(Order).where(Order.user_id == user.id)`.

---

## 21. Multi-Tenancy & API Versioning

### Part 1 — Multi-tenancy (SaaS)

A **multi-tenant** app serves many customers (**tenants** — companies, workspaces, schools) from one deployment, while keeping each tenant's data **isolated**. A single missing filter can leak one company's data to another — the most serious bug a SaaS can have.

#### Isolation models

| Model | How | Pros | Cons |
|---|---|---|---|
| **Shared tables** (`tenant_id` column) | Every row has `tenant_id`; every query filters by it | Cheapest, simplest ops, easy analytics | Leak risk if a filter is missed → needs strong guardrails |
| **Schema per tenant** (Postgres schemas) | Same DB, separate schema per tenant | Better isolation, per-tenant backup possible | Migrations × N schemas, connection/search_path handling |
| **Database per tenant** | Separate DB (or cluster) per tenant | Strongest isolation, per-tenant scaling/compliance | Expensive, complex ops at scale |

Most SaaS products start with **shared tables + strong guardrails**, and move big/regulated customers to dedicated databases later.

#### Resolving the current tenant

- ✅ From the **authenticated user/token** (JWT claim or the user's DB record) — the source of truth.
- ✅ **Subdomain** (`acme.app.com`) or path (`/t/acme/...`) — then **verify the user belongs to that tenant**.
- ⚠️ `X-Tenant-ID` header — only for trusted internal services; never trust it alone from browsers.

#### Implementation: shared tables with automatic filtering

Guardrail 1: the tenant comes from the user, via a dependency. Guardrail 2: **every ORM query is filtered automatically**, so forgetting a `where(tenant_id == ...)` can't leak data. The tenant is stored on the **session** (`Session.info`), so every query made with that session is scoped.

```python
from typing import Annotated
from fastapi import Depends, FastAPI, HTTPException
from sqlalchemy import String, UniqueConstraint, create_engine, event, select
from sqlalchemy.orm import DeclarativeBase, Mapped, Session, mapped_column, sessionmaker, with_loader_criteria
from sqlalchemy.pool import StaticPool

class Base(DeclarativeBase): ...

class TenantScoped:
    """Mixin: every model with tenant_id is filtered automatically."""
    tenant_id: Mapped[int] = mapped_column(index=True)

class Project(TenantScoped, Base):
    __tablename__ = "projects"
    __table_args__ = (UniqueConstraint("tenant_id", "name"),)   # uniqueness is PER TENANT
    id: Mapped[int] = mapped_column(primary_key=True)
    name: Mapped[str] = mapped_column(String(100))

# In-memory SQLite for the demo (StaticPool = one shared connection). Use Postgres in production.
engine = create_engine("sqlite://", connect_args={"check_same_thread": False}, poolclass=StaticPool)
SessionLocal = sessionmaker(bind=engine)

@event.listens_for(Session, "do_orm_execute")
def _add_tenant_filter(execute_state):
    tenant_id = execute_state.session.info.get("tenant_id")
    if execute_state.is_select and tenant_id is not None:
        execute_state.statement = execute_state.statement.options(
            with_loader_criteria(TenantScoped, lambda cls: cls.tenant_id == tenant_id, include_aliases=True)
        )

# --- dependencies ---
def get_current_user():                        # real app: decode JWT (see Authentication)
    return {"id": 1, "tenant_id": 10}

def tenant_session(user: Annotated[dict, Depends(get_current_user)]):
    db = SessionLocal(info={"tenant_id": user["tenant_id"]})   # every query on this session is scoped
    try:
        yield db
    finally:
        db.close()

TenantDb = Annotated[Session, Depends(tenant_session)]
CurrentUser = Annotated[dict, Depends(get_current_user)]
app = FastAPI()

@app.post("/projects", status_code=201)
def create_project(name: str, db: TenantDb, user: CurrentUser):
    project = Project(name=name, tenant_id=user["tenant_id"])   # tenant set from the USER, never from input
    db.add(project)
    db.commit()
    return {"id": project.id, "name": project.name}

@app.get("/projects")
def list_projects(db: TenantDb):
    return [{"id": p.id, "name": p.name} for p in db.scalars(select(Project).order_by(Project.id))]   # filtered automatically

@app.get("/projects/{project_id}")
def get_project(project_id: int, db: TenantDb):
    project = db.scalar(select(Project).where(Project.id == project_id))
    if project is None:
        raise HTTPException(404, "Project not found")            # other tenants' IDs look like 404
    return {"id": project.id, "name": project.name}
```

**Why not a `ContextVar` set in the dependency?** FastAPI runs a plain-`def` generator dependency's setup and teardown in **different threadpool contexts**, so `var.reset(token)` after `yield` fails ("Token was created in a different Context"), and a value set there isn't reliably visible in the route. Attaching the tenant to the session (or passing it explicitly) avoids that. (In `async def` dependencies contextvars behave as expected, but explicit is still clearer.)

Note: `db.get(Model, id)` may return an object from the session identity map without running a SELECT — use `select(...)` (or check `tenant_id`) for tenant-scoped lookups.

#### Defence in depth: Postgres Row-Level Security (RLS)

```sql
ALTER TABLE projects ENABLE ROW LEVEL SECURITY;
CREATE POLICY tenant_isolation ON projects
  USING (tenant_id = current_setting('app.current_tenant')::int);
-- per request/transaction:  SET LOCAL app.current_tenant = '10';
```

Even if application code forgets a filter, the database refuses to return other tenants' rows (the app must connect as a non-owner role without `BYPASSRLS`).

#### Multi-tenancy checklist

- [ ] Tenant derived from the authenticated user; membership verified for subdomain/path tenants
- [ ] Automatic query filtering (ORM criteria) + RLS for critical tables
- [ ] Unique constraints and indexes include `tenant_id` (`(tenant_id, email)`)
- [ ] **Tests that try to read/update another tenant's data** and expect 404/403
- [ ] Cache keys, file storage paths, search indexes and queues all include the tenant
- [ ] Background jobs carry `tenant_id` explicitly (context vars don't cross process boundaries)
- [ ] Per-tenant rate limits & quotas (noisy-neighbour protection)
- [ ] Tenant-aware logging/metrics; admin "impersonation" audited
- [ ] Data export & deletion per tenant (GDPR, offboarding)

---

### Part 2 — API versioning

Once clients (mobile apps, partners) depend on your API, you can't change it freely: old mobile app versions stay installed for years.

#### Breaking vs non-breaking changes

| Non-breaking (safe) | Breaking (needs a new version) |
|---|---|
| Add a new endpoint | Remove/rename an endpoint or field |
| Add an **optional** request field | Add a **required** request field |
| Add a field to a response | Change a field's type/format/meaning |
| Add a new enum value* | Change status codes or error format |
| Relax validation | Tighten validation, change auth requirements |

\*Only if clients handle unknown values gracefully — document that they must.

#### Strategies

| Strategy | Example | Notes |
|---|---|---|
| **URL path** | `/api/v1/users` | Most common, obvious, easy to route & cache |
| Header | `X-API-Version: 2` / `Accept: application/vnd.shop.v2+json` | Clean URLs, harder to test in a browser |
| Query param | `/users?version=2` | Simple but easy to forget |
| Date-based (Stripe style) | `Stripe-Version: 2025-06-30` pinned per account | Fine-grained; needs transformation layers |

#### URL versioning in FastAPI

```python
from fastapi import APIRouter, FastAPI, Response
from pydantic import BaseModel

# One service/data layer shared by all versions
USERS = {1: {"id": 1, "first_name": "Rohit", "last_name": "Dahiya", "email": "r@x.com"}}

class UserV1(BaseModel):          # v1 contract: single "name" field
    id: int
    name: str
    email: str

class UserV2(BaseModel):          # v2 contract: split names
    id: int
    first_name: str
    last_name: str
    email: str

v1 = APIRouter(prefix="/api/v1", tags=["v1"])
v2 = APIRouter(prefix="/api/v2", tags=["v2"])

@v1.get("/users/{user_id}", response_model=UserV1, deprecated=True)     # shown as deprecated in /docs
def get_user_v1(user_id: int, response: Response):
    u = USERS[user_id]
    response.headers["Deprecation"] = "true"
    response.headers["Sunset"] = "Wed, 31 Dec 2026 23:59:59 GMT"         # when v1 will be removed
    response.headers["Link"] = '</api/v2/users>; rel="successor-version"'
    return {"id": u["id"], "name": f'{u["first_name"]} {u["last_name"]}', "email": u["email"]}

@v2.get("/users/{user_id}", response_model=UserV2)
def get_user_v2(user_id: int):
    return USERS[user_id]

app = FastAPI()
app.include_router(v1)
app.include_router(v2)
```

Separate docs per version: build one `FastAPI()` sub-app per version and `app.mount("/api/v1", v1_app)` — each gets its own `/docs` and OpenAPI schema.

#### Versioning best practices

- **Version the contract, not the code**: share services/repositories; keep version-specific code in routers + schemas (adapters).
- Prefer **additive, non-breaking changes** — most changes shouldn't need a new version.
- Only bump the **major** version for breaking changes; keep at most 2 versions alive.
- **Deprecate before removing**: mark `deprecated=True`, send `Deprecation`/`Sunset` headers, announce in a changelog, email API consumers.
- **Measure usage per version** (logs/metrics by path prefix or header) before turning anything off.
- Mobile apps: combine API versioning with a **minimum supported app version** check (force-update screen).
- Contract tests per version so old versions don't break accidentally.

### Interview Qs

1. What are the three multi-tenancy isolation models and their trade-offs?
2. How do you determine the current tenant securely?
3. How do you make sure no query forgets the tenant filter? (automatic ORM criteria, RLS, tests)
4. Why must unique constraints include `tenant_id`?
5. What else besides DB queries must be tenant-aware? (cache, files, queues, rate limits, logs)
6. What counts as a breaking API change?
7. URL vs header vs date-based versioning — pros and cons?
8. How do you deprecate and sunset an API version safely?
9. How would you structure code to support v1 and v2 without duplicating business logic?

---

## 22. Middleware & CORS

Middleware runs **for every request** before the route and **after** the response is created.

```python
import time, uuid, logging
from fastapi import Request

@app.middleware("http")
async def add_request_id_and_timing(request: Request, call_next):
    request_id = request.headers.get("X-Request-ID", str(uuid.uuid4()))
    request.state.request_id = request_id               # available in handlers
    start = time.perf_counter()
    response = await call_next(request)                 # run the rest of the app
    duration_ms = (time.perf_counter() - start) * 1000
    response.headers["X-Request-ID"] = request_id
    response.headers["X-Process-Time-Ms"] = f"{duration_ms:.1f}"
    logging.getLogger("access").info("%s %s %s %.1fms", request.method, request.url.path, response.status_code, duration_ms)
    return response
```

### Built-in middleware

```python
from fastapi.middleware.cors import CORSMiddleware
from fastapi.middleware.gzip import GZipMiddleware
from fastapi.middleware.trustedhost import TrustedHostMiddleware
from fastapi.middleware.httpsredirect import HTTPSRedirectMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://myapp.com", "http://localhost:5173"],   # never "*" with credentials
    allow_credentials=True,
    allow_methods=["GET", "POST", "PUT", "PATCH", "DELETE"],
    allow_headers=["Authorization", "Content-Type"],
)
app.add_middleware(GZipMiddleware, minimum_size=1000)
app.add_middleware(TrustedHostMiddleware, allowed_hosts=["api.myapp.com", "localhost"])
```

Order: middleware added **last** runs **first** (outermost).

**Middleware vs dependencies**: middleware for cross-cutting concerns on every request (logging, timing, CORS, request IDs, security headers). Dependencies for per-route needs (auth, DB, pagination), with typed access and docs.

---

## 23. Lifespan Events

Run code **once at startup** (connect DB/Redis, load ML model, warm caches) and **once at shutdown** (close pools) — replaces the deprecated `@app.on_event("startup")`.

```python
from contextlib import asynccontextmanager
import httpx
import redis.asyncio as redis

@asynccontextmanager
async def lifespan(app: FastAPI):
    # startup
    app.state.http = httpx.AsyncClient(timeout=10)          # one shared client (connection pooling)
    app.state.redis = redis.from_url(settings.redis_url)
    app.state.model = load_ml_model("model.pkl")            # load heavy things ONCE
    yield
    # shutdown (graceful)
    await app.state.http.aclose()
    await app.state.redis.aclose()
    await engine.dispose()

app = FastAPI(lifespan=lifespan)

@app.get("/predict")
async def predict(request: Request, x: float):
    return {"y": request.app.state.model.predict([[x]]).tolist()}
```

---

## 24. Background Tasks & Job Queues

### BackgroundTasks — small fire-and-forget work after the response

```python
from fastapi import BackgroundTasks

def send_welcome_email(email: str, name: str):
    ...   # runs AFTER the response is sent, in the same process

@router.post("/users", status_code=201)
def create_user(data: UserCreate, background: BackgroundTasks, db: DbSession):
    user = create(db, data)
    background.add_task(send_welcome_email, user.email, user.name)
    return user
```

Limits: same process (lost if the server restarts), no retries, no scheduling, adds load to the web worker. Don't pass the request's DB session into a background task — open a new one.

### Real job queues for heavy/important work

| Tool | Notes |
|---|---|
| **Celery** (+ Redis/RabbitMQ) | Most popular, retries, scheduling (beat), mature |
| **ARQ** | Async, Redis-based, lightweight — good match for FastAPI |
| **Dramatiq**, **RQ**, **Taskiq** | Alternatives |

```python
# tasks.py (Celery)
from celery import Celery
celery_app = Celery("worker", broker=settings.redis_url, backend=settings.redis_url)

@celery_app.task(bind=True, autoretry_for=(ConnectionError,), retry_backoff=True, max_retries=5)
def generate_report(self, report_id: int):
    ...

# route: enqueue & return immediately
@router.post("/reports", status_code=202)
def request_report(params: ReportIn, user: CurrentUser):
    report = create_report_row(user.id, params)
    task = generate_report.delay(report.id)
    return {"report_id": report.id, "task_id": task.id, "status": "queued"}

@router.get("/reports/{report_id}")
def report_status(report_id: int): ...       # client polls, or use websockets/SSE/email when done
```

Use queues for: emails, PDF/report generation, image/video processing, ML inference batches, webhooks to third parties, anything slow or needing retries.

---

## 25. Task Queues in Depth: Celery & ARQ

`BackgroundTasks` runs work in the same process after the response — fine for tiny jobs, but lost on restart and never retried. Real background work (emails, reports, image processing, webhooks, syncs) belongs in a **task queue** with **separate worker processes**.

```
FastAPI (producer) ──enqueue(task, ids)──► Broker (Redis / RabbitMQ / SQS) ──► Worker processes (consumers)
      │ 202 Accepted + job_id                                                       │
      └──────── GET /jobs/{id} ◄──── Result backend / your DB (status, result) ◄──────┘
```

### 1. Celery

The most widely used Python task queue: retries, scheduling (beat), routing, chords/groups, many brokers, monitoring (Flower).

```python
# app/worker.py
from celery import Celery
from celery.schedules import crontab

celery_app = Celery("shop", broker="redis://localhost:6379/0", backend="redis://localhost:6379/1")
celery_app.conf.update(
    task_serializer="json", accept_content=["json"], result_serializer="json",   # never pickle untrusted data
    timezone="UTC", enable_utc=True,
    task_acks_late=True,                 # ack AFTER the task finishes → a crashed worker's task is redelivered
    task_reject_on_worker_lost=True,
    worker_prefetch_multiplier=1,        # don't hoard tasks (fair distribution for long tasks)
    task_time_limit=300,                 # hard kill after 5 min
    task_soft_time_limit=240,            # raises SoftTimeLimitExceeded first → chance to clean up
    result_expires=3600,
    task_routes={
        "app.tasks.send_email": {"queue": "emails"},
        "app.tasks.generate_report": {"queue": "reports"},     # slow jobs can't block emails
    },
    beat_schedule={
        "nightly-cleanup": {"task": "app.tasks.cleanup_expired_carts", "schedule": crontab(hour=2, minute=0)},
        "sync-rates-every-15m": {"task": "app.tasks.sync_exchange_rates", "schedule": 15 * 60},
    },
)
```

```python
# app/tasks.py
import httpx
from celery.utils.log import get_task_logger
from app.worker import celery_app

logger = get_task_logger(__name__)

@celery_app.task(
    bind=True,
    autoretry_for=(httpx.TransportError, httpx.HTTPStatusError),   # transient failures only
    retry_backoff=True, retry_backoff_max=600, retry_jitter=True,  # 1s, 2s, 4s … capped, randomized
    max_retries=5,
)
def send_email(self, email_id: int) -> None:
    with SessionLocal() as db:                         # a NEW session per task — never reuse the request's
        email = db.get(OutgoingEmail, email_id)
        if email is None or email.status == "sent":    # idempotency guard: already done → no-op
            return
        response = httpx.post(PROVIDER_URL, json=email.payload(), timeout=10,
                              headers={"Idempotency-Key": f"email-{email_id}"})
        response.raise_for_status()
        email.status = "sent"
        db.commit()
        logger.info("email %s sent (attempt %s)", email_id, self.request.retries + 1)

@celery_app.task(bind=True)
def generate_report(self, report_id: int) -> str:
    self.update_state(state="PROGRESS", meta={"percent": 0})
    rows = load_rows(report_id)
    for i, chunk in enumerate(chunked(rows, 1000), start=1):
        write_chunk(report_id, chunk)
        self.update_state(state="PROGRESS", meta={"percent": round(i * 1000 / max(len(rows), 1) * 100)})
    return upload_report(report_id)                    # returns a URL/key, not the file itself
```

```python
# FastAPI side: enqueue, return 202, poll status
from celery.result import AsyncResult

@router.post("/reports", status_code=202)
def request_report(params: ReportRequest, user: CurrentUser, db: DbSession):
    report = Report(owner_id=user.id, params=params.model_dump(), status="queued")
    db.add(report); db.commit()                          # COMMIT FIRST, then enqueue (see "enqueue after commit")
    task = generate_report.apply_async(args=[report.id], queue="reports")
    report.task_id = task.id; db.commit()
    return {"report_id": report.id, "status_url": f"/reports/{report.id}"}

@router.get("/reports/{report_id}")
def report_status(report_id: int, user: CurrentUser, db: DbSession):
    report = db.get(Report, report_id)
    if not report or report.owner_id != user.id:
        raise HTTPException(404)
    result = AsyncResult(report.task_id, app=celery_app)
    return {"state": result.state, "progress": result.info if result.state == "PROGRESS" else None,
            "url": result.result if result.successful() else None}
```

Calling tasks:

```python
send_email.delay(email_id)                                          # shortcut
send_email.apply_async(args=[email_id], countdown=60)                # run in 60 s
send_email.apply_async(args=[email_id], queue="emails", priority=9)
```

Running:

```bash
celery -A app.worker worker -Q emails,default --concurrency=8 --loglevel=INFO
celery -A app.worker worker -Q reports --concurrency=2              # separate worker pool for slow jobs
celery -A app.worker beat --loglevel=INFO                            # exactly ONE beat instance!
celery -A app.worker flower --port=5555                              # monitoring UI (protect it)
```

Workflows: `group` (parallel), `chain` (sequential), `chord` (parallel then a callback) — e.g. resize 20 images in parallel, then build a zip.

### 2. ARQ — async tasks for asyncio apps

**ARQ** is a small **asyncio**-native queue on Redis — a natural fit when your FastAPI code and libraries are already async.

```python
# app/arq_worker.py
from arq import Retry, cron
from arq.connections import RedisSettings

async def send_welcome_email(ctx, user_id: int) -> None:
    http = ctx["http"]                                   # shared client created in on_startup
    try:
        r = await http.post(PROVIDER_URL, json={"user_id": user_id}, timeout=10)
        r.raise_for_status()
    except Exception as exc:
        if ctx["job_try"] < 5:
            raise Retry(defer=ctx["job_try"] * 10) from exc   # retry in 10s, 20s, 30s…
        raise                                            # give up → job marked failed

async def nightly_cleanup(ctx) -> None:
    ...

async def on_startup(ctx):
    import httpx
    ctx["http"] = httpx.AsyncClient()

async def on_shutdown(ctx):
    await ctx["http"].aclose()

class WorkerSettings:
    functions = [send_welcome_email]
    cron_jobs = [cron(nightly_cleanup, hour=2, minute=0)]
    redis_settings = RedisSettings(host="localhost")
    on_startup, on_shutdown = on_startup, on_shutdown
    max_jobs = 20                                        # concurrent jobs per worker
    job_timeout = 300
# run:  arq app.arq_worker.WorkerSettings
```

```python
# FastAPI side
from contextlib import asynccontextmanager
from arq import create_pool

@asynccontextmanager
async def lifespan(app):
    app.state.arq = await create_pool(RedisSettings(host="localhost"))
    yield
    await app.state.arq.close()

@router.post("/users", status_code=201)
async def register(data: UserCreate, request: Request):
    user = await create_user(data)
    await request.app.state.arq.enqueue_job(
        "send_welcome_email", user.id,
        _job_id=f"welcome-{user.id}",                   # same id twice → enqueued only once (dedupe)
    )
    return user
```

### 3. Task design rules (the important part)

**1. Tasks must be idempotent.** Queues deliver **at least once**: with `acks_late`, a worker crash or timeout re-delivers the task; retries re-run it. Running twice must not charge twice or send two emails.

```python
import sqlite3   # works the same with Postgres: a UNIQUE constraint does the dedupe

def run_once(db: sqlite3.Connection, key: str, action) -> bool:
    """Run `action` only the first time `key` is seen. Returns True if it ran."""
    try:
        with db:                                         # transaction
            db.execute("INSERT INTO processed_tasks (key) VALUES (?)", (key,))
            action()                                     # if this raises, the INSERT rolls back → can retry
        return True
    except sqlite3.IntegrityError:
        return False                                     # duplicate delivery → skip
```

Other idempotency tools: check current state first (`if order.status == "paid": return`), upserts instead of inserts, provider idempotency keys, conditional updates (`UPDATE … WHERE status = 'pending'`).

**2. Pass IDs, not objects.** Send `order_id`, load fresh data in the task. Objects get stale, may not serialize, and bloat the broker.

**3. Enqueue only after the DB transaction commits.** Otherwise the worker may start before the row exists (or for a row that gets rolled back).

```python
class AfterCommit:
    """Collect side effects during a unit of work; fire them only after a successful commit."""
    def __init__(self):
        self._callbacks = []
    def add(self, fn, *args):
        self._callbacks.append((fn, args))
    def commit(self, db):
        db.commit()
        callbacks, self._callbacks = self._callbacks, []
        for fn, args in callbacks:
            fn(*args)
    def rollback(self, db):
        db.rollback()
        self._callbacks.clear()                          # nothing is enqueued for rolled-back work
```

For guaranteed delivery even if the enqueue call itself fails right after commit, use the **transactional outbox** (write an `outbox` row in the same transaction; a relay publishes it).

**4. Retry only transient errors**, with exponential backoff + jitter and a max; send permanently failing tasks to a **dead-letter queue / failed jobs table** and alert.

```python
import random

def backoff_delay(attempt: int, base: float = 1.0, cap: float = 600.0, jitter: bool = True) -> float:
    """attempt 0 → ~1s, 1 → ~2s, 2 → ~4s … capped. Full jitter spreads retries out."""
    delay = min(cap, base * 2 ** attempt)
    return random.uniform(0, delay) if jitter else delay
```

**5. Keep tasks short**; split big jobs into chunks/sub-tasks; set time limits; report progress.

```python
from itertools import islice

def chunked(iterable, size: int):
    it = iter(iterable)
    while batch := list(islice(it, size)):
        yield batch
```

**6. Separate queues** by priority/latency (emails vs reports vs imports) with their own workers, so a flood of slow jobs can't delay urgent ones.

**7. Resources per task**: open DB sessions/HTTP clients per task or per worker (startup hooks) — never reuse objects from the web request.

**8. Observability**: log with task ID, measure duration/failures/retries and **queue depth** (alert when it grows), use Flower or your metrics stack; propagate trace context from the request into the task.

**9. Security**: JSON serializer only (no pickle), broker not exposed publicly (password/TLS), validate task arguments like any input.

**10. Deploy workers separately** from the web app; scale workers by queue depth; use warm shutdown (finish current tasks on SIGTERM).

### 4. Scheduled (periodic) jobs

- Celery **beat** or ARQ **cron** — run **exactly one** scheduler instance (two beats = every job runs twice), or use a lock.
- Make scheduled jobs **idempotent** and **catch-up safe** (a missed run shouldn't corrupt data; a double run shouldn't duplicate).
- Store schedules in **UTC**; be careful with jobs at local midnight across DST changes.
- Long-running cron jobs: prevent overlaps (lock key with TTL).
- Alternatives: Kubernetes CronJobs, cloud schedulers (EventBridge, Cloud Scheduler) that enqueue a task.

### 5. Choosing a queue

| Tool | Style | Best for |
|---|---|---|
| **Celery** | Sync (prefork/threads/gevent), feature-rich | Most production apps; complex workflows; mature ecosystem |
| **ARQ** | asyncio, Redis only, small | Async FastAPI apps, simple jobs |
| **Dramatiq** | Sync, simpler than Celery, good defaults | Teams wanting Celery-like power with less config |
| **RQ** | Sync, Redis, very simple | Small apps |
| **Taskiq** | asyncio, pluggable brokers, FastAPI-friendly DI | Async apps needing more than ARQ |
| **SQS + Lambda / Cloud Tasks** | Managed | Serverless, no workers to run |

### Interview Qs

1. When would you use Celery instead of FastAPI `BackgroundTasks`?
2. What does "at-least-once delivery" mean for task design? How do you make tasks idempotent?
3. What do `acks_late`, `prefetch_multiplier` and time limits do?
4. Why pass IDs instead of objects to tasks?
5. Why must you enqueue a task only after the DB transaction commits? What is the outbox pattern?
6. How do you implement retries correctly? What is a dead-letter queue?
7. Why run only one Celery beat instance?
8. How do you report progress of a long-running task to the frontend?
9. How would you prevent slow report jobs from delaying password-reset emails?

---

## 26. WebSockets & Streaming

### WebSocket chat with a connection manager

```python
from fastapi import WebSocket, WebSocketDisconnect

class ConnectionManager:
    def __init__(self):
        self.rooms: dict[str, set[WebSocket]] = {}

    async def connect(self, room: str, ws: WebSocket):
        await ws.accept()
        self.rooms.setdefault(room, set()).add(ws)

    def disconnect(self, room: str, ws: WebSocket):
        self.rooms.get(room, set()).discard(ws)

    async def broadcast(self, room: str, message: dict):
        for ws in list(self.rooms.get(room, [])):
            try:
                await ws.send_json(message)
            except Exception:
                self.disconnect(room, ws)

manager = ConnectionManager()

@app.websocket("/ws/{room}")
async def chat(ws: WebSocket, room: str, token: str):         # ?token=... (browsers can't set WS headers)
    user = verify_ws_token(token)
    if not user:
        await ws.close(code=1008)                              # policy violation
        return
    await manager.connect(room, ws)
    try:
        while True:
            data = await ws.receive_json()
            await manager.broadcast(room, {"from": user.name, "text": data["text"]})
    except WebSocketDisconnect:
        manager.disconnect(room, ws)
```

In-memory managers only work with **one process**. With multiple workers/servers, broadcast through **Redis pub/sub** (or a broker).

### Streaming responses & Server-Sent Events (e.g. LLM token streaming)

```python
from fastapi.responses import StreamingResponse
import asyncio, json

async def event_stream():
    for i in range(5):
        yield f"data: {json.dumps({'progress': i * 20})}\n\n"   # SSE format
        await asyncio.sleep(1)
    yield "data: [DONE]\n\n"

@app.get("/progress")
async def progress():
    return StreamingResponse(event_stream(), media_type="text/event-stream",
                             headers={"Cache-Control": "no-cache"})

# Stream a large file / CSV export without loading it all in memory
@app.get("/export.csv")
def export_csv(db: DbSession):
    def rows():
        yield "id,email\n"
        for user in db.scalars(select(User).execution_options(yield_per=1000)):
            yield f"{user.id},{user.email}\n"
    return StreamingResponse(rows(), media_type="text/csv",
                             headers={"Content-Disposition": "attachment; filename=users.csv"})
```

---

## 27. Server-Sent Events & Streaming Answers in FastAPI

The previous section streamed with a plain `StreamingResponse`. Recent FastAPI versions have **built-in SSE**: return `yield`ed events from a path operation marked `response_class=EventSourceResponse`, and FastAPI encodes the wire format, sets the anti-buffering headers and sends keep-alive pings. The concepts (event ids, resume, in-band errors, proxy buffering) are explained in `nodejs.md` → "Streaming Responses & Server-Sent Events in Depth". This section shows the FastAPI way. It was tested with FastAPI 0.136: through `TestClient`, and against a real `uvicorn` server for client disconnects.

### What `EventSourceResponse` does for you

```python
from fastapi import FastAPI
from fastapi.sse import EventSourceResponse, ServerSentEvent

app = FastAPI()

@app.get("/progress", response_class=EventSourceResponse)
async def progress():
    for pct in (0, 50, 100):
        yield {"progress": pct}                                  # plain objects → JSON in a `data:` line
    yield ServerSentEvent(event="done", id="3", data={"ok": True}, retry=5_000)
```

```text
data: {"progress": 0}

data: {"progress": 50}

data: {"progress": 100}

event: done
data: {"ok": true}
id: 3
retry: 5000

```

- Works with **any method**, so `POST` streaming for chat is supported.
- Sets `Content-Type: text/event-stream`, `Cache-Control: no-cache` and `X-Accel-Buffering: no`.
- Sends a `: ping` comment when your generator has been silent for 15 s, so proxies don't close the idle connection.
- `data` is **always JSON-encoded**, strings included (`data="hi"` sends `data: "hi"`). Use `raw_data=` for pre-formatted text.
- Multi-line data is split into several `data:` lines correctly.
- A generator path operation **without** `EventSourceResponse` streams **JSON Lines** (`application/jsonl`), one JSON object per line. That's handy for exports and machine clients.

If your FastAPI version has no `fastapi.sse`, upgrade, or use the `sse-starlette` package (`EventSourceResponse` with similar features), or a `StreamingResponse` as in the previous section plus the headers above.

### A notifications feed that resumes after reconnects

```python
import asyncio
from dataclasses import dataclass
from typing import Annotated, Any

from fastapi import FastAPI, Header
from fastapi.sse import EventSourceResponse, ServerSentEvent

app = FastAPI()

@dataclass
class Entry:
    id: int
    event: str
    data: Any

# Demo storage (one process). With several workers or servers, use Redis Streams (XADD/XRANGE) for
# history and Redis pub/sub for fan-out, so every worker sees every event.
LOG: list[Entry] = []
SUBSCRIBERS: set[asyncio.Queue[Entry | None]] = set()

def publish(event: str, data: Any) -> Entry:
    entry = Entry(id=(LOG[-1].id + 1) if LOG else 1, event=event, data=data)
    LOG.append(entry)
    del LOG[:-1000]                                      # keep the last 1,000 for replay
    for queue in list(SUBSCRIBERS):
        try:
            queue.put_nowait(entry)
        except asyncio.QueueFull:                        # slow consumer: drop it; it resumes via Last-Event-ID
            SUBSCRIBERS.discard(queue)
            queue.get_nowait()
            queue.put_nowait(None)                       # sentinel: tell its stream to end
    return entry

def to_sse(entry: Entry) -> ServerSentEvent:
    return ServerSentEvent(event=entry.event, id=str(entry.id), data=entry.data)

@app.get("/notifications/stream", response_class=EventSourceResponse)
async def notifications_stream(
    last_event_id: Annotated[str | None, Header()] = None,   # the `Last-Event-ID` header the browser sends on reconnect
    since: int = 0,                                          # ?since= for the very first connection
):
    last_seen = int(last_event_id) if last_event_id and last_event_id.isdigit() else since
    queue: asyncio.Queue[Entry | None] = asyncio.Queue(maxsize=100)
    SUBSCRIBERS.add(queue)                     # subscribe FIRST, then replay: nothing can fall into the gap
    try:
        replayed = [e for e in LOG if e.id > last_seen]
        for entry in replayed:
            yield to_sse(entry)
        newest = replayed[-1].id if replayed else last_seen
        while (entry := await queue.get()) is not None:
            if entry.id > newest:              # skip events already sent during the replay
                yield to_sse(entry)
    finally:
        SUBSCRIBERS.discard(queue)             # runs on client disconnect too (the generator is cancelled)
```

Subscribing before replaying means an event published during the replay is either in the replayed list or in the queue, and the `id` check removes the duplicate. Parse `Last-Event-ID` leniently: a validation error would answer `422`, and `EventSource` never reconnects after a non-200 response.

### Streaming an LLM-style answer over POST

```python
import asyncio
from collections.abc import AsyncIterator
from typing import Annotated

from fastapi import FastAPI
from fastapi.sse import EventSourceResponse, ServerSentEvent
from pydantic import BaseModel, StringConstraints

app = FastAPI()

class ChatRequest(BaseModel):
    prompt: Annotated[str, StringConstraints(strip_whitespace=True, min_length=1, max_length=2000)]

class ModelError(Exception):
    pass

GENERATION = {"started": 0, "cancelled": 0}

async def generate_tokens(prompt: str) -> AsyncIterator[str]:
    """Stand-in for an LLM SDK's async token stream."""
    GENERATION["started"] += 1
    if prompt == "fail":
        raise ModelError("model overloaded")
    try:
        for word in f'You asked: "{prompt}". Streaming sends each token as soon as it is ready.'.split():
            await asyncio.sleep(0.03)
            yield word + " "
    except asyncio.CancelledError:
        GENERATION["cancelled"] += 1           # client disconnected: the upstream call stops here
        raise                                  # always re-raise CancelledError

@app.post("/chat", response_class=EventSourceResponse)
async def chat(body: ChatRequest):             # a bad body is rejected with 422 BEFORE streaming starts
    tokens = 0
    try:
        async for text in generate_tokens(body.prompt):
            yield ServerSentEvent(event="token", data={"text": text})
            tokens += 1
        yield ServerSentEvent(event="done", data={"tokens": tokens})
    except ModelError:
        # the 200 is already sent, so errors travel inside the stream
        yield ServerSentEvent(event="error", data={"message": "Generation failed, please retry"})
```

When the client disconnects, FastAPI cancels the generator. The `CancelledError` surfaces at the current `await`, so `finally:` blocks and `except CancelledError` handlers run. That's where you close the upstream SDK stream to stop paying for tokens nobody will read. Never swallow `CancelledError`.

The browser side is the same `fetch` + stream parser + React hook shown in `nodejs.md` (Streaming Responses section): `EventSource` can't send a `POST` body.

**Blocking SDKs.** A plain `def` generator path operation runs in the thread pool (FastAPI iterates it with `iterate_in_threadpool`), so a synchronous SDK doesn't block the event loop. Prefer the SDK's async client when there is one.

### Testing streams

```python
import json

from fastapi.testclient import TestClient

from main import app          # the chat app above

def parse_sse(lines):
    """Minimal test helper: group `field: value` lines into events."""
    event: dict = {}
    for line in lines:
        if line == "":
            if event:
                yield event
            event = {}
        elif not line.startswith(":"):
            field, _, value = line.partition(": ")
            event[field] = event[field] + "\n" + value if field in event else value

def test_chat_streams_tokens_then_done():
    client = TestClient(app)
    with client.stream("POST", "/chat", json={"prompt": "hi"}) as response:
        assert response.status_code == 200
        assert response.headers["content-type"].startswith("text/event-stream")
        events = list(parse_sse(response.iter_lines()))
    assert [e["event"] for e in events][-1] == "done"
    assert "".join(json.loads(e["data"])["text"] for e in events if e["event"] == "token").strip().startswith("You asked")

def test_empty_prompt_is_422_before_streaming():
    assert TestClient(app).post("/chat", json={"prompt": "   "}).status_code == 422
```

`TestClient` is fine for streams that **end**, like `/chat`. It **hangs on a stream that never ends**, such as a live feed, even after you `break` out of the loop, because it waits for the app to finish. Test endless feeds, and disconnect handling, against a real `uvicorn` server (started in a background thread) with `httpx.stream(...)`: break after a few events, then assert that your `finally` cleanup ran.

### Deployment notes

- **Workers and fan-out:** each Uvicorn/Gunicorn worker has its own `SUBSCRIBERS`. Fan out through Redis pub/sub (`redis.asyncio`), and keep history in Redis Streams or the database so any worker can replay.
- **Proxies:** `X-Accel-Buffering: no` is already set; also raise nginx's `proxy_read_timeout` for stream routes, and keep keep-alive pings (15 s) below every idle timeout on the path (AWS ALB defaults to 60 s).
- **Graceful shutdown:** open streams keep a worker busy. Use `uvicorn --timeout-graceful-shutdown 10` so deploys don't hang. Clients reconnect (and resume) on their own.
- **Don't wrap streams in response-buffering middleware** (some custom logging middlewares read the whole body). Log the start and end of streams instead.

### Interview Qs

1. How do you send SSE from FastAPI? → A generator path operation with `response_class=EventSourceResponse`, yielding objects (sent as JSON `data:`) or `ServerSentEvent(event=, id=, data=, retry=)`.
2. How does FastAPI keep idle SSE connections alive? → It sends a `: ping` comment when the generator has been quiet for 15 s.
3. What happens to your generator when the client disconnects? → It's cancelled: `CancelledError` is raised at the current `await`, so `finally` and cleanup run. Re-raise it.
4. How do you resume a feed after a reconnect? → Give every event an `id`, read the `Last-Event-ID` header, replay newer events from a log, then continue live. Subscribe before replaying and skip duplicates.
5. How are validation errors and mid-stream errors handled differently? → Body validation fails with `422` before streaming; once streaming has started, send an in-band `error` event.
6. What does a generator endpoint without `EventSourceResponse` return? → JSON Lines (`application/jsonl`).
7. How do you scale SSE across Uvicorn workers? → Redis pub/sub for fan-out and Redis Streams or a database for replayable history.

---

## 28. Pagination, Filtering & Sorting

### Offset pagination with a generic response model

```python
from pydantic import BaseModel
from typing import Generic, TypeVar

T = TypeVar("T")

class Page(BaseModel, Generic[T]):
    items: list[T]
    total: int
    page: int
    size: int
    pages: int

@router.get("/products", response_model=Page[ProductOut])
def list_products(
    db: DbSession,
    page: Annotated[int, Query(ge=1)] = 1,
    size: Annotated[int, Query(ge=1, le=100)] = 20,
    q: str | None = None,
    min_price: Annotated[float | None, Query(ge=0)] = None,
    sort: Literal["price", "-price", "newest"] = "newest",
):
    stmt = select(Product)
    if q:
        stmt = stmt.where(Product.name.ilike(f"%{q}%"))        # parameterized — safe
    if min_price is not None:
        stmt = stmt.where(Product.price >= min_price)

    total = db.scalar(select(func.count()).select_from(stmt.subquery()))
    order = {"price": Product.price.asc(), "-price": Product.price.desc(), "newest": Product.created_at.desc()}[sort]
    items = db.scalars(stmt.order_by(order).offset((page - 1) * size).limit(size)).all()
    return Page(items=items, total=total, page=page, size=size, pages=-(-total // size))
```

Whitelist sort fields (never pass a raw column name from the client into SQL).

### Cursor (keyset) pagination — for feeds & large tables

```python
@router.get("/feed")
def feed(db: DbSession, after_id: int | None = None, limit: int = Query(20, le=100)):
    stmt = select(Post).order_by(Post.id.desc()).limit(limit + 1)
    if after_id:
        stmt = stmt.where(Post.id < after_id)
    posts = db.scalars(stmt).all()
    has_more = len(posts) > limit
    posts = posts[:limit]
    return {"items": posts, "next_cursor": posts[-1].id if has_more else None}
```

Offset is simple but slow for deep pages and unstable with inserts; cursor pagination is fast and consistent.

---

## 29. Caching & Rate Limiting

### Redis cache (cache-aside)

```python
import json

async def get_product_cached(product_id: int, db: AsyncDb, r) -> dict:
    key = f"product:{product_id}"
    if cached := await r.get(key):
        return json.loads(cached)
    product = await db.get(Product, product_id)
    if not product:
        raise NotFoundError("Product not found")
    data = ProductOut.model_validate(product).model_dump(mode="json")
    await r.set(key, json.dumps(data), ex=300)          # TTL 5 minutes
    return data

# Invalidate on update
await r.delete(f"product:{product_id}")
```

HTTP caching: set `Cache-Control`/`ETag` headers for public GET endpoints so CDNs/browsers cache.

### Rate limiting with slowapi

```python
from slowapi import Limiter, _rate_limit_exceeded_handler
from slowapi.util import get_remote_address
from slowapi.errors import RateLimitExceeded

limiter = Limiter(key_func=get_remote_address, storage_uri=settings.redis_url)   # Redis → shared across workers
app.state.limiter = limiter
app.add_exception_handler(RateLimitExceeded, _rate_limit_exceeded_handler)

@router.post("/auth/token")
@limiter.limit("5/minute")                     # brute-force protection
def login(request: Request, form: Annotated[OAuth2PasswordRequestForm, Depends()]): ...

@router.get("/search")
@limiter.limit("60/minute")
def search(request: Request, q: str): ...
```

Behind a proxy, make sure the real client IP is used (Uvicorn `--proxy-headers --forwarded-allow-ips=...`). Rate limiting is often also done at the gateway (Nginx, Cloudflare, API Gateway).

---

## 30. Calling External APIs

Use **httpx** (sync + async), reuse one client (connection pooling), always set **timeouts**, retry only transient errors.

```python
import httpx
from tenacity import retry, stop_after_attempt, wait_exponential_jitter, retry_if_exception_type

class PaymentClient:
    def __init__(self, client: httpx.AsyncClient):
        self.client = client

    @retry(stop=stop_after_attempt(3), wait=wait_exponential_jitter(initial=0.3, max=3),
           retry=retry_if_exception_type((httpx.TransportError, httpx.HTTPStatusError)))
    async def create_order(self, amount_paise: int, idempotency_key: str) -> dict:
        r = await self.client.post(
            "https://api.payments.example/orders",
            json={"amount": amount_paise, "currency": "INR"},
            headers={"Idempotency-Key": idempotency_key},       # safe retries for POST
            timeout=httpx.Timeout(10.0, connect=3.0),
        )
        if r.status_code >= 500:
            r.raise_for_status()                                # 5xx → retry
        if r.status_code >= 400:
            raise AppError(f"Payment provider rejected: {r.text}")   # 4xx → don't retry
        return r.json()

def get_payment_client(request: Request) -> PaymentClient:
    return PaymentClient(request.app.state.http)                # shared client from lifespan
```

---

## 31. Integrations: Webhooks, Payments, Email & S3 Uploads

Concepts are explained in depth in the Node notes ("Webhooks & Payment Integration"); this section shows the **FastAPI/Python** way, with production rules.

### 1. Receiving webhooks securely

Rules: verify the **signature over the raw body**, reject **stale timestamps** (replay attacks), **dedupe by event ID** (providers deliver at least once), **respond 2xx fast** and process in the background.

```python
import hashlib, hmac, json, time
from fastapi import FastAPI, Request, HTTPException, BackgroundTasks

WEBHOOK_SECRET = b"whsec_test_secret"            # from settings (SecretStr) in real code
TOLERANCE_SECONDS = 300
processed_event_ids: set[str] = set()            # real app: DB table with a UNIQUE constraint on event_id

app = FastAPI()

def verify_signature(raw_body: bytes, header: str | None) -> None:
    # header format: "t=1727150000,v1=<hex hmac>"
    if not header:
        raise HTTPException(400, "Missing signature")
    parts = dict(item.split("=", 1) for item in header.split(",") if "=" in item)
    timestamp, signature = parts.get("t"), parts.get("v1")
    if not timestamp or not signature or not timestamp.isdigit():
        raise HTTPException(400, "Malformed signature")
    if abs(time.time() - int(timestamp)) > TOLERANCE_SECONDS:
        raise HTTPException(400, "Stale webhook")                       # replay protection
    expected = hmac.new(WEBHOOK_SECRET, f"{timestamp}.".encode() + raw_body, hashlib.sha256).hexdigest()
    if not hmac.compare_digest(expected, signature):                    # constant-time comparison
        raise HTTPException(401, "Invalid signature")

def handle_event(event: dict) -> None:
    ...  # fulfil order, send receipt, etc. — idempotent

@app.post("/webhooks/payments")
async def payments_webhook(request: Request, background: BackgroundTasks):
    raw = await request.body()                                          # RAW bytes — don't parse first
    verify_signature(raw, request.headers.get("X-Signature"))
    event = json.loads(raw)

    if event["id"] in processed_event_ids:                              # duplicate delivery → ack & ignore
        return {"status": "duplicate"}
    processed_event_ids.add(event["id"])

    background.add_task(handle_event, event)                            # real app: enqueue to Celery/ARQ
    return {"status": "received"}
```

With a provider SDK (e.g. Stripe) the verification is one call:

```python
import stripe

@app.post("/webhooks/stripe")
async def stripe_webhook(request: Request):
    payload = await request.body()
    try:
        event = stripe.Webhook.construct_event(payload, request.headers.get("stripe-signature"), settings.stripe_webhook_secret)
    except (ValueError, stripe.SignatureVerificationError):
        raise HTTPException(400, "Invalid webhook")
    if event["type"] == "payment_intent.succeeded":
        await queue.enqueue("fulfil_order", event["data"]["object"]["id"], event_id=event["id"])
    return {"received": True}
```

Idempotency in the database (safe even with concurrent duplicate deliveries):

```python
from sqlalchemy.exc import IntegrityError

def record_event_once(db, event_id: str, event_type: str) -> bool:
    db.add(WebhookEvent(id=event_id, type=event_type))       # id is the PRIMARY KEY / UNIQUE
    try:
        db.commit()
        return True                                          # first time we see it
    except IntegrityError:
        db.rollback()
        return False                                         # already processed
```

### 2. Payment flow (Razorpay/Stripe style)

```
1. POST /checkout      → server computes the amount FROM THE DB, creates a pending Order + provider order (idempotency key = order id)
2. Client pays on the provider's hosted checkout (card data never touches your server)
3. POST /payments/verify → server verifies the provider signature (UX: show "paid" quickly)
4. Webhook payment.captured → SOURCE OF TRUTH: mark paid idempotently, fulfil, send receipt
```

```python
import hmac, hashlib
from sqlalchemy import update

def verify_payment_signature(provider_order_id: str, payment_id: str, signature: str, key_secret: bytes) -> bool:
    expected = hmac.new(key_secret, f"{provider_order_id}|{payment_id}".encode(), hashlib.sha256).hexdigest()
    return hmac.compare_digest(expected, signature)

def mark_order_paid(db, provider_order_id: str, payment_id: str) -> bool:
    """State transition pending → paid, done atomically and idempotently."""
    result = db.execute(
        update(Order)
        .where(Order.provider_order_id == provider_order_id, Order.status == "pending")   # only from pending
        .values(status="paid", payment_id=payment_id)
    )
    db.commit()
    return result.rowcount == 1          # False → already paid (duplicate) or not pending
```

Rules: **amounts as integer paise/cents**, never trust client prices/"success" callbacks, **webhooks are the source of truth**, **idempotency keys** on outgoing charge/refund calls, an **order state machine** with conditional updates, a **reconciliation job** that compares your orders with the provider's records, and never store card data.

### 3. Sending email

**Never send email inside the request** — SMTP/API calls are slow and flaky. Enqueue a job (Celery/ARQ) or at least use `BackgroundTasks`.

#### Templates with Jinja2 (autoescape on!)

```python
from jinja2 import Environment, DictLoader, select_autoescape

env = Environment(
    loader=DictLoader({
        "welcome.html": "<h1>Welcome, {{ name }}!</h1><p><a href=\"{{ verify_url }}\">Verify your email</a></p>",
        "welcome.txt": "Welcome, {{ name }}!\nVerify your email: {{ verify_url }}",
    }),
    autoescape=select_autoescape(["html"]),       # escapes user data in HTML → prevents HTML/JS injection
)

def render_welcome(name: str, verify_url: str) -> tuple[str, str]:
    ctx = {"name": name, "verify_url": verify_url}
    return env.get_template("welcome.html").render(ctx), env.get_template("welcome.txt").render(ctx)
```

(Real apps use `FileSystemLoader("templates")`.)

#### Sending via a provider API (recommended) or SMTP

```python
import httpx
from email.message import EmailMessage
import smtplib

async def send_via_api(to: str, subject: str, html: str, text: str) -> None:
    # SES / SendGrid / Postmark / Resend all look roughly like this
    async with httpx.AsyncClient(timeout=10) as client:
        r = await client.post(
            "https://api.email-provider.example/v1/send",
            headers={"Authorization": f"Bearer {settings.email_api_key.get_secret_value()}"},
            json={"from": "Shop <no-reply@mail.shop.com>", "to": [to], "subject": subject, "html": html, "text": text},
        )
        r.raise_for_status()

def send_via_smtp(to: str, subject: str, html: str, text: str) -> None:
    msg = EmailMessage()
    msg["From"], msg["To"], msg["Subject"] = "Shop <no-reply@mail.shop.com>", to, subject
    msg.set_content(text)                          # plain-text part (deliverability + accessibility)
    msg.add_alternative(html, subtype="html")      # HTML part
    with smtplib.SMTP(settings.smtp_host, 587, timeout=10) as smtp:
        smtp.starttls()
        smtp.login(settings.smtp_user, settings.smtp_password.get_secret_value())
        smtp.send_message(msg)

@app.post("/users", status_code=201)
async def register(data: UserCreate, background: BackgroundTasks):
    user = await create_user(data)
    html, text = render_welcome(user.name, make_verify_url(user))
    background.add_task(send_via_api, user.email, "Welcome to Shop", html, text)   # after the response
    return user
```

#### Email best practices

- **Deliverability**: send from your own domain with **SPF, DKIM and DMARC** records; use a subdomain (`mail.shop.com`) for bulk/marketing; warm up new domains.
- Always include a **plain-text** version; keep HTML simple (tables, inline CSS).
- Handle **bounce & complaint webhooks** from the provider — stop sending to bad addresses.
- Marketing emails need an **unsubscribe link** and `List-Unsubscribe` header; transactional ones (receipts, password reset) are separate streams.
- **Retries with backoff** in the job queue; **idempotency** so a retried job doesn't send twice (store "sent" state per email type/user).
- Escape user content in templates; never put secrets or full tokens in logs.
- **Dev/test**: capture emails locally (Mailpit/MailHog) or mock the provider — never email real users from staging.

### 4. File uploads to S3 with pre-signed URLs

Uploading big files **through** your API wastes bandwidth/CPU and ties up workers. Instead, the API hands the client a **short-lived, pre-signed URL** and the client uploads **directly** to object storage.

```
1. Client → POST /uploads {filename, content_type, size}   (authenticated)
2. API validates type & size, picks the object KEY, returns a pre-signed POST (expires in ~5 min)
3. Client uploads the file directly to S3 using that URL + fields
4. Client → POST /uploads/complete {key}  (or S3 event → queue → worker)
5. API verifies the object (exists, size, content type), scans it if needed, saves the key in the DB
6. Downloads: API returns a short-lived pre-signed GET URL (bucket stays private)
```

```python
import uuid
import boto3
from pydantic import BaseModel, Field

s3 = boto3.client("s3", region_name="ap-south-1")
BUCKET = "shop-user-uploads"                   # PRIVATE bucket (block public access)
ALLOWED_TYPES = {"image/jpeg": ".jpg", "image/png": ".png", "application/pdf": ".pdf"}
MAX_BYTES = 10 * 1024 * 1024

class UploadRequest(BaseModel):
    content_type: str
    size: int = Field(gt=0, le=MAX_BYTES)

@app.post("/uploads")
def create_upload(req: UploadRequest, user: CurrentUser):
    if req.content_type not in ALLOWED_TYPES:
        raise HTTPException(415, "Unsupported file type")
    key = f"users/{user.id}/{uuid.uuid4()}{ALLOWED_TYPES[req.content_type]}"   # never use the client's filename as the key
    presigned = s3.generate_presigned_post(
        Bucket=BUCKET,
        Key=key,
        Fields={"Content-Type": req.content_type},
        Conditions=[
            {"Content-Type": req.content_type},
            ["content-length-range", 1, MAX_BYTES],        # S3 enforces the size limit
        ],
        ExpiresIn=300,
    )
    return {"key": key, "url": presigned["url"], "fields": presigned["fields"]}

@app.post("/uploads/complete")
def complete_upload(key: str, user: CurrentUser, db: DbSession):
    if not key.startswith(f"users/{user.id}/"):
        raise HTTPException(403, "Not your upload")      # prevent claiming someone else's object
    head = s3.head_object(Bucket=BUCKET, Key=key)        # verify it really exists
    if head["ContentLength"] > MAX_BYTES:
        raise HTTPException(400, "File too large")
    db.add(Attachment(user_id=user.id, key=key, size=head["ContentLength"], content_type=head["ContentType"]))
    db.commit()
    return {"ok": True}

@app.get("/attachments/{attachment_id}/download")
def download(attachment_id: int, user: CurrentUser, db: DbSession):
    att = db.get(Attachment, attachment_id)
    if not att or att.user_id != user.id:
        raise HTTPException(404)
    url = s3.generate_presigned_url("get_object", Params={"Bucket": BUCKET, "Key": att.key}, ExpiresIn=60)
    return {"url": url}
```

#### Upload best practices

- **Private buckets**; access only via short-lived pre-signed URLs (or a CDN with signed URLs/cookies).
- Enforce **size & type** in the pre-signed policy (not just on the client).
- Generate **random keys** namespaced by tenant/user; store the key, not a public URL.
- **Verify after upload** (head_object), and scan user files for malware if they're shared with others.
- **CORS** on the bucket for the frontend origin (PUT/POST only).
- **Lifecycle rules** to delete abandoned uploads (objects never "completed") and move old files to cheaper storage.
- Large files: **multipart uploads** (resumable, parallel parts).
- Serve images through an image CDN/resizer instead of the raw original.

### Interview Qs

1. How do you verify a webhook in FastAPI? Why must you use `await request.body()`?
2. How do you make webhook processing idempotent under concurrent duplicate deliveries?
3. Walk through a secure payment integration. Which step is the source of truth?
4. How do you mark an order paid exactly once? (conditional update on status)
5. Why shouldn't you send emails inside the request handler?
6. What are SPF, DKIM and DMARC?
7. Why use pre-signed URLs for uploads? How do you enforce file size limits with S3?
8. How do you stop users from accessing other users' files in S3?

---

## 32. Testing FastAPI

### TestClient (sync) with dependency overrides and a test DB

```python
# tests/conftest.py
import pytest
from fastapi.testclient import TestClient
from sqlalchemy import create_engine
from sqlalchemy.orm import sessionmaker
from sqlalchemy.pool import StaticPool
from app.main import app
from app.db.session import Base, get_db
from app.api.deps import get_current_user

engine = create_engine("sqlite://", connect_args={"check_same_thread": False}, poolclass=StaticPool)
TestingSession = sessionmaker(bind=engine, expire_on_commit=False)

@pytest.fixture
def db():
    Base.metadata.create_all(engine)
    session = TestingSession()
    yield session
    session.close()
    Base.metadata.drop_all(engine)

@pytest.fixture
def client(db):
    app.dependency_overrides[get_db] = lambda: db
    with TestClient(app) as c:                 # `with` runs lifespan startup/shutdown
        yield c
    app.dependency_overrides.clear()

@pytest.fixture
def auth_client(client, db):
    user = User(email="t@x.com", name="Test", hashed_password="x", role="admin")
    db.add(user); db.commit()
    app.dependency_overrides[get_current_user] = lambda: user
    return client
```

```python
# tests/test_users.py
def test_create_user(client):
    r = client.post("/api/v1/users", json={"email": "a@x.com", "name": "Asha", "password": "Secret123"})
    assert r.status_code == 201
    body = r.json()
    assert body["email"] == "a@x.com"
    assert "password" not in body and "hashed_password" not in body   # response model filtered it

def test_create_user_validation(client):
    r = client.post("/api/v1/users", json={"email": "not-an-email", "name": "A"})
    assert r.status_code == 422

def test_duplicate_email(client):
    payload = {"email": "a@x.com", "name": "Asha", "password": "Secret123"}
    client.post("/api/v1/users", json=payload)
    assert client.post("/api/v1/users", json=payload).status_code == 409

def test_requires_auth(client):
    assert client.get("/users/me").status_code == 401

def test_admin_can_delete(auth_client):
    assert auth_client.delete("/api/v1/users/1").status_code == 204
```

### Async tests with httpx

```python
import pytest
from httpx import AsyncClient, ASGITransport

@pytest.mark.anyio
async def test_health():
    async with AsyncClient(transport=ASGITransport(app=app), base_url="http://test") as ac:
        r = await ac.get("/health")
    assert r.status_code == 200
```

Tips:
- Use a real Postgres in CI (Docker / Testcontainers) for integration tests — SQLite behaves differently.
- Wrap each test in a transaction and roll back for speed and isolation.
- Mock external APIs (`respx` for httpx, or dependency overrides for client classes).
- Test **services** directly (no HTTP) for business logic; test **routes** for status codes, validation, auth.

---

## 33. OpenAPI Docs Customization

```python
app = FastAPI(
    title="Shop API",
    description="Orders, products and payments. **Markdown** supported.",
    version="2.1.0",
    contact={"name": "API Team", "email": "api@shop.com"},
    openapi_tags=[
        {"name": "auth", "description": "Login & tokens"},
        {"name": "products", "description": "Catalog"},
    ],
    docs_url="/docs",                     # set to None to disable in production
    redoc_url=None,
)

@router.post(
    "/products",
    response_model=ProductOut,
    status_code=201,
    tags=["products"],
    summary="Create a product",
    description="Creates a product. Requires the `admin` role.",
    response_description="The created product",
    responses={409: {"description": "SKU already exists"}, 403: {"description": "Not an admin"}},
    deprecated=False,
    operation_id="createProduct",         # nicer names for generated clients
)
def create_product(data: ProductCreate): ...

class ProductCreate(BaseModel):
    model_config = ConfigDict(json_schema_extra={"examples": [{"name": "Phone", "price": 19999, "sku": "PH-1"}]})
    name: str
    price: int = Field(description="Price in paise", gt=0)
    sku: str
```

The OpenAPI schema (`/openapi.json`) can **generate typed clients** for the frontend (e.g. `openapi-typescript`, `orval`, `@hey-api/openapi-ts`) → the frontend and backend types stay in sync.

---

## 34. Logging, Monitoring & Request IDs

```python
# app/core/logging.py — structured JSON logs with request IDs
import logging, sys, contextvars
from pythonjsonlogger.json import JsonFormatter

request_id_ctx: contextvars.ContextVar[str] = contextvars.ContextVar("request_id", default="-")

class RequestIdFilter(logging.Filter):
    def filter(self, record):
        record.request_id = request_id_ctx.get()
        return True

def setup_logging(level: str = "INFO"):
    handler = logging.StreamHandler(sys.stdout)
    handler.setFormatter(JsonFormatter("%(asctime)s %(levelname)s %(name)s %(message)s %(request_id)s"))
    handler.addFilter(RequestIdFilter())
    logging.basicConfig(level=level, handlers=[handler], force=True)

# middleware sets it per request
@app.middleware("http")
async def request_context(request: Request, call_next):
    rid = request.headers.get("X-Request-ID") or str(uuid.uuid4())
    token = request_id_ctx.set(rid)
    try:
        response = await call_next(request)
    finally:
        request_id_ctx.reset(token)
    response.headers["X-Request-ID"] = rid
    return response
```

Monitoring stack:
- **Errors**: Sentry (`sentry-sdk[fastapi]` auto-instruments).
- **Metrics**: Prometheus (`prometheus-fastapi-instrumentator`) → Grafana dashboards (latency p95/p99, error rate, RPS).
- **Tracing**: OpenTelemetry (`opentelemetry-instrumentation-fastapi`, SQLAlchemy, httpx) → Jaeger/Tempo/Datadog.
- **Health checks**: `/health` (liveness — process up) and `/ready` (readiness — DB/Redis reachable).

```python
@app.get("/ready")
async def ready(db: AsyncDb):
    await db.execute(text("SELECT 1"))
    await app.state.redis.ping()
    return {"status": "ready"}
```

---

## 35. Observability Hands-On in FastAPI (Metrics, Tracing, Error Tracking)

Concepts (RED/USE, cardinality, SLOs, burn rates, probes, incident workflow) are explained in `nodejs.md` → "Observability Hands-On". This section is the **Python/FastAPI** implementation. (Structured logs with request IDs are in the previous section.)

### 1. Prometheus metrics

Quickest: **`prometheus-fastapi-instrumentator`** adds RED metrics per route and a `/metrics` endpoint.

```python
from prometheus_fastapi_instrumentator import Instrumentator

Instrumentator(
    excluded_handlers=["/health", "/metrics"],
    should_group_status_codes=True,          # 2xx/4xx/5xx labels → low cardinality
).instrument(app).expose(app, include_in_schema=False)
```

Or build it yourself with **`prometheus_client`** (shows what's happening):

```python
import time
from fastapi import FastAPI, Request, Response
from prometheus_client import CONTENT_TYPE_LATEST, Counter, Gauge, Histogram, generate_latest

REQUEST_DURATION = Histogram(
    "http_request_duration_seconds", "HTTP request latency",
    ["method", "route", "status_class"],
    buckets=(0.01, 0.05, 0.1, 0.25, 0.5, 1, 2.5, 5),
)
ORDERS_CREATED = Counter("orders_created_total", "Orders created", ["payment_method"])
IN_FLIGHT = Gauge("http_requests_in_flight", "Requests being processed")

app = FastAPI()

@app.middleware("http")
async def prometheus_middleware(request: Request, call_next):
    IN_FLIGHT.inc()
    start = time.perf_counter()
    status = 500
    try:
        response = await call_next(request)
        status = response.status_code
        return response
    finally:
        IN_FLIGHT.dec()
        route = request.scope.get("route")
        REQUEST_DURATION.labels(
            method=request.method,
            route=getattr(route, "path", "unmatched"),      # "/orders/{order_id}" — the pattern, not the raw URL
            status_class=f"{status // 100}xx",
        ).observe(time.perf_counter() - start)

@app.get("/metrics", include_in_schema=False)
def metrics() -> Response:                               # restrict to the internal network in production
    return Response(generate_latest(), media_type=CONTENT_TYPE_LATEST)
```

**Multiple workers** (Gunicorn/Uvicorn `--workers N`): each process has its own counters → use `prometheus_client` **multiprocess mode** (`PROMETHEUS_MULTIPROC_DIR`) or run one process per container and let Prometheus scrape each.

### 2. OpenTelemetry tracing

```bash
pip install opentelemetry-distro opentelemetry-exporter-otlp
opentelemetry-bootstrap -a install                         # installs instrumentations for detected libraries

# zero-code: wraps the app at startup (FastAPI, SQLAlchemy, httpx, redis, … auto-instrumented)
OTEL_SERVICE_NAME=orders-api \
OTEL_EXPORTER_OTLP_ENDPOINT=http://otel-collector:4318 \
opentelemetry-instrument uvicorn app.main:app --host 0.0.0.0 --port 8000
```

Programmatic setup + manual spans for business steps:

```python
from opentelemetry import trace
from opentelemetry.exporter.otlp.proto.http.trace_exporter import OTLPSpanExporter
from opentelemetry.instrumentation.fastapi import FastAPIInstrumentor
from opentelemetry.sdk.resources import Resource
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.trace import Status, StatusCode

provider = TracerProvider(resource=Resource.create({"service.name": "orders-api"}))
provider.add_span_processor(BatchSpanProcessor(OTLPSpanExporter()))   # endpoint from OTEL_EXPORTER_OTLP_ENDPOINT
trace.set_tracer_provider(provider)
FastAPIInstrumentor.instrument_app(app, excluded_urls="health,metrics")

tracer = trace.get_tracer("orders")

async def checkout(cart, user):
    with tracer.start_as_current_span("checkout") as span:
        span.set_attributes({"cart.items": len(cart.items), "user.tier": user.tier})   # no PII
        try:
            return await charge_payment(await price_cart(cart))
        except Exception as exc:
            span.record_exception(exc)
            span.set_status(Status(StatusCode.ERROR, str(exc)))
            raise
```

Add the trace ID to every log line so you can jump from a log to its trace:

```python
import logging
from opentelemetry import trace

class TraceIdFilter(logging.Filter):
    def filter(self, record):
        ctx = trace.get_current_span().get_span_context()
        record.trace_id = format(ctx.trace_id, "032x") if ctx.is_valid else "-"
        return True
```

Flush on shutdown: call `provider.shutdown()` in the lifespan shutdown phase.

### 3. Error tracking (Sentry)

```python
import sentry_sdk

sentry_sdk.init(
    dsn=settings.sentry_dsn,
    environment=settings.environment,
    release=settings.app_version,           # errors grouped by deploy
    traces_sample_rate=0.1,
    send_default_pii=False,
)
# The FastAPI/Starlette integration is enabled automatically when those packages are installed.
```

### 4. SLO math in Python

```python
def error_budget_minutes(slo: float, window_days: int = 30) -> float:
    return (1 - slo) * window_days * 24 * 60

def burn_rate(observed_error_ratio: float, slo: float) -> float:
    return observed_error_ratio / (1 - slo)

error_budget_minutes(0.999)     # 43.2
burn_rate(0.0144, 0.999)        # 14.4 → page someone
```

### Checklist

- [ ] RED metrics per route pattern (+ in-flight gauge), `/metrics` not public, multiprocess mode if multiple workers
- [ ] OpenTelemetry auto-instrumentation (FastAPI, SQLAlchemy, httpx, Redis) + manual business spans
- [ ] Trace IDs in logs; spans flushed on shutdown
- [ ] Sentry with environment + release
- [ ] `/health` (liveness, no deps) and `/ready` (DB/Redis) endpoints

---

## 36. Security Best Practices

1. **Validate everything** with Pydantic; use `extra="forbid"` on input models to block unexpected fields (mass assignment).
2. **Separate input/output schemas** — never return ORM objects without a `response_model` (leaks hashed passwords, internal fields).
3. **Passwords**: Argon2/bcrypt via `pwdlib`/`passlib`; never log them.
4. **JWT**: short-lived access tokens, strong secret (≥ 32 random bytes) or RS256 keys, explicit `algorithms=[...]`, validate `exp`, rotate refresh tokens.
5. **Authorization on every route** — check ownership (IDOR), roles, and filter queries by user.
6. **SQL injection**: use the ORM / bound parameters; never build SQL with f-strings; whitelist sort/filter columns.
7. **CORS**: explicit origins, never `"*"` with credentials.
8. **Rate limit** login, signup, OTP and expensive endpoints.
9. **File uploads**: validate type & size, random filenames, store outside the app (S3), scan if needed.
10. **Secrets** via env/secret manager, `SecretStr`; never commit `.env`.
11. **HTTPS only** (TLS at the load balancer), HSTS, secure cookies (`HttpOnly`, `Secure`, `SameSite`).
12. **Disable docs** in production if the API is private (`docs_url=None, openapi_url=None`) or protect them.
13. **Don't leak errors** — generic 500 messages, details in logs only.
14. **Timeouts** on outbound calls; **SSRF** protection when fetching user-supplied URLs (allowlist hosts, block internal IPs).
15. **Dependencies**: pin with a lockfile, `pip-audit`, update regularly.
16. **Security headers** middleware (CSP, X-Content-Type-Options, X-Frame-Options) for anything serving HTML.
17. **Request size limits** at the proxy (Nginx `client_max_body_size`).

---

## 37. OWASP API Top 10 in FastAPI

The risks are explained in `nodejs.md` → "OWASP API Security Top 10 (2023)". This section shows the **FastAPI/Pydantic** way to prevent the most common ones.

### API1 — BOLA: scope every lookup to the current user

```python
from typing import Annotated
from fastapi import APIRouter, Depends, FastAPI, HTTPException, Query
from pydantic import BaseModel, ConfigDict, Field

class User(BaseModel):
    id: int
    role: str = "user"

def get_current_user() -> User:                       # real app: decode & verify the JWT/session
    return User(id=1)

CurrentUser = Annotated[User, Depends(get_current_user)]

INVOICES = {10: {"id": 10, "owner_id": 1, "total_paise": 5000, "internal_notes": "vip"},
            11: {"id": 11, "owner_id": 2, "total_paise": 9000, "internal_notes": "late payer"}}

class InvoiceOut(BaseModel):                          # API3: only these fields ever leave the server
    id: int
    total_paise: int

app = FastAPI()

@app.get("/invoices/{invoice_id}", response_model=InvoiceOut)
def get_invoice(invoice_id: int, user: CurrentUser):
    invoice = INVOICES.get(invoice_id)
    if invoice is None or invoice["owner_id"] != user.id:     # ownership check (SQL: WHERE id = :id AND owner_id = :uid)
        raise HTTPException(404, "Invoice not found")          # 404 — don't confirm it exists
    return invoice                                             # internal_notes filtered out by response_model
```

### API3 — Mass assignment: strict input models

```python
class ProfileUpdate(BaseModel):
    model_config = ConfigDict(extra="forbid")        # unknown fields → 422 instead of silently accepted
    name: str | None = Field(default=None, min_length=1, max_length=80)
    bio: str | None = Field(default=None, max_length=500)

@app.patch("/me")
def update_me(data: ProfileUpdate, user: CurrentUser):
    changes = data.model_dump(exclude_unset=True)     # only what was sent — and only allowed fields exist
    return {"updated": sorted(changes)}
# PATCH /me {"name": "R", "role": "admin"} → 422 "Extra inputs are not permitted"
```

Never pass `request.json()` straight into an ORM update; never return ORM objects without a `response_model`.

### API4 — Resource limits

```python
@app.get("/products")
def list_products(
    limit: Annotated[int, Query(ge=1, le=100)] = 20,          # ?limit=100000 → 422
    offset: Annotated[int, Query(ge=0, le=10_000)] = 0,       # deep offsets are expensive too
    q: Annotated[str | None, Query(max_length=100)] = None,
):
    return {"limit": limit, "offset": offset, "q": q}
```

Plus: rate limiting (slowapi / gateway), request body size limits at the proxy (`client_max_body_size`), upload size checks, timeouts on outbound calls and DB queries, and per-user quotas on expensive actions.

### API5 — Function-level authorization: protect the whole router

```python
def require_admin(user: CurrentUser) -> User:
    if user.role != "admin":
        raise HTTPException(403, "Admins only")
    return user

admin = APIRouter(prefix="/admin", dependencies=[Depends(require_admin)])   # every route below is protected

@admin.delete("/users/{user_id}", status_code=204)
def delete_user(user_id: int) -> None:
    ...

app.include_router(admin)
```

### API7 — SSRF guard for user-supplied URLs

```python
import ipaddress
import socket
from urllib.parse import urlsplit

ALLOWED_PORTS = {80, 443}

def is_blocked_ip(address: str) -> bool:
    ip = ipaddress.ip_address(address)
    if isinstance(ip, ipaddress.IPv6Address) and ip.ipv4_mapped:      # ::ffff:127.0.0.1
        ip = ip.ipv4_mapped
    return (ip.is_private or ip.is_loopback or ip.is_link_local or ip.is_multicast
            or ip.is_reserved or ip.is_unspecified or not ip.is_global)

def assert_safe_url(url: str, resolve=socket.getaddrinfo) -> list[str]:
    parts = urlsplit(url)
    if parts.scheme not in ("http", "https"):
        raise ValueError("Only http(s) URLs are allowed")
    if parts.username or parts.password:
        raise ValueError("Credentials in URL are not allowed")
    if not parts.hostname:
        raise ValueError("Invalid URL")
    port = parts.port or (443 if parts.scheme == "https" else 80)
    if port not in ALLOWED_PORTS:
        raise ValueError("Port not allowed")
    try:
        infos = resolve(parts.hostname, port, proto=socket.IPPROTO_TCP)
    except socket.gaierror as exc:
        raise ValueError("Host does not resolve") from exc
    addresses = sorted({info[4][0] for info in infos})
    if not addresses or any(is_blocked_ip(a) for a in addresses):
        raise ValueError("Destination not allowed")
    return addresses          # connect to one of THESE addresses (prevents DNS rebinding), with timeouts
```

Then fetch with `httpx` using `follow_redirects=False` (validate every redirect target again), a short timeout, and a response size cap.

### API8 — Misconfiguration checklist for FastAPI

- `debug=False` in production; generic 500 responses (custom exception handler), details only in logs.
- Disable or protect `/docs`, `/redoc`, `/openapi.json` for private APIs.
- Explicit CORS origins (never `"*"` with credentials); `TrustedHostMiddleware`; HTTPS redirect at the proxy.
- Security headers (via the proxy or a small middleware): HSTS, `X-Content-Type-Options: nosniff`, frame protection.
- Secrets from `pydantic-settings` (`SecretStr`), least-privilege DB user, dependencies pinned and audited (`pip-audit`).

### Security tests (pytest + TestClient)

```python
from fastapi.testclient import TestClient
client = TestClient(app)

def test_bola_other_users_invoice_is_404():
    assert client.get("/invoices/11").status_code == 404        # owned by user 2

def test_response_hides_internal_fields():
    assert "internal_notes" not in client.get("/invoices/10").json()

def test_mass_assignment_rejected():
    assert client.patch("/me", json={"name": "R", "role": "admin"}).status_code == 422

def test_pagination_capped():
    assert client.get("/products?limit=100000").status_code == 422

def test_admin_routes_reject_regular_users():
    assert client.delete("/admin/users/5").status_code == 403
```

---

## 38. Performance

- Use `async def` + async drivers (asyncpg, redis.asyncio, httpx.AsyncClient) for I/O-heavy endpoints; `def` for blocking libraries.
- **Never block the event loop** (see Section 13).
- **Reuse clients & connection pools** (create in lifespan, not per request).
- **DB**: indexes, `selectinload` to avoid N+1, select only needed columns, pagination, keep transactions short.
- **Caching** (Redis, HTTP cache headers, CDN).
- **Offload** slow work to background queues; return `202 Accepted`.
- **Multiple workers**: `fastapi run --workers 4` / `uvicorn --workers N` / Gunicorn with Uvicorn workers (≈ CPU cores).
- **uvloop + httptools** (installed with `uvicorn[standard]`) for a faster event loop and HTTP parser.
- **ORJSON** responses for big payloads (`default_response_class=ORJSONResponse`) — or return pre-serialized data.
- **Pydantic**: avoid validating huge responses twice; for big lists consider `TypeAdapter`.
- **Profile**: `py-spy`, `pyinstrument` middleware, OpenTelemetry traces; load test with `locust`/`k6`.
- **GZip** large responses (or at the proxy).

---

## 39. Deployment

### Running in production

```bash
fastapi run app/main.py --workers 4 --port 8000
# or
uvicorn app.main:app --host 0.0.0.0 --port 8000 --workers 4 --proxy-headers --forwarded-allow-ips="*"
# or Gunicorn as process manager
gunicorn app.main:app -k uvicorn.workers.UvicornWorker -w 4 -b 0.0.0.0:8000 --timeout 60 --graceful-timeout 30
```

In Kubernetes, run **one process per container** and scale with replicas instead of many workers.

### Dockerfile (multi-stage with uv)

```dockerfile
FROM python:3.13-slim AS builder
COPY --from=ghcr.io/astral-sh/uv:latest /uv /usr/local/bin/uv
WORKDIR /app
ENV UV_COMPILE_BYTECODE=1 UV_LINK_MODE=copy
COPY pyproject.toml uv.lock ./
RUN uv sync --frozen --no-dev --no-install-project
COPY . .
RUN uv sync --frozen --no-dev

FROM python:3.13-slim
WORKDIR /app
RUN useradd --create-home appuser
COPY --from=builder /app /app
ENV PATH="/app/.venv/bin:$PATH" PYTHONUNBUFFERED=1
USER appuser
EXPOSE 8000
HEALTHCHECK CMD python -c "import urllib.request; urllib.request.urlopen('http://localhost:8000/health')"
CMD ["fastapi", "run", "app/main.py", "--port", "8000"]
```

### docker-compose for local dev

```yaml
services:
  api:
    build: .
    ports: ["8000:8000"]
    env_file: .env
    depends_on: [db, redis]
    command: sh -c "alembic upgrade head && fastapi run app/main.py --port 8000"
  db:
    image: postgres:17
    environment: { POSTGRES_USER: app, POSTGRES_PASSWORD: app, POSTGRES_DB: app }
    volumes: [pgdata:/var/lib/postgresql/data]
  redis:
    image: redis:7
  worker:
    build: .
    command: celery -A app.workers.tasks worker --loglevel=info
    env_file: .env
    depends_on: [redis, db]
volumes: { pgdata: {} }
```

Behind **Nginx** / a cloud load balancer for TLS, compression, request size limits and static files. Platforms: AWS ECS/Fargate, Cloud Run, Render, Railway, Fly.io, Kubernetes, or serverless via Mangum (AWS Lambda).

---

## 40. Complete CRUD Example

A compact but production-shaped "notes" feature: schemas → model → repository → service → router, with auth and ownership.

```python
# app/schemas/note.py
from datetime import datetime
from pydantic import BaseModel, ConfigDict, Field

class NoteCreate(BaseModel):
    model_config = ConfigDict(extra="forbid", str_strip_whitespace=True)
    title: str = Field(min_length=1, max_length=200)
    content: str = Field(default="", max_length=10_000)
    tags: list[str] = Field(default_factory=list, max_length=10)

class NoteUpdate(BaseModel):
    model_config = ConfigDict(extra="forbid", str_strip_whitespace=True)
    title: str | None = Field(default=None, min_length=1, max_length=200)
    content: str | None = Field(default=None, max_length=10_000)
    tags: list[str] | None = None

class NoteOut(BaseModel):
    model_config = ConfigDict(from_attributes=True)
    id: int
    title: str
    content: str
    tags: list[str]
    created_at: datetime
    updated_at: datetime
```

```python
# app/models/note.py
from sqlalchemy import String, Text, ForeignKey, JSON, func
from sqlalchemy.orm import Mapped, mapped_column

class Note(Base):
    __tablename__ = "notes"
    id: Mapped[int] = mapped_column(primary_key=True)
    owner_id: Mapped[int] = mapped_column(ForeignKey("users.id", ondelete="CASCADE"), index=True)
    title: Mapped[str] = mapped_column(String(200))
    content: Mapped[str] = mapped_column(Text, default="")
    tags: Mapped[list[str]] = mapped_column(JSON, default=list)
    created_at: Mapped[datetime] = mapped_column(server_default=func.now())
    updated_at: Mapped[datetime] = mapped_column(server_default=func.now(), onupdate=func.now())
```

```python
# app/repositories/note_repo.py
from sqlalchemy import select, func
from sqlalchemy.ext.asyncio import AsyncSession

class NoteRepository:
    def __init__(self, db: AsyncSession):
        self.db = db

    async def get_for_owner(self, note_id: int, owner_id: int) -> Note | None:
        return await self.db.scalar(select(Note).where(Note.id == note_id, Note.owner_id == owner_id))

    async def list_for_owner(self, owner_id: int, q: str | None, offset: int, limit: int) -> tuple[list[Note], int]:
        stmt = select(Note).where(Note.owner_id == owner_id)
        if q:
            stmt = stmt.where(Note.title.ilike(f"%{q}%"))
        total = await self.db.scalar(select(func.count()).select_from(stmt.subquery()))
        rows = await self.db.scalars(stmt.order_by(Note.updated_at.desc()).offset(offset).limit(limit))
        return list(rows), total or 0

    def add(self, note: Note) -> None:
        self.db.add(note)

    async def delete(self, note: Note) -> None:
        await self.db.delete(note)
```

```python
# app/services/note_service.py
class NoteService:
    def __init__(self, db: AsyncDb):
        self.db = db
        self.repo = NoteRepository(db)

    async def create(self, owner_id: int, data: NoteCreate) -> Note:
        note = Note(owner_id=owner_id, **data.model_dump())
        self.repo.add(note)
        await self.db.commit()
        await self.db.refresh(note)
        return note

    async def get(self, owner_id: int, note_id: int) -> Note:
        note = await self.repo.get_for_owner(note_id, owner_id)   # ownership enforced in the query
        if not note:
            raise NotFoundError(f"Note {note_id} not found")
        return note

    async def update(self, owner_id: int, note_id: int, data: NoteUpdate) -> Note:
        note = await self.get(owner_id, note_id)
        for field, value in data.model_dump(exclude_unset=True).items():
            setattr(note, field, value)
        await self.db.commit()
        await self.db.refresh(note)
        return note

    async def delete(self, owner_id: int, note_id: int) -> None:
        note = await self.get(owner_id, note_id)
        await self.repo.delete(note)
        await self.db.commit()

NoteServiceDep = Annotated[NoteService, Depends()]
```

```python
# app/api/routes/notes.py
router = APIRouter(prefix="/notes", tags=["notes"])

@router.post("", response_model=NoteOut, status_code=201)
async def create_note(data: NoteCreate, user: CurrentUser, service: NoteServiceDep):
    return await service.create(user.id, data)

@router.get("", response_model=Page[NoteOut])
async def list_notes(user: CurrentUser, db: AsyncDb,
                     q: str | None = None,
                     page: Annotated[int, Query(ge=1)] = 1,
                     size: Annotated[int, Query(ge=1, le=100)] = 20):
    items, total = await NoteRepository(db).list_for_owner(user.id, q, (page - 1) * size, size)
    return Page(items=items, total=total, page=page, size=size, pages=-(-total // size))

@router.get("/{note_id}", response_model=NoteOut)
async def get_note(note_id: int, user: CurrentUser, service: NoteServiceDep):
    return await service.get(user.id, note_id)

@router.patch("/{note_id}", response_model=NoteOut)
async def update_note(note_id: int, data: NoteUpdate, user: CurrentUser, service: NoteServiceDep):
    return await service.update(user.id, note_id, data)

@router.delete("/{note_id}", status_code=204)
async def delete_note(note_id: int, user: CurrentUser, service: NoteServiceDep):
    await service.delete(user.id, note_id)
```

```python
# app/main.py
def create_app() -> FastAPI:
    setup_logging(settings.log_level)
    app = FastAPI(title=settings.app_name, lifespan=lifespan,
                  docs_url=None if settings.environment == "production" else "/docs")
    app.add_middleware(CORSMiddleware, allow_origins=[str(o) for o in settings.cors_origins],
                       allow_credentials=True, allow_methods=["*"], allow_headers=["*"])
    register_exception_handlers(app)
    app.include_router(auth.router)
    app.include_router(notes.router, prefix="/api/v1")
    return app

app = create_app()
```

The app-factory pattern (`create_app()`) makes it easy to build differently configured apps for tests.

---

## 41. Production Checklist

**Code & structure**
- [ ] Layered structure: routers → services → repositories; schemas separate from ORM models
- [ ] Type hints everywhere; `ruff` + `mypy`/`pyright` in CI
- [ ] `Annotated` dependency aliases (`DbSession`, `CurrentUser`, `Pagination`) to keep routes clean
- [ ] App factory + lifespan for startup/shutdown

**API design**
- [ ] Versioned routes (`/api/v1`), plural nouns, proper status codes
- [ ] Separate Create / Update / Out schemas; `response_model` on every route
- [ ] PATCH with `exclude_unset=True`
- [ ] Consistent error format via exception handlers
- [ ] Pagination on all list endpoints, with limits
- [ ] Idempotency keys for payment/order creation

**Data**
- [ ] Alembic migrations (never `create_all` in prod), reviewed
- [ ] Indexes on filter/join/sort columns; no N+1 (eager loading)
- [ ] Connection pooling configured; transactions short
- [ ] Money as integer paise/`Decimal`; datetimes timezone-aware UTC

**Security**
- [ ] Argon2/bcrypt passwords, short-lived JWTs, refresh rotation
- [ ] Authorization + ownership checks on every route
- [ ] CORS allowlist, rate limiting on auth, input limits, `extra="forbid"`
- [ ] Secrets from env/secret manager (`SecretStr`), docs disabled/protected if private

**Reliability**
- [ ] No blocking calls in `async def`
- [ ] Timeouts + retries (transient only) on outbound HTTP; shared clients
- [ ] Background queue for slow work; `BackgroundTasks` only for tiny tasks
- [ ] Health + readiness endpoints; graceful shutdown

**Observability**
- [ ] Structured JSON logs with request IDs; no secrets in logs
- [ ] Sentry for errors; Prometheus metrics; OpenTelemetry tracing

**Testing & delivery**
- [ ] Unit tests for services; API tests with TestClient/httpx + dependency overrides
- [ ] Integration tests against real Postgres in CI
- [ ] Docker image (non-root, slim), lockfile, CI/CD with migrations before deploy

---

## 42. FastAPI vs Flask vs Django vs Express

| | FastAPI | Flask | Django (+DRF) | Express (Node) |
|---|---|---|---|---|
| Type | Async API framework | Micro framework | Batteries-included full-stack | Minimal Node framework |
| Interface | ASGI | WSGI (async partially) | WSGI/ASGI | Node HTTP |
| Validation | Built-in (Pydantic, type hints) | Extensions (marshmallow) | DRF serializers / forms | Libraries (zod, joi) |
| Docs | Automatic OpenAPI/Swagger | Extensions | DRF spectacular | swagger-jsdoc etc. |
| ORM | Bring your own (SQLAlchemy/SQLModel) | Bring your own | Django ORM built in | Prisma/Drizzle/Mongoose |
| Admin panel | No | No | Yes | No |
| Async | First-class | Limited | Improving | Native |
| Best for | APIs, microservices, ML model serving | Small apps, simple APIs | Full web apps, admin-heavy, CMS | JS/TS teams, real-time apps |

---

## 43. Most Asked Interview Questions

### Basics

1. **What is FastAPI and why is it fast?** → ASGI (Starlette) + async, Pydantic v2 (Rust core), efficient serialization.
2. **What are Starlette and Pydantic used for in FastAPI?**
3. **WSGI vs ASGI?**
4. **How does FastAPI use type hints?** → Parse/validate/convert params & bodies, serialize responses, generate OpenAPI docs, editor support.
5. **Path vs query vs body parameters — how does FastAPI decide?** → In the path template → path; Pydantic model → body; simple types otherwise → query.
6. **What is a response model and why use it?**
7. **How are validation errors returned?** → 422 with a `detail` list; customizable via `RequestValidationError` handler.
8. **How do you raise HTTP errors?** → `HTTPException`; custom exceptions + handlers for consistency.
9. **What docs does FastAPI generate?** → `/docs` (Swagger UI), `/redoc`, `/openapi.json`.
10. **How do you organize a large FastAPI project?** → APIRouters + layered/feature structure.

### Intermediate

11. **Explain Dependency Injection in FastAPI. What is `Depends`?**
12. **How do `yield` dependencies work? Use case?** → DB sessions, resources with cleanup.
13. **Are dependencies cached?** → Yes, per request (`use_cache=False` to disable).
14. **`async def` vs `def` endpoints — how does FastAPI run each?**
15. **What happens if you call a blocking function inside `async def`?**
16. **How do you implement JWT authentication? OAuth2PasswordBearer?**
17. **How do you implement role-based access control?**
18. **How do you connect to a database? Sync vs async SQLAlchemy?**
19. **Why use Alembic?**
20. **Middleware vs dependencies — when to use which?**
21. **How do you handle CORS?**
22. **What are lifespan events? Why not create DB clients per request?**
23. **BackgroundTasks vs Celery — when to use which?**
24. **How do you handle file uploads? Large files?**
25. **How do you implement pagination? Offset vs cursor?**
26. **How do you test FastAPI apps? How to mock auth/DB?** → TestClient/httpx + `dependency_overrides`.
27. **Pydantic v1 vs v2 differences?**
28. **`field_validator` vs `model_validator`?**
29. **How to exclude fields from responses (e.g. password)?**
30. **PATCH semantics — how do you apply only sent fields?** → `model_dump(exclude_unset=True)`.

### Advanced

31. **How do you scale FastAPI?** → Multiple workers/replicas behind a load balancer, stateless design, Redis for shared state, async I/O, caching, queues, DB read replicas.
32. **How do WebSockets work in FastAPI? How to broadcast across multiple workers?** → Redis pub/sub.
33. **How do you stream responses (SSE / LLM tokens / big CSV)?** → `StreamingResponse` with generators.
34. **How do you implement rate limiting?** → slowapi + Redis, or at the gateway.
35. **How do you secure a FastAPI app in production?** (Section 36)
36. **How do you add request IDs and structured logging?** → Middleware + contextvars + JSON formatter.
37. **How do you deploy FastAPI?** → Docker, Uvicorn/Gunicorn workers, Nginx/LB, migrations, health checks.
38. **How would you serve an ML model with FastAPI?** → Load once in lifespan, `def` endpoint or thread/process pool for CPU inference, batch requests, queue for heavy jobs, response models for predictions.
39. **How do you keep frontend types in sync with the API?** → Generate TypeScript clients from the OpenAPI schema.
40. **Explain the request lifecycle in FastAPI.** → ASGI server receives request → middleware (outer → inner) → routing → dependency resolution (validate params, run deps) → path function → response model validation/serialization → yield-dependency cleanup → middleware (inner → outer) → response sent → background tasks run.

---

**End of FastAPI notes.**
