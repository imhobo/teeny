# teeny

A lightweight URL shortener API built with Java, Dropwizard, and PostgreSQL. Shorten long URLs into compact, shareable links with minimal overhead.

## Features

- **URL Shortening** — Generate short, unique keys for any valid URL
- **Custom Keys** — Optionally specify a custom alias for your shortened URL
- **Fast Redirects** — Resolve short keys to original URLs with an HTTP 302 redirect
- **RESTful API** — Clean JSON API for programmatic access
- **PostgreSQL Backed** — Persistent storage with JDBI for reliable data management
- **Production Ready** — Configurable logging, CI/CD pipeline, and systemd deployment

## Tech Stack

| Layer    | Technology                          |
|----------|-------------------------------------|
| Language | Java                                |
| Framework| Dropwizard 2.0.0                    |
| Database | PostgreSQL                          |
| Build    | Maven                               |
| CI/CD    | Woodpecker CI                       |

## API Endpoints

### Create a short URL

```
POST /api/shorten
Content-Type: application/json

{
  "url": "https://example.com/very/long/path"
}
```

**Response** `201 Created`
```json
{
  "shortKey": "abc123",
  "originalUrl": "https://example.com/very/long/path"
}
```

### Resolve a short URL

```
GET /{shortKey}
```

**Response** `302 Found` — redirects to the original URL.

## Quick Start

```bash
# Build the project
mvn package -DskipTests

# Run the server
java -jar target/teeny-1.0-SNAPSHOT.jar server config.yml
```

The server starts on `http://localhost:8080` by default. The admin interface is available on `http://localhost:8081`.

## Configuration

Configuration is managed via `config.yml`. Key settings include:

| Setting                    | Description                           |
|----------------------------|---------------------------------------|
| `database.driverClass`     | JDBC driver class (`org.postgresql.Driver`) |
| `database.user`            | Database username                     |
| `database.password`        | Database password                     |
| `database.url`             | JDBC connection URL                   |
| `logging.level`            | Log level (`DEBUG`, `INFO`, etc.)     |
| `logging.appenders`        | Log appender configuration            |

## License

This project is licensed under the Apache License 2.0 — see the [LICENSE](LICENSE) file for details.
