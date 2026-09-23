minggu 2 - Implementasi HTTP dan REST API

tujuan:
menerapkan konsep http, rest api, json dan status code pada projek laravel serta melakukan pengujian endpoint menggunakan postman.

perubahan:
mengaktifkan fitur api pada projek laravel menggunakan `php artisan install:api`. kemudian menambahkan endpoint pada `routes/api.php` untuk resource `posts`. endpoint yang dibuat yaitu `GET /api/posts` , `GET /api/posts/{id}`. response api menggunakan format json dengan status code yang sesuai.

endpoint atau contract:
method : get
endpoint, fungsi dan status : 'api/posts' . mengambil daftar post, 200.
endpoint, fungsi dan status : `/api/posts/{id}` , mengambilpost berdasarkan id , 200.
endpoint, fungsi dan status : `/api/posts/{id}` , id tidak ditemukan , 404.
contoh endpoint : `GET http://laravelcitra.test/api/posts/1` endpoint menggunakan method `get` karena digunakan untuk mengambil data. resource direpresentasikan dengan `/posts`, sedangkan `{id}` digunakan untuk menentukan post tertentu.

bukti pengujian:

- sukses response
request : `GET http://laravelcitra.test/api/posts/1`
hasil : status : 200 OK
: response : json
: data post berhasil di tampilkan
<!-- {
    "data": {
        "id": 1,
        "title": "Belajar Laravel REST API",
        "author": "Maria Citra"
    }
} -->
- error response
request : `GET http://laravelcitra.test/api/posts/999`
hasil : status : 404 not found
: response : json
: data post tidak ditemukan
<!-- {
    "message": "Post tidak ditemukan"
} -->

error case:
error terjadi ketika client meminta post dengan ID yang tidak tersedia.
request: `GET /api/posts/999`. api memberika status 404 not found karena resource yang diminta tidak ditemukan.

kesimpulan:
project laravel berhasil menerapkan http method get, rest api, json dan status code. pengujian ini menggunakan postman menunjukan bawa api memberikan 200 OK ketika data tersedia dan berhasil ditemukan sedangakan 404 not found ketika data tidak tersedia atau tidak ditemukan.

referensi:
dokumentasi laravel: https://laravel.com/docs
dokumentasi laravel routing: https://laravel.com/docs/routing
dokumentasi postman: htps:/learning.postman.com/docs/
MDN HTTP: https://developer.mozilla.org/en-US/docs/Web?HTTP

deklarasi penggunaan AI:
ai ini digunakan untuk alat bantu dan memahami konsep dalam HTTP, REST API, JSON dan status code. serta membantu refrensi mana saja yang harus di pilih dan membantu memahami dan menjelaskan projek yang belum dimengerti dan belum di pahami.
