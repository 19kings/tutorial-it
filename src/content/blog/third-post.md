---
title: 'Cara Agar bisa menjadi IT PRO'
description: 'Panduan langkah demi langkah mengatasi No Internet Access.'
pubDate: 'Jul 08 2024'
---

## Masalah
Seringkali ikon WiFi terhubung tapi ada tanda seru kuning. Ini artinya koneksi ke router aman, tapi router tidak bisa bicara ke internet.

## Solusi Teknis (DNS Flush)

Sebagai teknisi, langkah pertama adalah membersihkan cache DNS. Buka CMD sebagai Admin dan ketik:

```bash
ipconfig /flushdns
ipconfig /release
ipconfig /renew