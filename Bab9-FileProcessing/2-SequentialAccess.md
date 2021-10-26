[<< Pengantar File Processing](1-Pengantar.md)

# 9.2 - Sequential Access

**Sequential access** menyimpulkan bahwa file dapat direpresentasikan sebagai kumpulan karakter atau bytes yang panjangnya tidak diketahui. File berjenis **plaintext** umumnya dioperasikan secara sequential access. Dengan demikian, pembahasan seputar topik ini hanya seputar file berjenis plaintext saja.

## Operasi Pembacaan (Read)

Dalam membaca file berjenis plaintext, dapat menggunakan beberapa fungsi pada header **stdio.h** seperti: `fscanf`, `fgetc`, dan `fgets`. Cara penggunaan tiap-tiap fungsi tersebut dapat dilihat [di sini](https://cplusplus.com/reference/cstdio/).

Namun dalam kali ini kita akan membahas yang `fscanf` saja. Pada dasarnya, `fscanf` memiliki kinerja yang hampir mirip dengan fungsi `scanf`. Perhatikan contoh berikut:

Isi file **biodata.txt** sebelumnya:
```
Michael_Raditya
Informatika
2020
```

```c
FILE *f;

printf("Memuat dari biodata.txt ...");
f = fopen("biodata.txt", "r");
if (f != NULL) {
    char nama[100];
    char prodi[50];
    int angkatan;

    fscanf(f, "%s", nama);
    fscanf(f, "%s", prodi);
    fscanf(f, "%d", &angkatan);

    printf("Nama : %s\n", nama);
    printf("Prodi : %s\n", prodi);
    printf("Angkatan : %d\n", angkatan);

    fclose(f);
} else {
    printf("Tidak dapat membaca file biodata.txt"\n);
}

/*
Output:

Memuat dari biodata.txt ...
Nama : Michael_Raditya
Prodi : Informatika
Angkatan : 2020
*/
```

## Operasi Penulisan (Write)

Dalam menulis file berjenis plaintext, dapat menggunakan beberapa fungsi pada header **stdio.h** seperti: `fprintf`, `fputc`, dan `fputs`. Cara penggunaan tiap-tiap fungsi tersebut dapat diliht [di sini](https://cplusplus.com/reference/cstdio/)

```c
FILE *f;
char nama[100];
char prodi[50];
int angkatan;

printf("Masukkan nama : ");
scanf("%s", nama);

printf("Masukkan prodi : ");
scanf("%s", prodi);

printf("Masukkan angkatan : ");
scanf("%d", &angkatan);

printf("Menyimpan ke biodata.txt ...\n");
f = fopen("biodata.txt", "w");
if (f != NULL) {
    fprintf(f, "%s\n", nama);
    fprintf(f, "%s\n", prodi);
    fprintf(f, "%d\n", angkatan);
    fclose(f);
    printf("Sukses!\n");
} else {
    printf("Tidak dapat menulis ke file biodata.txt");
}

/*
Output:

Masukkan nama : Adriel_Alfeus
Masukkan prodi : Informatika
Masukkan angkatan : 2020
Menyimpan ke biodata.txt ...
Sukses!
*/
```

Isi file **biodata.txt** setelahnya:
```
Adriel_Alfeus
Informatika
2020
```

## Rewind

Kursor yang merujuk ke lokasi target operasi pembacaan/penulisan berikutnya dalam file sequential-access (plaintext) dapat direset menggunakan fungsi **rewind()** pada **stdio.h** dengan deklarasi sebagai berikut:
```c
void rewind(FILE *f);
```
Fungsi tersebut mengatur kursor pada file `f` supaya dikembalikan ke lokasi kursor pada awal file.

Namun patut diperhatikan bahwa operasi penulisan setelah dilakukan rewind dapat merusak representasi data yang ada di dalam file. Oleh karena itu, gunakanlah saja dengan berhati-hati apabila akan melibatkan penulisan ke dalam file lagi.

Sebagai contoh:
```c
FILE *f;

/* ... */

fprintf(f, "Lorem ipsum dolor\n");
rewind(f);
fprintf(f, "sit amet\n");
```

[Random Access >>](3-RandomAccess.md)