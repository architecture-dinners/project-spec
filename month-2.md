## Background

For this month, we'll add basic CRUD operations to our apps. This should be done via process-local persistence; we'll get to databases at a later point in time.


## The CRUD APIs

We want to add the following API endpoints to our Web Server.

### List
```
GET /posts?search=q

-- JSON Response
[
  {
    id: string, // UUID
    title: string,
    body: string,
    createdAt: string // RFC3339: 1985-04-12T23:20:50.52
  },
  ...
]
```

Lists all posts known to the system. If a `search` term is provided, the list should be filtered to include posts with matching `title` or `body` fields. All string comparisons should be [unicode case insensitive](https://golang.org/pkg/strings/#EqualFold). Posts should be ordered newest to oldest by the `createdAt` field.

### Read
```
GET /post/:uuid

-- JSON Response
{
  id: string, // UUID
  title: string,
  body: string,
  createdAt: string // RFC3339: 1985-04-12T23:20:50.52
}
```

Fetches a single post by UUID. If the given UUID does not exist, a `404` should be returned.

### Create
```
POST /posts

-- JSON Request
{
  title: string,
  body: string
}

-- JSON Response
{
  id: string, // UUID
  title: string,
  body: string,
  createdAt: string // RFC3339: 1985-04-12T23:20:50.52
}
```

Creates a new post and returns the record that was persisted with a randomly assigned ID (UUID v4). The endpoint should validate that both `title` and `body` are non-empty strings. A `400` should be returned if these conditions are not met.


### Update
```
PUT /post/:uuid

-- JSON Request
{
  title?: string,
  body?: string
}

-- JSON Response
{
  id: string, // UUID
  title: string,
  body: string,
  createdAt: string // RFC3339: 1985-04-12T23:20:50.52
}
```

Updates an existing post and returns the record that was persisted. If the given UUID does not exist, a `404` should be returned. Only keys that are present in the JSON Request should be updated. For a key that exists, it is only valid if the value is a non-empty string. A `400` should be returned if these conditions are not met.


### Delete
```
DELETE /post/:uuid

-- JSON Response
{
  id: string, // UUID
  title: string,
  body: string,
  createdAt: string // RFC3339: 1985-04-12T23:20:50.52
}
```

Deletes an existing post and returns that record that was removed. If the given UUID does not exist, a `404` should be returned.

## Items to Note

### UUIDs
The post IDs should be UUIDs. Please use UUIDv4 when generating new identifiers.

`123e4567-e89b-12d3-a456-426655440000`

### Timestamps
The timestamp strings should be formatted using the RFC3339 pattern. Timestamps should be returned in UTC.

`1985-04-12T23:20:50.52Z`
