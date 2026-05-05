## Module 8 Reflection

**1. Differences between unary, server streaming, and bidirectional streaming.**

**Unary**: Unary RPC adalah metode paling sederhana, dimana client mengirim satu request dan 
menerima satu response. Metode ini dapat digunakan untuk operasi sederhana seperti autentikasi atau 
pengambilan satu data.

**Server Streaming**: Server streaming memungkinkan client mengirim satu request, tetapi server 
mengirim banyak response secara bertahap. Metode ini dapat digunakan untuk data besar atau update 
yang berkelanjutan seperti riwayat transaksi atau live feed.

**Bidirectional Streaming**: Bidirectional streaming memungkinkan client dan server saling 
mengirim data secara terus-menerus dalam satu koneksi. Metode ini dapat digunakan untuk aplikasi real-time
seperti chat.

<br>

**2. Security considerations in Rust gRPC**

Aspek security dalam gRPC merupakan:

**Authentication**: verifikasi identitas user (seperti dengan menggunakan token atau OAuth)
**Authorization**: mengatur hak akses user terhadap service atau data tertentu
**Encryption**: menggunakan TLS agar data transmission secure

Tanpa security, sistem rentan terhadap akses ilegal dan kebocoran data.

<br>

**3. Challenges in bidirectional streaming**

- Mengelola komunikasi dua arah secara bersamaan (concurrency)
- Potensi race condition atau deadlock
- Penanganan error yang lebih kompleks karena kedua sisi aktif
- Menjaga stabilitas koneksi dalam jangka waktu yang panjang 
- Memastikan pesan tidak hilang dan tetap berurutan dalam aplikasi chat

<br>

**4. ReceiverStream advantages and disadvantages**

**Kelebihan:**

- Mudah digunakan dengan sistem async Rust (Tokio)
- Dapat mengkonversi channel ke stream dengan baik
- Cocok untuk data streaming yang menghandle continuous data

**Kekurangan:**

- Perlu pengelolaan channel manual
- Perlu pengaturan buffer yang tepat
- Bisa menambah kompleksitas jika tidak dikelola dengan baik

<br>

**5. Structuring code for modularity**

Untuk meningkatkan maintainability, beberapa hal yang dapat dilakukan adalah:
- Memisahkan service ke dalam file/module berbeda
- Menggunakan trait dan interface untuk abstraksi
- Menghindari duplikasi kode
- Menyusun proto file yang clean dan reusable

<br>

**6. Improving MyPaymentService**

- Validasi data pembayaran
- Integrasi dengan payment gateway 
- Error handling untuk transaksi gagal
- Logging dan audit
- Sistem keamanan (misalnya deteksi fraud)

<br>

**7. Impact of gRPC on system architecture**

gRPC meningkatkan performa karena menggunakan HTTP/2 dan Protobuf. Selain itu, komunikasi 
menjadi lebih efisien dan terstruktur.

Namun, gRPC kurang fleksibel dibanding REST dalam hal interoperabilitas dengan sistem lain 
yang berbasis JSON/HTTP API.

<br>

**8. HTTP/2 vs HTTP/1.1 / WebSocket**

**Kelebihan HTTP/2:**

- Multiplexing (banyak request dalam satu koneksi)
- Lebih cepat dan efisien
- Mendukung streaming

**Kekurangan:**

- Lebih kompleks
- Tidak semua sistem lama mendukung

<br>

**9. REST vs gRPC (real-time communication)**

**REST** menggunakan model request-response, sehingga kurang efisien untuk real-time karena harus polling.

**gRPC** mendukung streaming, sehingga komunikasi bisa berlangsung secara langsung dan lebih responsif.

Oleh karena itu, gRPC lebih baik untuk sistem interaktif seperti chat atau dashboard live.

<br>

**10. Protobuf vs JSON**

**Protobuf:**

- Lebih cepat dan efisien
- Ukuran data lebih kecil
- Harus memiliki schema

**JSON:**

- Lebih fleksibel dan mudah dibaca
- Tidak membutuhkan schema
- Ukuran data lebih besar dan lebih lambat
