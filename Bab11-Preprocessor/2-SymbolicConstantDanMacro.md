[<< Materi Sebelumnya (Pengantar Preprocessor)](1-Pengantar.md)

# 11.2 - Symbolic Constant dan Macro 
Symbolic Constant dan Macro merupakan salah dua penggunaan dari preprocessor **#define**. Pada dasarnya, keduanya akan menggantikan/mensubstitusi _identifier_ dengan sebuah pengganti atau _replacement_

## Symbolic Constant
Symbolic constant akan mengubah _identifier_ pada source code menjadi nilai dari symbolic constant tersebut. 
### Format:
Format terdiri dari 3 komponen yaitu preprocessor #define, identifier, dan replacement
```
#define identifier replacement
```
identifier berupa nama dari symbolic constant sedangkan replacement berupa apa yang akan digantikan oleh identifier. Replacement tidak terbatas pada angka dan tidak harus berupa nilai

### Contoh Penggunaan:
Penggunaan symbolic constant membuat source code lebih mudah untuk diubah karena programmer hanya perlu mengubah isi dari replacement

Contoh: 
```c
#include <stdio.h>
#define DATA_TYPE int

void foo1(DATA_TYPE x);
DATA_TYPE foo2();

int main(void){
    DATA_TYPE var;
    
    //code
    
    DATA_TYPE varArray[5];
    
    //code    
}
```
Yang dibaca oleh compiler:
```c
void foo1(int x);
int foo2();

int main(void){
    int var;
    
    //code
    
    int varArray[5];
    
    //code    
}
```
Pada kasus di atas, anggap sebuah source code memiliki sebuah variable yang akan terus berubah-ubah tipe datanya sesuai kebutuhan. 
Dengan menggunakan symbolic constant, programmer hanya perlu mengganti replacement dari symbolic constant DATA_TYPE. 
Contoh di atas berarti mengganti semua DATA_TYPE menjadi int yang berarti ``void foo1(int x)``, ``int foo2()``, ``int var``, dan ``int varArray[5]``.
Misal source code ingin variable bertipe data ``double`` maka hanya perlu mengubahnya menjadi ``#define DATA_TYPE double`` 

## Macro
Macro mirip dengan symbolic constant tetapi macro dapat menerima argument (atau dapat juga dibilang symbolic constant adalah macro tanpa argumen). Cara kerjanya sama dengan
symbolic constant ditambah sekarang menerima argumen dari user. Jumlah argumen bisa berapa saja sesuai kebutuhan

### Format
Macro dengan 1 argumen:
```
#define identifier(argument) replacement_with_argument
```

Macro dengan 2 argumen:
```
#define identifier(argument1, argument2) replacement_with_arguments
```
### Contoh Penggunaan
Penggunaan macro memungkinkan kita membuat suatu fungsi yang lebih mudah untuk diubah

Contoh:
```c
#include <stdio
#define DAMAGE(atk, def) (atk)*(100 - (def))/100

int main(void){
    int defense = 20;
    printf("Damage yang dihasilkan: ");
    printf("%d\n", DAMAGE(6000, defense));
}
```
Yang compiler baca:
```c
int main(void){
    int defense = 20;
    printf("Damage yang dihasilkan: ");
    printf("%d\n", 4800));
}
```
Pada kasus di atas, macro digunakan untuk menghitung nilai DAMAGE. 
Argumen untuk macro tersebut dapat diisi dengan nilai langsung (6000) ataupun nilai dari variabel (defense yang bernilai 20)
Macro DAMAGE akan digantikan dengan nilai 4800

#### Note
Tanda kurung pada argumen di bagian replacement penting digunakan untuk menghindari kesalahan pembacaan yang tidak diinginkan. 

Contoh: apabila macro tadi diubah menjadi ``#define DAMAGE(atk, def) atk*(100 - def)/100``, apabila diisikan DAMAGE(5500 + 500, 20) maka perhitungan akan menjadi
``5500 + 500*(100 - 20)/100`` yang menghasilkan ``5900``, sebuah kesalahan perhitungan

## Operator # dan \##
Penggunaan symbolic constant dan macro memerlukan cara khusus jika berhubungan dengan string
### Operator # atau Stringify
Operator ini merupakan operator unary dengan operand berada di kanan operator
Dengan memberikan # pada argumen di komponen replacement, maka argumen tersebut akan diubah menjadi string dan diapit oleh double quotes

Contoh:
```c
#include <stdio.h>
#define PRINT_VALUE(s, v) printf(#s, v)

int main(void){
        PRINT_VALUE(%d, 50);
}
```
Yang compiler baca:
```c
int main(void){
        printf("%d", 50);
}
```

### Operator \## atau Concat
Operator ini merupakan operator binary. Dengan memberikan ## di antara dua argumen, maka argumen tersebut akan digabung menjadi satu argumen 
Contoh:
```c
#include <stdio.h>
#define CONC(a, b) a ## b
#define TO_STRING(x) #x
#define CONC_AND_STRING(a, b) TO_STRING(a ## b)

int main(void){
        int CONC(man,tap) = 10;
        printf( CONC_AND_STRING(Hello, World) );
        puts("");
        printf( TO_STRING( CONC(Hello, World) ));
}
```
Yang dibaca compiler:
```c
int main(void){
        int mantap = 10;
        printf( "HelloWorld" );
        puts("");
        printf( "CONC(Hello, World)" );
}

/* OUTPUT
HelloWorld        
CONC(Hello, World)
*/
```
#### Note
Dapat dilihat bahwa penggunaan macro **tidak** dapat dinested (``TO_STRING( CONC(Hello, World)``) 
_tetapi_ komponen replacement dari macro dapat memuat macro lain (``#define CONC_AND_STRING(a, b) TO_STRING(a ## b)``)

## Operator \\
Operator ini digunakan apabila definisi statement preprocessor lebih dari satu baris

contoh:
```c
#define MACRO(x)  printf("Anda sedang menggunakan macro\n); \
                  printf("Argumen macro ini ialah " #x "\n"); \
                  printf("Keluar dari macro...\n");
```
