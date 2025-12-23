---
title: 'Cara Memperbaiki WiFi yang Tanda Seru (!)'
description: 'Panduan langkah demi langkah mengatasi No Internet Access.'
pubDate: 'Jul 08 2024'
heroImage: './wifi.jpg'
---

## Masalah
Seringkali ikon WiFi terhubung tapi ada tanda seru kuning. Ini artinya koneksi ke router aman, tapi router tidak bisa bicara ke internet.

## Solusi Teknis (DNS Flush)

Sebagai teknisi, langkah pertama adalah membersihkan cache DNS. Buka CMD sebagai Admin dan ketik:

```bash
ipconfig /flushdns
ipconfig /release
ipconfig /renew