---
title: 'Cara Setting Mikrotik (RB750r2) Untuk Usaha WiFi Voucheran'
description: 'Panduan lengkap konfigurasi dasar Mikrotik untuk usaha WiFi voucheran. Langkah demi langkah dengan Winbox.'
pubDate: 'Dec 21 2025'
heroImage: './mikrotik.jpg'
tags: ['Mikrotik', 'Jaringan', 'Tutorial']
---

Apakah Bli berencana membuka usaha WiFi atau RT/RW Net? Kunci utamanya ada di **Mikrotik**.
Banyak pemula takut karena melihat ribuan menu di Winbox. Padahal, untuk membuat sistem voucheran sederhana, caranya cukup mudah.

Di tutorial ini, saya akan memandu Bli melakukan *Basic Configuration* pada **Mikrotik RB750r2 (Hex Lite)**, seri sejuta umat yang murah meriah.

<figure style="text-align: center; margin: 1.5rem 0;">
    <img 
        src="/topologi.jpg" 
        alt="Topologi Jaringan" 
        style="background: white; padding: 10px; border-radius: 8px; width: 100%; max-width: 550px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 1: Topologi Sederhana untuk Pemula
    </figcaption>
</figure>

## 🛠️ Persiapan Alat
Sebelum mulai, pastikan Bli sudah punya:
1.  **Mikrotik RB750r2** (Atau tipe apa saja). 
2.  Kabel LAN (RJ45).
3.  Laptop dengan aplikasi **Winbox**.
4.  Koneksi Internet (ISP) dari modem utama.

## 1. Topologi Kabel
Jangan sampai salah colok! Ini urutan standarnya:
1. **Port 1 (Internet):** Colok kabel dari Modem ISP (Indihome/Biznet).
2. **Port 2 (LAN):** Colok kabel ke Laptop Bli (untuk setting).
3. **Port 3-5 (Hotspot):** Nanti dicolok ke Access Point (pemancar WiFi).

## 2. Reset Konfigurasi (Wajib!)
Biar bersih dari settingan pabrik, kita reset dulu:
1. Buka Winbox, login dengan MAC Address.
2. Masuk menu **System** > **Reset Configuration**.
3. Centang *No Default Configuration*.
4. Klik **Reset**. Tunggu sampai bunyi *bip*.

## 3. Memberi IP Address
Kita harus membedakan jalur Internet (WAN) dan jalur Lokal (LAN).
1. Masuk menu **IP** > **Addresses**.
2. Klik tanda **Tambah (+)**.
3. Isi IP Untuk Internet: `192.168.1.6/24` arahkan ke interface **ether1**.

<figure style="text-align: left; margin: 1.5rem 0;">
    <img 
        src="/address.jpg" 
        alt="Setting IP Address" 
        style="background: white; padding: 10px; border-radius: 8px; width: 100%; max-width: 400px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
</figure>

4. Isi IP Lokal:  `192.168.50.1/24` arahkan ke interface **ether2**.

<figure style="text-align: left; margin: 1.5rem 0;">
    <img 
        src="/address1.jpg" 
        alt="Setting IP Address" 
        style="background: white; padding: 10px; border-radius: 8px; width: 100%; max-width: 400px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
</figure>

## 4. Setting DHCP Client (Internet Masuk)
Supaya Mikrotik dapat internet dari modem ISP secara otomatis:
1. Masuk menu **IP** > **DHCP Client**.
2. Klik **(+)**, pilih interface **ether1**.
3. Klik OK. Pastikan statusnya *Bound*.

<figure style="text-align: left; margin: 1.5rem 0;">
    <img 
        src="/dhcp.jpg" 
        alt="Setting DHCP Client" 
        style="background: white; padding: 10px; border-radius: 8px; width: 100%; max-width: 400px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 3: Request Internet Otomatis
    </figcaption>
</figure>

## 5. Setting Hotspot Setup (Wizard)
Ini bagian paling ajaib. Mikrotik punya fitur *Wizard* yang gampang banget.
1. Masuk menu **IP** > **Hotspot**.
2. Klik tombol **Hotspot Setup**.
3. Pilih interface yang mau dijadikan Hotspot (misal: **ether3**).
4. Klik **Next** terus sampai diminta DNS Name.
5. Isi DNS Name: `wifi.desaku.net` (ini alamat login page nanti).
6. Buat user admin & password. Selesai!

> **Tips Ahli:** Jangan lupa setting DNS Google (8.8.8.8) di menu IP > DNS dan centang "Allow Remote Requests" agar internet ngebut.

## Kesimpulan
Sekarang, coba konek HP ke Access Point yang terhubung ke Mikrotik. Saat buka browser, Bli akan diarahkan ke halaman login. Selamat, sistem voucheran Bli sudah jadi!

Masih bingung atau mau terima beres?
**Hubungi Saya untuk Jasa Setting Mikrotik area Bali:**
👉 [Link WhatsApp Bli]