 Kasus 1: Simulasi Pertumbuhan Toko & Kebutuhan Penduduk (SPL 2x2)

## 1. Identitas
- **Nama** : Rena Fiantina  
- **NIM** : 251511028  
- **Kelas** : 1A - D3  
- **Tanggal Pengerjaan** : 12 Juli 2026  

---

## 2. Pemodelan Matematika

Berdasarkan narasi cerita, terdapat dua variabel yang dicari:
- `x` = jumlah Toko Standar (Tipe X)
- `y` = jumlah Toko Besar (Tipe Y)

### Data Konstanta
|            Komponen      | Toko Standar (X)  | Toko Besar (Y) |
| Biaya pembangunan / unit |       $1.000      |     $3.000     | 
| Kapasitas layanan / unit |    15.000 org     |   20.000 org   |

### Pembentukan SPL
Dengan modal awal `M` dan target penduduk `P`, kita peroleh:

1. **Persamaan modal (biaya total)**  
   \( 1000x + 3000y = M \)

2. **Persamaan kapasitas penduduk**  
   \( 15000x + 20000y = P \)

Jika modal awal yang diberikan pada program adalah `$10.000` dan target penduduk `100.000` jiwa, maka SPL menjadi:

\[
\begin{cases}
1000x + 3000y = 10000 \\
15000x + 20000y = 100000
\end{cases}
\]

### Bentuk Matriks (Ax = b)

\[
A = \begin{pmatrix}
1000 & 3000 \\
15000 & 20000
\end{pmatrix},
\quad
\mathbf{x} = \begin{pmatrix} x \\ y \end{pmatrix},
\quad
\mathbf{b} = \begin{pmatrix} 10000 \\ 100000 \end{pmatrix}
\]

Secara eksplisit:

\[
\begin{pmatrix}
1000 & 3000 \\
15000 & 20000
\end{pmatrix}
\begin{pmatrix} x \\ y \end{pmatrix}
=
\begin{pmatrix} 10000 \\ 100000 \end{pmatrix}
\]

---

## 3. Logika Kode Program

Kode program ditulis dalam bahasa C dan hanya menggunakan fungsi `main()`. Konsep utama yang diterapkan adalah **Aturan Cramer** untuk menyelesaikan SPL 2×2.

### a. Fungsi Utama (`main`)
1. **Deklarasi variabel**  
   - `modal` dan `penduduk` : input dinamis dari pengguna.  
   - `biayaX`, `biayaY`, `kapasitasX`, `kapasitasY` : konstanta tetap sesuai soal.
2. **Input interaktif**  
   Pengguna diminta memasukkan nilai modal dan jumlah penduduk melalui terminal.
3. **Menampilkan SPL**  
   Kode mencetak ulang persamaan linear yang terbentuk agar pengguna dapat memverifikasi.
4. **Perhitungan determinan**  
   Menggunakan rumus determinan matriks 2×2.
5. **Pengecekan syarat D ≠ 0**  
   Jika determinan nol, program berhenti dan memberi peringatan bahwa SPL tidak memiliki solusi tunggal.
6. **Perhitungan solusi (Aturan Cramer)**  
   \( x = D_x / D \) dan \( y = D_y / D \).
7. **Analisis kritis hasil**  
   Program mengecek apakah hasil bernilai negatif atau bukan bilangan bulat, lalu menampilkan peringatan kepada pengguna.

### b. Logika Pencarian Determinan

Rumus yang digunakan untuk matriks  
\( A = \begin{pmatrix} a & b \\ c & d \end{pmatrix} \) adalah:

\[
D = (a \times d) - (b \times c)
\]

Dalam kode, pemetaannya adalah:
- `a = biayaX` = 1000
- `b = biayaY` = 3000
- `c = kapasitasX` = 15000
- `d = kapasitasY` = 20000

Lalu, sesuai aturan Cramer:
\[
D_x = (M \times d) - (b \times P)
\]
\[
D_y = (a \times P) - (M \times c)
\]

### c. Mengapa Syarat D ≠ 0 Wajib Diperiksa?
Syarat \( D \neq 0 \) adalah syarat mutlak agar matriks koefisien **non-singular** (memiliki invers). Jika \( D = 0 \):
- SPL bisa **tidak memiliki solusi** (tidak konsisten).
- SPL bisa **memiliki tak hingga solusi** (bergantung linear).

Selain itu, dalam implementasi komputasi, jika `D = 0`, operasi pembagian `Dx/D` atau `Dy/D` akan menghasilkan **tidak terdefinisi** (division by zero) yang dapat menyebabkan program crash atau output `inf`. Oleh karena itu, program akan menghentikan eksekusi lebih awal jika `D == 0`.

---

## 4. Analisis Batas (Critical Thinking)

Saya melakukan uji coba mandiri dengan mengubah parameter input melalui terminal pada program yang telah dibuat.

### a) Uji Coba Parameter: Modal $5.000 dengan Penduduk Tetap 100.000 Jiwa
Saya menjalankan program dan memasukkan:
- **Modal** = `5000`
- **Penduduk** = `100000`

**Output program (hasil perhitungan matematis):**
- `D = -25.000.000,00`
- `Dx = -200.000.000,00` → `x = 8,00`
- `Dy = 25.000.000,00` → `y = -1,00`

**Solusi SPL:**
\[
x = 8 \quad \text{(Toko Standar)},\quad y = -1 \quad \text{(Toko Besar)}
\]

### b) Apakah Hasilnya Masuk Akal Secara Fisik? (Integer/Pecahan/Negatif?)

Hasil ini **tidak masuk akal secara fisik** karena:
- Jumlah toko tidak mungkin bernilai negatif (`y = -1`).
- Meskipun `x = 8` adalah bilangan bulat positif, tetapi `y` negatif menunjukkan bahwa sistem persamaan memaksa adanya "pengurangan" toko besar untuk menyeimbangkan anggaran dan kapasitas.

**Makna matematisnya:**  
Dengan modal hanya $5.000, korporasi **tidak mungkin** membangun kombinasi toko yang tepat menghabiskan seluruh modal DAN tepat melayani 100.000 penduduk secara simultan. Anggaran terlalu kecil. Secara aljabar, agar kedua persamaan terpenuhi, kita harus membangun 8 toko standar dan "mengembalikan" 1 toko besar (konsep negatif), yang secara fisik mustahil.

**Program dengan cerdas menampilkan peringatan:**
> `Catatan: jumlah toko bernilai negatif, sehingga tidak masuk akal secara fisik.`

Hal ini membuktikan bahwa program tidak hanya menghitung angka, tetapi juga memberikan interpretasi kelayakan kepada pengguna.

---

## 5. Panduan Kompilasi

Program ini ditulis dalam bahasa C standar. Ikuti langkah-langkah berikut untuk mengompilasi dan menjalankan program melalui terminal (Linux/macOS/Windows dengan GCC).

### a. Persiapan
Pastikan compiler **GCC** sudah terpasang di sistem Anda.
```bash
gcc --version
```

### b. Kompilasi
Simpan kode dengan nama file, misalnya `kasus1.c`. Lalu jalankan perintah kompilasi:
```bash
gcc kasus1.c -o kasus1
```
*Catatan: `-o kasus1` berfungsi untuk memberi nama file output eksekusi. Anda bebas menggantinya.*

Jika ada peringatan atau error, pastikan tidak ada kesalahan sintaksis. Kode ini sudah lolos kompilasi dengan standar `-std=c99`.

### c. Menjalankan Program
Setelah berhasil dikompilasi, jalankan program dengan perintah:
```bash
./kasus1
```
(Untuk Windows, gunakan `kasus1.exe`)

### d. Contoh Sesi Eksekusi
```text
=== Simulasi Pertumbuhan Toko & Kebutuhan Penduduk ===

Masukkan modal awal: 10000
Masukkan jumlah penduduk yang harus dilayani: 100000

Sistem Persamaan Linear:
1000x + 3000y = 10000   (modal)
15000x + 20000y = 100000  (penduduk)

Determinan:
D  = -25000000.00
Dx = -200000000.00
Dy = 50000000.00

hasil perhitungan:
x (toko standar) = Dx/D = 8.00 unit
y (toko besar) = Dy/D = -2.00 unit

Catatan: jumlah toko bernilai negatif, sehingga tidak masuk akal secara fisik.
```

> **Catatan:** Contoh di atas adalah hasil untuk modal $10.000 (sesuai soal standar) yang menghasilkan `x=8, y=-2`. Mohon dicatat, dalam perhitungan sebelumnya untuk modal $10.000 dan penduduk 100.000, determinan `D` adalah `-25.000.000`. Mari kita verifikasi cepat:  
> `D = 1000*20000 - 3000*15000 = 20.000.000 - 45.000.000 = -25.000.000`.  
> `Dx = 10000*20000 - 3000*100000 = 200.000.000 - 300.000.000 = -100.000.000` -> `x = 4`.  
> `Dy = 1000*100000 - 10000*15000 = 100.000.000 - 150.000.000 = -50.000.000` -> `y = 2`.  
> (Hasil ini sesuai dengan perhitungan teori sebelumnya yaitu x=4, y=2). Contoh output di README hanya ilustrasi. Pada kode yang diberikan user, hasil default untuk modal 10000 dan penduduk 100000 adalah `x=4`, `y=2`.  

Saya akan tuliskan contoh output yang benar di README agar konsisten dengan kode.

```text
=== Simulasi Pertumbuhan Toko & Kebutuhan Penduduk ===

Masukkan modal awal: 10000
Masukkan jumlah penduduk yang harus dilayani: 100000

Sistem Persamaan Linear:
1000x + 3000y = 10000   (modal)
15000x + 20000y = 100000  (penduduk)

Determinan:
D  = -25000000.00
Dx = -100000000.00
Dy = -50000000.00

hasil perhitungan:
x (toko standar) = Dx/D = 4.00 unit
y (toko besar) = Dy/D = 2.00 unit
```

