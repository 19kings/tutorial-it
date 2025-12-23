---
title: '[Mikrotik #2] Jangan Sampai Di-Hack! Cara Mengamankan Router Mikrotik'
description: 'Panduan keamanan dasar (Basic Security) Mikrotik. Wajib dilakukan sebelum router dipasang di tempat klien agar tidak dijebol hacker.'
pubDate: 'Dec 24 2025'
heroImage: './mikrotik2.jpg'
tags: ['Mikrotik', 'Security', 'Tutorial']
---
<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/mikrotik2.jpg" 
        alt="Setting Identity Mikrotik" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
    </figcaption>
</figure>

Di **[Part 1](/blog/cara-setting-mikrotik-internet-gateway)**, kita sudah berhasil membuat router online. Senang? Boleh. Puas? Jangan dulu.

Router yang baru keluar dari kardus (default) itu ibarat rumah kaca tanpa kunci. Siapapun yang tahu IP router Bli bisa masuk, mengacak-acak settingan, atau mencuri voucher hotspot.

Di tutorial ini, kita akan melakukan ritual **"Security Hardening"** alias mempertebal pertahanan router. Hukumnya **WAJIB**, bukan sunnah!

## 1. Ganti Password & Disable User Admin
Kesalahan pemula nomor 1: Membiarkan user default `admin` tanpa password. Ini sasaran empuk *brute force attack*.

Strategi terbaik bukan cuma ganti password, tapi **membuat user baru** dan **mematikan user lama**.

1. Masuk menu **System** > **Users**.
2. Klik **Tambah (+)**.
3. Buat user baru (misal: `bli-super`), Group: **full**, Password: (yang rumit).
4. Login ulang pakai user baru.
5. Disable (silang) user `admin` bawaan.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/user-list.jpg" 
        alt="Daftar User Mikrotik" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 1: Buat user baru, matikan user admin lama
    </figcaption>
</figure>

## 2. Matikan Service yang Tidak Perlu
Mikrotik secara default membuka banyak "pintu" (Port) seperti Telnet, FTP, WWW, SSH. Padahal kita cuma butuh **Winbox**. Pintu yang tidak dijaga adalah celah masuk hacker.

1. Masuk menu **IP** > **Services**.
2. Pilih service yang tidak dipakai (api, api-ssl, ftp, telnet, www).
3. Klik tanda **Silang (Disable)**.
4. Sisakan **winbox** (dan ssh kalau perlu).

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/ip-services.jpg" 
        alt="Mematikan Service Tidak Penting" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 2: Disable semua yang berwarna abu-abu, sisakan Winbox
    </figcaption>
</figure>

## 3. Ganti Port Winbox (Jurus Kamuflase)
Port standar Winbox adalah `8291`. Hacker yang scan jaringan pasti nyari port ini. Mari kita pindahkan ke port "ghaib" biar mereka bingung.

1. Di menu **IP Services** tadi, double klik **winbox**.
2. Ganti Port menjadi angka acak (range 1000-65000), misal: `8777`.
3. Klik **OK**.

> **PENTING:** Setelah ini, cara login di Winbox harus pakai titik dua.
> Contoh: `192.168.10.1:8777`

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/winbox-port.jpg" 
        alt="Ganti Port Winbox" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 3: Mengganti port default untuk mengecoh scanner
    </figcaption>
</figure>

## 4. Matikan Neighbor Discovery (Mode Siluman)
Pernah buka tab "Neighbors" di Winbox dan lihat banyak router muncul? Itu karena fitur Discovery. Kita tidak mau router kita "melambai-lambai" ke tetangga.

1. Masuk menu **IP** > **Neighbor**.
2. Klik tab **Discovery Settings**.
3. Ubah Interface menjadi **none** (atau hanya ke LAN khusus admin).
4. Klik **OK**.

## 5. Backup Konfigurasi (Nyawa Cadangan)
Router bisa rusak, tersambar petir, atau salah setting sampai terkunci. Backup adalah koentji!

1. Masuk menu **Files**.
2. Klik tombol **Backup**.
3. Beri nama: `backup-aman-tgl-sekian`. Password: (isi jika perlu).
4. Klik **Backup**.
5. **WAJIB:** Drag & Drop file backup tersebut dari Winbox ke Desktop Laptop Bli. Simpan di Google Drive.

<figure style="text-align: center; margin: 2rem 0;">
    <img 
        src="/backup.jpg" 
        alt="Menu Backup Mikrotik" 
        style="background: white; padding: 10px; border-radius: 8px; display: block; margin: 0 auto; width: 100%; max-width: 450px; box-shadow: 0 4px 10px rgba(0,0,0,0.5);"
    >
    <figcaption style="color: #94a3b8; font-size: 0.9rem; margin-top: 8px; font-style: italic;">
        Gambar 4: Jangan lupa simpan file backup di tempat aman
    </figcaption>
</figure>

## Kesimpulan: Router Sudah Kebal?
Setidaknya, router Bli sekarang sudah 90% lebih aman daripada router settingan pabrik. Hacker kroco (script kiddie) bakal malas nyerang karena port-nya sudah diganti dan servicenya tertutup.

**Apa Selanjutnya?**
Router sudah online ✅
Router sudah aman ✅
Saatnya kita bikin **Sistem Voucheran** biar bisa cari cuan!

👉 **Selanjutnya:** [Mikrotik #3: Cara Setting Hotspot & Bikin Voucher (Coming Soon)](/blog/mikrotik-part-3)