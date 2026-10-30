# Vaultleaf

An encrypted password vault that runs entirely in the browser. Deployed by Vercel from this folder (project: public-vault-leaf).

| Path | What it is |
| --- | --- |
| `index.html` | The whole app: styles, code and the passphrase word list in one file |
| `guide/` | The illustrated user and admin guide, also shown inside the app |
| `sw.js` | Service worker so the app opens offline |
| `manifest.webmanifest`, `icons/` | Add-to-home-screen support |
| `fonts/` | Self-hosted fonts (SIL Open Font License, see fonts/LICENSE.txt) |
| `vercel.json` | Security headers, including the Content Security Policy |

## Editing the app

The Content Security Policy only allows the exact `<script>` that is in `index.html` right now, by its SHA-256 hash (`sha256-N58/nTpIIWwuM5vNYtQ2y9vTza5R1x/IdM7ruXvpCHs=`).
If you change anything between `<script>` and `</script>`, update the hash in `vercel.json` or the page will load blank. To get the new hash:

```
python3 -c "import re,hashlib,base64;s=open('index.html').read().split('<script>',1)[1].split('</script>',1)[0];print('sha256-'+base64.b64encode(hashlib.sha256(s.encode()).digest()).decode())"
```

User data never touches this repository or Vercel: each vault is encrypted and stored in the visitor's own browser.
