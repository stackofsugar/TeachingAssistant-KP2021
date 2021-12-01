[<< Constructor dan Destructor](2-ConstructorDanDestructor.md)

# 13.3 - Class Pointer

Dalam praktiknya, apalagi dalam bahasa keluarga C/C++, kita sering menggunakan pointer untuk mereferensikan ke suatu obyek tertentu, sejalan dengan konsep pointer di mana hal tersebut memungkinkan kita untuk memanipulasi obyek tersebut di scope yang berbeda, serta mencegah banyak tindakan penyalinan suatu obyek dari variabel ke variabel lain.

## Kata Kunci "new" dan "delete"

Seperti fungsi **malloc**, C++ mempunyai kata kunci **new** untuk mengalokasikan suatu obyek bertipe class ke dalam memory dan juga sekaligus memanggil constructornya. Sebagai contoh:
```cpp
Weapon *deagle;

deagle = new Weapon("Desert Eagle", 750, 35, 7);
```

Kemudian obyek-obyek yang telah dibuat menggunakan kata kunci **new**, harus dihapus/dibebaskan dengan kata kunci **delete**, sama halnya fungsi **free** pada C library, sebagai contoh:
```cpp
Weapon *deagle;

deagle = new Weapon("Desert Eagle", 750, 35, 7);

/* ... */

delete deagle;
```
Ketika suatu obyek dihapus, maka destructor akan dipanggil terlebih dahulu sebelum menghapus

## Contoh Penerapan

Berikut adalah implementasi permainan shooter sederhana berbasis OOP dengan menggunakan banyak class pointer
```cpp
#include <stdio.h>
#include <string.h>

/* Deklarasi class */
class Player;
class Weapon;

/* Class Weapon */
class Weapon {
public:
    char name[50];
    int price;
    int damage;
    int rounds;
    Player *owner;

    /* Constructor dan destructor */
    Weapon(const char *name, int price, int damage, int rounds);
    ~Weapon();

    /* Deklarasi method pada class Weapon */
    void GetDescription(char *desc);
    void Fire(Player *target);
    void Reload(int rounds);
};

/* Class Player */
class Player {
public:
    char name[50];
    int health;
    Weapon *currentWpn;

    /* Constructor dan destructor */
    Player(const char *name, int health);
    ~Player(void);

    /* Deklarasi method pada class Player */
    void Equip(Weapon *wpn);
    void Print();
    void Attack(Player *opponent);
};

/* Entry point */
int main() {
    Weapon *deagle, *m4a1, *ak47;
    Player *sandman, *makarov;

    deagle = new Weapon("Desert Eagle", 750, 35, 7);
    m4a1 = new Weapon("M4A1", 3100, 20, 30);
    ak47 = new Weapon("AK-47", 2500, 25, 30);

    sandman = new Player("Sandman", 100);
    sandman->Equip(m4a1);
    sandman->Print();

    makarov = new Player("Vladimir Makarov", 100);
    makarov->Equip(ak47);
    makarov->Equip(m4a1);
    makarov->Print();

    makarov->Attack(sandman);
    sandman->Attack(makarov);
    sandman->Attack(makarov);
    makarov->Attack(sandman);
    sandman->Equip(deagle);
    sandman->Attack(makarov);
    sandman->Attack(makarov);

    delete sandman;
    delete makarov;

    delete deagle;
    delete m4a1;
    delete ak47;
}

/******************************************************************************
** Definisi constructor, destructor, dan method pada class Weapon
*/

Weapon::Weapon(const char *name, int price, int damage, int rounds) {
    printf("Weapon created: %s\n", name);

    strcpy(this->name, name);
    this->price = price;
    this->damage = damage;
    this->rounds = rounds;
    this->owner = NULL;
}

Weapon::~Weapon() {
    printf("Weapon destroyed: %s\n", this->name);
}

void Weapon::GetDescription(char *desc) {
    char ownerString[100];
    if (this->owner != NULL) {
        strcpy(ownerString, this->owner->name);
    } else {
        strcpy(ownerString, "none");
    }

    sprintf(desc, "%s ($: %d, %%: %d, n: %d, owner: %s)", this->name, this->price, this->damage, this->rounds, ownerString);
}

void Weapon::Fire(Player *target) {
    printf("%s: ", this->name);
    if (this->owner != NULL) {
        if (this->rounds > 0) {
            this->rounds = this->rounds - 1;
            if (target != NULL) {
                target->health = target->health - this->damage;
                printf("BANG! (dealt %d%% damage from %s to %s), %d rounds left", this->damage, this->owner->name, target->name, this->rounds);
            } else {
                printf("miss!, %d rounds left", this->rounds);
            }
        } else {
            printf("unable to fire because clip is empty");
        }
    } else {
        printf("unable to fire because of no owner");
    }
    printf("\n");
}

void Weapon::Reload(int rounds) {
    this->rounds = rounds;
    printf("Reloaded %s with %d rounds!\n", this->name, rounds);
}

/******************************************************************************
** Definisi constructor, destructor, dan method pada class Player
*/

Player::Player(const char *name, int health) {
    printf("%s entered the game\n", name);

    strcpy(this->name, name);
    this->health = health;
    this->currentWpn = NULL;

    printf("\n");
}

Player::~Player() {
    printf("%s left the game\n", this->name);

    printf("\n");
}

void Player::Equip(Weapon *wpn) {
    if (wpn != NULL) {
        if (wpn->owner == NULL) {
            if (this->currentWpn != NULL) {
                this->currentWpn->owner = NULL;
            }
            this->currentWpn = wpn;
            this->currentWpn->owner = this;
            printf("Equipped %s to %s\n", wpn->name, this->name);
        } else {
            printf("Unable to equip %s to %s (still owned by %s)\n", wpn->name, this->name, wpn->owner->name);
        }
    } else {
        if (this->currentWpn != NULL) {
            this->currentWpn->owner = NULL;
            this->currentWpn = NULL;
            printf("Unequipped %s from %s\n", this->currentWpn->name, this->name);
        } else {
            printf("%s has no weapon already\n", this->name);
        }
    }

    printf("\n");
}

void Player::Print() {
    char weaponString[100];

    if (this->currentWpn != NULL) {
        this->currentWpn->GetDescription(weaponString);
    } else {
        strcpy(weaponString, "none");
    }

    printf("[PLAYER INFORMATION]\n");
    printf(" Name: %s\n", this->name);
    printf(" Health: %d\n", this->health);
    printf(" Weapon: %s\n", weaponString);

    printf("\n");
}

void Player::Attack(Player *opponent) {    
    if (this->currentWpn != NULL) {
        if (opponent->health > 0) {
            printf("%s: attacking %s ...\n", this->name, opponent->name);

            this->currentWpn->Fire(opponent);
            if (opponent->health > 0) {
                printf("%s has %d health left\n", opponent->name, opponent->health);
            } else {
                printf("%s has been killed by %s (using %s)\n", opponent->name, this->name, this->currentWpn->name);
            }
        } else {
            printf("%s: opponent (%s) is already dying\n", this->name, opponent->name);
        }
    } else {
        printf("%s: unable to attack %s (don't have any weapon yet)\n", this->name, opponent->name);
    }

    printf("\n");
}

/*
Output:

Weapon created: Desert Eagle
Weapon created: M4A1
Weapon created: AK-47
Sandman entered the game

Equipped M4A1 to Sandman

[PLAYER INFORMATION]
 Name: Sandman
 Health: 100
 Weapon: M4A1 ($: 3100, %: 20, n: 30, owner: Sandman)

Vladimir Makarov entered the game

Equipped AK-47 to Vladimir Makarov

Unable to equip M4A1 to Vladimir Makarov (still owned by Sandman)

[PLAYER INFORMATION]
 Name: Vladimir Makarov
 Health: 100
 Weapon: AK-47 ($: 2500, %: 25, n: 30, owner: Vladimir Makarov)

Vladimir Makarov: attacking Sandman ...
AK-47: BANG! (dealt 25% damage from Vladimir Makarov to Sandman), 29 rounds left
Sandman has 75 health left

Sandman: attacking Vladimir Makarov ...
M4A1: BANG! (dealt 20% damage from Sandman to Vladimir Makarov), 29 rounds left
Vladimir Makarov has 80 health left

Sandman: attacking Vladimir Makarov ...
M4A1: BANG! (dealt 20% damage from Sandman to Vladimir Makarov), 28 rounds left
Vladimir Makarov has 60 health left

Vladimir Makarov: attacking Sandman ...
AK-47: BANG! (dealt 25% damage from Vladimir Makarov to Sandman), 28 rounds left
Sandman has 50 health left

Equipped Desert Eagle to Sandman

Sandman: attacking Vladimir Makarov ...
Desert Eagle: BANG! (dealt 35% damage from Sandman to Vladimir Makarov), 6 rounds left
Vladimir Makarov has 25 health left

Sandman: attacking Vladimir Makarov ...
Desert Eagle: BANG! (dealt 35% damage from Sandman to Vladimir Makarov), 5 rounds left
Vladimir Makarov has been killed by Sandman (using Desert Eagle)

Sandman left the game

Vladimir Makarov left the game

Weapon destroyed: Desert Eagle
Weapon destroyed: M4A1
Weapon destroyed: AK-47
*/
```

[Silabus >>](../silabus.md)
