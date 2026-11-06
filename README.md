# AI Decorator — public pages (draft, not published)

Static HTML for the privacy policy and support page that the App Store
listing (`fastlane/metadata/*/privacy_url.txt`, `support_url.txt`) and the
paywall legal text link to. **Nothing here is live** until Jonathan picks a
host and OKs publishing.

Proposed host: a new public repo `JonathanWilson1/PolicyDocuments` with
GitHub Pages. The old repo of that name is gone, which is why both policy
URLs 404. Recreating it under the same name brings the URL that every
already-shipped build links to back to life:

| File in this folder | Served at |
|---|---|
| `ai-decorator/privacy.html` | `https://jonathanwilson1.github.io/PolicyDocuments/ai-decorator/privacy.html` |
| `ai-decorator/support.html` | `https://jonathanwilson1.github.io/PolicyDocuments/ai-decorator/support.html` |
| `privacypolicys/2022/10/01/Privacy-Policy-Interior-Design.html` | old URL in shipped builds ≤ 2.3 (redirect) |
| `privacypolicys/2022/10/01/Privacy-Policy-Interior-Design-copy.html` | old URL in the ASC metadata (redirect) |

After publishing: point `privacy_url.txt` / `support_url.txt` at the new
URLs (metadata push needs Jonathan's OK) — the paywall already uses the new
privacy URL in this branch.
