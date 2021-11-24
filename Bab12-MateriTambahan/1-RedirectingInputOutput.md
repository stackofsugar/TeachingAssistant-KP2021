# Redirecting I/O

Secara default, kita menerima input dari **keyboard** dan mengeluarkan output ke **layar**. Keduanya merupakan standard input (stdin) dan standard output (stdout).
Kita dapat mengatur dari mana input didapat dan ke mana output akan dikeluarkan menggunakan **Redirecting I/O** atau pembelokkan input/output

Redirecting I/O termasuk dalam OS-dependant yang mana kemungkinan terdapat perbedaan antara OS

## Format
Semua operator berikut merupakan binary operator yang mana memiliki left operand dan right operand
```
left_operand operator right_operand
```
## Redirecting Input

### Operator <
Operator ini akan membelokkan file pada operand kanan sebagai input untuk operand kiri (yang merupakan executable)

Contoh penggunaan (pada Linux):
```
$ cat < myfile.txt
```

### Operator |
Operator yang sering disebut _pipe_ ini akan membelokkan output dari operand kiri sebagai input untuk operand kanan dengan kedua operand merupakan sebuah executable

Contoh penggunaan (pada Linux):
```
$ who | sort
```

## Redirecting Output

### Operator >
Operator ini membelokkan output dari operand kiri (executable) sebagai input untuk file pada operand kanan
Jika operand kanan sudah memiliki isi (tidak kosong), maka pembelokkan ini mengakibatkan isi tersebut dihapus dan ditimpa dengan output baru.

### Operator >>
Operator ini mirip seperti operator > tetapi **tidak** menimpa isi dari operand kanan melainkan **append** atau melanjutkan isinya

### Contoh Redirecting Output
Anggap file test1.txt dan test2.txt keduanya memiliki isi
```
Lorem Ipsum
Dolor Sit Amet
```
Lalu terdapat program sederhana redir_o.c sebagai berikut
```c
#include <stdio.h>

int main(){
    printf("Hello World\n");
}
```
Setelah itu kita mengcompile (menggunakan gcc) ```gcc redir_o.c -o redir_o.exe``` sehingga kita dapatkan executablenya

Jika anda menjalankan ```./redir_o.exe > test1.txt``` maka isi test1.txt akan berubah menjadi
```
Hello World
```

JIka anda menjalankan ```./redir_o.exe >> test2.txt```, apakah anda bisa menebak apa yang akan terjadi pada isi test2.txt?
