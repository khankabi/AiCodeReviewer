# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.


Alright — I’ll give you a **clear, step-by-step breakdown** so you can safely handle your `.env` before pushing your repo to GitHub without exposing secrets.

---

## **Step 1: Add `.env` to `.gitignore`**

Make sure your `.env` file is listed there so Git won’t track it in the future.

1. Open the **backend project folder**.
2. Edit or create `.gitignore`:

   ```gitignore
   # Ignore environment files
   .env
   ```
3. Save the file.

---

## **Step 2: Stop tracking `.env` if it’s already in Git**

If `.env` has ever been staged or committed, `.gitignore` won’t help until you untrack it.

Run:

```bash
git rm --cached .env
git commit -m "Remove .env from version control"
```

This removes it **from the repo**, but keeps it locally on your computer.

---

## **Step 3: Create `.env.example` for GitHub**

GitHub users need to know what environment variables to set up — but not your real keys.

1. Copy your `.env` file:

   ```bash
   cp .env .env.example
   ```
2. Open `.env.example` and **replace sensitive values** with placeholders:

   ```env
   API_KEY=your_api_key_here
   DB_URL=your_database_url_here
   PORT=5000
   ```
3. Commit `.env.example` to your repo:

   ```bash
   git add .env.example
   git commit -m "Add example env file"
   ```

---

## **Step 4: Remove `.env` from Git history (if you ever pushed it)**

If `.env` was **pushed** before, the keys are still in GitHub’s history. You must delete it from history.

The easiest method is with the `git filter-repo` tool:

1. Install filter-repo:

   ```bash
   pip install git-filter-repo
   ```
2. Run cleanup:

   ```bash
   git filter-repo --path .env --invert-paths
   ```
3. Force push cleaned repo:

   ```bash
   git push origin --force --all
   ```

This erases `.env` from all commits in history.

---

## **Step 5: Change your exposed keys**

If you ever pushed `.env` before, **assume it’s compromised** and regenerate your API keys from your service provider.

---

## **Step 6: Push safely to GitHub**

Once `.env` is ignored, history cleaned, and keys rotated:

```bash
git add .
git commit -m "Safe push without secrets"
git push origin main
```

---

If you want, I can **write you the exact Git commands** for your specific backend so you can just copy-paste and be done in a few minutes.
Do you want me to prepare that?
