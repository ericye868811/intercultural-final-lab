# Intercultural Final Lab — V2.4 Public Release

This folder is a **static PWA**. No build step, Node.js server, database, or API is required.

## What is included

- `index.html` — complete trainer and embedded question/knowledge data
- `manifest.webmanifest` — PWA manifest
- `service-worker.js` — offline app shell caching
- `assets/` — icons and social share image
- `404.html` — fallback page
- `PRIVACY.md` — local-data privacy note

## Mobile / PWA behavior

After deployment over **HTTPS**:

- Android/Chromium browsers can offer **Install app / Add to Home screen**.
- iPhone/iPad users can use Safari → Share → **Add to Home Screen**.
- After the first successful load, the site shell and embedded question bank can work offline.
- Each user's progress remains in that browser/device via `localStorage`.

## Recommended deployment for users in mainland China

### Option A — Tencent Cloud COS (manual upload, straightforward)

1. Create a COS bucket.
2. Upload the **contents of this folder** so `index.html` is at the bucket website root.
3. Enable static website hosting and set `index.html` as the index document.
4. Bind your own domain and enable HTTPS.
5. If the bucket/domain is hosted in mainland China, complete ICP filing as required.

Official guide: https://cloud.tencent.com/document/product/436/9512

### Option B — Alibaba Cloud OSS

1. Create an OSS bucket.
2. Upload the **contents of this folder** to the root.
3. Enable Static Website Hosting and set `index.html` as the default homepage.
4. Bind a custom domain + HTTPS.
5. For a mainland-China bucket, a custom domain generally needs ICP filing.

Official guide: https://help.aliyun.com/zh/oss/user-guide/static-website-hosting/

### Option C — Tencent EdgeOne Makers (Git-based deployment)

Tencent renamed EdgeOne Pages to **EdgeOne Makers** in 2026. It supports static sites and automated deployment from a Git repository. For this project there is no build command: publish the repository root containing `index.html`.

Official overview: https://cloud.tencent.com/document/product/1552/127367

## Important deployment detail

Keep these files at the same relative level:

```text
index.html
manifest.webmanifest
service-worker.js
404.html
assets/
  icon-192.png
  icon-512.png
  icon-maskable-512.png
  apple-touch-icon.png
  favicon.svg
  share-card.png
```

The PWA uses relative paths, so it can also work from a subdirectory.

## Updating the site

Replace the hosted files with the newer release. `service-worker.js` uses a versioned cache (`ic-final-lab-v2.4`), so new releases should increment the cache name.

## User-data model

This public release intentionally has no login. Each user gets an independent local training history. If you later want cross-device sync, rankings, class dashboards, or teacher analytics, those require a backend/authentication layer.
