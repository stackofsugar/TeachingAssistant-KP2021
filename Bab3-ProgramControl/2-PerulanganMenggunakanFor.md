[<< Materi Sebelumnya (Pemilihan dengan "switch") <<](1-PemilihanDenganSwitch.md)

# Perulangan menggunakan For statement

Setelah sebelumnya telah dijelaskan perulangan menggunakan **while statement** pada [Bab 2-4](https://github.com/stackofsugar/TeachingAssistant-KP2021/blob/main/Bab2-StructuredProgramming/4-PemilihanPerulangan.md), kali ini kita akan menggunakan **for statement**

## For statement
For statement adalah suatu statement perulangan/iterasi/loop yang memiliki tiga komponen yaitu inisialisasi, kondisi, dan update. For statement sering digunakan untuk _counter-controlled iteration_

**Apa itu _counter-controlled iteration_?**

_Counter-controlled iteration_ adalah salah satu metode perulangan yang mana perulangan tersebut dikendalikan oleh sebuah pencacah (_counter_) dan memiliki suatu kondisi yang menentukan apakah tetap dilakukan perulangan atau berhenti

## Syntax
```c
for(/* inisialisasi */ ; /* kondisi */ ; /* update */){
    /* yang akan diulang... */
}
```
- Inisialisasi: menentukan variabel apa yang akan menjadi pencacah/_counter_ (biasanya variabel bertipe `int` dan bernama `i`,`j`,`k`, dll. Namun, kalian tetap bebas mau pakai tipedata/nama apa saja)
- Kondisi: akan dilakukan perulangan apabila kondisi adalah BENAR atau TRUE dan berhenti apabila kondisi adalah SALAH atau FALSE
- Update: digunakan untuk meng-update nilai dari pencacah (biasanya berupa increment/decrement). Proses ini akan dieksekusi setelah isi dari `for statement` habis

**Note!!!**

Perhatikan urutan dari setiap komponen karena ketiganya harus berurutan serta perhatikan pemisah dari setiap komponen yaitu menggunakan `;` bukan `,`!

## Contoh penggunaan
```c
for( int i=0; i<3; i++ ){
    printf("Aku berada di dalam for statement\n");
}
```
Output:
```
Aku berada di dalam for statement
Aku berada di dalam for statement
Aku berada di dalam for statement
```
Analisa:
1. Variabel `i` **diinisialisasi** sebagai pencacah. Nilai awal dari `i` adalah 0
2. **Kondisi** `i<3` adalah **BENAR** (0 lebih kecil daripada 3) sehingga isi dari `for statement` dieksekusi
3. Setelah dieksekusi, dilakukan proses **update** sehingga nilai dari `i` adalah 1
4. **Kondisi** `i<3` adalah **BENAR** (1 lebih kecil daripada 3) sehingga isi dari `for statement` dieksekusi
5. Setelah dieksekusi, dilakukan proses **update** sehingga nilai dari `i` adalah 2
6. **Kondisi** `i<3` adalah **BENAR** (2 lebih kecil daripada 3) sehingga isi dari `for statement` dieksekusi
7. Setelah dieksekusi, dilakukan proses **update** sehingga nilai dari `i` adalah 3
8. **Kondisi** `i<3` adalah **SALAH** (3 TIDAK lebih kecil daripada 3) sehingga proses perulangan `for statement` selesai

**Note!!!**

Perhatikan tanda pertidaksamaan yang digunakan!
- apabila i=0 dan kondisi i<10 maka akan dilakukan loop sebanyak 10 kali
- apabila i=0 dan kondisi i<=10 maka akan dilakukan loop sebanyak 11 kali
- apabila i=1 dan kondisi i<10 maka akan dilakukan loop sebanyak 9 kali

## Extras

1. Pastikan pencacah mampu untuk _keluar_ dari kondisi perulangan. Contoh gagal:
```c
for( int i=5; i>=0; i++ ){
    printf("Hello");
}
```
Pada kode di atas, sampai kapanpun `i` diincrement pasti akan selalu lebih besar dari 0 sehingga akan menghasilkan _infinite loop_ dan program kalian tidak akan berhenti melakukan perulangan

[>> Materi Selanjutnya (Perulangan menggunakan "do...while") >>](#)

