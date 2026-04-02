# Spec 001: Catalog - Game Entity Contract

## Overview
Defines the data structure for game objects returned by the `savestategg-catalog-api`.

## Schema (JSON)
{
  "id": "uuid",
  "external_id": "int (IGDB ID)",
  "title": "string",
  "summary": "string (markdown supported)",
  "release_date": "ISO8601 string",
  "cover_url": "url",
  "platforms": ["string"],
  "genres": ["string"],
  "aggregated_rating": "float (0-100)"
}

## Acceptance Criteria
- Must provide a default placeholder URL if `cover_url` is null.
- `release_date` must be formatted as YYYY-MM-DD.