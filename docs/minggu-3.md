# Dokumentasi Tugas 3: API Contract dan Resource Modelling

- **Nama**: Maria Citra
- **NIM**: 202434001
- **Mata Kuliah**: Praktikum Manajemen Web Servis (Semester 5)
- **Topik**: API Contract dan Resource Modelling (Resource: Posts)

---

## 1. Pendahuluan dan Tujuan

Pada Tugas 3 ini, fokus pembelajaran adalah memahami dan menyusun **API Contract** serta melakukan **Resource Modelling** pada RESTful API. API Contract berfungsi sebagai acuan formal atau kesepakatan antara pengembang backend (*provider*) dan pengembang frontend/klien (*consumer*), sehingga format data, endpoint, parameter, dan status code terdefinisi secara jelas sebelum maupun sesudah implementasi.

### Tujuan Praktikum:
1. Memodelkan resource `posts` dengan menentukan atribut, tipe data, serta aturan akses datanya.
2. Menyusun API Contract terstandarisasi untuk endpoint yang tersedia pada layanan backend.
3. Mendokumentasikan spesifikasi request dan response untuk status sukses (`200 OK`) maupun skenario error (`404 Not Found`).
4. Memvalidasi implementasi endpoint pada Laravel terhadap API Contract menggunakan Postman.

---

## 2. User Stories

| ID | Role | Goal (Tujuan) | Benefit (Manfaat) |
| :--- | :--- | :--- | :--- |
| **US-01** | Client / Consumer | Mengambil seluruh daftar postingan (*posts*) | Pengguna dapat melihat katalog/daftar artikel yang tersedia secara lengkap. |
| **US-02** | Client / Consumer | Mengambil detail satu postingan berdasarkan `id` | Pengguna dapat membaca rincian postingan tertentu yang dipilih. |
| **US-03** | Client / Consumer | Mendapatkan respon informasi yang tepat saat postingan tidak ditemukan | Aplikasi klien dapat mengetahui bahwa data tidak ada dan menampilkan pesan yang ramah kepada pengguna tanpa terjadi *crash*. |

---

## 3. Resource Modelling (Resource: `posts`)

Resource modelling adalah proses mengidentifikasi entitas data, relasi, dan perilakunya di dalam arsitektur REST. Dalam sistem ini, entitas utama yang dimodelkan adalah `posts`.

### 3.1 Resource Dictionary

Tabel berikut menjelaskan kamus data (*resource dictionary*) untuk atribut entitas `posts`:

| Field | Tipe Data | Nullable / Required | Akses | Deskripsi & Aturan | Contoh Nilai |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `id` | Integer | Required (Auto) | Read-only | Pengidentifikasi unik dari setiap postingan | `1` |
| `title` | String | Required | Read-only / Writable | Judul dari postingan artikel | `"Belajar Laravel REST API"` |
| `author` | String | Required | Read-only / Writable | Nama pembuat atau penulis artikel | `"Maria Citra"` |

### 3.2 Response Envelope Pattern
Untuk menjaga konsistensi pada tingkat aplikasi klien, setiap respon sukses dibungkus dalam *envelope* berlabel properti `"data"`. Dengan konvensi ini:
- Respon koleksi (*list*) mengembalikan objek berisikan array objek pada properti `"data"`.
- Respon entitas tunggal (*detail*) mengembalikan objek tunggal di dalam properti `"data"`.
- Respon kegagalan/error mengembalikan objek berisikan properti `"message"`.

---

## 4. API Contract & Endpoint Matrix

### 4.1 Endpoint Matrix

| Method | Endpoint | Fungsi | Parameter | Success Response | Error Response |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `GET` | `/api/posts` | Mengambil seluruh daftar postingan | Tidak ada | `200 OK` | - |
| `GET` | `/api/posts/{id}` | Mengambil detail postingan berdasarkan ID | Path parameter: `id` (integer) | `200 OK` | `404 Not Found` |

### 4.2 Informasi Environment
- **Base URL**: `http://laravelcitra.test` (atau `http://localhost:8000`)
- **Default Headers**:
  - `Accept: application/json`

---

## 5. Rincian Spesifikasi Endpoint

### 5.1 GET /api/posts — Mengambil Daftar Postingan

Menampilkan seluruh koleksi resource `posts` yang tersedia pada sistem.

- **HTTP Method**: `GET`
- **Endpoint**: `/api/posts`
- **URL Penuh**: `http://laravelcitra.test/api/posts`
- **Request Headers**:
  ```http
  Accept: application/json
  ```
- **Request Body**: *None*

#### Response Sukses — 200 OK
- **Status Code**: `200 OK`
- **Content-Type**: `application/json`
- **Body**:
  ```json
  {
    "data": [
      {
        "id": 1,
        "title": "Belajar Laravel REST API",
        "author": "Maria Citra"
      },
      {
        "id": 2,
        "title": "Belajar HTTP dan JSON",
        "author": "Maria Citra"
      }
    ]
  }
  ```

---

### 5.2 GET /api/posts/{id} — Mengambil Detail Postingan (Sukses)

Mengambil data satu postingan berdasarkan parameter ID unik yang dicari.

- **HTTP Method**: `GET`
- **Endpoint**: `/api/posts/{id}`
- **URL Penuh**: `http://laravelcitra.test/api/posts/1`
- **Path Parameters**:
  - `id` (integer, required): ID postingan yang ingin ditampilkan (misal: `1` atau `2`).
- **Request Headers**:
  ```http
  Accept: application/json
  ```
- **Request Body**: *None*

#### Response Sukses — 200 OK
- **Status Code**: `200 OK`
- **Content-Type**: `application/json`
- **Body**:
  ```json
  {
    "data": {
      "id": 1,
      "title": "Belajar Laravel REST API",
      "author": "Maria Citra"
    }
  }
  ```

---

### 5.3 GET /api/posts/{id} — Resource Tidak Ditemukan (Error Case)

Kondisi yang terjadi ketika client meminta data postingan dengan ID yang tidak terdaftar di sistem.

- **HTTP Method**: `GET`
- **Endpoint**: `/api/posts/{id}`
- **URL Penuh**: `http://laravelcitra.test/api/posts/999`
- **Path Parameters**:
  - `id` (integer, required): ID postingan yang tidak ada di sistem (contoh: `999`).
- **Request Headers**:
  ```http
  Accept: application/json
  ```
- **Request Body**: *None*

#### Response Error — 404 Not Found
- **Status Code**: `404 Not Found`
- **Content-Type**: `application/json`
- **Body**:
  ```json
  {
    "message": "Post tidak ditemukan"
  }
  ```

---

## 6. Skenario Error & Penanganan Status Code

| Skenario | Request | Status Code | Respon Body | Alasan Pemilihan Status |
| :--- | :--- | :--- | :--- | :--- |
| ID Post terdaftar | `GET /api/posts/1` | `200 OK` | `{"data": {...}}` | Data ditemukan dan berhasil dikembalikan kepada client. |
| ID Post tidak terdaftar | `GET /api/posts/999` | `404 Not Found` | `{"message": "Post tidak ditemukan"}` | Resource yang ditargetkan oleh URI tidak ditemukan di server. Format error mengembalikan pesan informatif agar client dapat menangani kondisi data kosong dengan baik. |

---

## 7. Bukti Pengujian Postman

Pengujian dilakukan menggunakan Postman Collection `minggu 3 - tugas 3` (`docs/postman/week-03-api-contract.postman_collection.json`):

1. **Request: GET - List Posts**
   - **Method**: `GET`
   - **URL**: `http://laravelcitra.test/api/posts`
   - **Hasil Status**: `200 OK`
   - **Hasil Output**: Menampilkan array berisi daftar 2 postingan dalam properti `data`.

2. **Request: GET - Post Detail**
   - **Method**: `GET`
   - **URL**: `http://laravelcitra.test/api/posts/1`
   - **Hasil Status**: `200 OK`
   - **Hasil Output**: Mengembalikan objek tunggal postingan dengan ID 1 (`Belajar Laravel REST API`, author: `Maria Citra`).

3. **Request: GET - Post Not Found**
   - **Method**: `GET`
   - **URL**: `http://laravelcitra.test/api/posts/999`
   - **Hasil Status**: `404 Not Found`
   - **Hasil Output**: Mengembalikan objek JSON `{"message": "Post tidak ditemukan"}`.

Seluruh hasil pengujian pada Postman berjalan sukses dan konsisten terhadap API Contract yang telah didefinisikan.

---

## 8. Keputusan Desain (Design Decisions)

1. **Penamaan Noun Jamak (*Plural Resource*)**:
   Endpoint menggunakan `/posts` alih-alih `/post` sesuai dengan konvensi standar RESTful API untuk menunjukkan koleksi entitas.
2. **Kesesuaian HTTP Method**:
   Metode yang digunakan adalah `GET` karena operasi hanya bersifat membaca (*read-only*), aman (*safe*), dan idempoten (*idempotent*), tanpa mengubah status (*state*) pada server.
3. **Penggunaan Path Parameter untuk Identitas Entitas**:
   Menggunakan parameter jalur `{id}` pada `/api/posts/{id}` untuk merujuk secara spesifik ke satu instance resource.
4. **Standardisasi Envelope Data**:
   Membungkus respon data sukses dalam atribut `"data"` agar mempermudah deserialisasi dan integrasi di sisi client aplikasi.
5. **Kesesuaian Semantic Status Code**:
   - Menggunakan kode `200 OK` saat data ditemukan.
   - Menggunakan kode `404 Not Found` alih-alih `200 OK` dengan null/array kosong pada query detail resource, agar client dapat menangani status kegagalan sesuai standar HTTP.

---

## 9. Kesimpulan

Penerapan API Contract dan Resource Modelling pada resource `posts` memberikan kejelasan struktural bagi pengembang dalam memahami bentuk endpoint, format data, dan penanganan kondisi error. Pengujian melalui Postman membuktikan bahwa endpoint `GET /api/posts` dan `GET /api/posts/{id}` pada proyek Laravel telah memenuhi kontrak API yang disepakati dengan mengembalikan status `200 OK` untuk data valid dan `404 Not Found` untuk data yang tidak ditemukan.

---

## 10. Referensi

- Dokumentasi Laravel Routing: [https://laravel.com/docs/routing](https://laravel.com/docs/routing)
- Dokumentasi Laravel Controller & Response: [https://laravel.com/docs/responses](https://laravel.com/docs/responses)
- MDN Web Docs - HTTP Status Codes: [https://developer.mozilla.org/en-US/docs/Web/HTTP/Status](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- Postman Learning Center: [https://learning.postman.com/docs/](https://learning.postman.com/docs/)

---

## 11. Deklarasi Penggunaan AI

Dokumentasi ini disusun dengan bantuan AI sebagai alat bantu untuk memformat, menstrukturkan dokumen, serta merumuskan analisis API Contract dan Resource Modelling secara rapi dan komprehensif. Seluruh data endpoint, pengujian, dan respon JSON disesuaikan secara langsung dengan kode yang sudah ada pada proyek Laravel dan pengujian Postman.
