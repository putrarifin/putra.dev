---
layout: post
title: "Setup Cloudflare Zero Trust + WARP untuk Tim Kecil 🔐"
date: 2026-02-22 09:10:00 +0700
categories: cloudflare
emoticon: 🔐
---

Belakangan ini saya lagi sering pakai `Cloudflare Zero Trust` buat ngamanin akses internal tools (misalnya staging dashboard, admin panel, atau service internal lain) tanpa harus buka port publik sembarangan.

Yang saya suka: setup-nya relatif cepat, dan buat tim kecil cukup banget buat jadi lapisan security tambahan.

##### 1. Buat organisasi Zero Trust

- Masuk ke Cloudflare Dashboard
- Buka menu `Zero Trust`
- Pilih nama tim/organisasi
- Pilih login method (Google, GitHub, email OTP, dsb)

Setelah ini, kamu udah punya “gerbang” auth sebelum user bisa akses resource internal.

##### 2. Install WARP client di device

Install `Cloudflare WARP` di laptop/PC yang mau dipakai akses.

Contoh di macOS (pakai brew):
```bash
brew install --cask cloudflare-warp
```

Setelah install:
- Login pakai account yang sudah diizinkan di Zero Trust
- Pastikan status koneksi `Connected`

##### 3. Daftarkan aplikasi internal

Di menu `Access` → `Applications`:
- Tambah aplikasi baru
- Pilih domain/subdomain target (contoh: `staging.putra.dev`)
- Atur policy siapa saja yang boleh akses

Contoh policy paling basic:
- `Include`: email dengan domain kantor
- `Require`: MFA aktif

Dengan ini, URL internal kamu tetap bisa diakses normal, tapi wajib lolos auth policy dulu.

##### 4. Tips policy biar nggak terlalu longgar

Beberapa kebiasaan yang saya pakai:
- Pisahkan app `staging` dan `production` (jangan disatuin policy)
- Wajibkan MFA untuk role sensitif
- Pakai `session duration` yang pendek untuk dashboard admin
- Audit login log seminggu sekali

##### 5. Validasi cepat setelah setup

Coba cek dari device yang tidak login WARP. Harusnya akses ditolak / diminta login lewat Access.

Kalau mau cek DNS/routing dasar dari terminal:
```bash
curl -I https://staging.putra.dev
```

Kalau konfigurasi benar, biasanya akan kelihatan response yang melewati proteksi Access/Cloudflare.

<hr>

Buat saya, kombinasi `Zero Trust + WARP` ini cocok banget kalau kamu belum siap maintain VPN sendiri tapi tetap pengen internal tools lebih aman.

Sekian!
