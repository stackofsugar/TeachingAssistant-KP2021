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
```

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
```

[Silabus >](../silabus.md)
