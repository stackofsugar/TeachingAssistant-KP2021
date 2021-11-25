# 12.2 - Variable-Length Arguments

Pernahkan kalian berpikir bagaimana mekanisme fungsi **printf** dan **scanf** sehingga dapat menerima argumen yang jumlah dan tipe datanya berbeda-beda? Sebagai contoh:
```c
printf("My name is %s\n", name); /* menerima 2 argumen (2 string) */
printf("My name is %s and I am %d years old\n", name, age); /* menerima 3 argumen (2 string dan 1 int) */
```

Ternyata, beginilah bentuk umum deklarasi **printf** pada file **stdio.h**:
```c
int printf(const char *format, ...); /* terdapat argumen yang terdeklarasi sebagai: ... */
```

Hal itu disebut dengan **Variable-Length Argument**. Dinamakan seperti itu karena jumlah argumen yang dimasukkan bisa bervariasi tergantung dengan penggunaan. Fungsi yang menerima variable-length argument juga dapat disebut dengan **variadic function**.

Library/header yang berurusan dengan variable-length arguments adalah header **stdarg.h** yang memiliki 4 definisi utama:

- **va_list** - tipe data untuk menampung instance variable-length arguments
- **va_start(ap, param)** - macro untuk menginisialisasikan instance *ap* (bertipe *va_list*) dan pembacaan variable-length argumen dimulai setelah parameter *param*
- **va_arg(ap, type)** - macro untuk mendapatkan argumen berikutnya pada *ap* (bertipe *va_list*), dilengkapi keterangan tipe data yang digunakan
- **va_end(ap)** - macro untuk membebaskan memori yang digunakan *ap*

## Contoh Penggunaan

Menjumlahkan seluruh argumen dengan variadic function:
```c
#include <stdio.h>
#include <stdarg.h>

/* fungsi untuk menjumlahkan angka sebanyak `n` pada variable-length argument */
int sum(int n, ...) {
    int i;
    int result = 0;
    va_list ap;

    va_start(ap, n); /* variable-length argument dimulai setelah parameter `n` */
    for (i = 0; i < n; i++) {
        result = result + va_arg(ap, int); /* baca nilai berikutnya pada variable-length argument dengan tipe `int` */
    }
    va_end(ap);

    return result;
}

int main() {
    printf("32+14+29 = %d\n", sum(3, 32, 14, 29));
    printf("1+2+3+4+5 = %d\n", sum(5, 1, 2, 3, 4, 5));

    return 0;
}

/*
Output:

32+14+29 = 75
1+2+3+4+5 = 15
*/
```

Menggabungkan banyak string dengan variadic function
```c
#include <stdio.h>
#include <stdarg.h>
#include <string.h>

/* fungsi untuk menggabungkan banyak string sampai ditemukan `NULL` dan hasilnya disimpan dalam string `dest` */
void compose(char *dest, ...) {
    va_list ap;
    const char *str;
    int i = 0;

    va_start(ap, dest); /* variable-length argument dimulai setelah parameter `dest` */
    while ((str = va_arg(ap, const char *)) != NULL) { /* baca nilai berikutnya pada variable-length argument dengan tipe `const char *` */
        if (i == 0) {
            strcpy(dest, str); /* gunakan `strcpy` jika merupakan suku pertama */
        } else {
            strcat(dest, str); /* gunakan `strcat` jika merupakan suku kedua dan berikutnya */
        }
        i++;
    }
    va_end(ap);
}

int main() {
    char str[100];

    compose(str, "Hello, ", "world!", " My name is ", "John", NULL);
    printf("%s\n", str);

    return 0;
}

/*
Output:

Hello, world! My name is John
*/
```

Fungsi tiruan **printf**:
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdarg.h>

void print_string(const char *str);
void print_num(int n);

/* fungsi untuk menirukan `printf` */
/* asumsi fungsi `printf` tidak ada sehingga menggunakan fungsi `putchar` semuanya */
void print(const char *format, ...) {
    va_list ap;
    int i;

    va_start(ap, format);

    i = 0;
    while (format[i] != '\0') {
        if (format[i] == '?') {
            char type;

            type = format[i + 1];
            if (type == 's') {
                /* print string jika terdapat ?s */
                print_string(va_arg(ap, const char *));
            } else if (type == 'i') {
                /* print integer jika terdapat ?i */
                print_num(va_arg(ap, int));
            } else if (type == '?') {
                /* print tanda tanya jika terdapat ?? */
                putchar('?');
            }
            i = i + 2;
        } else {
            putchar(format[i]);
            i = i + 1;
        }
    }
    
    va_end(ap);
}

int main() {
    print("Hello world! My name is ?s and I am ?i years old\n", "John", 32);
    print("Temperature is ?i celcius\n", -5);
    print("How are you??\n");
    return 0;
}

void print_string(const char *str) {
    int i;

    for (i = 0; str[i] != '\0'; i++) {
        putchar(str[i]);
    }
}

void __print_num(int n, int i) {
    if (n == 0) {
        if (i == 0) {
            putchar('0');
        }
        return;
    }

    if (i == 0) {
        if (n < 0) {
            putchar('-');
        }
    }
    __print_num(abs(n) / 10, i + 1);
    putchar((char)((abs(n) % 10) + '0'));
}

void print_num(int n) {
    __print_num(n, 0);
}

/*
Output:

Hello world! My name is John and I am 32 years old
Temperature is -5 celcius
How are you?
*/
```
