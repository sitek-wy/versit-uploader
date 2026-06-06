# Versit Uploader

A fast, no-friction desktop uploader for file-hosting services. Drop files in, get shareable links out. Built for large files and bulk uploads, with a queue, live ETA, and support for multiple hosts.

Windows desktop application, distributed as a single self-contained `.exe` with built-in auto-updates.

---

## Highlights

- **Multi-host** — upload to [Uploadao](https://uploadao.com), [Rapidgator](https://rapidgator.net), and [1fichier](https://1fichier.com) from one app. Switch hosts from a dropdown; each host keeps its own login.
- **Built for big files** — fully streamed uploads keep memory usage flat (a few MB of RAM) whether the file is 5 MB or 60 GB.
- **Upload queue** — add many files, watch them process one after another or several at once.
- **Parallel uploads** — send multiple files simultaneously (configurable, 1–8).
- **Multi-threaded per file** — on Uploadao, each file is split into parallel chunks to saturate your connection.
- **Live progress** — per-file percentage plus an aggregate bar with combined speed and ETA for the whole batch.
- **Resilient** — automatic retry with backoff on dropped connections, so a momentary network blip doesn't fail an entire file.
- **Resume-friendly state** — your queue, resulting links, settings, and login are remembered between sessions.
- **Drag & drop** — drop files straight onto the window.
- **Auto-update** — checks for new versions on launch and updates itself in place.

---

## Download

Grab the latest `VersitUploader.exe` from the [**Releases**](https://github.com/sitek-wy/versit-uploader/releases/latest) page.

No installer, no dependencies — just run the `.exe`. Windows 10/11, 64-bit.

> On first launch SmartScreen may warn about an unrecognized publisher (the build is unsigned). Choose **More info → Run anyway**.

---

## Usage

1. **Pick a host** from the *Service* dropdown (Uploadao, Rapidgator, or 1fichier).
2. **Log in** (optional for Uploadao, required for Rapidgator and 1fichier). Tick *Remember me* to stay logged in.
   - Logged in → files are attached to your account.
   - Anonymous (Uploadao only) → files upload without an account.
   - **1fichier** → paste your API key into the *Password* field (the Login field is ignored).
3. **Add files** — click *Add files* or drag them onto the window.
4. **Tune throughput** (optional):
   - **Files at once** — how many files upload simultaneously (1–8).
   - **Threads/file** — parallel connections per file (Uploadao).
5. Click **Upload all**.
6. When a file finishes, its link appears in the row. **Double-click a row** to open the link, or use **Copy links** to copy every link at once.

The queue and links persist after you close the app, so you can come back to them later.

---

## Supported hosts

| Host | Auth | Upload model | Notes |
|------|------|--------------|-------|
| **Uploadao** | Optional (account or anonymous) | Multi-threaded chunked | Parallel chunks per file; fastest option |
| **Rapidgator** | Required (account) | Single streamed connection | Free accounts limited to 5 GB/file |
| **1fichier** | Required (API key) | Single streamed connection | Paste your **API key** into the *Password* field (Login is ignored) |

---

## Settings & data

The app stores its state in:

```
%APPDATA%\VersitUploader\config.json
```

This includes per-host login (passwords are base64-encoded, **not** strongly encrypted), your last-used settings (files-at-once, threads, public flag), and the saved queue with its links.

To reset everything, delete that folder.

---

## Auto-update

On launch the app checks for the latest version. If a newer one exists, it offers to download and install it, then relaunches automatically. No manual download needed.

---

## Security & privacy

- Credentials are stored locally only. Passwords are base64-encoded in `config.json` — this is obfuscation, not encryption. Use *Remember me* only on machines you trust.
- All transfers go directly to the chosen host over HTTPS. The app sends nothing to any third party.
- Treat your upload links as shareable URLs — anyone with the link can access a public file.

---

## License

Released for personal use. Not affiliated with Uploadao or Rapidgator.
