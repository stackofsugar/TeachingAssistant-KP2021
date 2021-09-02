[< Materi Sebelumnya (Perulangan menggunakan "do...while")](3-PerulanganMenggunakanDoWhile.md)

# 3.4 - Perulangan dengan "break" dan "continue"

## break

Dalam melakukan perulangan, pasti ada suatu kasus di mana perulangan tersebut harus berhenti di tengah jalan walaupun belum mencapai saatnya untuk berhenti (kondisi masih bernilai benar untuk ulangan berikutnya). Oleh karena itu, untuk memutus perulangan di tengah jalan menggunakan kata kunci **break**. Tentunya `break` dapat digunakan untuk semua jenis perulangan (for, while, do...while).

Kode berikut hanya menampilkan "Quack!" sebanyak 5 kali
```c
int i = 1;
while (i <= 10) {
    printf("Quack!\n");
    if (i == 5) {
        /* berhenti ketika mencapai perulangan ke lima, walaupun masih bisa dilanjutkan sampai i = 10 */
        break;
    }
    i++;
}

/*
Output:

Quack!
Quack!
Quack!
Quack!
Quack!
*/
```

<details>
<summary>Contoh source code (full)</summary>

```c
#include <stdio.h>
int main() {
  int i = 1;
  while (i <= 10) {
      printf("Quack!\n");
      if (i == 5) {
          /* berhenti ketika mencapai perulangan ke lima, walaupun masih bisa dilanjutkan sampai i = 10 */
          break;
      }
      i++;
  }
  return 0;
}

/*
Output:

Quack!
Quack!
Quack!
Quack!
Quack!
*/
```      
</details>

## continue

Kita juga terkadang perlu untuk membuat suatu tahap ulangan langsung melewati (*skip*) dan menuju ke tahap ulangan berikutnya tanpa mengeksekusi sisa-sisa perintahnya. Oleh karena itu, untuk melewatkan sisa-sisa perintah dan menuju ke tahap ulangan berikutnya, kita menggunakan kata kunci **continue**. Tentunya `continue` dapat digunakan untuk semua jenis perulangan (for, while, do...while).

Kode berikut menampilkan 1 2 4 5 (angka 3 dilewatkan)
```c
int i;
for (i = 1; i <= 5; i++) {
    if (i == 3) {
        /* langsung menuju ulangan berikutnya yaitu untuk i = 4 tanpa mengeksekusi perintah-perintah setelah ini (printf) */
        /* dengan demikian, ketika i = 3, maka printf tidak tereksekusi sehingga angka 3 tidak tertampil di console */
        continue;
    }
    printf("%d ", i); /* print nilai dari variabel i */
}

/*
Output:

1 2 4 5
*/
```

<details>
<summary>Contoh source code (full)</summary>

```c
#include <stdio.h>
int main() {
    int i;
    for (i = 1; i <= 5; i++) {
        if (i == 3) {
            /* langsung menuju ulangan berikutnya yaitu untuk i = 4 tanpa mengeksekusi perintah-perintah setelah ini (printf) */
            /* dengan demikian, ketika i = 3, maka printf tidak tereksekusi sehingga angka 3 tidak tertampil di console */
            continue;
        }
        printf("%d ", i); /* print nilai dari variabel i */
    }
    return 0;
}

/*
Output:

1 2 4 5
*/
```
</details>
    
## Bonus : infinite loop

*Terima kasih kepada Hezkiel Bram Setiawan (IF 2021) karena telah berkontribusi terhadap materi tambahan namun esensial ini*

Salah satu kegunaan **break** yang penting adalah kemampuannya yang dapat memutus rantai **infinte loop** (perulangan tak terhingga), yang dalam hal ini kondisi pada perulangan *while* atau *for* selalu bernilai benar (tidak pernah salah), contohnya adalah seperti: `while (1 == 1)`, maka perulangan tersebut akan berjalan selamanya. Dengan demikian, untuk dapat keluar dari perulangan tak terhingga, perlu menggunakan kata kunci **break**

Sekarang perhatikan contoh berikut:
```c
/* while (1) dapat dinyatakan sebagai infinite loop karena kondisi (1) akan dianggap benar oleh komputer */
while (1) {
    /* bagian ini terletak dalam infinite loop */
    
    int input;
    
    printf("Masukkan 1 untuk menampilkan Quack!, masukkan 2 untuk keluar dari program: ");
    scanf("%d", &input);
    
    if (input == 1) {
        printf("Quack!\n");
    } else if (input == 2) {
        printf("Good bye :)\n");
        break; /* putuskan rantai infinite loop */
    }
}

/*
Output:

Masukkan 1 untuk menampilkan Quack!, masukkan 2 untuk keluar dari program: 1
Quack!
Masukkan 1 untuk menampilkan Quack!, masukkan 2 untuk keluar dari program: 1
Quack!
Masukkan 1 untuk menampilkan Quack!, masukkan 2 untuk keluar dari program: 2
Good bye :)
*/
```

Perulangan `for` tanpa inisialisasi, kondisi, dan update juga dapat digunakan untuk menciptakan infinite loop:
```c
for (;;) {
    /* bagian ini terletak dalam infinite loop */
    /* ... */
}
```

[Silabus >](../silabus.md)
