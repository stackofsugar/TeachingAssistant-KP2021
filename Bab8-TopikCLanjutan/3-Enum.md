[<< Materi Sebelumnya (Bit Manipulation)](2-BitManipulation.md)

# 8.3 - Enumeration

## Pengantar

Enumeration, atau sering disebut enum, adalah sebuah tipe data non-primitif yang digunakan untuk menyimpan konstanta/banyak konstanta integer yang diinterpretasikan seperti halnya variabel. Perbedaannya adalah nilai dari enum ini tidak disimpan di memori, melainkan di-resolve kembali menuju nilai integer saat kode kalian di-compile.
Untuk lebih memahami pentingnya enum, lihatlah potongan kode di bawah ini

```c
int user_choice;
printf("Silakan pilih operasi di bawah ini!\n");
printf("[0] Keluar\n[1] Login\n[3] Register\n[4] Lain-lain\n> ");
scanf("%d", &user_choice);
```

Jika kalian atau programmer lain ingin melihat kembali kode tersebut beberapa waktu kemudian, yang kalian temukan adalah potongan kode di bawah ini.

```c
if (user_choice == 0) {
    // ...
}
else if (user_choice == 1) {
    // ...
}
else if (user_choice == 3) {
    // ...
}
// ...
```

Kalian, yang sudah lama tidak melihat kode kalian tersebut, atau programmer lain yang mungkin pertama kali melihat kode kalian pasti akan sangat kesulitan untuk memahami kode kalian, karena harus scroll atas dan bawah untuk memahami keseluruhan dari 2 potongan kode di atas. Sebagai contoh, ini contoh potongan kode yang sama, dengan menggunakan enum

```c
if (user_choice == eKeluar) {
    // ...
}
else if (user_choice == eLogin) {
    // ...
}
else if (user_choice == eRegister) {
    // ...
}
// ...
```

Terlihat lebih mudah dipahami kan? Bukan itu saja kelebihan enum, masih ada banyak hal-hal terkait optimisasi user di kode kalian yang dapat kalian capai menggunakan enum.

## Deklarasi/Definisi

Kalian dapat mendeklarasikan enum kalian dengan cara di bawah.

```c
enum NamaEnumKalian {
    nilai1,
    nilai2,
    nilai3,
    dan_lainnya
};
```

Lalu, untuk menggunakannya, kalian harus mendefinisikan penggunaan enum kalian.

```c
enum NamaEnumKalian enum_kalian;
enum NamaEnumKalian enum_kalian2 = nilai2;
```

Atau dengan cara ini, langsung mendefinisikan enum dalam deklarasi enum kalian

```c
enum NamaEnumKalian {
    nilai1,
    nilai2,
    nilai3,
    dan_lainnya
} nilai_kalian;
```

Nilai dari konstanta kalian akan di-assign mulai dari 0, sehingga `nilai1` bernilai 0, `nilai2` 1, `nilai3` 2, dan seterusnya. Nilai ini dapat kalian override dengan menambahkan tanda sama dengan dan nilai baru kalian pada saat deklarasi enum, seperti contoh di bawah ini.

```c
enum NamaHari {
    Senin = 1,
    Selasa,
    Rabu,
    Kamis = 120,
    Jumat,
    Sabtu,
    Minggu
};
```

Coba tebak/praktikkan, berapa nilai dari masing-masing elemen enum? (hint = Kalian dapat mencetak nilai enum selayaknya variabel integer).

## Penggunaan

Perhatikan kode di bawah ini.

```c
#include <stdio.h>

enum RuanganUjian {
    eRuangKelas12_A,
    eRuangKelas12_B,
    eRuangAulaBesar_A,
    eRuangAulaBesar_B,
    eRuangAulaKecil,
    eRuangSerbaguna,
};

int main() {
    enum RuanganUjian ruang_ujian = eRuangAulaKecil;

    if (ruang_ujian == eRuangAulaKecil) {
        printf("Menggunakan Ruang Aula Kecil\n");
    }
}

/*
Output:
Menggunakan Ruang Aula Kecil
*/
```

Enum dapat digunakan untuk menandai pilihan secara lebih efisien. Tanpa enum, kalian antara harus melakukan `char ruang_ujian[] = "RuangAulaKecil" ` dan melakukan `strcmp()` setiap kali mengecek yang sangat tidak efisien, atau melakukan `int ruang_ujian = 5` yang membingungkan, atau membuat variabel tiap ruangan (seperti enum tapi menggunakan variabel) yang tidak efisien, karena **tiap** variabel berbobot 4 bytes, sedangkan **seluruh** enum berbobot 4 bytes.

[Kembali ke Silabus >>](../silabus.md)
