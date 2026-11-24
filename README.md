# 🌾 Krishi Farm

A farm-to-table website for **Krishi Farm, Sherpur, Haridwar, Uttarakhand**. Customers can browse 10 fresh vegetables, choose a weight, add them to a cart, and send their order to the farm on WhatsApp. Payment is by UPI or Cash on Delivery.

> *"Jay Jawan Jay Kisan"*

---

## Features

- **Home / Hero:** farm logo, a quote and a "Shop Now" button.
- **Products:** 10 vegetables with price per kg and a weight selector (0.5, 1, 2, 3, 5 kg). The price updates live.
- **Cart:** saved in the browser (`localStorage`), so it survives a page refresh.
- **Checkout:** name, 10-digit phone and delivery address are validated.
- **Payments:**
  - **UPI:** opens GPay, PhonePe or Paytm with the amount filled in, and shows a QR code. The customer then enters the 12-digit UTR.
  - **Cash on Delivery.**
- **WhatsApp ordering:** the finished order is sent to the farm's WhatsApp number as a formatted message.
- **Sign In / Sign Up:** email and password accounts using Supabase.
- **🌾 Our Story button** (top-left, beside the logo) opens a panel with:
  - the owner's name (Parteek Saini),
  - 26+ years of farming,
  - customer reviews with ratings,
  - a step-by-step guide for each vegetable: ploughing → sowing → irrigation → growth → harvest.
- **Gallery, About and Contact** sections, with a Google Maps link.
- **UI:** glass-style design, scroll animations, a preloader and a mobile menu.

## Vegetables

Tomato · Potato · Onion · Carrot · Brinjal · Green Chilli · Cucumber · Cabbage · Spinach · Sweet Corn

## Tech Stack

| Purpose | Tool |
|---|---|
| Pages | HTML, CSS, vanilla JavaScript |
| Styling | [Tailwind CSS](https://tailwindcss.com) (CDN) |
| Authentication | [Supabase](https://supabase.com) (`supabase-js` v2 from CDN) |
| UPI QR code | [qrcodejs](https://github.com/davidshimjs/qrcodejs) |
| Font | Google Fonts, Dancing Script |

There is **no build step and no backend**. Everything is static files.

## Project Structure

```
.
├── index.html      # Main website (home, products, gallery, about, contact, cart, auth, Our Story)
├── shop.html       # Stand-alone shop page with its own cart and checkout
├── README.md
└── pic/
    ├── Gemini-logo.png          # Farm logo
    ├── fram1.jpg … fram6.jpg    # Gallery photos (names as used in the code)
    └── farm2.jpg, farm3.jpg
```

> Create the `pic/` folder yourself and add your images. If an image is missing, the logo and gallery photo are hidden automatically and the page still works.
> `.heic` photos do not display in browsers. Convert them to `.jpg` first.

## Getting Started

1. Put `index.html`, `shop.html` and the `pic/` folder in one directory.
2. Open `index.html` in a browser. Or serve the folder locally:
   ```bash
   python3 -m http.server 8000
   # then visit http://localhost:8000
   ```
3. An internet connection is needed for the CDN scripts, fonts, QR library and Supabase.

## Configuration

Most settings are constants in the `<script>` section of `index.html`. Search for the name to find it.

| Constant | What it does |
|---|---|
| `OWNER_NAME` | Owner name in the Our Story panel (currently `Parteek Saini`). |
| `FARM_SINCE` | Start year, calculated as the current year minus 26. Change the `26` to update it. |
| `REVIEWS` | Customer reviews: `name`, `place`, `rating` (1–5), `text`. **The reviews included are samples, so replace them with real ones.** |
| `GROWING` | Season, days to harvest and the 5 growing steps for each vegetable. |
| `PRODUCTS` | Vegetable names, emojis and price per kg (in ₹). |
| `WEIGHTS` | Weight options in the dropdown. |
| `UPI_ID` | **Required for online payment.** Set it to the farm's real UPI ID (e.g. `name@bank`). While it is still `YOUR_UPI_ID@bank`, online payment is blocked and only Cash on Delivery works. |
| `UPI_NAME` | Name shown in the UPI app. |
| `WA_NUMBER` | WhatsApp number that receives orders, with country code and no `+` (e.g. `917088205958`). |
| `SUPABASE_URL`, `SUPABASE_ANON_KEY` | Your Supabase project's URL and **anon public** key (Project Settings → API). |

`shop.html` has its own copy of the cart and payment settings. Update both files if you change prices or payment details.

### Setting up Supabase

1. Create a project at [supabase.com](https://supabase.com).
2. Copy the **Project URL** and the **anon public** key into `index.html`.
3. In **Authentication → Providers**, enable **Email**.
4. Decide whether to require email confirmation. If it is on, new users must confirm by email before they can sign in.
5. Add your site's address under **Authentication → URL Configuration**.

> ⚠️ Only use the **anon** key in front-end code. Never put the `service_role` key in this project.

## How an Order Works

1. The customer picks vegetables and weights and adds them to the cart.
2. In the cart they enter name, phone and address, then choose a payment method.
3. **COD:** a WhatsApp message with the order is sent to the farm right away.
4. **UPI:** the customer pays through their UPI app, enters the UTR, and then the order is sent on WhatsApp.
5. The farm checks the UTR in its UPI app and confirms the order on WhatsApp.

> Payments are **not verified automatically**. The farm must confirm each UTR manually before dispatch.

## Customising Content

- **Prices or vegetables:** edit `PRODUCTS` in `index.html`. If you add a vegetable, add a matching entry (same `id`) to `GROWING` so it appears in Our Story.
- **Farm text and contact details:** edit the About and Contact sections in the HTML.
- **Colours and background:** change the Tailwind classes and the `body::before` rule in the `<style>` block.

## Deployment

The site is fully static, so any static host works, such as GitHub Pages, Netlify, Vercel or Cloudflare Pages. Upload the files (including `pic/`) and set the Supabase redirect URL to your live address.

## Contact

**Krishi Farm**
📍 Sherpur, Haridwar, Uttarakhand 247663
📞 +91 7088205958
✉️ shivkrishif@gmail.com

---

© Krishi Farm, Sherpur, Haridwar. All rights reserved.
