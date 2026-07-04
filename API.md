# JioSaavn API

Base URL: `http://localhost:3000/api`

All endpoints return JSON with the structure: `{ success: boolean, data: T }`

---

## Songs

### Get songs by IDs or link

```
GET /api/songs
```

| Query Param | Type | Required | Description |
|-------------|------|----------|-------------|
| `ids` | string | No* | Comma-separated list of song IDs (e.g. `3IoDK8qI,4IoDK8qI`) |
| `link` | string (url) | No* | Direct JioSaavn song link (e.g. `https://www.jiosaavn.com/song/houdini/OgwhbhtDRwM`) |

\* Either `ids` or `link` must be provided.

**Response:** `{ success: boolean, data: Song[] }`

### Get song by ID

```
GET /api/songs/{id}
```

| Path Param | Type | Required | Description |
|------------|------|----------|-------------|
| `id` | string | Yes | ID of the song (e.g. `3IoDK8qI`) |

**Response:** `{ success: boolean, data: Song[] }`

### Get song suggestions

```
GET /api/songs/{id}/suggestions
```

| Path Param | Type | Required | Description |
|------------|------|----------|-------------|
| `id` | string | Yes | ID of the song (e.g. `yDeAS8Eh`) |

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `limit` | number | No | `10` | Number of suggestions to retrieve |

**Response:** `{ success: boolean, data: Song[] }`

---

## Albums

### Get album by ID or link

```
GET /api/albums
```

| Query Param | Type | Required | Description |
|-------------|------|----------|-------------|
| `id` | string | No* | Album ID (e.g. `23241654`) |
| `link` | string (url) | No* | Direct JioSaavn album link (e.g. `https://www.jiosaavn.com/album/future-nostalgia/ITIyo-GDr7A_`) |

\* Either `id` or `link` must be provided.

**Response:** `{ success: boolean, data: Album }`

---

## Artists

### Get artist by ID or link

```
GET /api/artists
```

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `id` | string | No* | — | Artist ID (e.g. `1274170`) |
| `link` | string (url) | No* | — | Direct JioSaavn artist link (e.g. `https://www.jiosaavn.com/artist/dua-lipa-songs/r-OWIKgpX2I_`) |
| `page` | number | No | `0` | Page number |
| `songCount` | number | No | `10` | Number of songs to fetch |
| `albumCount` | number | No | `10` | Number of albums to fetch |
| `sortBy` | enum | No | `popularity` | Sort field (`popularity`, `latest`, `alphabetical`) |
| `sortOrder` | enum | No | `desc` | Sort direction (`asc`, `desc`) |

\* Either `id` or `link` must be provided.

**Response:** `{ success: boolean, data: Artist }`

### Get artist by ID

```
GET /api/artists/{id}
```

| Path Param | Type | Required | Description |
|------------|------|----------|-------------|
| `id` | string | Yes | Artist ID (e.g. `1274170`) |

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `page` | number | No | `0` | Page number |
| `songCount` | number | No | `10` | Number of songs to retrieve |
| `albumCount` | number | No | `10` | Number of albums to retrieve |
| `sortBy` | enum | No | `popularity` | Sort field (`popularity`, `latest`, `alphabetical`) |
| `sortOrder` | enum | No | `desc` | Sort direction (`asc`, `desc`) |

**Response:** `{ success: boolean, data: Artist }`

### Get artist songs

```
GET /api/artists/{id}/songs
```

| Path Param | Type | Required | Description |
|------------|------|----------|-------------|
| `id` | string | Yes | Artist ID (e.g. `1274170`) |

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `page` | number | No | `0` | Page number |
| `sortBy` | enum | No | `popularity` | Sort field (`popularity`, `latest`, `alphabetical`) |
| `sortOrder` | enum | No | `desc` | Sort direction (`asc`, `desc`) |

**Response:** `{ success: boolean, data: ArtistSong[] }`

### Get artist albums

```
GET /api/artists/{id}/albums
```

| Path Param | Type | Required | Description |
|------------|------|----------|-------------|
| `id` | string | Yes | Artist ID (e.g. `1274170`) |

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `page` | number | No | `0` | Page number |
| `sortBy` | enum | No | `popularity` | Sort field (`popularity`, `latest`, `alphabetical`) |
| `sortOrder` | enum | No | `desc` | Sort direction (`asc`, `desc`) |

**Response:** `{ success: boolean, data: ArtistAlbum[] }`

---

## Search

All search endpoints require a `query` parameter.

### Global search

```
GET /api/search
```

| Query Param | Type | Required | Description |
|-------------|------|----------|-------------|
| `query` | string | Yes | Search query (e.g. `Imagine Dragons`) |

**Response:** `{ success: boolean, data: { songs, albums, artists, playlists } }`

### Search songs

```
GET /api/search/songs
```

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `query` | string | Yes | — | Search query (e.g. `Believer`) |
| `page` | number | No | `0` | Page number |
| `limit` | number | No | `10` | Results per page |

**Response:** `{ success: boolean, data: SearchSong[] }`

### Search albums

```
GET /api/search/albums
```

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `query` | string | Yes | — | Search query (e.g. `Evolve`) |
| `page` | number | No | `0` | Page number |
| `limit` | number | No | `10` | Results per page |

**Response:** `{ success: boolean, data: SearchAlbum[] }`

### Search artists

```
GET /api/search/artists
```

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `query` | string | Yes | — | Search query (e.g. `Adele`) |
| `page` | number | No | `0` | Page number |
| `limit` | number | No | `10` | Results per page |

**Response:** `{ success: boolean, data: SearchArtist[] }`

### Search playlists

```
GET /api/search/playlists
```

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `query` | string | Yes | — | Search query (e.g. `Indie`) |
| `page` | number | No | `0` | Page number |
| `limit` | number | No | `10` | Results per page |

**Response:** `{ success: boolean, data: SearchPlaylist[] }`

---

## Playlists

### Get playlist by ID or link

```
GET /api/playlists
```

| Query Param | Type | Required | Default | Description |
|-------------|------|----------|---------|-------------|
| `id` | string | No* | — | Playlist ID (e.g. `82914609`) |
| `link` | string (url) | No* | — | Direct JioSaavn playlist link (e.g. `https://www.jiosaavn.com/featured/its-indie-english/AMoxtXyKHoU_`) |
| `page` | number | No | `0` | Page number |
| `limit` | number | No | `10` | Songs per page |

\* Either `id` or `link` must be provided.

**Response:** `{ success: boolean, data: Playlist }`

---

## Error Response

All endpoints may return error responses:

```json
{
  "success": false,
  "message": "error description"
}
```

| Status Code | Description |
|-------------|-------------|
| `400` | Bad request — missing or invalid parameters |
| `404` | Resource not found |
| `500` | Internal server error |
