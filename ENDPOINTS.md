# Endpoints

The container exposes an HTTP server with the callable API functions listed
below. By default it listens on [`http://localhost:3000`](http://localhost:3000)
(see [CONFIGURATION.md](./CONFIGURATION.md) to change the port).

The `<indexer>` path segment selects which source to resolve against. Currently
supported indexers:

| Indexer | Description |
|---|---|
| `videasy` | Videasy source |

## Overview

| Type | Endpoint | Query | Description | Input | Output |
|---|---|---|---|---|---|
| `GET` | `/health` | - | Healthcheck endpoint | - | `{ health }` |
| `GET` | `/api/<indexer>/movie` | `name, tmdbId, imdbId, serverUrl, emulate_url, headers` | Movie streams endpoint | - | `{ streams, subtitles }` |
| `GET` | `/api/<indexer>/series` | `name, season, episode, tmdbId, imdbId, serverUrl, emulate_url, headers` | Series streams endpoint | - | `{ streams, subtitles }` |

## `GET /health`

Healthcheck. Returns whether the service is up.

**Response**

```json
{
  "health": "healthy"
}
```

## `GET /api/<indexer>/movie`

Resolve the available streams for a movie.

**Query parameters**

| Name | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | Title of the movie |
| `tmdbId` | u32 | yes | TMDB id of the movie |
| `imdbId` | string | yes | IMDB id of the movie |
| `serverUrl` | string | yes | Upstream server URL the indexer resolves against |
| `emulate_url` | URL | yes | URL the bridge emulates as the request origin |
| `headers` | map<string,string> | yes | Headers to forward when emulating the request |

**Response** - `{ streams, subtitles }`

## `GET /api/<indexer>/series`

Resolve the available streams for a single series episode.

**Query parameters**

| Name | Type | Required | Description |
|---|---|---|---|
| `name` | string | yes | Title of the series |
| `season` | u16 | yes | Season number |
| `episode` | u16 | yes | Episode number |
| `tmdbId` | u32 | yes | TMDB id of the series |
| `imdbId` | string | yes | IMDB id of the series |
| `serverUrl` | string | yes | Upstream server URL the indexer resolves against |
| `emulate_url` | URL | yes | URL the bridge emulates as the request origin |
| `headers` | map<string,string> | yes | Headers to forward when emulating the request |

**Response** - `{ streams, subtitles }`

## Error responses

On failure an endpoint returns a JSON body with an `error` field and a non-2xx
status code:

| Status | Cause |
|---|---|
| `400 Bad Request` | Unknown/invalid indexer name |
| `500 Internal server error` | Something failed on the server side |

```json
{
  "error": "Invalid indexer name passed in (unrecognized)."
}
```
