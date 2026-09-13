1. **identitas API**
* nama API: JSONPlaceholder
* penyedia: JSONPlaceholder
* jenis API: REST API
* layanan yang disediakan: JSONPlaceholder menyediakan data palsu yang dapat digunakan untuk testing dan prototyping aplikasi. API ini menyediakan beberapa resource seperti Users, posts, comments, albums, todos
* pengguna API: API ini dapat digunakan oleh developer atau aplikasi yang membutuhkan data untuk pengujian, pembelajaran dan pembuatan prototype. 
* endpoint yang digunakan: 'https://jsonplaceholder.typicode.com/users/1' endpoint ini digunakan untuk mengambil data pengguna dengan id 1. 



2\. **masalah atau kebutuhan pengguna**

* developer membutuhkan data yang dapat digunkan untuk  menguji komunikasi antara aplikasi client dengan sebuah REST API   tanpa harus membuat server dan database sendiri
* JSONPlaceholder dapat digunakan untuk menyediakan data user dalam format JSON. data tersebut dapat digunakan untuk menguji proses request dan responses pada aplikasi



3**. hasil pengujian endpoint**

pengujian dilakukan menggunkan postman



* request berhasil:

|komponen|hasil|
|-|-|
|method|get|
|url|https://jsonplaceholder.typicode.com/users/1|
|path parameter|id=1|
|header|tidak ada header|
|status code|200 OK|

response berisi data pengguna dalam format JSON



* beberapa data yang diperoleh

|field|nilai|
|-|-|
|id|1|
|name|Leanne Graham|
|username|bret|
|email|Sincere@april.biz|

response menunjukkan bahwa request berhasil  dan data penggina dengan ID 1 dapat di temukan



4\. **peta system**

alur sederhana system Ketika client  meminta data pengguna adalh

Postman / Client

&#x20;      |

&#x20;      | GET /users/1

&#x20;      v

JSONPlaceholder API

&#x20;      |

&#x20;      v

User Data

&#x20;      |

&#x20;      | data pengguna

&#x20;      v

JSONPlaceholder API

&#x20;      |

&#x20;      | 200 OK + JSON

&#x20;      v

Postman / Client



**penjelasan:** client berupa postman mengirim request GET ke JSONPlaceholder API. API menerima request dengan endpoint /users/1 dan memproses permintaan untuk mengambil data pengguna. data pengguna kemudian dikembalikan oleh API dalambentuk JSON. 



5\. **kondisi berhasil dan gagal**

* kondisi berhasil : https://jsonplaceholder.typicode.com/users/1

menghasilkan 200  OK yang artinya request berhasil dan data pengguna dengan ID dapat diterima. 

* kondisi gagal :

https://jsonplaceholder.typicode.com/users/999

menghasilkan 404 not found dan respon body yang diterima adalag {} dengan artian data pengguna dengan ID 999 tidak ditemukan. 



6\. **ide proyek semester**

* nama proyek: handmade shop API
* pengguna

system digunakan oleh

&#x20;- pelanggan: untuk  melihat produk handmade, melihat detail produk dan melakukan pemesanan

&#x20;- admin: untuk mengelola produk handmade, data pelanggan, pesanan dan status pesanan. 

* masalah atau kebutuhan:

&#x20;- pelanggan membutuhkan cara yang mudah untuk melihat berbagai produk handmade dan melakukan pemesanan secara online

&#x20;- admin membutuhkan system untuk mengelola data produk  dan pesanan dengan lebij terstruktur

REST API digunkan sebagai penghubung  antara aplikasi client dengan server sehingga data produk dan pesanan dapat dikirim dan diterima dalam format JSON. 

* resource awal

&#x20;- products = data produk handmade

&#x20;- customers = data pelanggan

&#x20;- orders = data pesanan

&#x20;- order\_details = detail produk dalam pesanan

* contoh endpoint awal

|method|endpoint|fungsi|
|-|-|-|
|GET|/api/products|menampilkan daftar produk handmade|
|GET|/api/products/{id}|menampilkan detail produk|
|POST|/api/orders|membuat pesanan|
|GET |/api/orders/{id}|melihat detail pesanan|
|PUT|/api/orders/{id}/status|mengubah status pesanan|

* batas proyek

&#x20;- tahap awal berfokus pada pengelolaan produk handmade, pembuatan pesanan, dan pemantauan status pesanan

&#x20;- fitur pembayaran online, pengiriman, dan notifikasi otomatis masih belum focus Utama untu proyek

* teknologi 

&#x20;- Laravel

&#x20;- PHP

&#x20;- MySQL

&#x20;- REST API

&#x20;- JSON

7\. **referensi resmi**

https://jsonplaceholder.typicode.com/guide

8\. **deklarasi penggunaan AI**

AI digunakan untuk alat bantu memahami materi API, Menyusun struktur, ide. pengujian API dilakukan secara langsung menggunakan postman. hasil request dan response dicatat berdasarkan hasil pengujian yang dilakukan. 



