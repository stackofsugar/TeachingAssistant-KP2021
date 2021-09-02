[<< Materi Sebelumnya (Algoritma, Pseudocode, dan Source Code) <<](2-AlgoritmaPseudocodeSourcecode.md)

# 2.3 - Operasi Assignment dan Aritmatika
Sebuah operasi adalah proses yang melibatkan *operand* dan operator, untuk menggambarkan sebuah kejadian. Secara matematis, kita sudah sering menemukan operasi, seperti `1 + 1 = 2`.

## Operasi Aritmatika
Pada dasarnya, operasi aritmatika yang didukung oleh bahasa C meliputi beberapa operator seperti yang dijelaskan pada tabel di bawah ini. Mari kita buat dua variabel sebagai contoh, `a = 20` dan `b = 15`.

|Operator|Nama|Contoh|
|:------:|----|------|
|+|Penambahan|`a + b = 35`|
|-|Pengurangan|`a - b = 5`|
|*|Perkalian|`a * b = 300`|
|/|Pembagian|`b / a = 0.75`|
|%|Modulo|`7 % b = 7`|
|++|*Increment*|`a++ = 21`|
|--|*Decrement*|`a-- = 19`|

Karena operasi penambahan, pengurangan, perkalian, dan pembagian seharusnya sudah cukup dimengerti, penjeasan akan dimulai pada operator modulo/modulus/*remainder*.

- Operator Modulo
Operator ini digunakan untuk mencari remainder atau sisa hasil bagi. Jika kita melakukan operasi `25 % 7 = 4`, dapat diinterpretasikan sebagai `25 / 7 = 3 sisa 4`. Jadi, kita ingin mencari sisa dari operasi `25 / 7`.
- Operasi Increment
Operasi ini menambahkan nilai 1 pada variabel yang di-increment. Jika kita memiliki variabel `a = 10`, melakukan operasi `a++` sama saja dengan melakukan operasi `a = a + 1`, yang memiliki hasil `11`.
- Operasi Decrement
Kebalikan dari operasi increment, decrement mengurangkan 1 nilai pada variabel yang di-decrement. Jika kita memiliki variabel `b = 7`, maka `b--` akan membuat menjadikan `b = 6`.

> Untuk lebih memahami fungsi dari operator, kalian dapat mencoba-coba operator di atas pada IDE kalian.

## Operasi Assignment
Operasi assignment (atau beberapa kali disebut penugasan) adalah operasi sederhana yang melibatkan operator `=`.  Operator tersebut "mengambil" nilai dari sisi kanan, dan memberikannya untuk sisi kiri. Lihat potongan kode di bawah.
```c
int a = 10, b = 20, c, d;

c = a;
// Membuat c bernilai sama dengan a, yaitu 10

d = a + b;
// Membuat d bernilai sama dengan a ditambah b, yaitu 30
```
Selain operasi assignment dasar di atas, ada beberapa "turunan" dari operasi assignment yang berhubungan sangat erat dengan [operasi aritmatika](#operasi-aritmatika). *Behavior* atau tingkah laku dari operator-operator di bawah dapat dimisalkan sebagai "laukukan operasi turunan, lalu masukkan hasilnya di *operand* kiri". Perhatikan tabel di bawah ini.

|Operasi|Tingkah laku|
|:-----:|------------|
|+=|`a += b` ekuivalen dengan `a = a + b`|
|-=|`a -= b` ekuivalen dengan `a = a - b`|
|*=|`a *= b` ekuivalen dengan `a = a * b`|
|/=|`a /= b` ekuivalen dengan `a = a / b`|
|%=|`a %= b` ekuivalen dengan `a = a % b`|

## Operator Lanjutan
Selain dua jenis operator dasar tersebut, masih banyak operator lain yang akan dijelaskan pada materi-materi berikutnya, seperti:
- Operator Pembanding
- Operator Logis
- Operator Bitwise
- Lain-lainnya, seperti conditional/ternary, pointer, dan reference.

[>> Materi Berikutnya (Pemilihan dan Perulangan Sederhana) >>](4-PemilihanPerulangan.md) 
