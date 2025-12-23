---
title: '[Mikrotik #1] Cara Setting Mikrotik dari Nol sampai Konek Internet'
description: 'Tutorial dasar Mikrotik Part 1: Konfigurasi Basic Internet Gateway. Langkah demi langkah untuk pemula agar router bisa online.'
pubDate: 'Dec 23 2025'
heroImage: './mikrotik1.jpg'
tags: ['Mikrotik', 'Tutorial', 'Basic']
---
<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/mikrotik1.jpg" 
        alt="Setting Identity Mikrotik" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
    </figcaption>
</figure>

Selamat datang di seri **"Mikrotik Zero to Hero"**.
Di seri pertama ini, kita tidak akan membahas hal rumit dulu. Target kita sederhana: **Bagaimana caranya router Mikrotik ini bisa menerima internet dari modem ISP, lalu menyebarkannya ke laptop/HP kita.**

Tanpa basa-basi, mari kita buka Winbox!

## 1. Beri Nama Router (Identity)
Hal pertama yang wajib dilakukan seorang profesional adalah memberi nama perangkat. Jangan biarkan namanya default "MikroTik", nanti bingung kalau punya banyak router.

1. Masuk menu **System** > **Identity**.
2. Ubah namanya, misal: `Router-Utama` atau `Mikrotik-Bli`.
3. Klik **OK**.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/identity.jpg" 
        alt="Setting Identity Mikrotik" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 1: Memberi Identitas Router
    </figcaption>
</figure>

## 2. Setting IP Address Lokal (LAN)
Kita tentukan alamat gerbang (Gateway) untuk jaringan lokal kita.
Biasanya Port 1 untuk Internet (ISP), dan Port 2 untuk Laptop/Lokal.

1. Masuk menu **IP** > **Addresses**.
2. Klik tanda **Tambah (+)**.
3. Masukkan Address: `192.168.10.1/24` (Bisa diganti sesuai selera).
4. Interface: Pilih **ether2** (Jalur ke Laptop/Hub).
5. Klik **OK**.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/address1.jpg" 
        alt="Setting IP Address LAN" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 2: Mengatur IP Lokal di Ether2
    </figcaption>
</figure>

## 3. Minta Internet ke ISP (DHCP Client)
Agar Mikrotik dapat internet dari modem (Indihome/Biznet) secara otomatis tanpa ribet setting IP WAN manual.

1. Masuk menu **IP** > **DHCP Client**.
2. Klik tanda **Tambah (+)**.
3. Interface: Pilih **ether1** (Jalur colokan modem).
4. Pastikan *Use Peer DNS* dan *Use Peer NTP* tercentang.
5. Klik **OK**. Tunggu sampai statusnya **"Bound"**.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/dhcp.jpg" 
        alt="Setting DHCP Client" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 3: Status Bound artinya sudah dapat internet
    </figcaption>
</figure>

## 4. Buka Gerbang Internet (Firewall NAT)
Ini langkah paling krusial! Tanpa ini, laptop Bli tidak akan bisa browsing meski router sudah konek. Kita perlu mengaktifkan *Masquerade*.

1. Masuk menu **IP** > **Firewall** > Tab **NAT**.
2. Klik tanda **Tambah (+)**.
3. **Tab General:** Chain = `srcnat`, Out. Interface = `ether1`.
4. **Tab Action:** Action = `masquerade`.
5. Klik **OK**.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/nat.jpg" 
        alt="Setting Firewall NAT" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 4: Teknik Masquerade agar klien bisa browsing
    </figcaption>
</figure>

## 5. Bagikan IP ke Klien (DHCP Server)
Biar laptop atau HP yang connect tidak perlu isi IP manual (Static), kita buat server DHCP otomatis.

1. Masuk menu **IP** > **DHCP Server**.
2. Klik tombol **DHCP Setup** (Jangan klik tambah, pakai Setup biar gampang).
3. Pilih Interface: **ether2**.
4. Klik **Next** Terus sampai sukses (Selesai).

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/dhcp-server.jpg" 
        alt="DHCP Setup Wizard" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 5: Wizard DHCP Server yang memudahkan hidup
    </figcaption>
</figure>

## 6. Pengujian (Testing)
Sekarang cabut kabel LAN di laptop, lalu colok lagi (biar request IP baru).
Buka **New Terminal** di Winbox, lalu ketik: **ping google.com**
<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/ping-google.jpg" 
        alt="DHCP Setup Wizard" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 5: Test Ping google.com
    </figcaption>
</figure>

## 🎉 Misi Selesai: Router Sudah Online!

Selamat! Kalau ping ke `google.com` sudah **Reply**, berarti Mikrotik Bli sudah resmi berfungsi sebagai **Gateway Internet**. Sekarang semua laptop atau HP yang colok ke Mikrotik sudah bisa browsing, YouTube-an, dan download sepuasnya.

**TAPI TUNGGU DULU... ⚠️**

Router ini ibarat rumah baru yang **belum ada kuncinya**.
Secara fungsi memang jalan, tapi secara keamanan masih **NOL**. Siapapun bisa iseng masuk ke Winbox Bli, ganti password, atau malah mematikan internet satu kantor. Bahaya, kan?

Jangan buru-buru dipasang di tempat klien dulu. Kita harus mengamankannya di **Part 2**.

---

### 📚 Lanjut ke Materi Berikutnya?
Di tutorial selanjutnya, kita akan belajar teknik *Security Hardening* agar router Bli kebal dari serangan hacker pemula dan tetangga yang iseng.

👉 **Selanjutnya:** [Mikrotik #2: Dasar Keamanan Router & Firewall (Wajib Baca!)](/blog/mikrotik-part-2)

---
*Punya kendala atau error saat ping? Tulis di kolom komentar atau DM saya di Instagram. Salam IT Expert!* 💻🔥