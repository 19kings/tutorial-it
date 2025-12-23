---
title: '[Mikrotik #4] Anti Lag! Cara Bagi Bandwidth Biar Game & YouTube Lancar'
description: 'Tutorial manajemen bandwidth Mikrotik menggunakan Simple Queue. Cara membatasi kecepatan download agar satu orang tidak menghabiskan koneksi internet.'
pubDate: 'Dec 26 2025'
tags: ['Mikrotik', 'Bandwidth', 'Tutorial']
---

Internet cepat itu percuma kalau tidak diatur.
Bayangkan Bli punya internet 20Mbps. Kalau ada satu orang download update Game (Steam/Mobile Legends) yang memakan 19Mbps, maka sisa 1Mbps diperebutkan satu kampung. Hasilnya? **LAG PARAH.**

Di Part 4 ini, kita akan belajar menjadi "Polisi Lalu Lintas" di router kita menggunakan fitur **Simple Queue**.

## 1. Konsep: Jangan Pelit, Tapi Adil
Tujuan kita bukan membuat internet jadi pelan, tapi memastikan **pemerataan**.
* Jaringan Admin/Pribadi: **Unlimited** (Prioritas).
* Jaringan Hotspot/Tamu: **Dilimit** (Misal max 3Mbps per orang).

## 2. Membuat Rule Limiter Sederhana
Kita akan membatasi agar Jaringan Hotspot (`10.5.50.0/24`) tidak bisa menyedot internet lebih dari 5Mbps total (contoh).

1. Masuk menu **Queues**.
2. Pastikan di tab **Simple Queues**.
3. Klik **Tambah (+)**.
4. **Name:** `Limit-Anak-Hotspot`.
5. **Target:** Isi IP Network Hotspot, misal `10.5.50.0/24`.
6. **Max Limit (Upload/Download):**
   * Upload: `1M`
   * Download: `5M` (Sesuaikan dengan paket internet Bli).
7. Klik **OK**.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/queue-add.jpg" 
        alt="Setting Simple Queue" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 1: Membatasi satu jaringan hotspot agar tidak mengganggu jaringan utama
    </figcaption>
</figure>

## 3. Prioritas Trafik (Parent Queue)
Bagaimana kalau kita mau limit **Per User** tapi juga ada **Limit Total**?
Di Part 3 (Hotspot) kita sudah bikin User Profile 2Mbps. Itu adalah limit per HP.
Tapi kalau ada 10 orang login, 10 x 2Mbps = 20Mbps. Internet jebol.

Solusinya adalah **Parent Queue**.
* Buat Queue Total (Seperti langkah no 2 di atas).
* Pastikan rule Hotspot Profile menginduk ke rule ini (Biasanya otomatis di Mikrotik modern).

## 4. Monitoring Trafik (Merah vs Hijau)
Ini cara taunya settingan kita berhasil atau tidak.
Coba konek ke WiFi Hotspot, lalu buka YouTube 4K atau Speedtest.

Lihat di Winbox menu Queues:
* **Hijau:** Pemakaian santai (0-50%).
* **Kuning:** Mulai padat (50-75%).
* **Merah:** Mentok limit (100%).

Kalau warnanya merah, berarti limiter bekerja! User tidak akan bisa narik bandwidth lebih dari yang ditentukan.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/queue-traffic.jpg" 
        alt="Indikator Trafik Queue" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 2: Kalau sudah merah, artinya polisi tidur bekerja menahan kecepatan
    </figcaption>
</figure>

## Kesimpulan
Dengan Simple Queue, Bli bisa tidur nyenyak. Tidak perlu takut lagi internet lemot gara-gara ada bocil download game bergiga-giga. Semua dapat jatah yang adil.

Trafik sudah rapi, sekarang saatnya kita **OTOMATISASI BISNIS**. Masak mau bikin voucher satu-satu terus? Capek dong.

👉 **Selanjutnya:** [Mikrotik #5: Cara Install Mikhmon & Cetak Ribuan Voucher (Final)](/blog/mikrotik-part-5)