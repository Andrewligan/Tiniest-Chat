
## OpenRouter Static API Frontend

A single‑page HTML client that lets you talk directly to the [OpenRouter](https://openrouter.ai) API from your browser.
No backend, no build step – just drop the file somewhere and open it.

---

### Features

* **Zero‑server** usage – load the file from disk (`file://`) *or* run it from any static host.
* Select any model listed by the `/models` endpoint.
* Dark‑mode friendly, responsive UI.

---

## Quick Start (open from disk)

1. Clone or download this repository.
2. Double‑click `index.html` (or open with Ctrl/Cmd + O in your browser).
3. Paste your OpenRouter API key when prompted.

> **Heads‑up** When opened via `file://`, the browser sends `Origin: null` and most APIs will block the request.  If you see a CORS error, use one of the static‑server options below.

---

## Running a tiny local server

```bash
# Python ≥ 3.7
python -m http.server 8080  # now visit http://localhost:8080/index.html

# …or, with Node
npx serve -l 8080 .
```

Any static‑file server will work; the page only needs an Origin header that is *not* `null`.

---

## Deploying

| target                      | one‑liner                                                                                    |
| --------------------------- | -------------------------------------------------------------------------------------------- |
| **GitHub Pages**            | Push to a branch named `gh-pages` or configure Pages to serve `/` from the `root` of `main`. |
| **Vercel / Netlify**        | Select **Static Site Import**, point it at this repo, leave the build command empty.         |
| **Any Nginx / Apache host** | Copy the contents of the repo to your web‑root.                                              |

---

## Usage examples

### 1 – Chat completion (browser)

1. Choose a chat model such as `mistralai/mistral-7b-instruct`.
2. Type your message and press **Send**.
3. The console will show the underlying `POST /chat/completions` request.

### 2 – Plain completion (cURL)

```bash
curl https://openrouter.ai/api/v1/completions \
  -H "Authorization: Bearer $OPENROUTER_KEY" \
  -H "Content-Type: application/json" \
  -d '{
        "model": "openai/text-davinci-003",
        "prompt": "Write a haiku about surfboards"
      }'
```

### 3 – Download & self‑host

```bash
git clone https://github.com/your‑org/openrouter‑static-frontend.git
cd openrouter‑static-frontend
python -m http.server 8080
```

---

## Security notes

* **Never commit real API keys.** Use environment variables or paste at runtime.
* The client stores the key in memory only; refresh the page to purge it.
* When deployed on a public URL, CORS pre‑flight succeeds because OpenRouter allows any origin – your browser still prevents other sites from stealing your key.

---

## Contributing

1. Fork the repository.
2. Create a feature branch: `git checkout -b feat/your‑idea`.
3. Commit, push, and open a PR.

---

## License

MIT – see the [LICENSE](LICENSE) file for full text.
