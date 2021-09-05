[<< Materi Sebelumnya (Silabus) <<](../silabus.md)
# 4.1 Pengenalan Function

Fungsi merupakan kumpulan pernyataan yang menjalankan suatu tugas. Setiap program C setidaknya memiliki satu fungsi yaitu fungsi `main`. Kalian setidaknya dapat membagi kode anda dalam beberapa fungsi yang berbeda dengan tiap fungsi mengerjakan tugas yang spesifik. Deklarasi fungsi menyatakan nama, return type, dan parameter dari suatu fungsi. Ketika, mendefinisikan suatu fungsi, Kalian juga dapat menuliskan isi dari fungsi tersebut.

C standard library menydiakan beberapa fungsi bawaan yang dapat dipanggil langsung oleh program kalian. Contoh fungsi bawaan tersebut diantaranya adalah printf() yang digunakan untuk menampilkan output ke console, lalu ada fungsi scanf() yang untuk menerima input dari console, dan masih banyak lagi.

## Mendefinisikan Function

```c
/* return_type */ /* function_name */(/* parameters... */){
	/* perintah... */
	return /* suatu nilai */; /* opsional, jika return type bukan void */
}
```

- __Return type__   : return_type merupakan tipe data dari nilai yang dikembalikan oleh fungsi, tetapi terdapat fungsi yang tidak perlu menggunakan pengembalian nilai, yaitu fungsi yang memiliki return_type **void**.
- __Function name__ : function_name adalah nama dari suatu fungsi yang memiliki keunikan agar membedakan dengan fungsi yang lain
- __Parameters__    : ketika suatu fungsi dipanggil, kalian memberikan nilai ke parameter untuk nantinya disubstitusikan dalam body function tersebut. Parameter sendiri bersifat opsional sehingga beberapa fungsi mungkin tidak terdapat parameter (diisi dengan `()` kosong)
- __Body Function__ : berisikan suatu kode yang mendefinisikan bagaimana fungsi tersebut bekerja.

### Example

Berikut merupakan fungsi untuk menghitung volume n-buah kubus identik (memiliki panjang sisi yang sama) yang menghasilkan suatu nilai (return value) bertipe `double`.

```c
/*
Fungsi ini memiliki
- Return type : double
- Function name : hitung_volume_n_kubus
- Parameters : double panjang_sisi, int n
*/
double hitung_volume_n_kubus(double panjang_sisi, int n) {
	double total_volume = 0.0;
	int i;

	/* ulang sebanyak n kali */
	for (i = 1; i <= n; i++) {
		/* hitung volume 1 kubus */
		double volume_satu_kubus = panjang_sisi * panjang_sisi * panjang_sisi;

		/* tambahkan ke total volume */
		total_volume = total_volume + volume_satu_kubus;
	}

	return total_volume; /* hasil dari fungsi adalah total volume seluruh kubus */
}
```

## Mendeklarasikan Function
Deklarasi fungsi berfungsi untuk memberitahu compiler nama fungsi dan bagaimana fungsi tersebut dipanggil. Dengan adanya deklarasi fungsi, isi dari suatu fungsi dapat didefinisikan secara terpisah

```c
/* return_type */ /* function_name */(/* parameters... */);
```

Jika fungsi `hitung_volume_n_kubus` dideklarasikan terlebih dahulu, akan menjadi seperti berikut,

```c
double hitung_volume_n_kubus(double panjang_sisi, int n);
```

Sebenarnya, nama dari parameter tidak terlalu penting saat fungsi tersebut dideklarasikan atau dapat dihilangkan. Maka dari itu dapat juga dituliskan sebagai berikut,

```c
double hitung_volume_n_kubus(double, int); /* panjang_sisi dan n dihilangkan, tinggal tipe data dari tiap-tiap parameter saja */
```

**N.B.** Deklarasi fungsi diharuskan ketika kalian mendefinisikan fungsi pada suatu file dan memanggil fungsi tersebut pada file yang lain, mendeklarasikan fungsi diletakkan pada bagian atas dari  _code_ yang memanggil fungsi tersebut. 

## Memanggil Function

Memanggil fungsi adalah kegiatan di mana kita menjalankan fungsi yang telah kita definisikan sebelumnya dengan memasukkan nilai tertentu sebagai parameter. Sebelum dipanggil, ada baiknya fungsi tersebut dideklarasikan atau didefinisikan terlebih dahulu sehingga tidak terjadi error.

Pada saat memanggil suatu fungsi, kalian perlu memasukkan nilai untuk tiap-tiap parameter bersamaan dengan nama fungsi.

Jika fungsi tersebut me-*return* (atau menghasilkan) suatu nilai, maka nilai yang dikembalikan tersebut dapat disimpan terlebih dahulu.

Contoh adalah jika anda ingin memanggil fungsi `hitung_volume_n_kubus` yang telah dideklarasikan tadi dengan `panjang_sisi` bernilai 4.0 dan `n` bernilai 10, maka penggunaannya adalah:
```c
double hasil;

/* ... */

/* variabel `hasil` akan bernilai 640.0 (karena 4*4*4 = 64 untuk 1 kubus kemudian dikalikan dengan 10 yaitu 640 */
hasil = hitung_volume_n_kubus(4.0, 10);
```

### Source Code


<details>
<summary>Contoh Source Code</summary>
  
```c
#include <stdio.h>

/* pendeklarasian fungsi */
double hitung_volume_n_kubus(double panjang_sisi, int n); 

int main(){
	double sisi;
	int jumlah;
	double hasil;

	printf("Masukkan panjang sisi kubus: ");
	scanf("%lf", &sisi);

	printf("Masukkan jumlah kubus: ");
	scanf("%d", &jumlah);

	/* pemanggilan fungsi */
	/* nilai yang dimasukkan sebagai parameter adalah variabel `sisi` sebagai panjang_sisi dan `jumlah` sebagai n */
	/* seluruh perintah dalam definisi fungsi hitung_volume_n_kubus kemudian dijalankan dan menghasilkan suatu nilai atau return value yang kemudian disimpan dalam variabel `hasil` */
	hasil = hitung_volume_n_kubus(sisi, jumlah);
	
	printf("Volume total : %f\n", hasil);

	return 0;
}

/* pendefinisian fungsi */
double hitung_volume_n_kubus(double panjang_sisi, int n) {
	double total_volume = 0.0;
	int i;

	/* ulang sebanyak n kali */
	for (i = 1; i <= n; i++) {
		/* hitung volume 1 kubus */
		double volume_satu_kubus = panjang_sisi * panjang_sisi * panjang_sisi;

		/* tambahkan ke total volume */
		total_volume = total_volume + volume_satu_kubus;
	}

	return total_volume; /* hasil dari fungsi adalah total volume seluruh kubus */
}

/*
Output:

Masukkan panjang sisi kubus: 4
Masukkan jumlah kubus: 10
Volume total : 640.000000
*/
```
</details>

<details>
<summary>Contoh source code fungsi yang memiliki return type "void"</summary>

```c
#include <stdio.h>

/* pendeklarasian fungsi */
void quack(int n);

int main(){
    int jumlah;
    
    printf("Masukkan jumlah quack: ");
    scanf("%d", &jumlah);
    
    /* pemanggilan fungsi */
    quack(jumlah);
	
    return 0;
}

/* pendefinisian fungsi */
void quack(int n) {
    int i;
    
    for (i = 1; i <= n; i++) {
        printf("Quack!\n");
    }
}

/*
Output:

Masukkan jumlah quack: 4 
Quack!
Quack!
Quack!
Quack!
*/
```
</details>

<details>
<summary>Contoh source code fungsi yang tidak memiliki satupun parameter</summary>

```c
#include <stdio.h>

/* pendeklarasian fungsi */
void quack_3_kali();

int main(){
	/* pemanggilan fungsi */
	quack_3_kali();

	return 0;
}

/* pendefinisian fungsi */
void quack_3_kali() {
    printf("Quack!\n");
    printf("Quack!\n");
    printf("Quack!\n");
}
```
</details>
