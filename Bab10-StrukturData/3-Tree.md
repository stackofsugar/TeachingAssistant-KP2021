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

Insersi (insertion) BST adalah proses penambahan node baru ke dalam suatu binary search tree.

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

## Source Code BST

Lihatlah dan pahami contoh source code implementasi binary search tree sederhana (insertion dan traversal) pada slides yang telah diberikan dosen pada kuliah teori.

## Contoh Penerapan BST

Pernahkah anda bertanya-tanya tentang bagaimana mengoperasikan array dengan indeks bukan berbasis angka melainkan berbasis string atau yang lain? Sebagai contoh:
```c
struct Mahasiswa {
    char nama[100];
    char prodi[50];
    int angkatan;
};

/* ... */

/* mahasiswa teridentifikasi bukan berdasarkan index angka, melainkan string berupa NIM */
printf("Nama mahasiswa: %s\n", mhsList["M0520047"].nama); /* mampukah bahasa C melakukan ini? */
```

Konsep tersebut sebenarnya sudah umum di bahasa pemrograman tingkat tinggi yang lain seperti **dictionary** dalam bahasa **Python dan C#**, **HashMap** dalam bahasa **Java**, **std::map** dalam bahasa **C++**, atau **associative array** dalam bahasa **PHP**. Sayangnya library bahasa C tidak mendukung ini sehingga harus diimplementasikan secara manual. Dan binary search tree (BST) lah yang merupakan struktur data yang berada di balik konsep-konsep tersebut. Oleh karena itu, binary search tree (BST) dapat digunakan untuk mengidentifikasi suatu elemen dalam koleksi berdasarkan suatu **key**.

Berikut adalah contoh implementasinya:
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Mahasiswa {
    char nama[100];
    char prodi[20];
    int angkatan;
};

/* merepresentasikan suatu node dalam BST */
struct MahasiswaNode {
    char key[10];           /* key: indeks berupa string yang menyatakan NIM */
    struct Mahasiswa value; /* value: data mahasiswa sesuai dengan indeks tersebut */

    /* link yang mengarah ke elemen anaknya (sisi kiri dan kanan) */
    struct MahasiswaNode *leftChild, *rightChild;
};

/* menambah mahasiswa */
/* proses insertion ke BST  */
void tambahMahasiswa(struct MahasiswaNode **tree, const char *key, const struct Mahasiswa *value) {
    if (*tree != NULL) {
        struct MahasiswaNode *curNode;

        curNode = *tree;
        if (strcmp(key, curNode->key) < 0) {
            tambahMahasiswa(&curNode->leftChild, key, value);
        } else if (strcmp(key, curNode->key) > 0) {
            tambahMahasiswa(&curNode->rightChild, key, value);
        } else {
            printf("Mahasiswa dengan NIM %s sudah ada sebelumnya\n", key);
        }
    } else {
        struct MahasiswaNode *newNode;

        newNode = (struct MahasiswaNode *)malloc(sizeof(struct MahasiswaNode));
        strcpy(newNode->key, key);
        newNode->value = *value;
        newNode->leftChild = NULL;
        newNode->rightChild = NULL;

        *tree = newNode;
    }
}

/* menampilkan secara inorder */
/* akibat: key/NIM akan ditampilkan secara terurut */
void tampilkanDataMahasiswa(struct MahasiswaNode *tree) {
    if (tree != NULL) {
        /* left */
        tampilkanDataMahasiswa(tree->leftChild);

        /* root */
        printf("%s: %s, Prodi %s, Angkatan %d\n", tree->key, tree->value.nama, tree->value.prodi, tree->value.angkatan);

        /* right */
        tampilkanDataMahasiswa(tree->rightChild);
    }
}

struct MahasiswaNode *cariMahasiswa(struct MahasiswaNode *tree, const char *key) {
    if (tree != NULL) {
        struct MahasiswaNode *curNode;

        curNode = tree;
        if (strcmp(key, curNode->key) < 0) {
            return cariMahasiswa(curNode->leftChild, key);
        } else if (strcmp(key, curNode->key) > 0) {
            return cariMahasiswa(curNode->rightChild, key);
        } else {
            return curNode;
        }
    }
    return NULL;
}

/* menghapus secara postorder */
void hapusSemuaMahasiswa(struct MahasiswaNode **tree) {
    if (*tree != NULL) {
        struct MahasiswaNode *curNode;

        curNode = *tree;
        hapusSemuaMahasiswa(&curNode->leftChild);   /* left */
        hapusSemuaMahasiswa(&curNode->rightChild);  /* right */

        /* root */
        free(curNode);
        *tree = NULL;
    }
}

/* menghapus mahasiswa berdasarkan NIM */
/* selalu beri NULL pada argumen `parent` tiap kali pemanggilan */
void hapusMahasiswa(struct MahasiswaNode **tree, const char *key, struct MahasiswaNode *parent) {
    if (*tree != NULL) {
        struct MahasiswaNode *curNode;

        curNode = *tree;
        if (strcmp(key, curNode->key) < 0) {
            hapusMahasiswa(&curNode->leftChild, key, curNode);
        } else if (strcmp(key, curNode->key) > 0) {
            hapusMahasiswa(&curNode->rightChild, key, curNode);
        } else {
            if ((curNode->leftChild == NULL) && (curNode->rightChild == NULL)) {
                if (parent != NULL) {
                    if (curNode == parent->leftChild) {
                        parent->leftChild = NULL;
                    } else if (curNode == parent->rightChild) {
                        parent->rightChild = NULL;
                    }
                } else {
                    *tree = NULL;
                }
                free(curNode);
            } else if ((curNode->leftChild != NULL) && (curNode->rightChild == NULL)) {
                if (parent != NULL) {
                    if (curNode == parent->leftChild) {
                        parent->leftChild = curNode->leftChild;
                    } else if (curNode == parent->rightChild) {
                        parent->rightChild = curNode->leftChild;
                    }
                } else {
                    *tree = NULL;
                }
                free(curNode);
            } else if ((curNode->leftChild == NULL) && (curNode->rightChild != NULL)) {
                if (parent != NULL) {
                    if (curNode == parent->leftChild) {
                        parent->leftChild = curNode->rightChild;
                    } else if (curNode == parent->rightChild) {
                        parent->rightChild = curNode->rightChild;
                    }
                } else {
                    *tree = NULL;
                }
                free(curNode);
            } else if ((curNode->leftChild != NULL) && (curNode->rightChild != NULL)) {
                struct MahasiswaNode *successor;

                successor = curNode->rightChild;
                while (successor->leftChild != NULL) {
                    successor = successor->leftChild;
                }

                if (parent != NULL) {
                    if (curNode == parent->leftChild) {
                        parent->leftChild = successor;
                    } else if (curNode == parent->rightChild) {
                        parent->rightChild = successor;
                    }
                } else {
                    *tree = NULL;
                }

                free(curNode);
            }
        }
    }
}

int main() {
    struct MahasiswaNode *tree = NULL;
    struct Mahasiswa mhs;
    struct MahasiswaNode *cari;

    strcpy(mhs.nama, "Budi Setiawan");
    strcpy(mhs.prodi, "Informatika");
    mhs.angkatan = 2020;
    tambahMahasiswa(&tree, "M0520015", &mhs);

    strcpy(mhs.nama, "Rizal Setiabudi");
    strcpy(mhs.prodi, "Informatika");
    mhs.angkatan = 2019;
    tambahMahasiswa(&tree, "M0519064", &mhs);

    strcpy(mhs.nama, "Yusuf Hendrawan");
    strcpy(mhs.prodi, "Informatika");
    mhs.angkatan = 2021;
    tambahMahasiswa(&tree, "M0521079", &mhs);

    strcpy(mhs.nama, "Joko Susilo");
    strcpy(mhs.prodi, "Informatika");
    mhs.angkatan = 2020;
    tambahMahasiswa(&tree, "M0520041", &mhs);

    printf("Menampilkan semua data ...\n");
    tampilkanDataMahasiswa(tree);
    printf("\n");

    printf("Mencari nama dari M0519064 ...\n");
    cari = cariMahasiswa(tree, "M0519064");
    if (cari != NULL) {
        printf("Nama: %s\n", cari->value.nama);
    } else {
        printf("Tidak ketemu :(\n");
    }
    printf("\n");

    printf("Mencari nama dari M0519065 ...\n");
    cari = cariMahasiswa(tree, "M0519065");
    if (cari != NULL) {
        printf("Nama: %s\n", cari->value.nama);
    } else {
        printf("Tidak ketemu :(\n");
    }
    printf("\n");

    printf("Mengganti nama dari M0519064 ...\n");
    cari = cariMahasiswa(tree, "M0519064");
    /* kita anggap datanya memang benar-benar ada */
    strcpy(cari->value.nama, "Rizal Setiaji");
    tampilkanDataMahasiswa(tree);
    printf("\n");

    printf("Menghapus M0520041 ...\n");
    hapusMahasiswa(&tree, "M0520041", NULL);
    tampilkanDataMahasiswa(tree);
    printf("\n");

    printf("Menambahkan M0520015 ...\n");
    strcpy(mhs.nama, "Bagus Haryono");
    strcpy(mhs.prodi, "Informatika");
    mhs.angkatan = 2020;
    tambahMahasiswa(&tree, "M0520015", &mhs); /* error: sudah ada sebelumnya */
    printf("\n");

    printf("Menghapus semua mahasiswa ...\n");
    hapusSemuaMahasiswa(&tree);
    tampilkanDataMahasiswa(tree); /* seharusnya tidak menampilkan apa-apa */
    printf("\n");

    return 0;
}

/*
Output:

Menampilkan semua data ...
M0519064: Rizal Setiabudi, Prodi Informatika, Angkatan 2019
M0520015: Budi Setiawan, Prodi Informatika, Angkatan 2020
M0520041: Joko Susilo, Prodi Informatika, Angkatan 2020
M0521079: Yusuf Hendrawan, Prodi Informatika, Angkatan 2021

Mencari nama dari M0519064 ...
Nama: Rizal Setiabudi

Mencari nama dari M0519065 ...
Tidak ketemu :(

Mengganti nama dari M0519064 ...
M0519064: Rizal Setiaji, Prodi Informatika, Angkatan 2019
M0520015: Budi Setiawan, Prodi Informatika, Angkatan 2020
M0520041: Joko Susilo, Prodi Informatika, Angkatan 2020
M0521079: Yusuf Hendrawan, Prodi Informatika, Angkatan 2021

Menghapus M0520041 ...
M0519064: Rizal Setiaji, Prodi Informatika, Angkatan 2019
M0520015: Budi Setiawan, Prodi Informatika, Angkatan 2020
M0521079: Yusuf Hendrawan, Prodi Informatika, Angkatan 2021

Menambahkan M0520015 ...
Mahasiswa dengan NIM M0520015 sudah ada sebelumnya

Menghapus semua mahasiswa ...

*/
```

[Silabus >>](../silabus.md)

