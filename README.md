# Kasus 1: Simulasi Pertumbuhan Toko & Kebutuhan Penduduk (SPL 2×2)

## 1. Identitas

- Nama : Rena Fiantina
- NIM : 251511028
- Kelas : 1A - D3
- Tanggal Pengerjaan : 12 Juli 2026



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

Jika modal awal yang diberikan pada program adalah $10.000 dan target penduduk 100.000 jiwa, maka SPL menjadi:

1000x + 3000y = 10000

15000x + 20000y = 100000

## Bentuk Matriks (Ax = b)

```
| 1000   3000 |   | x |   =   | 10000  |
|15000  20000 | × | y |       |100000  |
```

# 3. Logika Kode Program

Kode program ditulis dalam bahasa C dan hanya menggunakan fungsi main(). Konsep utama yang diterapkan adalah Aturan Cramer untuk menyelesaikan Sistem Persamaan Linear (SPL) 2×2.

## a. Fungsi Utama (main)

1. **Deklarasi variabel**
   - modal dan penduduk sebagai input dari pengguna.
   - biayaX, biayaY, kapasitasX, dan kapasitasY sebagai konstanta tetap sesuai soal.

2. **Input modal dan penduduk**
   - Pengguna diminta memasukkan nilai modal dan jumlah penduduk melalui terminal.

3. **Menampilkan SPL**
   - Program mencetak kembali persamaan linear yang terbentuk agar pengguna dapat memverifikasi data yang dimasukkan.

4. **Perhitungan determinan**
   - Program menghitung nilai determinan matriks koefisien (D) serta determinan pengganti (Dx dan Dy) menggunakan Aturan Cramer.

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
- Modal = 5000
- Penduduk = 100000

Hasil perhitungan program:
- D = -25.000.000,00
- Dx = -200.000.000,00 sehingga x = 8,00
- Dy = 25.000.000,00 sehingga y = -1,00

Solusi SPL:
- x = 8 (Toko Standar)
- y = -1 (Toko Besar)

## b. Apakah Hasilnya Masuk Akal Secara Fisik?
Hasil tersebut tidak masuk akal secara fisik, karena jumlah toko tidak mungkin bernilai negatif.

Walaupun nilai x = 8 merupakan bilangan bulat positif, nilai y = -1 menunjukkan bahwa sistem persamaan memerlukan "jumlah toko negatif" agar kedua persamaan terpenuhi. Hal tersebut tidak mungkin terjadi dalam dunia nyata.

Secara praktis, kombinasi modal sebesar $5.000 dengan target pelayanan 100.000 penduduk tidak dapat direalisasikan menggunakan data biaya dan kapasitas yang diberikan.
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

Simpan program dengan nama kasus1.c, kemudian jalankan:

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

Contoh di atas menggunakan data standar pada soal, yaitu modal $10.000 dan target 100.000 penduduk, sehingga diperoleh solusi:

- x = 4 unit Toko Standar
- y = 2 unit Toko Besar


# Kasus 2: Analisis Efektivitas Pupuk (SPL 3×3)

## 2. Pemodelan Matematika

Berdasarkan narasi cerita, terdapat tiga variabel yang dicari:

- x = Profit per ton Pupuk A (dalam dolar)
- y = Profit per ton Pupuk B (dalam dolar)
- z = Profit per ton Pupuk C (dalam dolar)

## Data yang Diketahui

| Blok Lahan | Ton Pupuk A | Ton Pupuk B | Ton Pupuk C | Total Profit |
|-------------|------------:|------------:|------------:|-------------:|
| Blok 1 | 2 | 1 | 1 | $17.000 |
| Blok 2 | 1 | 2 | 1 | $16.000 |
| Blok 3 | 1 | 1 | 2 | $15.000 |

## Pembentukan SPL

Dari data di atas diperoleh sistem persamaan linear:

1. Blok 1

   2x + y + z = 17000

2. Blok 2

   x + 2y + z = 16000

3. Blok 3

   x + y + 2z = 15000

## Bentuk Matriks (Ax = b)

```text
| 2  1  1 |   | x |   =   |17000|
| 1  2  1 | × | y |       |16000|
| 1  1  2 |   | z |       |15000|
```

---

# 3. Logika Kode Program

Kode program ditulis dalam bahasa C dengan modular. Program dibagi menjadi beberapa fungsi sehingga tidak perlu menuliskan kode yang sama berulang kali. Metode penyelesaian SPL yang digunakan adalah Aturan Cramer untuk matriks 3×3.

## a. Fungsi-fungsi dalam Program

### 1. Fungsi minor2x2()

Fungsi ini digunakan untuk menghitung determinan matriks 2×2.

Rumus yang digunakan:

det = (a × d) - (b × c)

### 2. Fungsi determinan3x3()

Fungsi ini digunakan untuk menghitung determinan matriks 3×3 menggunakan metode ekspansi kofaktor pada baris pertama dengan bantuan fungsi minor2x2. 

Untuk matriks:

```text
| a  b  c |
| d  e  f |
| g  h  i |
```

Determinan dihitung menggunakan rumus:

det = a(ei - fh) - b(di - fg) + c(dh - eg)

Dan setiap minor (operasi pengurangan yang didalam kurung) dihitung menggunakan fungsi minor2x2().

### 3. Fungsi gantiKolom()

Fungsi ini digunakan untuk mengganti salah satu kolom matriks koefisien dengan vektor konstanta.

Fungsi ini digunakan untuk membentuk matriks:

- Ax
- Ay
- Az

sesuai dengan Aturan Cramer.

### 4. Fungsi cetakMatriks()

Fungsi ini digunakan untuk menampilkan matriks koefisien ke layar agar pengguna dapat memverifikasi data yang dimasukkan.

### 5. Fungsi main()

Fungsi utama mengatur seluruh alur program, yaitu:

1. Menerima input matriks koefisien dan vektor konstanta.
2. Menampilkan matriks koefisien.
3. Menghitung determinan utama (D).
4. Memeriksa syarat D ≠ 0.
5. Membentuk matriks Ax, Ay, dan Az.
6. Menghitung determinan Dx, Dy, dan Dz.
7. Menghitung nilai x, y, dan z menggunakan Aturan Cramer.
8. Menampilkan profit per ton masing-masing pupuk.

## b. Logika Pencarian Determinan

Untuk matriks:

```text
| a  b  c |
| d  e  f |
| g  h  i |
```

Determinan dihitung menggunakan ekspansi kofaktor pada baris pertama.

Rumus yang digunakan adalah:

D = a(ei - fh) - b(di - fg) + c(dh - eg)

Dalam program:

- minor2x2(m[1][1], m[1][2], m[2][1], m[2][2]) menghitung nilai (ei - fh)
- minor2x2(m[1][0], m[1][2], m[2][0], m[2][2]) menghitung nilai (di - fg)
- minor2x2(m[1][0], m[1][1], m[2][0], m[2][1]) menghitung nilai (dh - eg)

Nilai-nilai tersebut kemudian digunakan untuk memperoleh determinan utama D.

Selanjutnya program membentuk matriks Ax, Ay, dan Az dengan mengganti kolom yang sesuai menggunakan vektor konstanta.

Kemudian dihitung:

x = Dx / D

y = Dy / D

z = Dz / D

## c. Mengapa Syarat D ≠ 0 Wajib Diperiksa?

Sama seperti yang dikasus sebelumnya, nilai determinan menentukan apakah SPL memiliki solusi tunggal.

Jika D ≠ 0, matriks koefisien memiliki invers sehingga solusi dapat dihitung menggunakan Aturan Cramer. Sebaliknya, jika D = 0 maka:

- SPL tidak memiliki solusi.
- SPL memiliki tak hingga solusi.

Selain itu, apabila D = 0 maka proses pembagian Dx/D, Dy/D, maupun Dz/D akan menyebabkan pembagian dengan nol sehingga program tidak dapat menghitung solusi. Oleh karena itu program akan menghentikan proses dan menampilkan pesan bahwa sistem tidak memiliki solusi tunggal.

---

# 4. Analisis Batas

## a. Uji Coba Parameter: Mengubah Total Profit Blok 1

Pada pengujian ini, matriks koefisien tetap menggunakan data pada soal, sedangkan total profit Blok 1 diubah dari $17.000 menjadi $5.000.

Input yang digunakan:

Matriks koefisien:

```text
| 2  1  1 |
| 1  2  1 |
| 1  1  2 |
```

Vektor konstanta:

```text
| 5000 |
|16000 |
|15000 |
```

Hasil perhitungan program:

- D = 4,00
- Dx = -14000,00 sehingga x = -3500,00
- Dy = 32000,00 sehingga y = 8000,00
- Dz = 28000,00 sehingga z = 7000,00

Solusi SPL:

- x = -3500
- y = 8000
- z = 7000

## b. Apakah Hasilnya Masuk Akal Secara Fisik?

Hasil tersebut tidak masuk akal secara fisik karena profit per ton pupuk tidak mungkin bernilai negatif.

Nilai x = -3500 menunjukkan bahwa data yang dimasukkan tidak konsisten secara ekonomi. Dengan total profit Blok 1 yang terlalu kecil dibandingkan blok lainnya, sistem persamaan memaksa nilai profit pupuk A menjadi negatif agar seluruh persamaan tetap terpenuhi.

Program pada Kasus 2 belum memberikan peringatan untuk solusi negatif. Oleh karena itu pengguna sebaiknya:

- Memeriksa kembali data input.
- Memastikan data tonase dan total profit konsisten.
- Menyadari bahwa solusi negatif tidak dapat diterapkan dalam kondisi nyata.

## c. Skenario Lain: Mengubah Koefisien Menjadi Identik

Jika seluruh baris matriks koefisien dibuat sama, misalnya:

```text
|1 1 1|
|1 1 1|
|1 1 1|
```

Maka determinan matriks akan bernilai nol.

Akibatnya:

- D = 0
- Program menampilkan pesan bahwa sistem tidak memiliki solusi tunggal.

Hal tersebut sesuai dengan teori karena ketiga persamaan memberikan informasi yang sama sehingga tidak cukup untuk menentukan tiga variabel secara unik.

---

# 5. Panduan Kompilasi

Program ditulis menggunakan bahasa C standar dan dapat dikompilasi menggunakan GCC.

## a. Persiapan

Pastikan compiler GCC sudah terpasang.

```bash
gcc --version
```

## b. Kompilasi

Simpan program dengan nama kasus2.c, kemudian jalankan:

```bash
gcc kasus2.c -o kasus2
```

## c. Menjalankan Program

```bash
kasus2.exe
```

## d. Contoh Sesi Eksekusi

```text
=== Simulasi Evaluasi Produktivitas Kelapa Sawit ===

Masukkan koefisien tonase (matriks 3x3), baris per blok lahan:

Blok 1 - ton A, ton B, ton C:
  pupuk A : 2
  pupuk B : 1
  pupuk C : 1

Blok 2 - ton A, ton B, ton C:
  pupuk A : 1
  pupuk B : 2
  pupuk C : 1

Blok 3 - ton A, ton B, ton C:
  pupuk A : 1
  pupuk B : 1
  pupuk C : 2

Masukkan total profit tiap blok:
  Blok 1 : 17000
  Blok 2 : 16000
  Blok 3 : 15000

Matriks Koefisien A:
  [     2.00     1.00     1.00 ]
  [     1.00     2.00     1.00 ]
  [     1.00     1.00     2.00 ]

Determinan D  = 4.00
Determinan Dx = 20000.00
Determinan Dy = 16000.00
Determinan Dz = 12000.00

Hasil (Aturan Cramer):
Profit/ton Pupuk A (x) = 5000.00
Profit/ton Pupuk B (y) = 4000.00
Profit/ton Pupuk C (z) = 3000.00
```

Contoh di atas menggunakan data standar pada soal sehingga diperoleh:

- x = 5000 dolar per ton Pupuk A
- y = 4000 dolar per ton Pupuk B
- z = 3000 dolar per ton Pupuk C

Hasil tersebut memenuhi ketiga persamaan sehingga dapat diinterpretasikan sebagai profit per ton masing-masing jenis pupuk.

Hasil tersebut memenuhi kedua persamaan dan dapat diterapkan secara fisik karena kedua nilai bernilai positif.
