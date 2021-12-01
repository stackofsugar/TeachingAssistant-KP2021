[<< Silabus](../silabus.md)

# 13.1 - Konsep Class dan Object

## Pengantar

**Object-Oriented Programming (OOP)** adalah suatu metode pemrograman di mana dalam praktiknya banyak memanfaatkan **class** dan **object** sebagai komponen utamanya. Java dan C# adalah contoh bahasa pemrograman yang memfokuskan pada OOP. Bahasa C sendiri tidak memiliki dukungan terhadap OOP. Namun, bahasa C++ yang mana merupakan pembaruan dari bahasa C memiliki dukungan terhadap OOP.

## Class dan Object

Dalam bahasa C, kita telah mengenal istilah **struct**. Coba perhatikan contoh berikut:
```c
#include <stdio.h>
#include <string.h>

/* Struct yang menyatakan informasi mengenai suatu obyek senjata */
struct Weapon {
    char name[50];
    int price;
    int damage;
    int rounds;
};

/* Berbagai function untuk bekerja dengan struct Weapon */
void PrintWeapon(struct Weapon *wpn);
void FireWeapon(struct Weapon *wpn);
void UpgradeWeapon(struct Weapon *wpn, int damageUpgrade);
void ReloadWeapon(struct Weapon *wpn, int rounds);

int main() {
    /* Deklarasikan variabel (deagle) berupa obyek dari struct Weapon */
    struct Weapon deagle;

    strcpy(deagle.name, "Desert Eagle");
    deagle.price = 750;
    deagle.damage = 35;
    deagle.rounds = 7;

    PrintWeapon(&deagle);

    FireWeapon(&deagle);
    FireWeapon(&deagle);

    UpgradeWeapon(&deagle, 5);
    FireWeapon(&deagle);

    ReloadWeapon(&deagle, 7);
    FireWeapon(&deagle);

    return 0;
}

void PrintWeapon(struct Weapon *wpn) {
    printf("%s ($: %d, %%: %d, n: %d)\n", wpn->name, wpn->price, wpn->damage, wpn->rounds);
}

void FireWeapon(struct Weapon *wpn) {
    if (wpn->rounds > 0) {
        wpn->rounds = wpn->rounds - 1;
        printf("%s: BANG! (%d damage dealt), %d rounds left\n", wpn->name, wpn->damage, wpn->rounds);
    } else {
        printf("%s: clip is empty\n", wpn->name);
    }
}

void UpgradeWeapon(struct Weapon *wpn, int damageUpgrade) {
    int oldDamage = wpn->damage;
    int newDamage = wpn->damage + damageUpgrade;

    wpn->damage = newDamage;
    printf("Upgraded %s damage from %d%% to %d%% (+%d%%)\n", wpn->name, oldDamage, newDamage, damageUpgrade);
}

void ReloadWeapon(struct Weapon *wpn, int rounds) {
    wpn->rounds = rounds;
    printf("Reloaded %s with %d rounds\n", wpn->name, rounds);
}

/*
Output:

Desert Eagle ($: 750, %: 35, n: 7)
Desert Eagle: BANG! (35 damage dealt), 6 rounds left
Desert Eagle: BANG! (35 damage dealt), 5 rounds left
Upgraded Desert Eagle damage from 35% to 40% (+5%)
Desert Eagle: BANG! (40 damage dealt), 4 rounds left
Reloaded Desert Eagle with 7 rounds
Desert Eagle: BANG! (40 damage dealt), 6 rounds left
*/
```

Dalam code di atas, sudah terdapat obyek yaitu **deagle** yang mana memiliki tipe **struct Weapon**. Kode di atas merupakan fondasi utama dalam pemrograman berbasis obyek (OOP). Selanjutnya, akan kita modifikasi kode tersebut dengan bahasa **C++** dengan menggunakan **class** sebagai gantinya struct, berikut adalah hasilnya:

```cpp
/* Simpan sebagai file berekstensi .cpp */

#include <stdio.h>
#include <string.h>

/* Class yang menyatakan informasi mengenai suatu obyek senjata */
class Weapon {
public:
    char name[50];
    int price;
    int damage;
    int rounds;

    /* Berbagai method untuk bekerja dengan class Weapon */
    void Print();
    void Fire();
    void Upgrade(int damageUpgrade);
    void Reload(int rounds);
};


int main() {
    /* Deklarasikan variabel (deagle) berupa obyek dari class Weapon */
    Weapon deagle;

    strcpy(deagle.name, "Desert Eagle");
    deagle.price = 750;
    deagle.damage = 35;
    deagle.rounds = 7;

    deagle.Print();

    deagle.Fire();
    deagle.Fire();

    deagle.Upgrade(5);
    deagle.Fire();

    deagle.Reload(7);
    deagle.Fire();

    return 0;
}

void Weapon::Print() {
    printf("%s ($: %d, %%: %d, n: %d)\n", this->name, this->price, this->damage, this->rounds);
}

void Weapon::Fire() {
    if (this->rounds > 0) {
        this->rounds = this->rounds - 1;
        printf("%s: BANG! (%d damage dealt), %d rounds left\n", this->name, this->damage, this->rounds);
    } else {
        printf("%s: clip is empty\n", this->name);
    }
}

void Weapon::Upgrade(int damageUpgrade) {
    int oldDamage = this->damage;
    int newDamage = this->damage + damageUpgrade;

    this->damage = newDamage;
    printf("Upgraded %s damage from %d%% to %d%% (+%d%%)\n", this->name, oldDamage, newDamage, damageUpgrade);
}

void Weapon::Reload(int rounds) {
    this->rounds = rounds;
    printf("Reloaded %s with %d rounds\n", this->name, rounds);
}

/*
Output:

Desert Eagle ($: 750, %: 35, n: 7)
Desert Eagle: BANG! (35 damage dealt), 6 rounds left
Desert Eagle: BANG! (35 damage dealt), 5 rounds left
Upgraded Desert Eagle damage from 35% to 40% (+5%)
Desert Eagle: BANG! (40 damage dealt), 4 rounds left
Reloaded Desert Eagle with 7 rounds
Desert Eagle: BANG! (40 damage dealt), 6 rounds left
*/
```

Dapat dilihat bahwa fitur utama dari class adalah memungkinkan berbagai **method** (function untuk bekerja dengan obyek terkait) untuk didefinisikan dalam class tersebut sehingga dapat digunakan oleh pemrogram layaknya pemanggilan fungsi seperti biasa sehingga kode menjadi lebih rapi dan terstruktur.

Dapat dilihat juga bahwa terdapat kata kunci **this** yang mana merupakan variabel yang diciptakan oleh compiler yang merujuk kepada obyek tempat pemanggilan fungsi tersebut terjadi. Sehingga, kita dapat memanipulasi keadaan obyek tersebut menggunakan kata kunci **this**.

[Constructor dan Destructor >>](2-ConstructorDanDestructor.md)