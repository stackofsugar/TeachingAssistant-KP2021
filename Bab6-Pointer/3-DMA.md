[<< Pass By Reference](2-PassByRef.md)

# 6.3 - Dynamic Memory Allocation

Apa itu Dynamic Memory Allocation? **Dynamic Memory Allocation (DMA)** adalah suatu teknik di mana kita mengalokasikan sebuah memori untuk diisi dengan suatu data guna dipertahankan sampai program selesai berjalan. Karena memori berkaitan erat dengan pointer (yang mana pointer merupakan penunjuk ke suatu alamat memori), maka konsep ini tidak dapat dipisahkan dari pointer.

Perhatikan kode berikut:
```c
if (choice == 1) {
    /* Variabel `data` terletak pada suatu alamat memori tertentu, sebut saja X */
    int data = 5;

    /* Di sini, alamat memori X masih berisi variabel `data` */
    printf("Data: %d\n", data);
}
/* Namun di sini, alamat memori X sudah tidak berisi apapun lagi */
/* Dikarenakan variabel `data` telah dihancurkan pada scope sebelumnya karena sudah keluar dari batasan scope */
```

Lalu perhatikan modifikasi berikut:
```c
int *address;
int choice = 1;

/* ... */

if (choice == 1) {
    /* Lakukan dynamic memory allocation untuk mengalokasikan int berukuran 4 byte pada pointer menggunakan fungsi malloc() pada stdlib.h */
    /* Misalkan hasilnya yang berupa pointer mengarah ke alamat memori X */
    int *data = (int *)malloc(sizeof(int));

    *data = 5;

    /* Di sini, alamat memori X berisi nilai dari memori yang ditunjuk oleh pointer `data` */
    /* Pointer `data` mengarah ke suatu memori (X), tetapi tidak mengarah ke variabel apapun pada program */ 
    /* Hal ini berbeda dengan topik sebelumnya, yang mana pointer-pointer pada topik sebelumnya selalu dibuat mengarah ke variabel tertentu */
    printf("Data: %d\n", *data);

    /* Catat alamat memori X tersebut ke dalam variabel `address` */
    address = data;
}
/* Dan di sini, alamat memori X juga masih berisi nilai yang terkandung pada `data` meskipun sudah keluar dari scope sebelumnya */
/* Di sini `address` merujuk ke alamat memori X */
/* Lakukan dereferencing untuk mengakses nilainya */
printf("Data: %d\n", *address);

/*
Output:

Data: 5
Data: 5
*/
```

Sehingga dynamic memory allocation menjamin bahwa data yang terletak pada memori yang telah dialokasikan akan tetap bertahan sampai program exit (atau sampai memori tersebut dihancurkan/dibebaskan dengan fungsi **free**). Kita akan bahas fungsi **malloc** dan **free** setelah ini.

## Fungsi stdlib.h: malloc() dan free()

Fungsi **malloc()** dan **free()** keduanya terletak pada header **stdlib.h**. Kedua fungsi tersebut merupakan dasar dari konsep manajemen memori (memory management) dalam bahasa C yang mana programmer bertanggung jawab secara penuh atas alokasi dan pembebasan memori.

### malloc()

**malloc** berguna untuk mengalokasikan memori untuk digunakan pada program.

Berikut adalah deklarasi dari fungsi **malloc()**:
```c
/*
Parameter:
- size_t size : ukuran dari memori (dalam bytes) yang akan dialokasikan (size_t adalah sinonim dari unsigned long)

Return value:
- Pointer yang menunjukkan lokasi memori yang telah dialokasikan
- Dapat dikonversi (casting) ke tipe pointer apapun sesuai dengan ukuran memorinya, sebagai contoh: (int *)malloc(sizeof(int))
*/
void *malloc(size_t size);
```
Untuk memasukkan parameter `size` bisa menggunakan kata kunci `sizeof(<Tipe Data>)`, misal `sizeof(int)` jika ingin mengalokasikan memori berjenis int(eger) dan dengan demikian, ukurannya adalah 4 bytes.

### free()

**free** berguna untuk menghancurkan/membebaskan memori yang telah digunakan pada program supaya menghemat RAM dan tidak terjadi kebocoran memori (memory leak).

Berikut adalah deklarasi dari fungsi **free()**:
```c
/*
Parameter:
- void *ptr : lokasi memori yang akan dihancurkan/dibebaskan
*/
void free(void *ptr);
```

### Contoh Implementasi

```c
int *data;

/* ... */

data = (int *)malloc(sizeof(int));
*data = 32;
printf("Data: %d\n", *data);
free(data);

/*
Output:

Data: 32
*/
```

## Array Menggunakan DMA

Pada bab sebelumnya ([Array](../Bab5-Array/1-PengenalanArray.md)) pernah disinggung bahwa menciptakan array dalam bahasa C bisa juga menggunakan konsep memory management terkhusus jika ukuran array bergantung pada suatu variabel, tepatnya menggunakan fungsi **malloc**. Berikut adalah contohnya:

```c
int *price_list;
int count;
int i;

printf("Masukkan jumlah barang : ");
scanf("%d", &count);

/* Alokasikan array of integer yang menampung elemen pada memori yang banyaknya sesuai dengan nilai pada `count` */
/* Sehingga jika terdapat 5 elemen yang dialokasikan, total kapasitas memori yang dibutuhkan adalah 20 bytes = 5 * 4 bytes */
price_list = (int *)malloc(count * sizeof(int));

for (i = 0; i < count; i++) {
    printf("Masukkan harga barang ke-%d : ", (i + 1));
    scanf("%d", &price_list[i]);
}

printf("=== LIST HARGA BARANG (Jumlah: %d) ===\n", count);
for (i = 0; i < count; i++) {
    printf("Harga barang ke-%d : $%d\n", (i + 1), price_list[i]);
}

/* Bebaskan memori apabila sudah tidak diperlukan lagi */
free(price_list);

/*
Output:

Masukkan jumlah barang : 5
Masukkan harga barang ke-1 : 750
Masukkan harga barang ke-2 : 1500
Masukkan harga barang ke-3 : 2500
Masukkan harga barang ke-4 : 3100
Masukkan harga barang ke-5 : 4750
=== LIST HARGA BARANG (Jumlah: 5) ===
Harga barang ke-1 : $750
Harga barang ke-2 : $1500
Harga barang ke-3 : $2500
Harga barang ke-4 : $3100
Harga barang ke-5 : $4750
*/
```


[Silabus >>](../silabus.md)
