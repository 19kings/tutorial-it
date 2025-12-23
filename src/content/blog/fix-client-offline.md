---
title: 'Mengatasi Error "Client is Offline" pada Firebase & Netlify'
description: 'Panduan lengkap memperbaiki masalah koneksi Firestore saat deploy ke Netlify.'
pubDate: 'Dec 09 2024'
heroImage: './firebase-client-offline-error.png'
tags: ['Firebase', 'Troubleshooting', 'Netlify']
---

Saat menghubungkan Astro dengan Firebase, seringkali semuanya berjalan lancar di `localhost`, tapi hancur saat di-deploy ke Netlify.

## Analisis Masalah

Biasanya error ini muncul di Console Browser (tekan F12) dengan tanda merah menyala.

> **Failed to get document because the client is offline.**

Penyebab utamanya bukan karena internet mati, melainkan **AdBlocker** atau **Salah Config**.