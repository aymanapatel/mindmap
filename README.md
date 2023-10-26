# Obsidian Quartz with Publish


> [Obisdian Quartz](https://github.com/jackyzha0/quartz) which is the free version of Obsidian Publish


# TODO: 

1. Put all folders to this Repo
     - Follow this [doc](https://quartz.jzhao.xyz/)

# Hosting


There are multiple ways of hosting


## 1. Cloudflare Pages


## 2. Github Pages


- Add Quartz in `<repo>/.github/workflows/deploy.yml`
- Note that there are issues wrt folder paths. 

```
name: Deploy Quartz site to GitHub Pages
 
on:
  push:
    branches:
      - v4
 
permissions:
  contents: read
  pages: write
  id-token: write
 
concurrency:
  group: "pages"
  cancel-in-progress: false
 
jobs:
  build:
    runs-on: ubuntu-22.04
    steps:
      - uses: actions/checkout@v3
        with:
          fetch-depth: 0 # Fetch all history for git info
      - uses: actions/setup-node@v3
        with:
          node-version: 18.14
      - name: Install Dependencies
        run: npm ci
      - name: Build Quartz
        run: npx quartz build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v2
        with:
          path: public
 
  deploy:
    needs: build
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```


## 3. Vercel
