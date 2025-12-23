---
title: '[Mikrotik #5] Ternak Uang Otomatis: Cara Install Mikhmon & Cetak Voucher'
description: 'Tutorial lengkap instalasi Mikhmon untuk manajemen Hotspot. Generate ratusan voucher sekali klik, print struk, dan laporan keuangan otomatis.'
pubDate: 'Dec 27 2025'
tags: ['Mikrotik', 'Mikhmon', 'Bisnis']
---

Ini adalah **FINAL BOSS** dari seri Mikrotik Zero to Hero.
Kalau Bli sudah sampai di tahap ini, selamat! Bli sudah siap menjadi juragan WiFi sesungguhnya.

Kita akan menggunakan **Mikhmon (Mikrotik Monitor)**. Aplikasi gratis buatan anak bangsa (Laksamadi Ganco) yang mendunia. Fungsinya untuk membuat ribuan voucher, mengatur harga, dan melihat laporan penghasilan harian.

## 1. Persiapan di Mikrotik (Wajib!)
Sebelum install aplikasinya, router harus disiapkan dulu.

1. **Hidupkan API:** Masuk *IP* > *Services*. Pastikan service **api** (port 8728) aktif/hijau.
2. **Setting Jam (PENTING):** Voucher ada masa aktifnya (misal 3 jam). Kalau jam di router ngaco (tahun 1970), voucher akan error.
   * Masuk *System* > *SNTP Client*.
   * Centang **Enabled**.
   * Primary NTP: `id.pool.ntp.org`.
   * Klik OK. Pastikan jam di *System > Clock* sudah sesuai WIB/WITA.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/api-ntp.jpg" 
        alt="Persiapan API dan NTP Client" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 1: Wajib aktifkan API dan sinkronisasi jam
    </figcaption>
</figure>

## 2. Download & Jalankan Mikhmon
Kita pakai versi PC/Laptop biar gampang.
1. Download Mikhmon v3 di website resminya (laksa19.github.io).
2. Extract file ZIP-nya.
3. Klik 2x **MikhmonServer.exe**.
4. Klik tombol **Open Mikhmon**. Browser akan terbuka.
5. Login default -> User: `mikhmon`, Password: `1234`.

## 3. Sambungkan Mikhmon ke Mikrotik
1. Di dashboard Mikhmon, klik menu (garis tiga) > **Add Router**.
2. **Session Name:** `WiFi-Bli` (Bebas).
3. **IP Mikrotik:** Masukkan IP Gateway Hotspot (`10.5.50.1`).
4. **Username & Password:** Isi user admin Mikrotik Bli.
5. **Hotspot Name:** `WiFi Kencang Jaya` (Nama di struk).
6. **DNS Name:** `wifi.desaku.net` (Harus sama persis dengan settingan Part 3).
7. Klik **Save**, lalu klik **Connect**.
8. Kalau sukses, statusnya akan jadi **Online** (Hijau).

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/mikhmon-connect.jpg" 
        alt="Menghubungkan Mikhmon ke Router" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 2: Jika ping OK, berarti Mikhmon sudah terhubung
    </figcaption>
</figure>

## 4. Bikin Profil Harga (Jualan)
1. Masuk menu **Hotspot** > **User Profile** > **Add Profile**.
2. **Name:** `3Jam-3Ribu`.
3. **Rate Limit:** `1M/3M` (Up/Down).
4. **Expired Mode:** `Remove` & `Record`.
5. **Validity:** `3h` (Masa aktif 3 jam).
6. **Price / Selling Price:** `3000`.
7. **Lock User:** `Enable` (Biar 1 kode gak dipake rame-rame).
8. Klik **Save**.

## 5. Generate Voucher (Cetak Duit)
Ini momen ajaibnya.
1. Masuk menu **Hotspot** > **Users** > **Generate**.
2. **Qty:** `50` (Mau bikin berapa biji?).
3. **Server:** `all`.
4. **User Mode:** `Username = Password` (Biar pembaca gak ribet ngetik).
5. **Profile:** Pilih `3Jam-3Ribu`.
6. Klik **Generate**.
7. Klik **Print**.

Tadaaa! 🎉 50 kode voucher sudah jadi rapi siap digunting dan dijual.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/voucher-print.jpg" 
        alt="Hasil Cetak Voucher Mikhmon" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 3: Voucher siap jual. Tinggal gunting dan tunggu pembeli.
    </figcaption>
</figure>

## 🏁 Penutup Seri Zero to Hero
Luar biasa! Bli sudah menyelesaikan 5 tahap transformasi:
1.  **Konek Internet** (Dasar).
2.  **Aman dari Hacker** (Security).
3.  **Setting Hotspot** (Sistem).
4.  **Manajemen Bandwidth** (Kualitas).
5.  **Cetak Voucher Otomatis** (Bisnis).

Sekarang, router Mikrotik Bli bukan lagi sekadar alat elektronik, tapi sudah menjadi **Mesin Aset** yang menghasilkan uang.

Terima kasih sudah mengikuti seri ini. Sampai jumpa di tutorial "Season 2" yang lebih canggih!
*Salam IT Expert!* 🚀🔥