[<< Array dan Linked List](1-ArrayLinkedList.md)

# 10.2 - Stack dan Queue

**Stack** dan **queue** merupakan suatu struktur data yang memiliki operasi-operasi tertentu sesuai dengan definisinya masing-masing. Karena sering melibatkan penambahan dan penghapusan elemen, maka struktur data ini cocok diterapkan menggunakan **linked list** dengan demikian dapat dikatakan sebagai struktur data turunan dari linked list.

## Stack

Stack dapat digambarkan sebagai struktur data yang dapat mensimulasikan **tumpukan**. Terdapat tiga operasi utama dalam stack yaitu: **push**, **pop**, dan **top**.

### Operasi Push

Menambahkan elemen ke tumpukan paling atas stack. Untuk kasus `struct Weapon`, dapat menggunakan code berikut:
```c
void weapons_push(struct WeaponList *stack, const struct Weapon *data) {
    /* misalkan tumpukan paling atas adalah elemen terakhir linked list */

    /* tambahkan ke posisi terakhir linked list */
    insertWeapon(stack, stack->last, data);
}
```

### Operasi Pop

Menghapus elemen dari tumpukan paling atas stack. Untuk kasus `struct Weapon`, dapat menggunakan code berikut:
```c
void weapons_pop(struct WeaponList *stack) {
    /* misalkan tumpukan paling atas adalah elemen terakhir linked list */

    /* hapus dari posisi terakhir linked list */
    deleteWeapon(stack, stack->last);
}
```

### Operasi Top

Mengakses elemen/node yang terletak pada tumpukan paling atas stack. Untuk kasus `struct Weapon`, dapat menggunakan code berikut:
```c
struct WeaponNode *weapons_top(struct WeaponList *stack) {
    /* misalkan tumpukan paling atas adalah elemen terakhir linked list */

    /* akses posisi terakhir linked list */
    return stack->last;
}
```

## Queue

Queue dapat digambarkan sebagai struktur data yang dapat mensimulasikan **antrean**. Terdapat tiga operasi utama dalam queue yaitu: **enqueue**, **dequeue**, dan **head**

### Operasi Enqueue

Menambahkan elemen ke urutan akhir antrean. Untuk kasus `struct Weapon`, dapat menggunakan code berikut:
```c
void weapons_enqueue(struct WeaponList *queue, const struct Weapon *data) {
    /* misalkan urutan pertama antrean adalah elemen pertama linked list */
    /* dan urutan terakhir antrean adalah elemen terakhir linked list */

    /* tambahkan ke urutan terakhir antrean (elemen terakhir linked list) */
    insertWeapon(queue, queue->last, data);
}
```

### Operasi Dequeue

Menghapus elemen di urutan pertama antrean. Untuk kasus `struct Weapon`, dapat menggunakan code berikut:
```c
void weapons_dequeue(struct WeaponList *queue) {
    /* misalkan urutan pertama antrean adalah elemen pertama linked list */
    /* dan urutan terakhir antrean adalah elemen terakhir linked list */

    /* hapus urutan pertama antrean (elemen pertama linked list) */
    deleteWeapon(queue, queue->first);
}
```

### Operasi Head

Mengakses elemen/node yang berada di urutan pertama antrean. Untuk kasus `struct Weapon`, dapat menggunakan code berikut:
```c
struct WeaponNode *weapons_head(struct WeaponList *queue) {
    /* misalkan urutan pertama antrean adalah elemen pertama linked list */
    /* dan urutan terakhir antrean adalah elemen terakhir linked list */

    /* akses posisi pertama linked list */
    return queue->first;
}
```

[Tree >>](3-Tree.md)
