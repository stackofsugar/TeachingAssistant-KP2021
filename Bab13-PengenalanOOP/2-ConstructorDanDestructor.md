[<< Konsep Class dan Object](1-KonsepClassObject.md)

# 13.2 - Constructor dan Destructor

Constructor dan Destructor adalah sebuah fungsi _spesial_ pada konsep OOP. 
Keduanya mirip seperti fungsi pada umumnya tetapi fungsi ini **TIDAK** memiliki return type
dan namanya harus persis dengan nama classnya. Khusus untuk Destructor tidak memiliki parameter pula

## Constructor
 
Constructor merupakan sebuah fungsi yang otomatis terpanggil ketika suatu objek ter-_instantiate_ atau tercipta/terbuat.
Fungsi ini dapat digunakan dan dimanfaatkan untuk berbagai tujuan. Contoh yang umum digunakan ialah untuk menginisialisasi
_data member_ atau _class attribute_.

### Syntax
```c 
NamaKelas( /*parameters*/ ){
  // code
}
```

### Penggunaan
Contoh penggunaan berikut akan meng-efesiensi-kan inisialisasi data member dari ``class Weapon``

Pada source code sebelumnya, setiap data member diberikan nilai satu per satu
```cpp
#include <stdio.h>
#include <string.h>

class Weapon {
public:
    char name[50];
    int price;
    int damage;
    int rounds;
    
    // code
};

int main() {
    Weapon deagle;

    strcpy(deagle.name, "Desert Eagle");
    deagle.price = 750;
    deagle.damage = 35;
    deagle.rounds = 7;
}
```

Pada contoh berikut menggunakan constructor untuk menginisialisasi setiap data member saat meng-instantiate objek
```cpp
#include <stdio.h>
#include <string.h>

class Weapon {
public:
    char name[50];
    int price;
    int damage;
    int rounds;
    
    //constructor
    Weapon( char* _name, int _price, int _damage, int _rounds ){
      strcpy(name, _name);
      price = _price;
      damage = _damage;
      rounds = _rounds;
    }
    
    // code
};

int main() {
    Weapon deagle("Desert Eagle", 750, 35, 7);
}
```

Dapat dilihat bahwa instansiasi objek ``deagle`` sekaligus memberikan nilai untuk setiap datamembernya pada satu baris menggunakan constructor 

## Destructor

Destructor merupakan sebuah fungsi yang otomatis terpanggil ketika suatu objek _destroyed_ atau dihancurkan. Perlu diingat bahwa objek sama halnya seperti variable biasa 
yang akan dihancurkan otomatis ketika keluar dari scopenya

### Syntax

Destructor memiliki syntax yang sama seperti Constructor tetapi nama fungsi diawali dengan _tilde_(~) dan tidak menerima parameter
```cpp
~NamaKelas(){
  // code
}
```

### Penggunaan

Pada penggunaan berikut constructor mengirimkan pesan ketika objek dibuat dan destructor mengirimkan pesan ketika objek dihancurkan. Hal ini berguna untuk _debugging_
```cpp
#include <stdio.h>

class Foo{
public:
    int id;
    Foo(int _id){
        id = _id;
        printf("-----> objek dari kelas Foo dengan id %d dibuat\n", id);
    }
  
    //destructor
    ~Foo(){
        printf("=====> objek dari kelas Foo dengan id %d dihancurkan\n", id);
    }
};

int main(void){
    printf("AWAL DARI SCOPE MAIN\n");
    Foo f100(100);
    
    do{
        printf("\nAWAL DARI SCOPE DO-WHILE\n");
        Foo f123(123);
        printf("AKHIR DARI SCOPE DO-WHILE\n");
    } while(0);    
    
    printf("\nAKHIR DARI SCOPE MAIN\n");
}

/* Output
AWAL DARI SCOPE MAIN
-----> objek dari kelas Foo dengan id 100 dibuat     

AWAL DARI SCOPE DO-WHILE
-----> objek dari kelas Foo dengan id 123 dibuat     
AKHIR DARI SCOPE DO-WHILE
=====> objek dari kelas Foo dengan id 123 dihancurkan

AKHIR DARI SCOPE MAIN
=====> objek dari kelas Foo dengan id 100 dihancurkan
*/
```

[Class Pointer >>](3-ClassPointer.md)
