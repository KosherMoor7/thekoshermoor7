# The Kosher Moor — Website Guide

A sovereign herbal marketplace built as a single-page HTML application hosted on GitHub Pages.

---

## How to Add New Products

There are two ways to add products to the storefront:

---

### Method 1 — Admin Dashboard (Recommended)

The built-in admin panel lets you publish products live to the storefront instantly, with no code editing required.

**Step 1 — Open the Admin Dashboard**

On any page of the site, press **Ctrl + Shift + Alt + A** on your keyboard to open the admin login gate.

**Step 2 — Log In**

Enter your admin username and password. Your credentials are stored in the `ADMIN_CREDS` object near the bottom of `index.html` (search for `ADMIN_CREDS`). The defaults shown in the code comments are:
- **Username:** `km_owner`
- **Password:** see `ADMIN_CREDS.passHash` comment in `index.html`

**Step 3 — Enter the 2FA Code**

After logging in you will be prompted for a 6-digit 2FA code. Use the backup code stored in `ADMIN_CREDS.totpBackupCode` inside `index.html`.

**Step 4 — Go to the Products Tab**

Inside the dashboard, click the **📦 Products** tab (it is selected by default).

**Step 5 — Fill in the Product Form**

| Field | Description | Example |
|-------|-------------|---------|
| **Product Name** | The display name of the product | `Sacred Moringa Blend` |
| **Category** | Choose the category from the dropdown | `🌿 Supplement / Herb` |
| **Price ($)** | Numeric price in USD | `29.99` |
| **Badge Label** | Optional short badge shown on the card | `New`, `Bestseller`, `Sale` |
| **Product Description** | A sentence or two describing the product | `Cold-pressed, full-spectrum moringa...` |
| **Product Image** | Click the upload area or drag-and-drop a JPG/PNG/WEBP (max 50 MB) | — |

**Step 6 — Publish**

Click **◆ Publish Product Live**. The product will appear on the storefront immediately. A green confirmation banner confirms it was published and saved to the database.

**Step 7 — Manage Existing Products**

The **Current Product Catalog** table below the form lists all products. From there you can:
- **Edit** a product (pre-fills the form with existing values)
- **Delete** a product (with a confirmation prompt)

---

### Method 2 — Direct Edit in `index.html`

Use this method to add a product permanently as a default/seed item (useful if the Railway/Supabase backend is not connected).

**Step 1 — Open `index.html`** in your code editor and search for:

```
const DB = {
  products: [
```

**Step 2 — Add a new product object** to the `products` array. Copy an existing entry as a template and change the values:

```js
{
  id: 9,                        // next available integer (one more than the current highest id)
  name: 'My New Product',       // display name
  cat: 'herb',                  // category key (see table below)
  price: '24.99',               // price as a string
  badge: 'New',                 // optional badge (leave '' for none)
  emoji: '🌿',                  // emoji shown when no image is set
  stock: 100,                   // starting stock count
  sales: 0                      // starting sales count
}
```

**Step 3 — Update `nextId.products`** (a few lines below) to one more than the highest `id` you used:

```js
nextId: { products: 10, leads: 1, reviews: 4 }
```

**Step 4 — Save the file** and push it to GitHub. GitHub Pages will redeploy automatically within a minute or two.

---

#### Category Keys

| Key | Label | Emoji |
|-----|-------|-------|
| `tea` | Sacred Teas | 🍵 |
| `tincture` | Tinctures | 🧪 |
| `herb` | Herbal Supplements | 🌿 |
| `merch` | KM Merch | 👕 |
| `care` | Lawn / Auto | 🌱 |
| `consult` | Consulting | 🧠 |
| `digital` | Digital | 💻 |
| `service` | Service | 🔧 |
| `other` | Other | 📦 |

> **Note:** Products added via Method 2 only appear until the site loads products from the Railway/Supabase database. If the backend is connected, use Method 1 to ensure products persist.

---

## Site Structure

```
index.html   — The entire website (single-file app)
CNAME        — Custom domain configuration (thekoshermoor.com)
README.md    — This guide
```

The site is hosted on **GitHub Pages** at [thekoshermoor.com](https://thekoshermoor.com).
