---
layout: post
title: "Deploy Static Site ke Cloudflare Pages + Custom Domain 🚀"
date: 2026-02-22 09:35:00 +0700
categories: cloudflare
emoticon: 🚀
---

Kalau kamu punya static web (Jekyll, Astro, Vite, bahkan HTML biasa), `Cloudflare Pages` itu salah satu opsi deploy paling enak yang pernah saya pakai.

Flow-nya simpel: connect repo, set build command, publish. Done.

##### 1. Push project ke GitHub

Pastikan project kamu udah ada di GitHub dan branch utama jelas (`main` / `master`).

##### 2. Connect ke Cloudflare Pages

- Buka Cloudflare Dashboard
- Masuk ke `Workers & Pages`
- Klik `Create application` → `Pages`
- Connect repository GitHub

Pilih repo yang mau di-deploy.

##### 3. Isi konfigurasi build

Untuk project Jekyll basic, kurang lebih bisa seperti ini:

- Build command:
```bash
bundle exec jekyll build
```

- Output directory:
```bash
_site
```

Kalau framework lain, tinggal sesuaikan command dan output foldernya.

##### 4. Pasang custom domain

Setelah deploy sukses:
- Buka project Pages kamu
- Masuk ke tab `Custom domains`
- Tambah domain, misalnya: `putra.dev`

Cloudflare biasanya otomatis bantu setting DNS record yang dibutuhkan.

##### 5. Redirect www -> apex (opsional tapi saya sarankan)

Biar URL konsisten, saya biasanya pakai redirect rule:
- dari `www.putra.dev/*`
- ke `https://putra.dev/$1`
- status `301`

##### 6. Cek cepat hasil deploy

```bash
curl -I https://putra.dev
curl -I https://www.putra.dev
```

Harusnya:
- domain utama balik `200`
- domain `www` kena redirect `301` ke domain utama (kalau kamu aktifkan rule redirect)

<hr>

Yang saya suka dari Pages: preview per-PR, deploy cepat, dan setup SSL otomatis. Buat blog/personal site, ini udah lebih dari cukup.

Sekian!
