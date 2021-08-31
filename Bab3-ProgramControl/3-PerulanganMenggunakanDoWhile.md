[<< Materi Sebelumnya (Perulangan menggunakan "for") <<](2-PerulanganMenggunakanFor.md)

# Perulangan Menggunakan "do...while"

Perulangan menggunakan `do...while` merupakan sebuah model perulangan "turunan" dari `while`. Cara kerjanya pun sangat simpel, hanya sedikit berbeda dengan cara kerja statement `while`, di mana perulangan menggunakan `do...while` **menjamin bahwa loop dieksekusikan sekali**. Sebelum kalian melanjutkan, pastikan kalian sudah memahami cara kerja dan penggunaan statement `while` [di sini](https://github.com/stackofsugar/TeachingAssistant-KP2021/blob/main/Bab2-StructuredProgramming/4-PemilihanPerulangan.md#perulangan-while). Jika kalian sudah memahaminya, perhatikan potongan kode di bawah ini.

```c
int i = 150;

while (i == 100) {
  printf("Never gonna give you up");
}
```


Jika kita coba untuk menjalankan kode di atas, kita tidak akan mendapatkan *output* apapun. Hal ini dikarenakan kondisi dari `while` di atas, yaitu `i == 100`, tidak akan pernah tercapai karena `i` tidak pernah diubah dalam kode. Namun, mari kita coba untuk mengubah perulangan kita untuk menggunakan `do...while`.

```c
int i = 150;

do {
  printf("Never gonna give you up");
} while (i == 100);
```
*Output* pada *console*:
```
Never gonna give you up
```

Bisa dilihat pada contoh di atas, jika kita menggunakan statement `do...while`, meskipun kondisi `i == 100` tidak terpenuhi, perintah `printf()` kita tetap berjalan sekali.

[>> Materi Berikutnya (Perulangan dengan "break" dan "continue") >>](4-PerulanganBreakContinue.md)
