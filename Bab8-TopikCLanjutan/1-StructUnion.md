[<< Silabus](../silabus.md)

# 8.1 - Struct dan Union

## Struct

### Pengantar

Coba perhatikan kode di bawah
```c
char weapon_names[5][50] = {"Desert Eagle", "H&K MP5", "AK-47", "M4A1", "AWP Magnum"};
int weapon_prices[5] = {750, 1500, 2500, 3100, 4750};
int weapon_damages[5] = {35, 15, 25, 20, 100};
int weapon_rounds[5] = {7, 30, 30, 30, 10};
```

**Apa yang dapat anda simpulkan dari kode di atas?** Jadi kode di atas mendeklarasikan dan mendefinisikan 4 variabel bertipe array yang memiliki kesamaan yang umum yaitu: tiap elemennya merepresentasikan deskripsi dari suatu obyek yaitu weapon/senjata, dan memiliki jumlah elemen yang sama yaitu 5.

Array `weapon_names` menyimpan informasi nama-nama tiap senjata, kemudian array `weapon_prices` menyimpan informasi harga tiap senjata, kemudian array `weapon_damages` menyimpan informasi kekuatan tiap senjata, kemudian array `weapon_rounds` menyimpan informasi jumlah peluru (per magazin) tiap senjata. Dengan demikian, dapat ditarik kesimpulan bahwa indeks 0 merupakan milik *Desert Eagle* (dengan price 750, damage 35, dan rounds 7), indeks 1 merupakan milik *H&K MP5* (dengan price 1500, damage 15, dan rounds 30), indeks 2 merupakan milik *AK-47* (dengan price 2500, damage 25, dan rounds 30), dan seterusnya.

**Permasalahan.** Coba bayangkan ketika anda ingin memasukkan seluruh informasi tentang suatu senjata menuju suatu function melalui argument. Apakah seperti berikut?
```c
/* (asumsi tidak terdapat global variable terkait array yang telah dibuat tadi) */
void print_weapon(const char *name, int price, int damage, int rounds) {
    printf("Weapon name: %s\n", name);
    printf(" Price: $%d\n", price);
    printf(" Damage: %d%%\n", damage);
    printf(" Rounds: %d\n", rounds);
}

int main() {
    char weapon_names[5][50] = {"Desert Eagle", "H&K MP5", "AK-47", "M4A1", "AWP Magnum"};
    int weapon_prices[5] = {750, 1500, 2500, 3100, 4750};
    int weapon_damages[5] = {35, 15, 25, 20, 100};
    int weapon_rounds[5] = {7, 30, 30, 30, 10};

    /* Print informasi senjata H&K MP5 (indeks: 1) */
    print_weapon(weapon_names[1], weapon_prices[1], weapon_damages[1], weapon_rounds[1]);

    /* Print informasi senjata M4A1 (indeks: 3) */
    print_weapon(weapon_names[3], weapon_prices[3], weapon_damages[3], weapon_rounds[3]);

    return 0;
}

/*
Output:

Weapon name: H&K MP5
 Price: $1500
 Damage: 15%
 Rounds: 30
Weapon name: M4A1
 Price: $3100
 Damage: 20%
 Rounds: 30
*/
```
Bagian mana yang kurang baik? Dapat dilihat pada parameter fungsi `print_weapon` terdapat 4 variabel yang merepresentasikan suatu obyek yang sama yaitu senjata. Coba bayangkan apabila anda ingin menambahkan informasi lagi untuk obyek senjata (misal: `clips`, `ammo_type`, `manufacturer`, dan lain-lain). Akibatnya adalah parameter fungsi tersebut akan selalu bertambah dan seluruh pemanggilan fungsi juga harus dimodifikasi untuk menyesuaikan jumlah informasi yang terkandung. Tentunya hal seperti itu sangatlah tidak efektif untuk program yang memiliki skala yang besar. Oleh karena itu, hal tersebut dapat diatasi dengan penggunaan **struct**.

**Solusi.** Kode di atas dapat dimodifikasi menjadi:
```c
/* Definisikan suatu tipe data struct yang merepresentasikan suatu obyek senjata */
struct Weapon {
    char name[50];
    int price;
    int damage;
    int rounds;
};

/* (asumsi tidak terdapat global variable terkait array yang telah dibuat tadi) */
void print_weapon(const struct Weapon *wpn) {
    /* Gunakan representasi obyek senjata dengan tipe data pointer `struct Weapon` */
    /* Akses informasi di dalamnya menggunakan (variable)->(informasi), misal wpn->name */
    printf("Weapon name: %s\n", wpn->name);
    printf(" Price: $%d\n", wpn->price);
    printf(" Damage: %d%%\n", wpn->damage);
    printf(" Rounds: %d\n", wpn->rounds);
}

int main() {
    /* Ubah menjadi satu array yang elemen-elemennya terdiri dari `struct Weapon` */
    struct Weapon weapon_list[5] = {
        /* Urutan: name, price, damage, rounds (sesuai urutan pada struct Weapon) */
        {"Desert Eagle", 750, 35, 7},
        {"H&K MP5", 1500, 15, 30},
        {"AK-47", 2500, 25, 30},
        {"M4A1", 3100, 20, 30},
        {"AWP Magnum", 4750, 100, 10}
    };

    /* Print informasi senjata H&K MP5 (indeks: 1) */
    /* Menggunakan pass-by-reference supaya benar-benar merujuk ke elemen dalam array sehingga tidak ada penyalinan data */
    print_weapon(&weapon_list[1]);

    /* Print informasi senjata M4A1 (indeks: 3) */
    /* Menggunakan pass-by-reference supaya benar-benar merujuk ke elemen dalam array sehingga tidak ada penyalinan data */
    print_weapon(&weapon_list[3]);

    return 0;
}

/*
Output:

Weapon name: H&K MP5
 Price: $1500
 Damage: 15%
 Rounds: 30
Weapon name: M4A1
 Price: $3100
 Damage: 20%
 Rounds: 30
*/
```

### Deklarasi Tipe Data Struct

Tipe data suatu struct dapat dideklarasikan dengan format:
```c
struct /*NamaStruct*/;
```

Sebagai contoh:
```c
struct Weapon;
```
Kode di atas mendeklarasikan sebuah struct bernama `Weapon`.

### Definisi Tipe Data Struct

Tipe data suatu struct dapat didefinisikan dengan format:
```c
struct /*NamaStruct*/ {
    /* Member variable 1 */;
    /* Member variable 2 */;
    /* Member variable 3 */;
    /* dst... */
};
```

Sebagai contoh:
```c
struct Weapon {
    char name[50];
    int price;
    int damage, rounds;
};
```
Member variable (variabel anggota) yang terdapat pada struct Weapon adalah: `name` dengan tipe data **char[50]**, `price` dengan tipe data **int**, `damage` dengan tipe data **int**, dan `rounds` dengan tipe data **int**. Deklarasi suatu member variable mirip dengan deklarasi variabel pada umumnya.

### Deklarasi Variable Bertipe Struct

Suatu variable yang bertipe suatu struct (yang selanjutnya akan disebut sebagai **obyek**) dapat dideklarasikan dengan format:
```c
struct /*NamaStruct*/ /*NamaVariabel*/;
```

Sebagai contoh:
```c
struct Weapon deagle;
struct Weapon ak47, m4a1;
```
Kode di atas mendeklarasikan 3 variable atau obyek (`deagle`, `ak47`, dan `m4a1`) yang semuanya bertipe `struct Weapon`.

### Inisialisasi Variable Bertipe Struct

Suatu variable yang bertipe suatu struct dapat diinisialisasi (diisi dengan nilai awal) dengan format:

**Bersamaan dengan deklarasi:**
```c
struct /*NamaStruct*/ /*NamaVariabel*/ = {/*NilaiMember1*/, /*NilaiMember2*/, /*NilaiMember3*/, /* dst... */};
```
Sebagai contoh:
```c
struct Weapon deagle = {"Desert Eagle", 750, 35, 7};
```
Kode di atas menginisialisasikan obyek `deagle` dengan `name` adalah *Desert Eagle*, `price` adalah 750, `damage` adalah 35, dan `rounds` adalah 7.

**Terpisah dari deklarasi:**
```c
/* Inisialisasi Obyek.Member1 */;
/* Inisialisasi Obyek.Member2 */;
/* Inisialisasi Obyek.Member3 */;
/* dst... */
```
Sebagai contoh:
```c
struct Weapon deagle;

/* Inisialisasi obyek deagle */
strcpy(deagle.name, "Desert Eagle"); /* Inisialisasi deagle.name (#include <string.h> terlebih dahulu) */
deagle.price = 750; /* Inisialisasi deagle.price */
deagle.damage = 35; /* Inisialisasi deagle.damage */
deagle.rounds = 7; /* Inisialisasi deagle.rounds */
```

### Operasi Assignment Pada Struct

Suatu obyek atau variable bertipe struct dapat diisi oleh obyek lain dengan tipe struct yang sama menggunakan operasi assignment (=), sebagai contoh:
```c
struct Weapon m4a1;
struct Weapon weapon_list[5] = {
    {"Desert Eagle", 750, 35, 7},
    {"H&K MP5", 1500, 15, 30},
    {"AK-47", 2500, 25, 30},
    {"M4A1", 3100, 20, 30},
    {"AWP Magnum", 4750, 100, 10}
};

/* Isi variable `m4a1` dengan elemen keempat (indeks: 3) dari array `weapon_list` */
m4a1 = weapon_list[3];

print_weapon(&m4a1);

/*
Output:

Weapon name: M4A1
 Price: $3100
 Damage: 20%
 Rounds: 30
*/
```

### Membaca Data Pada Struct

Data yang termuat dalam member variable pada suatu obyek bertipe struct dapat diakses menggunakan tanda titik (.) untuk pembacaan (read)
```c
struct Weapon deagle = {"Desert Eagle", 750, 35, 7};

/* Membaca variable `deagle` */
printf("Weapon name: %s\n", deagle.name);
printf(" Price: $%d\n", deagle.price);
printf(" Damage: %d%%\n", deagle.damage);
printf(" Rounds: %d\n", deagle.rounds);

/*
Output:

Weapon name: Desert Eagle
 Price: $750
 Damage: 35%
 Rounds: 7
*/
```

### Menulis Data Pada Struct

Sama seperti pembacaan data, data yang termuat dalam member variable pada suatu obyek bertipe struct dapat diakses menggunakan tanda titik (.) untuk operasi penulisan (write)
```c
struct Weapon deagle = {"Desert Eagle", 750, 35, 7};

printf("Damage sebelum diupgrade: %d%%\n", deagle.damage);

/* Ubah nilai salah satu member pada `deagle` */
deagle.damage = 50;

printf("Damage setelah diupgrade: %d%%\n", deagle.damage);

/*
Output:

Damage sebelum diupgrade: 35%
Damage setelah diupgrade: 50%
*/
```

### Pointer Pada Struct

Dalam prakteknya, umumnya variabel dengan tipe data struct jika dimasukkan sebagai salah satu argumen dalam fungsi adalah dalam bentuk **pointer**. Mengapa? Karena teknik tersebut mencegah terjadinya penyalinan obyek yang mana membuat ruang penyimpanan (memori) tidak efisien. Dengan demikian, kita lebih memilih untuk mengambil referensi (pointer) suatu obyek kemudian mengaksesnya daripada mengambil salinan dari obyek yang sudah ada yang mana membuat memori menjadi lebih boros, apalagi jika ukuran struct besar (terdapat banyak member dengan ukuran yang besar pula). Berikut adalah perbandingannya:
```c
/* Mengambil referensi (pointer) suatu obyek */
void print_weapon(const struct Weapon *wpn) {
    /* Akses member variable menggunakan -> jika pointer */
    /* Total memori terpakai dalam scope ini: sesuai dengan ukuran pointer `wpn` (4 atau 8 bytes tergantung CPU masing-masing) */
    printf("Weapon name: %s\n", wpn->name);
    printf(" Price: $%d\n", wpn->price);
    printf(" Damage: %d%%\n", wpn->damage);
    printf(" Rounds: %d\n", wpn->rounds);
}
```
```c
/* Mengambil salinan suatu obyek */
void print_weapon(struct Weapon wpn) {
    /* Akses member variable menggunakan . jika bukan pointer */
    /* Total memori terpakai dalam scope ini: sesuai dengan ukuran `wpn` (sekitar 62 bytes menurut ukuran `struct Weapon`) */
    printf("Weapon name: %s\n", wpn.name);
    printf(" Price: $%d\n", wpn.price);
    printf(" Damage: %d%%\n", wpn.damage);
    printf(" Rounds: %d\n", wpn.rounds);
}
```

**Pass By Reference - Read/Write Access:**
```c
void upgrade_weapon(struct Weapon *wpn) {
    /* Pointer `wpn` tidak read-only (const) sehingga nilai yang terkandung di dalamnya dapat dimanipulasi */
    wpn->damage = wpn->damage + 10; /* Tambah damage sebesar 10 */
}

int main() {
    struct Weapon deagle = {"Desert Eagle", 750, 35, 7};

    printf("Damage sebelum diupgrade: %d\n", deagle.damage);
    upgrade_weapon(&deagle); /* Pass by reference */
    printf("Damage setelah diupgrade: %d\n", deagle.damage);

    return 0;
}

/*
Output:

Damage sebelum diupgrade: 35
Damage setelah diupgrade: 45
*/
```

**Pass By Reference - Read Only Access:**
```c
void print_weapon(const struct Weapon *wpn) {
    /* Ingat bahwa `wpn` hanya bisa dibaca saja (read-only) karena pointer bertipe `const` */
    printf("Weapon name: %s\n", wpn->name);
    printf(" Price: $%d\n", wpn->price);
    printf(" Damage: %d%%\n", wpn->damage);
    printf(" Rounds: %d\n", wpn->rounds);
}

int main() {
    struct Weapon deagle = {"Desert Eagle", 750, 35, 7};

    print_weapon(&deagle); /* Pass by reference (read-only) */

    return 0;
}

/*
Output:

Weapon name: Desert Eagle
 Price: $750
 Damage: 35%
 Rounds: 7
*/
```

**Dynamic Memory Allocation:**

Satu obyek saja:
```c
struct Weapon *deagle;

deagle = (struct Weapon *)malloc(sizeof(struct Weapon));
strcpy(deagle->name, "Desert Eagle");
deagle->price = 750;
deagle->damage = 35;
deagle->rounds = 7;

print_weapon(deagle); /* Pass by reference */
```

Implementasi dalam array (lebih dari satu obyek):
```c
struct Weapon *weapon_list;
int weapon_count = 2;

weapon_list = (struct Weapon *)malloc(weapon_count * sizeof(struct Weapon));

strcpy(weapon_list[0].name, "Desert Eagle");
weapon_list[0].price = 750;
weapon_list[0].damage = 35;
weapon_list[0].rounds = 7;

strcpy(weapon_list[1].name, "M4A1");
weapon_list[1].price = 3100;
weapon_list[1].damage = 20;
weapon_list[1].rounds = 30;

print_weapons(weapon_list, weapon_count); /* Masukkan array (otomatis pass by reference) */
```

### Contoh Source Code

<details>
<summary>Lihat source code</summary>

```c
#include <stdio.h>
#include <stdlib.h>

struct Weapon {
    char name[50];
    int price;
    int damage;
    int rounds;
};

void print_weapons(const struct Weapon *weapon_list, int weapon_count);

int main() {
    int i;
    int weapon_count;
    struct Weapon *weapon_list;

    printf("Enter number of weapons: ");
    scanf("%d", &weapon_count);

    weapon_list = (struct Weapon *)malloc(weapon_count * sizeof(struct Weapon));
    for (i = 0; i < weapon_count; i++) {
        printf("Weapon #%d name (no spaces): ", i + 1);
        scanf("%s", weapon_list[i].name);

        printf("Weapon #%d price: ", i + 1);
        scanf("%d", &weapon_list[i].price);

        printf("Weapon #%d damage: ", i + 1);
        scanf("%d", &weapon_list[i].damage);

        printf("Weapon #%d rounds: ", i + 1);
        scanf("%d", &weapon_list[i].rounds);
    }

    /* Tampilkan semua senjata */
    print_weapons(weapon_list, weapon_count);

    free(weapon_list);

    return 0;
}

void print_weapons(const struct Weapon *weapon_list, int weapon_count) {
    int i;

    printf(" === WEAPONS LIST ===\n");
    for (i = 0; i < weapon_count; i++) {
        printf("[%d] %s\n", i + 1, weapon_list[i].name);
        printf(" Price: $%d\n", weapon_list[i].price);
        printf(" Damage: %d%%\n", weapon_list[i].damage);
        printf(" Rounds: %d\n", weapon_list[i].rounds);
    }
}

/*
Output:

Enter number of weapons: 3
Weapon #1 name (no spaces): Desert_Eagle
Weapon #1 price: 750
Weapon #1 damage: 35
Weapon #1 rounds: 7
Weapon #2 name (no spaces): H&K_MP5
Weapon #2 price: 1500
Weapon #2 damage: 15
Weapon #2 rounds: 30
Weapon #3 name (no spaces): M4A1
Weapon #3 price: 3100
Weapon #3 damage: 20
Weapon #3 rounds: 30
 === WEAPONS LIST ===
[1] Desert_Eagle
 Price: $750
 Damage: 35%
 Rounds: 7
[2] H&K_MP5
 Price: $1500
 Damage: 15%
 Rounds: 30
[3] M4A1
 Price: $3100
 Damage: 20%
 Rounds: 30
*/
```
</details>

## Union

Konsep union sebenarnya hampir mirip dengan konsep struct. Hanya saja tiap member variable pada union dipaksa berukuran sama dan mengarah ke alamat memori yang sama semua. Sebagai perbandingan:
```c
/* Menggunakan struct */
struct Vector3D {
    int intComponents[3]; /* Data terletak di alamat memori X berukuran 12 bytes */
    float floatComponents[3]; /* Data terletak di alamat memori Y berukuran 12 bytes */
    double doubleComponents[3]; /* Data terletak di alamat memori Z berukuran 24 bytes */
}; /* Total size: 48 bytes (ukuran intComponents + ukuran floatComponents + ukuran doubleComponents */
```
```c
/* Menggunakan union */
union Vector3D {
    int intComponents[3]; /* Data terletak di alamat memori X berukuran 24 bytes (sesuai ukuran member terbesar) */
    float floatComponents[3]; /* Data terletak di alamat memori X berukuran 24 bytes (sesuai ukuran member terbesar) */
    double doubleComponents[3]; /* Data terletak di alamat memori X berukuran 24 bytes (member terbesar) */
}; /* Total size: 24 bytes */
```
Dapat disimpulkan bahwa perubahan nilai salah satu member variable pada variable bertipe union juga mempengaruhi nilai member variable yang lain karena juga berada pada alamat memori yang sama.

Perhatikan kode di bawah untuk mengetahui kinerja union
```c
union Number {
    int iVal;
    long long llVal;
    float fVal;
    double dblVal;
};

int main() {
    union Number num;

    num.iVal = 32;
    num.fVal = 64.0f;
    /* Sekarang 64.0f adalah nilai yang sebenarnya tersimpan dalam `num` */
    /* `num.iVal` sudah tidak 32 lagi, melainkan sudah tidak bermakna apa-apa */

    /* Tidak menampilkan nilai 32, melainkan representasi bilangan floating point dari 64.0 dalam bentuk integer (FYI bilangan floating point disimpan dalam komputer dalam bentuk unsigned integer) */
    printf("num.iVal = %d\n", num.iVal);

    /* Menampilkan nilai 64.0 karena operasi assignment terakhir kali adalah `num.fVal = 64.0f;` */
    printf("num.fVal = %f\n", num.fVal);

    return 0;
}

/*
Output:

num.iVal = 1115684864
num.fVal = 64.000000
*/
```

Konsep union sebenarnya hanya ditemukan dalam bahasa C dan termasuk dalam kategori jarang dipakai karena pada bahasa pemrograman populer lain tidak terdapat konsep union. Akan tetapi, tidak salah juga apabila ikut dipelajari sehingga anda dapat menguasai bahasa pemrograman C secara menyeluruh.

### Contoh Source Code

<details>
<summary>Lihat source code</summary>

```c
#include <stdio.h>

#define NUM_INT     0
#define NUM_DOUBLE  1

union NumberValue {
    int iVal;
    double dblVal;
}; /* Ukuran: 8 bytes (ukuran member variable terbesar, `dblVal`) */

struct Number {
    int type;
    union NumberValue value; /* Memakan memori 8 bytes saja */
};

struct Number addTwoNumbers(struct Number a, struct Number b) {
    struct Number result;

    switch (a.type) {
    case NUM_INT:
        result.type = NUM_INT;
        result.value.iVal = a.value.iVal + b.value.iVal;
        break;
    case NUM_DOUBLE:
        result.type = NUM_DOUBLE;
        result.value.dblVal = a.value.dblVal + b.value.dblVal;
        break;
    }

    return result;
}

void printNumber(struct Number num) {
    switch (num.type) {
    case NUM_INT:
        printf("Number: %d\n", num.value.iVal);
        break;
    case NUM_DOUBLE:
        printf("Number: %lf\n", num.value.dblVal);
        break;
    }
}

int main() {
    struct Number num1, num2, result;

    num1.type = NUM_INT;
    num1.value.iVal = 3;
    num2.type = NUM_INT;
    num2.value.iVal = 5;
    result = addTwoNumbers(num1, num2);
    printNumber(result);

    num1.type = NUM_DOUBLE;
    num1.value.dblVal = 10.0;
    num2.type = NUM_DOUBLE;
    num2.value.dblVal = 15.0;
    result = addTwoNumbers(num1, num2);
    printNumber(result);

    return 0;
}

/*
Output:

Number: 8
Number: 25.000000
*/
```
</details>

## Type Aliasing

Untuk mempersingkat penulisan dalam bekerja menggunakan struct dan union, seringkali diterapkan suatu *type aliasing* menggunakan kata kunci **typedef**. Sebagai contoh:

Versi 1:
```c
struct Weapon {
    char name[50];
    int price;
    int damage;
    int rounds;
};

typedef struct Weapon Weapon;
```

Versi 2:
```c
typedef struct Weapon {
    char name[50];
    int price;
    int damage;
    int rounds;
} Weapon;
```

Versi 3:
```c
typedef struct {
    char name[50];
    int price;
    int damage;
    int rounds;
} Weapon;
```

Ketika menggunakan type aliasing, kita tidak perlu menuliskan `struct` berulangkali pada source code dalam bekerja menggunakan struct. Dengan demikian, kode berikut sah-sah saja apabila type aliasing di atas diterapkan:
```c
/* sudah tidak `const struct Weapon *` lagi */
void print_weapon(const Weapon *wpn) {
    printf("Weapon name: %s\n", wpn->name);
    printf(" Price: $%d\n", wpn->price);
    printf(" Damage: %d%%\n", wpn->damage);
    printf(" Rounds: %d\n", wpn->rounds);
}

int main() {
    /* sudah tidak `struct Weapon` lagi */
    Weapon deagle;

    strcpy(deagle.name, "Desert Eagle");
    deagle.price = 750;
    deagle.damage = 35;
    deagle.rounds = 7;

    print_weapon(&deagle);

    return 0;
}

/*
Output:

Weapon name: Desert Eagle
 Price: $750
 Damage: 35%
 Rounds: 7
*/
```

[Materi Selanjutnya (Bit Manipulation) >>](2-BitManipulation.md)
