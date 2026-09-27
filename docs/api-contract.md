# API Contract — Handmade Shop

## User Stories

### User Story 1
- Role: Customer
- Goal: Melihat daftar produk handmade yang tersedia
- Benefit: Customer dapat mengetahui produk yang tersedia sebelum melakukan pemesanan.

### User Story 2
- Role: Customer
- Goal: Membuat dan mengubah data produk handmade
- Benefit: Data produk dapat dikelola melalui API secara terstruktur.

## Resource Dictionary

### Resource: products

| Field | Type | Required saat create | Akses | Aturan | Contoh |
| --- | --- | --- | --- | --- | --- |
| id | integer | Tidak | Read-only | Auto-generated | 1 |
| name | string | Wajib | Writable | Minimal 3 karakter | "Tas Rajut Handmade" |
| description | string | Wajib | Writable | - | "Tas rajut buatan tangan berbahan katun berkualitas" |
| price | number | Wajib | Writable | Harus lebih dari 0 | 75000 |
| stock | integer | Wajib | Writable | Minimal 0 | 10 |
| category | string | Wajib | Writable | - | "Rajutan" |
| created_at | datetime | Tidak | Read-only | Auto-generated | "2026-09-27T10:00:00Z" |

## Endpoint Matrix

### Resource: products

| Method | Endpoint | Success | Error |
| --- | --- | --- | --- |
| GET | /api/products | 200 OK | - |
| POST | /api/products | 201 Created | 422 Unprocessable Entity |
| GET | /api/products/{product} | 200 OK | 404 Not Found |
| PATCH | /api/products/{product} | 200 OK | 404 Not Found, 422 Unprocessable Entity |
| DELETE | /api/products/{product} | 204 No Content | 404 Not Found |

**Keterangan:**
- Endpoint menggunakan kata benda jamak "products".
- `{product}` digunakan untuk mengidentifikasi satu produk.
- Format response menggunakan JSON kecuali DELETE yang berhasil menggunakan 204 No Content.

## Create Request

- **Endpoint:** `POST /api/products`
- **Headers:**
  - `Content-Type: application/json`
  - `Accept: application/json`

**Request Body:**
```json
{
  "name": "Buket Bunga Mini",
  "description": "Buket bunga handmade dengan desain sederhana.",
  "price": 75000,
  "stock": 10,
  "category": "Buket"
}
```

### 201 Created — Success Response

```json
{
  "data": {
    "id": 1,
    "name": "Buket Bunga Mini",
    "description": "Buket bunga handmade dengan desain sederhana.",
    "price": 75000,
    "stock": 10,
    "category": "Buket",
    "created_at": "2026-09-27T10:00:00Z"
  }
}
```

## 404 Not Found

- **Endpoint:** `GET /api/products/{product}`

**Response Body:**
```json
{
  "message": "Product not found",
  "errors": null
}
```

## 422 Unprocessable Content

- **Endpoint:** `POST /api/products`

**Response Body:**
```json
{
  "message": "The given data was invalid.",
  "errors": {
    "name": [
      "The name field is required."
    ],
    "price": [
      "The price must be greater than 0."
    ]
  }
}
```

## 200 OK

- **Endpoint:** `GET /api/products`

**Response Body:**
```json
{
  "data": [
    {
      "id": 1,
      "name": "Buket Bunga Mini",
      "description": "Buket bunga handmade dengan desain sederhana.",
      "price": 75000,
      "stock": 10,
      "category": "Buket",
      "created_at": "2026-09-27T10:00:00Z"
    }
  ]
}
```

## Design Decisions

- Menggunakan resource `products` dengan endpoint berbentuk plural noun agar struktur API konsisten.
- Menggunakan PATCH untuk perubahan sebagian field produk tanpa harus mengirim seluruh data produk.
