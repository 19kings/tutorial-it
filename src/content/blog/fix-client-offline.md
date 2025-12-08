---
title: 'Mengatasi Error "Client is Offline" pada Firebase & Netlify'
description: 'Panduan lengkap memperbaiki masalah koneksi Firestore saat deploy ke Netlify. Solusi untuk error permission dan environment variables.'
pubDate: 'Dec 09 2024'
heroImage: './firebase-client-offline-error.png'
---

Saat menghubungkan Astro dengan Firebase, seringkali semuanya berjalan lancar di `localhost`, tapi hancur saat di-deploy ke Netlify. Salah satu error paling menyebalkan adalah:

> **Failed to get document because the client is offline.**

Artikel ini akan membedah penyebab dan solusinya berdasarkan pengalaman debug real-time.

## Analisis Masalah

Biasanya error ini muncul di Console Browser (tekan F12) dengan tanda merah menyala.


*Gambar: Pesan error yang muncul di Console Chrome.*

Penyebab utamanya bukan karena internet mati, melainkan:
1.  **AdBlocker:** Extension browser memblokir script Google.
2.  **Environment Variables:** Salah konfigurasi antara Local dan Server.
3.  **Security Rules:** Database masih terkunci.

## Solusi 1: Cek Environment Variables (Paling Fatal)

Ini kesalahan pemula yang sering terjadi. Kita update file `.env` di laptop, tapi lupa update di Netlify.

**Di Laptop (Local):**
File `.env` bisa dibaca langsung.

**Di Netlify (Server):**
Anda WAJIB memasukkan ulang variabel tersebut di menu:
`Site Configuration` > `Environment Variables`.

Pastikan **Project ID** sama persis:
```ini
PUBLIC_FIREBASE_PROJECT_ID=web-it-dfa3a