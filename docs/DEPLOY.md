# Deployment Notes

## Front end
GitHub Pages serves `index.html` from the repository root (main branch).

## Worker
All Worker and D1 commands now prefer the **local** binary installed by `npm install` (see `package.json` scripts).

```bash
npm run dev          # local development
npm run deploy       # production deploy