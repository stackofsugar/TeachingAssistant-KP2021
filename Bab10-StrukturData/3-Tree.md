[<< Stack dan Queue](2-StackQueue.md)

# Tree

## Pengertian Tree

Tree adalah sebuah struktur data non linear yang memiliki dua atau lebih "link" dan sering divisualisasikan sebagai sebuah pohon.
Komponen dari Tree ialah **node** yang berisi data dan pointer atau link untuk node berikutnya.
Tree yang memiliki _maksimal_ dua link (child kiri dan child kanan) disebut **Binary Tree**. 
Binary Tree yang mana sudah ditentukan jika child kiri memiliki nilai yang lebih kecil daripada nilai root
dan child kanan memiliki nilai yang lebih besar daripada nilai root disebut **Binary Search Tree (BST)**. Kali ini kita akan mempelajari BST

### Contoh Tree
```
        100
      /  |  \
    30  23   46
   / \       |
  10  6      2 
```
### Contoh Binary Tree
```
        100
        /  \
       32  12
      / \    \
     1  4     8
```
### Contoh Binary Search Tree
```
         50
        /  \
       12   62
      /  \  / \ 
     1  20 61 63 
```

## Insersi BST
Algoritma:
- Apabila nilai lebih besar dari root, maka pointer bergerak ke node kanan
- Apabila nilai lebih kecil dari root, maka pointer bergerak ke node kiri
- Apabila pointer menunjuk ke NULL, maka buat node baru dan simpan nilai di lokasi tersebut

### Contoh kasus
```
         20
        /  \
       12   32
      /     / \ 
     1     21  63 
```
BST di atas didapat dengan memasukan angka secara urut yaitu ``20, 12, 32, 1, 21, 63``.
Kalian dapat melihat proses insersi pada [link ini](https://www.cs.usfca.edu/~galles/visualization/BST.html)

## Traversal
Traversal adalah teknik untuk mengunjungi node-node pada tree. Saat melakukan traversal, anggap tree hanya memiliki 3 bagian yaitu root, subtree kiri, dan subtree kanan. 
Terdapat 3 jenis traversal yaitu:
- Pre Order: root, left, right
- In Order: left, root, right
- Post Order: left, right, root

### Contoh 
```
         50
        /  \
       12   62
      /  \  / \ 
     1  20 61 63 
```
Hasil PreOrder  : 50, 12, 1, 20, 62, 61, 63 \
Hasil InOrder   : 1, 12, 20, 50, 61, 62, 63 \
Hasil PostOrder : 1, 20, 12, 61, 63, 62, 50

#### Tips menghafal
root menjadi titik fokus. Cara yang menjadi _patokan_ ialah In Order dengan root di tengah.
_Pre_ artinya sebelum berarti root berada di awal.
_Post_ artinya sesudah berarti root berada di akhir.

[Silabus >>](../silabus.md)

