# Posts And Images

Use posts for reviewed editorial or distribution artifacts derived from sessions, wiki pages, projects, threads, or other source-grounded context.

## Draft Default

Agents should create review drafts unless:

- target environment is clear
- source facts are concrete
- public safety has passed
- user or workflow explicitly approves publishing

When creating a draft through `POST /api/posts`, send `_status: "draft"` or omit `_status`, and omit `publishedAt`.

## Canonical Endpoint

Use the canonical collection endpoint. Do not use draft/autosave query params or version endpoints for normal agent post proposals.

```http
POST /api/posts
```

For updates, fetch or patch posts with `depth=0` whenever possible:

```http
PATCH /api/posts/:id?depth=0
```

Hard rule: never send populated media/upload objects back in a post PATCH payload. Payload upload relationship nodes must preserve scalar ids only.

If the working payload came from a populated read, sanitize every upload node before PATCH so:

- `upload.value` is a string or number media id
- `fields.media` is a string or number media id
- `meta.image` is a string or number media id
- no `upload.value`, `fields.media`, or `meta.image` contains an object with media fields such as `url`, `filename`, `mimeType`, `sizes`, or `createdAt`

Minimal draft payload:

```json
{
  "title": "Draft title",
  "slug": "draft-title",
  "visibility": "public",
  "_status": "draft",
  "content": {
    "root": {
      "type": "root",
      "children": []
    }
  }
}
```

## Visibility

Posts support:

- `public`
- `authenticated`
- `member`
- `admin`

Do not use `member` unless the source material is meant for confirmed members.

## Images

Posts support:

- Header/card image: set `meta.image` to a Payload media ID.
- Inline article image: upload image to Payload media, then insert a Lexical `mediaBlock` node.

Do not use Markdown image syntax in post content. Portal renders Payload Lexical JSON.

Inline media block:

```json
{
  "type": "block",
  "fields": {
    "blockType": "mediaBlock",
    "media": 123
  },
  "format": "",
  "version": 2
}
```

If a populated media block has this shape:

```json
{
  "type": "block",
  "fields": {
    "blockType": "mediaBlock",
    "media": {
      "id": 123,
      "url": "/api/media/file/example.png"
    }
  }
}
```

Patch it as:

```json
{
  "type": "block",
  "fields": {
    "blockType": "mediaBlock",
    "media": 123
  }
}
```
