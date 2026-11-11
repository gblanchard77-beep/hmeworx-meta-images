# hmeworx-meta-images

Tiny authenticated image host for short-lived HmeWorx JPEGs that Meta Graph fetches.
Separate from kcwt-meta-images. Public reads live at `/hmeworx/i/<64hex>.jpg`.

## Env (names only)

| Name | Purpose |
| --- | --- |
| `HMEWORX_META_IMAGES_SECRET` | Shared secret for `POST /upload` and `DELETE /hmeworx/i/<id>.jpg` |
| `HMEWORX_META_IMAGES_PUBLIC_BASE` | Public https origin returned in upload JSON |
| `PORT` | Listen port (Railway sets) |
| `DATA_DIR` | File store (default `/data/hmeworx`) |

## Routes

- `POST /upload` + `X-Auth-Secret` → `{"id","url"}` for `/hmeworx/i/<64 hex>.jpg`
- `GET /hmeworx/i/<64 hex>.jpg` → image or 404
- `DELETE /hmeworx/i/<64 hex>.jpg` + `X-Auth-Secret` → 204
- `GET /health` → `ok`
- Anything else → 404 (no listing)

No custom domain. Default `*.up.railway.app` only.
