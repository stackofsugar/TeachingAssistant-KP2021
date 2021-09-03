[<< Materi Sebelumnya (Silabus) <<](../silabus.md)
# 4.1 Pengenalan Function

Fungsi merupakan kumpulan pernyataan yang menjalankan suatu tugas. Setiap C++ program setidaknya memiliki satu fungsi yaitu fungsi main(). Kalian setidaknya dapat membagi kode anda dalam beberapa fungsi yang berbeda dengan tiap fungsi mengerjakan tugas yang spesifik. Deklarasi fungsi menyatakan nama, return type, dan parameter dari suatu fungsi. Ketika, mendefinisikan suatu fungsi, Kalian juga dapat menuliskan isi dari fungsi tersebut.

C++ standard library menydiakan beberapa fungsi bawaan yang dapat dipanggil langsung oleh program kalian. Contoh fungsi bawaan tersebut diantaranya adalah strcat() yang digunakan untuk menggabungkan dua buah string, lalu ada fungsi memcpy() yang digunakan ketika menyalin dari satu lokasi memori ke lokasi yang lain, dan masih banyak lagi.

## Defining Function

```
  return_type function_name(parameter list){
    body_function;
  }
```

- __Return type__   : return_type merupakan tipe data dari nilai yang dikembalikan oleh fungsi, tetapi terdapat fungsi yang tidak perlu menggunakan pengembalian nilai, yaitu fungsi yang memiliki return_type **void**.
- __Function name__ : function_name adalah nama dari suatu fungsi yang memiliki keunikan agar membedakan dengan fungsi yang lain. 
- __Parameter__     : ketika suatu fungsi dipanggil, kalian memberikan nilai ke parameter, parameter sendiri bersifat opsional sehingga beberapa fungsi mungkin tidak terdapat parameter
- __Body Function__ : berisikan suatu kode yang mendefinisikan bagaimana fungsi tersebut bekerja.

### Example
Berikut merupakan fungsi untuk menentukan nilai terbesar dari ketiga parameter dengan menggunakan pemilihan if else.

```
  int biggest(int num1, int num2, int num3){
    
    //deklarasi variabel lokal
    int max;
    
    if(num1 > num2 && num1 > num3) max = num1;
    else if(num2 > num1 && num2 > num3) max = num2;
    else{
      max = num3;
    }
    
    return max;
  }
```

## Function Declarations
Deklarasi fungsi berfungsi untuk memberitahu compiler nama fungsi dan bagaimana fungsi tersebut dipanggil. Dengan adanya deklarasi fungsi, isi dari suatu fungsi dapat didefinisikan secara terpisah

```
  return_type function_name( parameter list );
```

Jika fungsi _biggest_ dideklarasikan, akan menjadi seperti berikut,

```
  int biggest(int num1, int num2, int num3);
```

Sebenarnya, nama dari parameter tidak terlalu penting saat fungsi tersebut dideklarasikan. Maka dari itu dapat juga dituliskan sebagai berikut,

```
  int biggest (int, int, int);
```

Deklarasi fungsi diharuskan ketika kalian mendefinisikan fungsi pada suatu file dan memanggil fungsi tersebut pada file yang lain, mendeklarasikan fungsi diletakkan pada bagian atas dari  _code_ yang memanggil fungsi tersebut. 
