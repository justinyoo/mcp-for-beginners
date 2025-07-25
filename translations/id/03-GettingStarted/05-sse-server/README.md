<!--
CO_OP_TRANSLATOR_METADATA:
{
  "original_hash": "1681ca3633aeb49ee03766abdbb94a93",
  "translation_date": "2025-06-17T22:21:22+00:00",
  "source_file": "03-GettingStarted/05-sse-server/README.md",
  "language_code": "id"
}
-->
Sekarang setelah kita mengetahui sedikit lebih banyak tentang SSE, mari kita buat server SSE selanjutnya.

## Latihan: Membuat Server SSE

Untuk membuat server kita, kita perlu mengingat dua hal:

- Kita perlu menggunakan web server untuk membuka endpoint untuk koneksi dan pesan.
- Bangun server kita seperti biasa dengan menggunakan tools, resources, dan prompt saat kita menggunakan stdio.

### -1- Membuat instance server

Untuk membuat server kita, kita menggunakan tipe yang sama seperti dengan stdio. Namun, untuk transport, kita perlu memilih SSE.

---

Mari kita tambahkan route yang dibutuhkan selanjutnya.

### -2- Menambahkan route

Mari kita tambahkan route yang menangani koneksi dan pesan masuk:

---

Selanjutnya, mari kita tambahkan kemampuan pada server.

### -3- Menambahkan kemampuan server

Sekarang setelah kita mendefinisikan semuanya yang spesifik untuk SSE, mari kita tambahkan kemampuan server seperti tools, prompt, dan resources.

---

Kode lengkap Anda seharusnya terlihat seperti ini:

---

Bagus, kita sudah memiliki server menggunakan SSE, sekarang mari kita coba jalankan.

## Latihan: Debugging Server SSE dengan Inspector

Inspector adalah alat yang sangat bagus yang sudah kita lihat di pelajaran sebelumnya [Membuat server pertama Anda](/03-GettingStarted/01-first-server/README.md). Mari kita lihat apakah kita bisa menggunakan Inspector di sini juga:

### -1- Menjalankan inspector

Untuk menjalankan inspector, Anda harus terlebih dahulu memiliki server SSE yang berjalan, jadi mari kita lakukan itu sekarang:

1. Jalankan server

---

1. Jalankan inspector

    > ![NOTE]
    > Jalankan ini di jendela terminal yang berbeda dari tempat server berjalan. Perlu diingat juga, Anda perlu menyesuaikan perintah di bawah ini agar sesuai dengan URL tempat server Anda berjalan.

    ```sh
    npx @modelcontextprotocol/inspector --cli http://localhost:8000/sse --method tools/list
    ```

    Menjalankan inspector terlihat sama di semua runtime. Perhatikan bagaimana kita, alih-alih memberikan path ke server dan perintah untuk memulai server, kita memberikan URL tempat server berjalan dan juga menentukan route `/sse`.

### -2- Mencoba alat ini

Hubungkan server dengan memilih SSE di dropdown dan isi kolom url dengan alamat tempat server Anda berjalan, misalnya http://localhost:4321/sse. Sekarang klik tombol "Connect". Seperti sebelumnya, pilih untuk menampilkan daftar tools, pilih sebuah tool dan berikan nilai input. Anda akan melihat hasil seperti gambar di bawah:

![Server SSE berjalan di inspector](../../../../translated_images/sse-inspector.d86628cc597b8fae807a31d3d6837842f5f9ee1bcc6101013fa0c709c96029ad.id.png)

Bagus, Anda sudah bisa bekerja dengan inspector, sekarang mari kita lihat bagaimana kita bisa bekerja dengan Visual Studio Code selanjutnya.

## Tugas

Cobalah membangun server Anda dengan lebih banyak kemampuan. Lihat [halaman ini](https://api.chucknorris.io/) untuk, misalnya, menambahkan tool yang memanggil API. Anda yang menentukan seperti apa server tersebut. Selamat mencoba :)

## Solusi

[Solusi](./solution/README.md) Berikut adalah solusi yang mungkin dengan kode yang berfungsi.

## Poin Penting

Poin penting dari bab ini adalah sebagai berikut:

- SSE adalah transportasi kedua yang didukung selain stdio.
- Untuk mendukung SSE, Anda perlu mengelola koneksi dan pesan masuk menggunakan framework web.
- Anda dapat menggunakan baik Inspector maupun Visual Studio Code untuk menggunakan server SSE, sama seperti server stdio. Perhatikan perbedaannya sedikit antara stdio dan SSE. Untuk SSE, Anda perlu menjalankan server secara terpisah dan kemudian menjalankan alat inspector Anda. Untuk alat inspector, ada juga beberapa perbedaan yaitu Anda perlu menentukan URL.

## Contoh

- [Java Calculator](../samples/java/calculator/README.md)
- [.Net Calculator](../../../../03-GettingStarted/samples/csharp)
- [JavaScript Calculator](../samples/javascript/README.md)
- [TypeScript Calculator](../samples/typescript/README.md)
- [Python Calculator](../../../../03-GettingStarted/samples/python)

## Sumber Tambahan

- [SSE](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events)

## Selanjutnya

- Selanjutnya: [HTTP Streaming dengan MCP (Streamable HTTP)](/03-GettingStarted/06-http-streaming/README.md)

**Penafian**:  
Dokumen ini telah diterjemahkan menggunakan layanan terjemahan AI [Co-op Translator](https://github.com/Azure/co-op-translator). Meskipun kami berusaha untuk akurasi, harap diingat bahwa terjemahan otomatis mungkin mengandung kesalahan atau ketidakakuratan. Dokumen asli dalam bahasa aslinya harus dianggap sebagai sumber yang sah. Untuk informasi penting, disarankan menggunakan terjemahan profesional oleh manusia. Kami tidak bertanggung jawab atas kesalahpahaman atau salah tafsir yang timbul dari penggunaan terjemahan ini.