[<< Materi sebelumnya (Multidimensional Array) <<](2-ArrayMultidimensi.md)

# 5.3 Array Sebagai Parameter Fungsi

Layaknya tipe data lainnya, kalian pun dapat mengirimkan/passing sebuah array ke sebuah fungsi. Terdapat dua tipe yaitu pass array secara keseluruhan dan pass elemen array.

## Pass array secara keseluruhan
Caranya ialah dengan mengset parameter fungsi untuk menerima tipe array. Jangan lupa juga untuk mengirimkan panjang dari array tersebut. 
Contoh pass array of int ke fungsi bernama **foo**:
```c 
int foo(int arr[], int panjang_arr)
```
Saat mengirimkan array sebagai argumen, masukkan **nama array** nya
```c
int arr[3] = {0};
foo(arr, 3);
```
Tipe passing ini ialah _pass by reference_ yang berarti kita bisa memodifikasi array yang dipassing. Mengapa begitu? kalian akan mempelajarinya lebih lanjut pada materi **pointer** di pertemuan yang mendatang

Contoh implementasi
```c
void ubahArray(int arr[], int arr_length, int index, int new_value){
    if(index < arr_length) { //memastikan index yang akan diubah tidak melebihi panjang array
        arr[index] = new_value;
    } else {
        printf("index array tidak valid\n");
    }    
}
void tampilkanArray(int arr[], int arr_length){
    printf("Isi dari array:\n");
    for(int i=0; i<arr_length;i++){
        printf("index ke-%d = %d\n", i, arr[i]);
    }
}

int main(void){
    int numbers[5] = {1, 3, 5, 7, 9};
    printf("Array mula-mula\n");
    tampilkanArray(numbers, 5);
    ubahArray(numbers, 5, 2, 100);
    printf("Array setelah dimodifikasi\n");
    tampilkanArray(numbers, 5);
}

/* OUTPUT
Array mula-mula
Isi dari array:
index ke-0 = 1
index ke-1 = 3
index ke-2 = 5
index ke-3 = 7
index ke-4 = 9
Array setelah dimodifikasi
Isi dari array:
index ke-0 = 1
index ke-1 = 3
index ke-2 = 100
index ke-3 = 7
index ke-4 = 9
*/

```

## Pass elemen array

Caranya ialah seperti pass variable pada umumnya yaitu mengset parameter sesuai tipe data
```c
int foo(int value_from_array)
```
Kirim elemen array dengan mengakses array menggunakan index yang diinginkan
```c
int arr[3] = {100,200,300}
foo(arr[1]); //akan mengirimkan isi dari arr index ke 1, yaitu 200
```
Perlu diperhatikan bahwa proses passing diatas ialah _pass by value_

## Extras

### 1. Alternatif parameter

Kalian dapat juga mengset parameter fungsi untuk menerima tipe array menggunakan cara berikut
```c
int foo(int* arr, int panjang_arr)
```
   
### 2. Hanya ingin membaca array, bukan memodifikasi array

Jika kalian hanya ingin mengakses isi dari array TANPA mengubahnya, kalian bisa menambahkan **const** pada parameter array tersebut. **const** atau constant membuat array tidak dapat dimodifikasi.\
Kalian akan memperdalam **const** di pertemuan mendatang.
```c
int foo(const int* arr, int panjang_arr)
```

[Menuju Silabus >>](../silabus.md)


   
 
        
