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




name: Checkout Code

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  checkout:
    runs-on: ubuntu-latest

    steps:
      - name: ⬇ Checkout Code
        uses: actions/checkout@v3

      - name: 📁 Show Directory Structure
        run: ls -R || echo "⚠ Failed to list files"





name: Deploy to GitHub Pages

on:
  push:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Upload site to GitHub Pages
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'

      - name: Deploy to GitHub Pages
        uses: actions/deploy-pages@v4

      - name: 🚀 Deploy to GitHub Pages
        uses: actions/deploy-pages@v4



