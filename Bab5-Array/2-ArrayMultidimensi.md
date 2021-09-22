[<< Materi Sebelumnya (Pengenalan Array)](1-PengenalanArray.md)

# 5.2 - Array Multidimensi

**Array multidimensi** (*multidimensional array*) adalah array yang memiliki lebih dari satu baris. Perhatikan potongan kode di bawah ini.

```c
int arr[] = { 1, 2, 3, 4, 5 };
```

Dalam memori akan direpresentasikan sebagai:

```
arr[0] -> 1
arr[1] -> 2
arr[2] -> 3
arr[3] -> 4
arr[4] -> 5
```

Bagaimana jika kita ingin membuat representasi vektor dua dimensi (seperti dibawah) menggunakan array di C?

```
1 2 3
4 5 6
7 8 9
```

**Array multidimensi** dapat menjawab pertanyaan tersebut. Array multidimensi dapat dideklarasikan seperti potongan kode di bawah ini.

```c
int x[3][4];
```

Elemen-elemen dalam di atas dapat direpresentasikan sebagai:

![Representasi array 2 dimensi](https://cdn.programiz.com/sites/tutorial2program/files/two-dimensional-array_0.jpg)

Selain itu, kita juga dapat membuat array dengan dimensi yang lebih besar, seperti array tiga dimensi. Kita dapat mendeklarasikannya seperti potongan kode di bawah ini.

```c
int arr[2][3][4];
```

## Inisialisasi
Seperti pada array pada materi sebelumnya, kita dapat menginisiasi array multidimensi baik secara langsung atau satu persatu.

### Secara langsung
Karena ini merupakan array lebih dari 1 dimensi, maka tidak bisa digunakan `{elemen0, elemen1, elemen2}`, namun dengan `{{elemen0.0, elemen0.1, elemen0.2}, {elemen1.0, elemen1.1, elemen1.2}}` pada array 2 dimensi. Cara inisiasinya juga ada berbagai macam, seperti potongan kode di bawah ini.

```c
int arr1[2][3] = {{1, 3, 0}, {-1, 5, 9}};
         
int arr2[][3] = {{1, 3, 0}, {-1, 5, 9}};
                
int arr3[2][3] = {1, 3, 0, -1, 5, 9};
```
> Ketiga cara di atas menghasilkan array yang sama.

### Satu persatu

```c
int arr[2][2];

arr[0][0] = 1;
arr[0][1] = 2;
arr[1][0] = 3;
arr[1][1] = 4;
```

## Cara Mengakses
Array multidimensi dapat diakses sebagaimana array 1 dimensi di akses, yaitu dengan menggunakan operator `[]`. Perhatikan potongan kode di bawah.

```c
                //     0          1          2
                //  0  1  2    0  1  2    0  1  2
int arr2d[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};

/*
arr2d[0][1] = 2
arr2d[2][2] = 9
arr2d[1][2] = 6
*/
```

Cara yang sama dapat diaplikasikan ke array 3 dimensi. Perhatikan contoh di bawah.

```c
                  //         0                 1
                  //     0       1         0       1
                  //    0  1    0  1      0  1    0  1
int arr3d[2][2][2] = {{{1, 2}, {3, 4}}, {{5, 6}, {7, 8}}};

/*
arr3d[0][0][0] = 1
arr3d[1][0][1] = 6
arr3d[0][1][1] = 4
*/
```

Biasanya, programmer mengakses array multidimensi dengan menggunakan perulangan `for` atau sejenisnya. Perhatikan contoh kode di bagian paling bawah untuk mempelajarinya.

<details>
  <summary>Contoh penggunaan array 2 dimensi</summary>
  
```c
#include <stdio.h>

int main() {
    int matrix_num_row, matrix_num_col, matrix[100][100];
    // Menggunakan [100][100] karena [variabel1][variabel2] tidak kompatibel di semua compiler

    printf("== Aplikasi Pembuat Matriks 2D ==\nJumlah baris matriks yang ingin kamu buat: ");
    scanf("%d", &matrix_num_row);
    printf("Jumlah kolom matriks yang ingin kamu buat: ");
    scanf("%d", &matrix_num_col);

    if ((matrix_num_col > 100) || (matrix_num_row > 100)) {
        printf("Maaf, jumlah maksimal kolom dan baris adalah 100\n");
        return 1;
    }

    printf("Masukkan matriks anda baris demi baris di bawah:\n");

    for (int i = 0; i < matrix_num_row; i++) {
        for (int j = 0; j < matrix_num_col; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }

    printf("Matrix anda:\n");

    for (int i = 0; i < matrix_num_row; i++) {
        for (int j = 0; j < matrix_num_col; j++) {
            printf("%d ", matrix[i][j]);
        }
        printf("\n");
    }
}

/* Contoh output:
== Aplikasi Pembuat Matriks 2D ==
Jumlah baris matriks yang ingin kamu buat: 2
Jumlah kolom matriks yang ingin kamu buat: 3
Masukkan matriks anda baris demi baris di bawah:
1 2 3
4 5 6
Matrix anda:
1 2 3
4 5 6
*/
```
  
</details>
  
[Materi Selanjutnya (Array Sebagai Parameter Fungsi) >>](3-ArraySebagaiParameterFungsi.md)
