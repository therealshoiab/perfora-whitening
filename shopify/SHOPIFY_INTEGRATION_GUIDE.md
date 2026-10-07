# 🛍️ Connecting Perfora Whitening Store to Your Shopify Store

This guide explains how to import the **Perfora Purple Whitening Store** landing page directly into your Shopify store as a custom standalone page template so you can manage orders, inventory, payments (UPI, Cards, COD), and shipping through Shopify Admin.

---

## ⚡ Quick 3-Step Setup

### Step 1: Add the Custom Template in Shopify

1. In your **Shopify Admin**, go to **Online Store** → **Themes**.
2. Next to your current active theme (e.g. Dawn), click the three dots **`...`** and select **Edit code**.
3. In the left sidebar under the **Templates** folder, click **Add a new template**.
4. Configure the pop-up:
   - **Template type**: select `page`
   - **File name**: enter `perfora` (Shopify will name it `page.perfora.liquid`)
5. Open [`shopify/page.perfora.liquid`](file:///c:/Users/Baha/Documents/PerforaPerfume/shopify/page.perfora.liquid).
6. Copy its entire contents, paste it into the new Shopify template file (replacing any default starter code), and click **Save** (top right).

> **Why this works seamlessly**: The template starts with `{% layout none %}`. This prevents your Shopify theme's default header and footer from cluttering the custom design, rendering the landing page 100% full-screen exactly as designed.

---

### Step 2: Create the Landing Page in Shopify

1. In your Shopify Admin, go to **Online Store** → **Pages**.
2. Click **Add page** (top right).
3. Set the **Title**: `Perfora Purple Whitening Toothpaste` (or any title you prefer).
4. On the right-side panel under **Theme template**, click the dropdown and select **`perfora`**.
5. Set Visibility to **Visible** and click **Save**.
6. Click **View page** to see your live landing page on your Shopify store URL (e.g. `https://your-store.myshopify.com/pages/perfora-purple-whitening-toothpaste`)!

---

### Step 3: Link Your Products & Variant IDs

To ensure that clicking **"Proceed to Checkout"** adds the exact product to Shopify's cart and native checkout:

#### Method A: Automatic Matching via Product Handles (Easiest)
When creating or editing the products in Shopify Admin, set their URL handles (**Search engine listing** → **Edit** → **URL handle**) to match:

| # | Product Name | Shopify URL Handle |
|---|---|---|
| **0** | Perfora Purple Whitening Toothpaste, 75 g | `perfora-purple-whitening-toothpaste` |
| **1** | Perfora Activated Charcoal Whitening Toothpaste, 100 g | `perfora-activated-charcoal-whitening-toothpaste` |
| **2** | Perfora Teeth Whitening Combo (2 Brushes + Charcoal Paste) | `perfora-teeth-whitening-combo` |
| **3** | Perfora Teeth Whitening Strips (6 Strips) | `perfora-teeth-whitening-strips` |
| **4** | Perfora Purple Teeth Whitening Strips (6 Strips) | `perfora-purple-teeth-whitening-strips` |
| **5** | Perfora Purple Teeth Whitening Toothpaste Serum, 30 ml | `perfora-purple-teeth-whitening-toothpaste-serum` |

The Liquid template will automatically query these handles and populate the variant IDs!

#### Method B: Direct Variant ID Mapping
If your products already exist with different names/handles:
1. Open each product in **Shopify Admin** → **Products**.
2. Click on the variant (or inspect the URL in your browser bar: the number at the very end of `.../variants/XXXXXXXXXXXXXX` is your **Variant ID**).
3. In `page.perfora.liquid`, find the `SHOPIFY_VARIANTS` object (around line 10) and paste the numbers:
```javascript
var SHOPIFY_VARIANTS = {
  0: "48123456789012", // 1. Perfora Purple Whitening Toothpaste, 75 g
  1: "48123456789013", // 2. Perfora Activated Charcoal Toothpaste
  2: "48123456789014", // 3. Whitening Combo
  3: "48123456789015", // 4. Whitening Strips
  4: "48123456789016", // 5. Purple Strips
  5: "48123456789017"  // 6. Whitening Serum
};
```
4. Click **Save**.

---

## 🛒 How Checkout & Sales Work

1. **Shopify Native Checkout**:
   - When a visitor adds items and clicks **"Proceed to Checkout"**, they are taken directly into Shopify's secure checkout page.
   - Shopify automatically handles customer contact info, delivery address, shipping rates, and payment methods (Razorpay, Cashfree, PhonePe, Paytm, UPI, Cards, NetBanking, and Cash on Delivery).
   - Every completed order instantly appears in your **Shopify Admin** → **Orders** tab for fulfillment.

2. **Dual Checkout (WhatsApp Backup)**:
   - The cart drawer includes a secondary **"Order via WhatsApp"** button.
   - Customers who prefer personal chat support can toggle this option to send their order details directly to your WhatsApp number.

---

## 🏠 (Optional) Set As Your Main Homepage

If you want this landing page to serve as the front page of your Shopify store (`https://yourstore.com/`):
1. In Shopify Admin, go to **Online Store** → **Navigation**.
2. Under Main menu / footer, link to the new page.
3. Or in **Themes** → **Customize**, replace the index layout with a custom Liquid section targeting `page.perfora`.
