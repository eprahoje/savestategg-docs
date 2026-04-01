# Spec 001 — Catalog Contract

| Field | Value |
|---|---|
| **Spec ID** | 001 |
| **Title** | Catalog — Game Entity API Contract |
| **Status** | Draft |
| **Author** | SaveStateGG Team |
| **Created** | 2026-03-31 |
| **Related ADR** | [0001-initial-architecture.md](../arch/0001-initial-architecture.md) |

---

## Overview

This document specifies the shape of the **Game** entity as exposed by the SaveStateGG API. It serves as the contract between the back-end (API) and the front-end (Web UI) teams, and must be agreed upon before any implementation begins.

Any deviation from this contract must result in an updated spec version and a corresponding changelog entry below.

---

## Endpoint

```
GET /api/v1/catalog/games/{slug}
```

### Path Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `slug` | `string` | ✅ | URL-friendly unique identifier for the game (e.g., `the-last-of-us-part-i`) |

### Query Parameters

_None at this time._

### Response

**Status:** `200 OK`  
**Content-Type:** `application/json`

---

## Mock Response — Game Entity

```json
{
  "data": {
    "id": "01HXZ3F2QKBV8J7MCTW5YPNE4",
    "slug": "the-last-of-us-part-i",
    "title": "The Last of Us Part I",
    "releaseDate": "2022-09-02",
    "developer": "Naughty Dog",
    "publisher": "Sony Interactive Entertainment",
    "genres": ["Action", "Adventure", "Survival Horror"],
    "platforms": ["PlayStation 5", "PC"],
    "coverImageUrl": "https://cdn.savestategg.com/covers/the-last-of-us-part-i.jpg",
    "summary": "Experience the emotional storytelling and the tense, desperate combat of the award-winning The Last of Us, built from the ground up for PlayStation 5.",
    "aggregateRating": {
      "average": 4.5,
      "count": 13847
    },
    "externalIds": {
      "igdb": 119388,
      "rawg": 452636
    }
  },
  "meta": {
    "requestId": "req_01HXZ3F2QKBV8J7MCTW5YPNE5",
    "timestamp": "2026-03-31T23:00:00.000Z"
  }
}
```

---

## Error Responses

### `404 Not Found` — Game does not exist

```json
{
  "error": {
    "code": "GAME_NOT_FOUND",
    "message": "No game was found with the slug 'the-last-of-us-part-i'.",
    "requestId": "req_01HXZ3F2QKBV8J7MCTW5YPNE5"
  }
}
```

---

## Field Definitions

| Field | Type | Nullable | Description |
|---|---|---|---|
| `id` | `string` (ULID) | No | Globally unique, sortable identifier for the Game (see [ULID spec](https://github.com/ulid/spec)). |
| `slug` | `string` | No | URL-safe, human-readable unique identifier. Lowercase, hyphen-separated. |
| `title` | `string` | No | The official localized title of the game. |
| `releaseDate` | `string` (ISO 8601 date) | Yes | Original worldwide release date in `YYYY-MM-DD` format. Null if not yet released. |
| `developer` | `string` | Yes | Name of the primary development studio. |
| `publisher` | `string` | Yes | Name of the publisher responsible for distribution. |
| `genres` | `string[]` | No | Ordered list of genre tags. Minimum one entry. |
| `platforms` | `string[]` | No | List of platforms the game is available on. Minimum one entry. |
| `coverImageUrl` | `string` (URL) | Yes | Absolute URL to the game's cover artwork hosted on the SaveStateGG CDN. |
| `summary` | `string` | Yes | Short textual description of the game (max 1000 characters). |
| `aggregateRating.average` | `number` | Yes | Computed average rating from all user Reviews. Null if no reviews exist. |
| `aggregateRating.count` | `integer` | No | Total number of Reviews contributing to the aggregate rating. |
| `externalIds.igdb` | `integer` | Yes | Corresponding record ID in the IGDB database. Null if not mapped. |
| `externalIds.rawg` | `integer` | Yes | Corresponding record ID in the RAWG database. Null if not mapped. |

---

## Changelog

| Version | Date | Author | Summary |
|---|---|---|---|
| 1.0.0 | 2026-03-31 | SaveStateGG Team | Initial draft |
