[<< Materi Sebelumnya (Struct dan Union)](1-StructUnion.md)

# 8.2 - Bit Manipulation

Apa itu Bit Manipulation? Bit Manipulation adalah tindakan memanipulasi bit secara algoritmik atau data lain yang lebih pendek atau kecil dari satu byte. Dan bahasa C sangat efisien dalam melakuakn memanipulasi bit ini.

Sayangnya Bahasa C tidak memiliki fungsi bawaan untuk menampilkan angka dalam bentuk binary jadi kita harus membuat fungsi kita sendiri. Berikut contohnya:
```c
#include <stdio.h>

int BIT_LENGTH;

void printBinary(unsigned int n) {
    for (unsigned int i = 1 << (BIT_LENGTH - 1); i > 0; i /= 2) {
        if ((n & i) != 0) {
            printf("1");
        }
        else {
            printf("0");
        }
    }
}

int main() {
    BIT_LENGTH = 4;
    printf("Angka 5 Dalam bentuk binary = ");
    printBinary(5);
    printf("\n");
    printf("Angka 2 Dalam bentuk binary = ");
    printBinary(2);
    printf("\n");
}

/*
Output:
Angka 5 Dalam bentuk binary = 0101
Angka 2 Dalam bentuk binary = 0010
*/

```
Cara diatas mungkin bukan cara yang terbaik untuk mencetak angka dalam bentuk binary, tetapi yang penting adalah kita dapat memahami binary-nya terlebih dahulu.

## Bitwise Operators

| Operator   | Nama Operator        |
|:----------:|:--------------------:|
| &          | Bitwise AND          | 
| \|         | Bitwise OR           | 
| ^          | Bitwise XOR          | 
| ~          | Bitwise NOT (unary)  | 
| <<         | Left shift           | 
| >>         | Right shift          | 


### Bitwise AND ( & )
Operator biner yang beroperasi dengan melakukan perbandingan pada tiap bit. **Jika kedua bit yang dibandingkan bernilai 1**, makahasil bitnya adalah 1, jika tidak 0.
```
Contoh 9 & 5

9 --> 1001
5 --> 0101
      ----
    = 0001 => 1
```
```c
#include <stdio.h>

int BIT_LENGTH;
void printBinary(unsigned int n);

int main() {
    BIT_LENGTH = 4;
    printf("Hasil dari 9 & 5 = %d\n", (9 & 5));
    printBinary(9);
    printf("\n");
    printBinary(5);
    printf("\n");
    printf("------ &\n");
    printBinary(9 & 5);
    printf("\n");
}
```

### Bitwise OR ( | )
Operator biner yang beroperasi dengan melakukan perbandingan pada tiap bit. **Jika salah satu atau kedua bit yang dibandingkan bernilai 1**, maka hasil bitnya adalah 1, jika tidak 0.

```
Contoh 9 | 5

9 --> 1001
5 --> 0101
      ----
    = 1101 => 13
```
```c
#include <stdio.h>

int BIT_LENGTH;
void printBinary(unsigned int n);

int main() {
    BIT_LENGTH = 4;
    printf("Hasil dari 9 | 5 = %d\n", (9 | 5));
    printBinary(9);
    printf("\n");
    printBinary(5);
    printf("\n");
    printf("------ |\n");
    printBinary(9 | 5);
    printf("\n");
}
```

### Bitwise XOR ( ^ )
Operator biner yang beroperasi dengan melakukan perbandingan pada tiap bit. **Jika salah satu bit yang dibandingkan bernilai 1 (bukan keduanya)**, maka hasil bitnya adalah 1, jika tidak 0.

```
Contoh 9 ^ 5

9 --> 1001
5 --> 0101
      ----
    = 1100 => 12
```
```c
#include <stdio.h>

int BIT_LENGTH;
void printBinary(unsigned int n);

int main() {
    BIT_LENGTH = 4;
    printf("Hasil dari 9 ^ 5 = %d\n", (9 ^ 5));
    printBinary(9);
    printf("\n");
    printBinary(5);
    printf("\n");
    printf("------ ^\n");
    printBinary(9 ^ 5);
    printf("\n");
}
```

### Bitwise NOT ( ~ )
Bitwise NOT adalah operator unary yang membalik bit angka. Jika bit ke-i adalah 0, maka akan dibalik menjadi 1 dan begitu pula sebaliknya.

```
Contoh ~9

9 --> 1001
      ----
    = 0110 => 6
```
```c
#include <stdio.h>

int BIT_LENGTH;
void printBinary(unsigned int n);

int main() {
    BIT_LENGTH = 4;
    printf("Hasil dari ~9 = %d\n", ~9 & 15);
    printBinary(9);
    printf("\n");
    printf("------ ~\n");
    printBinary(~9);
    printf("\n");
}
```
Kenapa kita menggunakan **& 15** dalam operasi diatas?
Hal ini karena operator NOT bekerja dengan membalikkan semua bit, tidak bisa dibatasi.<br>
Misalnya:<br>
&nbsp; 9 = ...0000 0000 0000 1001<br>
~9 = ...1111 1111 1111 0110<br>

Dan hasilnya akkan menjadi -10 atau angka yang sangat besar jika dalam bilangan positif oleh karena itu dengan menggunakan **AND 15** kita dapat memotong bit tersebut ke jumlah bit yang kita inginkan (4 bit)

~9 = ...1111 1111 1111 0110<br>
15 = ...0000 0000 0000 1111<br>
-------------------------------- &

Hasilnya menjadi 0110 atau 6

### Right Shift ( >> )
Operator biner yang beroperasi dengan melakukan **Shift atau Geser Kanan** sebanyak *n* kali dengan *n* adalah nilai yang berada setelah operator >>. 

```
Contoh 51

51 -----> 00110011
51 >> 1 = 00011001
51 >> 3 = 00000110
```
```c
#include <stdio.h>

int BIT_LENGTH;
void printBinary(unsigned int n);

int main() {
    BIT_LENGTH = 8;
    printf("Hasil dari 51 >> 1 = %d\n", (51 >> 1));
    printBinary(51);
    printf("\n");
    printf("-------- >>\n");
    printBinary(51 >> 1);
    printf("\n\n");
    printf("Hasil dari 51 >> 3 = %d\n", (51 >> 3));
    printBinary(51);
    printf("\n");
    printf("-------- >>\n");
    printBinary(51 >> 3);
    printf("\n");
}
```

### Left Shift ( << )
Operator biner yang beroperasi dengan melakukan **Shift atau Geser Kiri** sebanyak *n* kali dengan *n* adalah nilai yang berada setelah operator <<. 

```
Contoh 51

51 -----> 00110011
51 << 1 = 01100110
51 << 3 = 10011000
```
```c
#include <stdio.h>

int BIT_LENGTH;
void printBinary(unsigned int n);

int main() {
    BIT_LENGTH = 8;
    printf("Hasil dari 51 << 1 = %d\n", (51 << 1 & 0xFF));
    printBinary(51);
    printf("\n");
    printf("-------- <<\n");
    printBinary(51 << 1);
    printf("\n\n");
    printf("Hasil dari 51 << 3 = %d\n", (51 << 3 & 255));
    printBinary(51);
    printf("\n");
    printf("-------- <<\n");
    printBinary(51 << 3);
    printf("\n");

    /*
    0xFF adalah bilangan hexadecimal yang nilainya = 255 = 1111 1111 (dalam bit) yang digunakan untuk memotong angka menjadi 8 bit
    */
}
```

[Materi Selanjutnya (Enumeration) >>](3-Enum.md)
