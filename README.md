# Front-End-E-Shopping-Site-
Created a Front-End Project for developing E-Shopping Site. The Project includes developing of user interface using html and enhancing it with css. It also includes various functionalities of E-Shopping Site using javascript.
git config --global user.name "Vaibhav Dutt Trivedi"
git config --global user.email "your-email@example.com"

git init
git checkout -b main
git add .
git commit -m "Initial commit"
git remote add origin https://github.com/vaibhav-2709/test.git
git push -u origin main

name: HTML CI Check

on:
  push:
    branches: [main]

jobs:
  validate:
    runs-on: ubuntu-latest

    steps:
      - name: ⬇️ Checkout Code
        uses: actions/checkout@v3

      - name: 🧪 Validate HTML
        uses: Cyb3r-Jak3/html5validator-action@v1
        with:
          root: "./"

      - name: 🧪 Validate CSS (Stylelint)
        uses: stylelint/stylelint-action@v1
        with:
          files: '**/*.css'

      - name: ✅ CI Passed
        if: success()
        run: echo "✅ All validations passed. Ready to deploy."

      - name: ❌ CI Failed
        if: failure()
        run: echo "❌ Validation failed. Fix issues before deployment."

name: Deploy HTML Site

on:
  workflow_run:
    workflows: ["HTML CI Check"]
    types:
      - completed

jobs:
  deploy:
    if: ${{ github.event.workflow_run.conclusion == 'success' }}
    runs-on: ubuntu-latest

    steps:
      - name: ⬇️ Checkout Repository
        uses: actions/checkout@v3

      - name: ⚙️ Setup Pages
        uses: actions/configure-pages@v3

      - name: 📦 Upload to GitHub Pages
        uses: actions/upload-pages-artifact@v2
        with:
          path: "."

      - name: 🚀 Deploy to GitHub Pages
        uses: actions/deploy-pages@v2

      - name: ✅ Deployment Success
        if: success()
        run: echo "🎉 Site successfully deployed to GitHub Pages."

      - name: ❌ Deployment Failed
        if: failure()
        run: echo "🚨 Deployment failed! Please check logs."



