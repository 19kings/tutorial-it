---
title: '[Mikrotik #3] Cara Setting Hotspot & Jualan Voucher (Auto Cuan)'
description: 'Panduan membuat sistem Hotspot Mikrotik lengkap dengan limit kecepatan (Bandwidth Management) dan pembuatan User Voucher siap jual.'
pubDate: 'Dec 25 2025'
heroImage: './mikrotik3.jpg'
tags: ['Mikrotik', 'Hotspot', 'Bisnis']
---
<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/mikrotik3.jpg" 
        alt="Setting Identity Mikrotik" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
    </figcaption>
</figure>

Sudah connect internet? (Part 1) ✅
Sudah aman? (Part 2) ✅

Sekarang saatnya kita bicara **BISNIS**. Fitur Hotspot di Mikrotik adalah alasan utama kenapa alat ini laku keras. Dengan fitur ini, Bli bisa memaksa orang login dulu sebelum bisa internetan, membatasi kecepatan biar gak lemot, dan tentu saja: **Jualan Voucher.**

Karena kita pakai **RB750r2** (yang gak ada WiFi-nya), pastikan Bli sudah mencolokkan kabel dari **Ether 3** ke **Access Point** (pemancar WiFi) eksternal.

## 1. Beri IP Address Khusus Hotspot
Jangan campur jaringan Admin (LAN) dengan jaringan Tamu (Hotspot). Kita pisah jalurnya.

1. Masuk menu **IP** > **Addresses**.
2. Klik **Tambah (+)**.
3. Address: `10.5.50.1/24` (IP ini bebas, yang penting beda sama LAN).
4. Interface: **ether3** (arah ke Access Point).
5. Klik **OK**.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/ip-hotspot.jpg" 
        alt="Setting IP Address untuk Hotspot" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 1: Membedakan jalur LAN dan Hotspot itu wajib
    </figcaption>
</figure>

## 2. Hotspot Setup Wizard (Jurus Satu Tombol)
Jangan setting manual satu-satu, pusing. Pakai Wizard saja.

1. Masuk menu **IP** > **Hotspot**.
2. Klik tombol **Hotspot Setup** (kotak abu-abu).
3. **Hotspot Interface:** Pilih `ether3`. Next.
4. **Local Address:** Otomatis terisi `10.5.50.1/24`. Next.
5. **Address Pool:** Biarkan default. Next.
6. **Certificate:** Pilih `none`. Next.
7. **SMTP Server:** `0.0.0.0` (biarkan). Next.
8. **DNS Servers:** Isi `8.8.8.8` dan `8.8.4.4`. Next.

### PENTING: DNS Name
Saat diminta **DNS Name**, isi dengan alamat login yang cantik. Jangan kosong!
* Contoh: `wifi.desaku.net` atau `login.net`.
* *Ingat alamat ini, karena ini yang akan diketik pelanggan di browser.*

9. **Create Local Hotspot User:** Isi user admin hotspot (buat cadangan). Next.
10. **Setup has completed successfully.** 🎉

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/hotspot-setup.jpg" 
        alt="Wizard Hotspot Mikrotik" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 2: Ikuti Wizard sampai muncul pesan Success
    </figcaption>
</figure>

## 3. Membuat Profil Paket (Limit Kecepatan)
Biar internet tidak disedot satu orang (Netcut), kita harus batasi kecepatannya.

1. Di menu **IP Hotspot**, pindah ke tab **User Profiles**.
2. Klik **Tambah (+)**.
3. **Name:** Misal `Paket-2Jam`.
4. **Rate Limit (rx/tx):** Isi `1M/2M` (Upload 1Mbps, Download 2Mbps).
5. **Shared Users:** `1` (Satu voucher cuma buat satu HP).
6. Klik **OK**.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/user-profile.jpg" 
        alt="Setting Rate Limit Bandwidth" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 3: Kunci anti lemot ada di kolom Rate Limit
    </figcaption>
</figure>

## 4. Membuat User Voucher (Cetak Uang)
Sekarang kita buat username dan password untuk dijual ke pelanggan.

1. Pindah ke tab **Users**.
2. Klik **Tambah (+)**.
3. **Server:** `all`.
4. **Name:** `tamu1` (ini username).
5. **Password:** `123` (ini password).
6. **Profile:** Pilih `Paket-2Jam` yang tadi dibuat.
7. Klik **OK**.

Sekarang, siapa saja yang login pakai `tamu1` akan otomatis kecepatannya dikunci di 2Mbps.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/user-hotspot.jpg" 
        alt="Membuat User Manual" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 4: User ini yang nanti dikasih ke pelanggan
    </figcaption>
</figure>

## 5. Uji Coba (Login Page)
1. Sambungkan HP Bli ke WiFi Access Point tadi.
2. Biasanya otomatis muncul "Sign in to network".
3. Kalau tidak muncul, buka browser ketik: `wifi.desaku.net` (sesuai DNS Name tadi).
4. Masukkan user `tamu1` dan pass `123`.
5. Kalau berhasil masuk Google, selamat! Sistem voucheran Bli sudah jalan.

---

### 💡 Tips Pro: "Capek Bikin Voucher Satu-Satu?"
Kalau pelanggannya ada 100, gempor jari kita kalau input manual pakai cara di atas.
Para pengusaha WiFi biasanya pakai alat bantu bernama **Mikhmon** (Mikrotik Monitor) untuk generate ribuan voucher sekali klik dan print struknya.

Tapi itu materi tingkat lanjut. Nikmati dulu keberhasilan setting dasar ini!

👉 **Selanjutnya:** [Mikrotik #4: Cara Bagi Bandwidth Biar Game & YouTube Lancar)](/blog/mikrotik-part-4)