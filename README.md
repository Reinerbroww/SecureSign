<div align="center">

___  ___  ___ _   _ ___ ___ ___ ___ ___ _  _ 
/ __|| __||  _| | | | _ \ __/ __|_ _/ __| \| |
\__ \| _| | (_| |_| |   / _|\__ \| | (_ | .  |
|___/|___| \___|\___/|_|_\___|___/___\___|_|\_|

### 🔐 Hybrid Cryptography System with Digital Signature

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![PyCryptodome](https://img.shields.io/badge/PyCryptodome-3.x-green?style=for-the-badge)](https://pycryptodome.readthedocs.io)
[![License](https://img.shields.io/badge/License-MIT-yellow?style=for-the-badge)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)]()

*Enkripsi data dengan AES + RSA, tandatangani dengan DSA — semua dalam satu sistem.*

</div>

---

## 📖 Tentang Project

**CipherCore** adalah sistem kriptografi hybrid yang menggabungkan tiga algoritma kriptografi utama:

- **AES (CBC Mode)** — untuk enkripsi data yang cepat dan efisien
- **RSA (OAEP)** — untuk mengamankan AES key secara asimetris
- **DSA** — untuk membuat dan memverifikasi tanda tangan digital

Project ini dibuat sebagai bagian dari **Ujian Akhir Semester (UAS) mata kuliah Keamanan Informasi / Kriptografi**.

---

## ✨ Fitur Utama

| Fitur | Keterangan |
|-------|-----------|
| 🔒 **Hybrid Encryption** | AES mengenkripsi data, RSA mengenkripsi AES key |
| ✍️ **Digital Signature** | DSA untuk autentikasi & non-repudiation dokumen |
| 🧾 **Integrity Check** | SHA-256 untuk verifikasi data tidak diubah |
| 📁 **File-based Input** | Plaintext dibaca dari file eksternal |
| 💾 **Auto Save** | Hasil enkripsi, key, dan signature disimpan otomatis |

---

## 🗂️ Struktur Project

```
CipherCore/
│
├── 📄 main.py                    ← Entry point utama
│
├── 📁 algorithms/
│   ├── 🔷 aes.py                 ← Enkripsi AES (CBC Mode)
│   ├── 🔶 rsa.py                 ← Enkripsi RSA (OAEP)
│   └── 🔴 dsa.py                 ← Digital Signature (DSA)
│
├── 📁 files/
│   ├── plaintext.txt             ← Input: teks yang akan dienkripsi
│   ├── encrypted_aes.txt         ← Output: hasil enkripsi AES
│   ├── encrypted_rsa.txt         ← Output: AES key terenkripsi (RSA)
│   └── signature.txt             ← Output: tanda tangan digital DSA
│
└── 📁 keys/
    ├── rsa_private.pem           ← RSA Private Key
    ├── rsa_public.pem            ← RSA Public Key
    ├── dsa_private.pem           ← DSA Private Key
    └── dsa_public.pem            ← DSA Public Key
```

---

## ⚙️ Cara Instalasi & Penggunaan

### 1. Clone Repository

```bash
git clone https://github.com/username/CipherCore.git
cd CipherCore
```

### 2. Install Dependencies

```bash
pip install pycryptodome
```

### 3. Siapkan Plaintext

Edit file `files/plaintext.txt` dan isi dengan teks yang ingin dienkripsi:

```
Ini adalah pesan rahasia yang akan dienkripsi...
```

### 4. Jalankan Program

```bash
python main.py
```

---

## 🔄 Alur Sistem

```
📄 plaintext.txt
        │
        ▼
┌───────────────────┐
│  1. Baca File     │
└────────┬──────────┘
         │
         ├──────────────────────────────────────────┐
         │                                          │
         ▼                                          ▼
┌─────────────────┐                      ┌──────────────────┐
│  2. Hash SHA256 │                      │  3. DSA Sign     │
│  (Integrity)    │                      │  (Auth)          │
└────────┬────────┘                      └────────┬─────────┘
         │                                        │
         ▼                                        ▼
┌─────────────────┐                      📄 signature.txt
│  4. AES Encrypt │
│  (CBC Mode)     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  5. RSA Encrypt │
│  (AES Key)      │
└────────┬────────┘
         │
         ▼
📄 encrypted_aes.txt
📄 encrypted_rsa.txt
         │
         ▼
┌─────────────────┐
│  6. Decrypt &   │
│  Verify         │
└────────┬────────┘
         │
         ▼
✅ Data Terverifikasi
```

---

## 🧠 Penjelasan Algoritma

### 🔷 AES — Advanced Encryption Standard
> AES adalah algoritma enkripsi simetris, artinya kunci yang sama dipakai untuk enkripsi dan dekripsi.

- **Mode**: CBC (Cipher Block Chaining) — lebih aman dari ECB karena setiap blok data di-XOR dengan blok sebelumnya sebelum dienkripsi
- **Key Size**: 128-bit (16 byte)
- **IV**: Random 16 byte untuk setiap sesi enkripsi

### 🔶 RSA — Rivest–Shamir–Adleman
> RSA adalah algoritma enkripsi asimetris, menggunakan dua kunci berbeda (public & private).

- **Key Size**: 2048-bit
- **Padding**: OAEP (Optimal Asymmetric Encryption Padding) — lebih aman dari PKCS#1 v1.5
- **Fungsi**: Mengenkripsi AES key (bukan data langsung) — inilah yang disebut *Hybrid Encryption*

### 🔴 DSA — Digital Signature Algorithm
> DSA dipakai untuk tanda tangan digital, bukan enkripsi. Fungsinya membuktikan keaslian dokumen dan identitas pengirim.

- **Key Size**: 2048-bit
- **Hash**: SHA-256 (data di-hash dulu sebelum ditandatangani)
- **Mode**: FIPS 186-3 (standar resmi DSA)

### 🧾 SHA-256 — Secure Hash Algorithm
> SHA-256 menghasilkan hash unik 256-bit dari data. Dipakai untuk verifikasi integritas — jika data diubah satu karakter pun, hash-nya akan berbeda.

---

## 📦 Dependencies

| Library | Versi | Fungsi |
|---------|-------|--------|
| `pycryptodome` | 3.x | AES, RSA, DSA, SHA-256 |
| `base64` | built-in | Encoding binary ke teks |
| `os` | built-in | Manajemen file & direktori |

---

## 📊 Contoh Output

```
============================================================
   SISTEM KRIPTOGRAFI - AES + RSA + DSA
============================================================

📄 ISI PLAINTEXT:
Dokumen Rahasia - Sistem Kriptografi UAS
...

🧾 HASH DATA ASLI:
6508979afa7a5ee5d8d5a53dc1527efe2d455b3448d165962524ccd208862184

🔑 ENCRYPTED AES KEY (RSA):
WD4SBYo8KME/3AB2Mg43PZL3dx...

✍️  DIGITAL SIGNATURE (DSA):
Ufhq+QQFoqbQoI+fQl/KRl+Q+Jt...

✅ TANDA TANGAN VALID — Dokumen asli & pengirim terverifikasi
✅ STATUS: DATA ASLI & TIDAK BERUBAH — Integritas terjaga
```

---

## 🛡️ Konsep Keamanan

| Konsep | Implementasi |
|--------|-------------|
| **Confidentiality** | AES + RSA (data tidak bisa dibaca tanpa kunci) |
| **Integrity** | SHA-256 (data tidak bisa diubah tanpa terdeteksi) |
| **Authentication** | DSA (membuktikan identitas pengirim) |
| **Non-repudiation** | DSA (pengirim tidak bisa menyangkal telah menandatangani) |

---

## 👨‍💻 Author

> Dibuat untuk memenuhi tugas **UAS Mata Kuliah Kriptografi / Keamanan Informasi**

---

<div align="center">

**⭐ Kalau project ini membantu, jangan lupa kasih star ya!**

*Built with Python & PyCryptodome*

</div>
