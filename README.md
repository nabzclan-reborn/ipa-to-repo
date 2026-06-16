# 📦 IPA to Repo

Convert any IPA download URL into a ready-to-use repository JSON for iOS app signers like AltStore, Scarlet, Esign, and more.

## 🆕 What's New

- **No more Python** — fully rewritten in Node.js
- **Fast responses** — uses HTTP range requests to pull only the metadata we need (~200KB) instead of downloading the full IPA
- **Smart caching** — results cached for 10 minutes; same URL returns instantly on repeat requests
- **Icon hosting** — app icons extracted and served directly as a URL, no more base64 blobs
- **Production error codes** — every failure returns a structured error with a stable code
- **Nothing stored permanently** — all cached data and icons are automatically deleted after 10 minutes

## 🌐 Endpoint

```
https://ipa-to-repo.sidelix.vip
```

## ⚠️ Important

- Nabzclan banned users are blocked from this endpoint — appeal here: [https://appeal-ban.nabzclan.vip](https://appeal-ban.nabzclan.vip)
- IPA URLs must be **publicly accessible direct download links** — no auth, no login redirects
- Cloud storage links (Google Drive, Dropbox defaults) usually don't work — adjust sharing settings to get a raw direct link

## 📖 API Status

[Visit Status Page](https://uptime.nabzclan.vip/status/public-apis)

![Status Badge](https://uptime.nabzclan.vip/api/badge/4/status?style=plastic)

---

## 🛠️ Usage

### Request

```
GET https://ipa-to-repo.sidelix.vip/?ipa_url=<your_ipa_url>
```

| Parameter | Required | Description |
|-----------|----------|-------------|
| `ipa_url` | ✅ | Direct download URL to a `.ipa` file |

### Test

```
https://ipa-to-repo.sidelix.vip/?ipa_url=https://cloud-s3.nabzclan.vip/nabzclan-public-cdn-stuff/GBox_v6.0.2.ipa
```

### Example Response

```json
{
  "name": "IPA TO Repo - YourAppName",
  "identifier": "vip.sidelix.ipa-to-repo-yourappname",
  "sourceURL": "https://ipa-to-repo.sidelix.vip/?ipa_url=https%3A%2F%2Fexample.com%2Fyourfile.ipa",
  "iconURL": "https://ipa-to-repo.sidelix.vip/imgs/logo/logo_400x400.jpg",
  "website": "https://sidelix.vip",
  "subtitle": "Sidelix IPA Repo — install any IPA directly on your device",
  "META": {
    "repoName": "IPA TO Repo - YourAppName",
    "repoIcon": "https://ipa-to-repo.sidelix.vip/imgs/logo/logo_400x400.jpg"
  },
  "apps": [
    {
      "name": "YourAppName",
      "type": 1,
      "bundleID": "com.example.yourapp",
      "bundleIdentifier": "com.example.yourapp",
      "version": "1.0.0",
      "versionDate": "2026-06-16",
      "fullDate": "20260616120000",
      "size": 12345678,
      "down": "https://example.com/yourfile.ipa",
      "downloadURL": "https://example.com/yourfile.ipa",
      "developerName": "",
      "localizedDescription": "Repo to install the YourAppName app",
      "icon": "https://ipa-to-repo.sidelix.vip/icons/a3f8c2...png",
      "iconURL": "https://ipa-to-repo.sidelix.vip/icons/a3f8c2...png"
    }
  ]
}
```

---

## 📲 Adding to iOS App Signers

Use the `sourceURL` from the JSON response as the repo URL in your signer.

### 🔵 Scarlet

1. Open **Scarlet** → **Sources** → tap **+**
2. Paste the `sourceURL` and tap **Add**
3. Your app will appear in the available apps list

### 🟢 AltStore

1. Open **AltStore** → **Sources** tab → tap **+**
2. Paste the `sourceURL` and tap **Add Source**
3. The app will be listed and ready to sideload

### 🔴 Esign

1. Open **Esign** → **Repo** → tap **+**
2. Paste the `sourceURL` and tap **Add**
3. Your app will be visible and ready to install

---

## ❌ Errors

All errors return a consistent JSON shape:

```json
{
  "error": {
    "code": "IPA_103",
    "status": 502,
    "message": "Remote server returned an error",
    "detail": "HTTP 403 — https://example.com/yourfile.ipa",
    "timestamp": "2026-06-16T12:00:00.000Z"
  }
}
```

| Code | Status | Meaning |
|------|--------|---------|
| `IPA_001` | 400 | Invalid or missing `ipa_url` parameter |
| `IPA_002` | 403 | Access to this service has been restricted |
| `IPA_101` | 502 | Too many redirects following the IPA URL |
| `IPA_102` | 504 | IPA download timed out |
| `IPA_103` | 502 | Remote server returned an HTTP error |
| `IPA_104` | 502 | Network error contacting the IPA server |
| `IPA_105` | 422 | Remote file is empty |
| `IPA_106` | 502 | Server did not return a Content-Length header |
| `IPA_201` | 422 | File is not a valid ZIP/IPA archive |
| `IPA_202` | 422 | `Info.plist` not found inside the IPA |
| `IPA_203` | 422 | Failed to parse `Info.plist` |
| `IPA_204` | 422 | IPA is missing required metadata (name, bundle ID, or version) |
| `IPA_301` | 500 | Failed to save app icon |
| `IPA_500` | 500 | Unexpected internal error |

---

## 🔍 Health Check

```
GET https://ipa-to-repo.sidelix.vip/health
```

```json
{
  "status": "ok",
  "cached_entries": 42,
  "icons_dir": "/www/wwwroot/ipa-to-repo.sidelix.vip/icons",
  "db_path": "/www/wwwroot/ipa-to-repo.sidelix.vip/cache.db",
  "uptime_secs": 86400
}
```

---

## 🛠 Troubleshooting

| Issue | Fix |
|-------|-----|
| `IPA_001` | Make sure `ipa_url` starts with `http://` or `https://` and is URL-encoded |
| `IPA_002` | Your access has been restricted — [appeal here](https://appeal-ban.nabzclan.vip) |
| `IPA_103` / `IPA_104` | Your IPA host may be blocking requests — test the URL in a browser first |
| `IPA_201` | The URL may point to an HTML page or redirect rather than an actual IPA |
| `IPA_202` | The IPA may be malformed or missing its `Payload/` folder structure |
| Icon not showing | IPA may use an asset catalog (`.car`) for icons — not extractable; default icon used instead |
| Slow first response | First request fetches live from the source. Same URL within 10 minutes is instant |

---

**Disclaimer**: This service is intended for legal use only. Ensure you have the rights to distribute any IPA files you use with this service. Unauthorized distribution of IPA files may violate copyright laws.
