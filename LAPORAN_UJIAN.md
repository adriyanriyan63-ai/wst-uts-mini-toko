# Laporan UTS Web Software Tools

**Nama:** [Isi nama]
**Nomor Induk Mahasiswa:** [Isi NIM]
**Kelas:** [Isi kelas]
**Tanggal:** 11 November 2026

## A. Bukti pemeriksaan masalah
| Masalah | Alat yang digunakan | Bukti pemeriksaan | Perkiraan penyebab | Perbaikan | Hasil setelah perbaikan |
|---|---|---|---|---|---|
| Produk | Node.js dan PowerShell (`Invoke-WebRequest`) | Sebelum perbaikan, `/api/barang` merespons HTTP 404, sedangkan `/api/products` merespons HTTP 200 dan mengembalikan 4 produk. Setelah perbaikan, halaman menampilkan 4 produk. | URL endpoint pada `public/app.js` tidak sesuai dengan endpoint yang disediakan server. | Mengubah URL fetch dari `/api/barang` menjadi `/api/products`. | Endpoint mengembalikan 4 produk dan daftar produk tampil pada halaman. |
| Tombol keranjang | Inspeksi kode JavaScript dan uji browser | Selector `.add-to-cart` tidak cocok dengan kelas tombol `.add-button`, sehingga handler klik tidak terpasang. Setelah selector disamakan, klik tombol menampilkan 1 barang di keranjang dengan total Rp 75.000. | Selector event listener berbeda dari kelas pada tombol yang dirender. | Mengubah selector event listener menjadi `.add-button`. | Tombol berhasil menambahkan Mouse Nirkabel ke keranjang; jumlah dan total belanja diperbarui. |
| Total belanja | Pengujian otomatis Node.js (`node --test`) | Sebelum perbaikan, 2 dari 7 tes gagal: barang berjumlah 2 dihitung Rp 75.000, seharusnya Rp 150.000; kombinasi jumlah 2 dan 3 dihitung Rp 225.000, seharusnya Rp 600.000. Setelah perbaikan, 7 dari 7 tes lulus. | Fungsi `calculateTotal` menjumlahkan harga satuan tanpa mengalikannya dengan jumlah barang. | Mengubah perhitungan menjadi `item.price * item.quantity` untuk setiap barang. | Semua skenario jumlah barang menghasilkan total yang sesuai; 7 tes lulus. |

## B. Hasil pengujian
- Jumlah pengujian sebelum perbaikan total belanja: 7 tes; 5 berhasil dan 2 gagal.
- Jumlah pengujian berhasil setelah perbaikan: 7 dari 7 tes.
- Catatan perubahan pada fungsi yang diperiksa: `loadProducts` mengambil data dari endpoint `/api/products`; `renderProducts` memasang handler pada tombol `.add-button`; `calculateTotal` menjumlahkan harga setiap produk dikalikan jumlahnya.

## C. Kualitas kode
- Temuan sebelum perbaikan: endpoint daftar produk tidak cocok dengan server, selector event tombol tidak cocok dengan kelas tombol, dan perhitungan total mengabaikan jumlah barang.
- Perbaikan yang dilakukan: menyamakan endpoint dan selector dengan implementasi server/antarmuka serta menghitung subtotal sebagai harga dikalikan jumlah.
- Hasil pemeriksaan ulang: `npm run lint` lulus untuk 2 file. `npm run format:check` belum lulus karena format `public/app.js` belum sesuai dengan formatter Biome; format file tidak diubah dalam pengerjaan ini.

## D. Git
- Branch (jika membuat): `main`.
- Ringkasan commit: commit terakhir `9ceaf88 init`. Perbaikan dan laporan saat ini belum dibuatkan commit baru.
- Hasil pemeriksaan `git status`: branch `main` sejajar dengan `origin/main`; `LAPORAN_UJIAN.md`, `public/app.js`, dan `src/cart.js` berstatus modified.

## E. Pemakaian kecerdasan buatan (jika digunakan)
- Nama alat: GitHub Copilot.
- Pertanyaan/instruksi yang diberikan: meminta bantuan memeriksa dan memperbaiki masalah daftar produk, tombol keranjang, dan total belanja, serta mencatat bukti perbaikannya.
- Bagian jawaban yang diterapkan: mengganti endpoint menjadi `/api/products`, memasang handler pada `.add-button`, dan menghitung total menggunakan harga dikalikan jumlah.
- Cara memeriksa apakah saran tersebut benar: membandingkan endpoint dengan server, menguji tombol melalui browser, menjalankan `node --test` (7 tes lulus), serta menjalankan pemeriksaan Biome.

## F. Refleksi singkat
- Satu pelajaran paling penting dari ujian ini: saya belajar memeriksa bukti sebelum mengubah kode dan menguji setiap perbaikan. Endpoint harus sesuai dengan server, selector event harus sesuai dengan elemen, dan total belanja harus memperhitungkan jumlah setiap barang.
