# Cloudflare Worker with Svelte Frontend

This project sets up a Cloudflare Worker with a Svelte frontend using the latest tools.

---

## ✅ Prerequisites

Make sure you have the following installed:

- [Node.js](https://nodejs.org/) v20.0 or higher  
- [npm](https://www.npmjs.com/)
- [Cloudflare Wrangler CLI](https://developers.cloudflare.com/workers/wrangler/install/)

To install Wrangler globally:

```bash
npm install -D wrangler@latest
```

---

## 🚀 Setup

### 1. Create a new Cloudflare Worker with Svelte

```bash
npm create cloudflare@latest -- <name-of-worker>
```

Follow the prompts and select **Svelte** when asked for a template.

### 2. Replace Svelte Page

Replace the file at:

```
my-svelte-app/src/routes/+page.svelte
```

with your custom version from the `worker`.

### 3. Deploy

```bash
npm run deploy
```

Your worker should now be live.

---

## 🌐 Worker Address

You can access the deployed app at:

```
https://worker-svelte.alireza78-bk.workers.dev/
```

---

## 📁 Project Structure (after setup)

```
my-svelte-app/
├── src/
│   └── routes/
│       └── +page.svelte    <-- Replace this file
├── wrangler.toml
├── package.json
└── ...
```

---

## 🛠 Notes

- Be sure to set up any required environment variables using:

```bash
npx wrangler secret put <YOUR_SECRET_NAME>
```

- For API calls from the frontend, use relative paths or Workers’ full URLs depending on your setup.

---