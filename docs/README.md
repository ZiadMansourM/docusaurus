# Testing [docusaurus](https://docusaurus.io/) for [SilverKey Technologies](https://www.silverkeytech.com/)

```yml
name: Deploy to GitHub Pages
on:
  push:
    branches:
      - master
    paths:
      - 'docs/**'
jobs:
  build-deploy:
    name: Build Docs and Deploy to GitHub Pages
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: Download Node.js
      uses: actions/setup-node@v3
      with:
        node-version: 16
    - name: npm install and build
      run: |
        cd docs
        npm install
        npm run build
    - name: Deploy
      uses: s0/git-publish-subdir-action@develop
      env:
        REPO: self
        BRANCH: docs
        FOLDER: docs/build
        GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```