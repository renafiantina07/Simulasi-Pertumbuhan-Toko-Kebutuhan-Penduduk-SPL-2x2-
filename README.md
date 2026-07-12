# Kasus 1: Simulasi Pertumbuhan Toko & Kebutuhan Penduduk (SPL 2×2)

## 1. Identitas

- **Nama** : Rena Fiantina
- **NIM** : 251511028
- **Kelas** : 1A - D3
- **Tanggal Pengerjaan** : 12 Juli 2026

---

# 2. Pemodelan Matematika

Berdasarkan narasi cerita, terdapat dua variabel yang dicari:
- x = jumlah Toko Standar (Tipe X)
- y = jumlah Toko Besar (Tipe Y)

## Data Konstanta

| Komponen | Toko Standar (X) | Toko Besar (Y) |
|-----------|-----------------:|---------------:|
| Biaya pembangunan / unit | $1.000 | $3.000 |
| Kapasitas layanan / unit | 15.000 orang | 20.000 orang |

## Pembentukan SPL

Dengan modal awal dan target penduduk, diperoleh dua persamaan linear:
1. Persamaan modal (biaya total)
   1000x + 3000y = modal awal

2. Persamaan kapasitas penduduk
   15000x + 20000y = target penduduk

Jika modal awal yang diberikan pada program adalah **$10.000** dan target penduduk **100.000 jiwa**, maka SPL menjadi:

1000x + 3000y = 10000
15000x + 20000y = 100000

## Bentuk Matriks (Ax = b)

```
| 1000   3000 |   | x |   =   | 10000  |
|15000  20000 | × | y |       |100000  |
```

# 3. Logika Kode Program

Kode program ditulis dalam bahasa C dan hanya menggunakan fungsi `main()`. Konsep utama yang diterapkan adalah **Aturan Cramer** untuk menyelesaikan Sistem Persamaan Linear (SPL) 2×2.

## a. Fungsi Utama (`main`)

1. **Deklarasi variabel**
   - modal dan penduduk sebagai input dari pengguna.
   - biayaX, biayaY, kapasitasX, dan kapasitasY sebagai konstanta tetap sesuai soal.

2. **Input interaktif**
   - Pengguna diminta memasukkan nilai modal dan jumlah penduduk melalui terminal.

3. **Menampilkan SPL**
   - Program mencetak kembali persamaan linear yang terbentuk agar pengguna dapat memverifikasi data yang dimasukkan.

4. **Perhitungan determinan**
   - Program menghitung nilai determinan matriks koefisien (`D`) serta determinan pengganti (`Dx` dan `Dy`) menggunakan Aturan Cramer.

5. **Pengecekan syarat D ≠ 0**
   - Jika determinan bernilai nol, program akan berhenti karena SPL tidak memiliki solusi tunggal.

6. **Perhitungan solusi**
   - Nilai variabel dihitung menggunakan rumus:

     x = Dx / D
     y = Dy / D

7. **Analisis hasil**
   - Program memeriksa apakah hasil bernilai negatif atau bukan bilangan bulat. Jika demikian, program memberikan peringatan kepada pengguna.

## b. Logika Pencarian Determinan

Untuk matriks:
```
| a  b |
| c  d |
```
Rumus determinannya adalah:
D = (a × d) - (b × c)
Pada program, nilai variabel dipetakan sebagai berikut:
- a = biayaX = 1000
- b = biayaY = 3000
- c = kapasitasX = 15000
- d = kapasitasY = 20000
- M = Modal awal
- P = Penduduk

Selanjutnya dihitung:
Dx = (M × d) - (b × P)
Dy = (a × P) - (M × c)

Kemudian solusi diperoleh dari:
x = Dx / D
y = Dy / D

## c. Mengapa Syarat D ≠ 0 Wajib Diperiksa?

Nilai determinan menentukan apakah SPL mempunyai solusi tunggal atau tidak.
Jika D ≠ 0, matriks koefisien memiliki invers sehingga solusi dapat dihitung menggunakan Aturan Cramer.
Sebaliknya, jika D = 0, maka terdapat dua kemungkinan:
- SPL tidak memiliki solusi.
- SPL memiliki tak hingga banyak solusi.
Selain itu, dalam implementasi program, apabila D = 0 maka proses pembagian Dx/D maupun Dy/D akan menyebabkan error. Oleh karena itu, program harus memeriksa nilai determinan terlebih dahulu sebelum menghitung solusi.

---

# 4. Analisis Batas 

## a. Uji Coba Parameter: Modal $5.000 dengan Penduduk Tetap 100.000 Jiwa
Input yang diberikan:
- **Modal** = 5000
- **Penduduk** = 100000

Hasil perhitungan program:
- D = -25.000.000,00
- Dx = -200.000.000,00 sehingga x = 8,00
- Dy = 25.000.000,00 sehingga y = -1,00

Solusi SPL:
- x = 8 (Toko Standar)
- y = -1 (Toko Besar)

## b. Apakah Hasilnya Masuk Akal Secara Fisik?
Hasil tersebut **tidak masuk akal secara fisik**, karena jumlah toko tidak mungkin bernilai negatif.

Walaupun nilai x = 8 merupakan bilangan bulat positif, nilai y = -1 menunjukkan bahwa sistem persamaan memerlukan "jumlah toko negatif" agar kedua persamaan terpenuhi. Hal tersebut tidak mungkin terjadi dalam dunia nyata.

Secara praktis, kombinasi modal sebesar **$5.000** dengan target pelayanan **100.000 penduduk** tidak dapat direalisasikan menggunakan data biaya dan kapasitas yang diberikan.
Karena itu program memberikan peringatan bahwa hasil perhitungan tidak layak diterapkan.
Contoh pesan yang ditampilkan program:

```text
Catatan: jumlah toko bernilai negatif, sehingga tidak masuk akal secara fisik.
```
Hal ini menunjukkan bahwa program tidak hanya menghitung solusi matematika, tetapi juga melakukan validasi sederhana terhadap kelayakan hasil.


# 5. Panduan Kompilasi

Program ini ditulis menggunakan bahasa C standar dan dapat dikompilasi menggunakan GCC.
## a. Persiapan

Pastikan compiler GCC terpasang.

```bash
gcc --version
```

## b. Kompilasi

Simpan program dengan nama `kasus1.c`, kemudian jalankan:

```bash
gcc kasus1.c 
```
## c. Menjalankan Program

```bash
kasus1.exe
```

## d. Contoh Sesi Eksekusi

```text
=== Simulasi Pertumbuhan Toko & Kebutuhan Penduduk ===

Masukkan modal awal: 10000
Masukkan jumlah penduduk yang harus dilayani: 100000

Sistem Persamaan Linear:
1000x + 3000y = 10000 (modal)
15000x + 20000y = 100000 (penduduk)

Determinan:
D  = -25000000.00
Dx = -100000000.00
Dy = -50000000.00

Hasil Perhitungan:
x (Toko Standar) = 4.00 unit
y (Toko Besar) = 2.00 unit
```

Contoh di atas menggunakan data standar pada soal, yaitu modal **$10.000** dan target **100.000 penduduk**, sehingga diperoleh solusi:

- x = 4 unit Toko Standar
- y = 2 unit Toko Besar

Hasil tersebut memenuhi kedua persamaan dan dapat diterapkan secara fisik karena kedua nilai bernilai positif.
