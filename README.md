# RenderShot Screenshot — GitHub Action

Capture a website screenshot (PNG / JPEG / WebP) in any GitHub workflow and save it as a file. Powered by the [RenderShot](https://rendershot.dev) screenshot & PDF API — no local Chromium, no browser maintenance.

## Quick start

1. Get a free API key on [RapidAPI](https://rapidapi.com/eduardoalcantarasp/api/screenshot-e-pdf-render).
2. Add it as a repository secret named `RENDERSHOT_API_KEY`.
3. Use the action:

```yaml
- name: Capture screenshot
  uses: edubraqd/rendershot-action@v1
  with:
    api-key: ${{ secrets.RENDERSHOT_API_KEY }}
    url: https://example.com
    output: screenshot.webp
    type: webp
    full-page: true
```

## Full example

```yaml
name: Preview
on: [workflow_dispatch]
jobs:
  shot:
    runs-on: ubuntu-latest
    steps:
      - uses: edubraqd/rendershot-action@v1
        with:
          api-key: ${{ secrets.RENDERSHOT_API_KEY }}
          url: https://stripe.com
          output: preview.webp
          type: webp
          full-page: true
          device: iphone_15
          dark-mode: true
          block-cookie-banners: true
      - uses: actions/upload-artifact@v4
        with:
          name: preview
          path: preview.webp
```

## Inputs

| Input | Required | Default | Description |
|---|---|---|---|
| `api-key` | yes | — | RenderShot API key (`x-api-key`). Use a secret. |
| `url` | yes | — | Page to capture. |
| `output` | no | `screenshot.png` | File path to write. |
| `type` | no | `png` | `png`, `jpeg` or `webp`. |
| `full-page` | no | `true` | Capture the full scrollable page. |
| `device` | no | — | Device preset: `iphone_15`, `iphone_se`, `pixel_7`, `galaxy_s9`, `ipad`, `ipad_pro`. |
| `wait-for-selector` | no | — | Wait for a CSS selector before capturing. |
| `delay` | no | — | Extra wait in ms. |
| `dark-mode` | no | `false` | Emulate dark color scheme. |
| `block-ads` | no | `false` | Block ad/tracker requests. |
| `block-cookie-banners` | no | `true` | Hide cookie/consent banners. |
| `base-url` | no | `https://api.rendershot.dev` | API base URL. |

## Notes

- The API key is masked in logs (`::add-mask::`).
- Non-2xx responses fail the step with a readable error.
- Quotas and rate limits follow your RenderShot/RapidAPI plan.

## Links

- Website: https://rendershot.dev
- API docs: https://api.rendershot.dev/docs
- Get a key (RapidAPI): https://rapidapi.com/eduardoalcantarasp/api/screenshot-e-pdf-render
- Examples (cURL, Node, Python, PHP): https://github.com/edubraqd/rendershot-examples

## License

MIT — see [LICENSE](LICENSE).
