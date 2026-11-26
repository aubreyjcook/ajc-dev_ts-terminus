# ajc-dev_ts-terminus
Terminal based in TS

## Build & Run

```
npm run build
npm run preview
```

## For deployment
add vite.config.ts to the terminus root

```
import { defineConfig } from 'vite'

export default defineConfig({
    base: '/<repo-name>/',
})
```

```
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: true

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 20
          cache: npm
      - run: npm ci
      - run: npm run build
      - uses: actions/configure-pages@v5
      - uses: actions/upload-pages-artifact@v3
        with:
          path: dist
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - id: deployment
        uses: actions/deploy-pages@v4
```

See https://github.com/aubreyjcook/_META_DOMAIN.ajc/blob/main/guidelines/technology-specific-guidelines/frameworks/vite.md