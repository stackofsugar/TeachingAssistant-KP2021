[<< Materi Sebelumnya (Silabus) <<](../silabus.md)
# 3.1 - Pemilihan dengan Switch

Switch case sangat berguna ketika ingin melakukan perbandingan untuk banyak kasus

## Syntax:

```c
switch (/* expression */)
{
    case /* konstan */:
        /* perintah... */
        break; /* opsional */

    case /* konstan */:
        /* perintah... */
        break; 
        
    default:  /* opsional */
        break; 
}
```


## Penjelasan:

Contoh penggunaan switch dalam program C adalah sebagai berikut:
- ketika `pilihan` bernilai 1 maka potongan kode dibawah akan menampilkan **kamu memilih angka 1**
- ketika `pilihan` bernilai 2 maka potongan kode dibawah akan menampilkan **kamu memilih angka 2**
- ketika `pilihan` **tidak** bernilai 1 atau 2 maka potongan kode dibawah akan menampilkan **kamu tidak memilih angka 1 dan 2**

```c
switch (pilihan)
{
    case 1:
        printf("kamu memilih angka 1\n");
        break; 

    case 2:
        printf("kamu memilih angka 2\n");
        break; 
        
    default:  
        printf("kamu tidak memilih angka 1 dan 2\n");
        break; 
}
```

**switch** statement bisa memiliki **case: labels** sebanyak-banyaknya asalkan setiap **label** bernilai konstan dan unik.

**break** merupakan hal yang penting dalam switch, karena jika tidak digunakan maka semua pernyataan setelah **label yang cocok**, akan dijalankan atau dieksekusi sampai ketemu **break**. contohnya: 

- ketika `pilihan` bernilai 1 maka potongan kode dibawah akan menampilkan <br> **aku 1** <br> **aku 2**
- ketika `pilihan` bernilai 2 maka potongan kode dibawah akan menampilkan <br> **aku 2**
- ketika `pilihan` bernilai 3 maka potongan kode dibawah akan menampilkan <br> **aku 3** <br> **aku 4** <br> **aku default**


```c
switch (pilihan)
{
    case 1:
        printf("aku 1\n");

    case 2:
        printf("aku 2\n");
        break;

    case 3:
        printf("aku 3\n");

    case 4:
        printf("aku 4\n");
        
    default:  
        printf("aku default\n");
}
```

### Case Ranges:
Case Ranges adalah ekstension dari bahasa C yang berarti ini bukan C standar (tidak bisa digunakan pada semua compiler C)

Cara menggunakannya seperti ini:
```
case rendah ... tinggi
```
Dengan menggunakan Case Ranges penulisan code menjadi lebih cepat dan mudah dibaca.<br> Berikut perbandingannya:
- Tidak menggunakan Case Ranges
  ```c
    switch (pilihan)
    {
        case 1:
        case 2:
        case 3:
        case 4:
        case 5:
            printf("angkamu diantara 1 - 5\n");
            break;
    }
  ```
- Menggunakan Case Ranges
  ```c
    switch (pilihan)
    {
        case 1 ... 5:
            printf("angkamu diantara 1 - 5\n");
            break;
    }
    ```

### Source code
<details>
  <summary>Contoh Source Code</summary>

  ```c
#include <stdio.h>

int main() {
    double angkaPertama, angkaKedua, hasil;
    char op;
    printf("Masukkan Angka Pertama, Operator, Angka Kedua. yang mana Operatornya diantara (+, -, *, /): ");
    scanf("%lf %c %lf", &angkaPertama, &op, &angkaKedua);

    switch (op) {
        case '+':
            hasil = angkaPertama + angkaKedua;
            break;
        case '-':
            hasil = angkaPertama - angkaKedua;
            break;
        case '*':
            hasil = angkaPertama * angkaKedua;
            break;
        case '/':
            hasil = angkaPertama / angkaKedua;
            break;
        default:
            printf("Operator mu salah");
    }
    printf("%.1lf %c %.1lf = %.1lf\n", 
        angkaPertama, op, angkaKedua, hasil);
}
  ```
</details>

[>> Materi Berikutnya (Perulangan menggunakan "for") >>](2-PerulanganMenggunakanFor.md) 
