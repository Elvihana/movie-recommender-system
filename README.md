# Movie Recommender System Project

Proyek ini berfokus pada pembuatan **Sistem Rekomendasi Film** sederhana menggunakan Python dan library Pandas serta NumPy. Proyek ini mendemonstrasikan bagaimana data performa film dan peringkat dari pengguna dapat diproses untuk menghasilkan rekomendasi tayangan yang relevan.

## Latar Belakang
Di era digital, jumlah konten film dan hiburan berkembang sangat pesat, sehingga pengguna sering kali mengalami kesulitan (*information overload*) dalam memilih tayangan yang sesuai dengan preferensi mereka. Melalui rekayasa data dan pemanfaatan metrik penilaian konten, sebuah sistem rekomendasi dapat dibangun untuk menyaring katalog film yang luas dan memberikan saran film terbaik secara otomatis kepada pengguna.

## Tujuan Proyek
1. Melakukan memuat data (*data unloading*) dari dataset ulasan film berbasis web.
2. Membersihkan data mentah dari nilai `NULL` dan memformat ulang penulisan data kosong `\N` agar menjadi objek penanda yang valid (`np.nan`).
3. Mentransformasi kolom kategori seperti genre yang awalnya berbentuk teks string biasa menjadi format objek data bertipe daftar (*list*) untuk kemudahan analisis.
4. Mengimplementasikan logika perhitungan skor rekomendasi film untuk menyajikan daftar film terbaik yang terkurasi bagi audiens.

## Dataset
Proyek ini menggunakan dua dataset utama yang diakses langsung via URL:
1. **`title.basics.tsv`**: Berisi informasi mendasar mengenai metadata film. Kolomnya meliputi:
   * `tconst`: ID unik untuk setiap judul film.
   * `titleType`: Jenis format tayangan (misal: *short*, *movie*, *tvEpisode*).
   * `primaryTitle` & `originalTitle`: Judul utama dan judul asli film.
   * `isAdult`: Penanda konten dewasa.
   * `startYear` & `endYear`: Tahun rilis awal dan tahun berakhirnya tayangan.
   * `runtimeMinutes`: Durasi waktu tayang film dalam menit.
   * `genres`: Genre yang melekat pada film tersebut.
2. **`title.ratings.tsv`**: Berisi informasi metrik performa penilaian dan jumlah voting dari penonton untuk setiap film.

*Sumber Dataset*: 
* `https://dqlabcdn.xeratic.com/dqlab-dataset/title.basics.tsv`
* `https://dqlabcdn.xeratic.com/dqlab-dataset/title.ratings.tsv`

## Tahapan Analisis
Proses pengerjaan di dalam Jupyter Notebook dibagi menjadi beberapa langkah kunci:
1. **Import Library & Load Data**: Memasukkan pustaka `pandas` serta `numpy` serta membaca dataset bertipe `.tsv` menggunakan pemisah tab (`sep='\t'`).
2. **Data Exploration & Profiling**: Menampilkan sampel baris teratas, memeriksa tipe data kolom menggunakan `.info()`, serta melakukan agregasi jumlah nilai `NULL` pada tiap kolom data.
3. **Data Cleaning**: 
   * Membuang baris yang tidak memiliki judul (`primaryTitle` atau `originalTitle`) dan yang tidak memiliki informasi genre.
   * Mengganti teks string bawaan berupa `\N` yang bermakna kosong pada kolom tahun dan durasi menjadi format `np.nan`.
   * Mengubah tipe data (*casting*) kolom numerik tersebut menjadi `float64`.
4. **Data Transformation**: Membuat fungsi kustom bernama `transform_to_list` untuk memecah string genre yang dipisahkan oleh tanda koma menjadi elemen daftar (*list*) terpisah.
5. **Recommender System Modeling**: Menggabungkan data rating penonton dengan katalog informasi film untuk dihitung nilai tertimbangnya sebagai basis penentuan rekomendasi.

## Model yang Digunakan
Sistem rekomendasi ini dibangun dengan pendekatan **Knowledge-Based Recommendation** dan manipulasi matriks data menggunakan library **Pandas**. Pendekatan ini mengandalkan pembersihan kualitas fitur data, penyaringan kondisi film yang valid, dan pengurutan nilai statistik skor popularitas serta rating rata-rata dari pengguna untuk merumuskan daftar rekomendasi.

## Hasil
* Kumpulan data mentah yang semula berjumlah 9.025 baris berhasil disaring dari baris korup/kosong sehingga menyisakan 9.000 data film bersih yang siap diolah.
* Nilai durasi, genre, dan tahun tayang berhasil dirapikan ke dalam tipe data pemrograman yang tepat.
* Algoritma berhasil menyusun urutan film-film teratas yang direkomendasikan berdasarkan kalkulasi bobot ulasan gabungan secara objektif.

## Kesimpulan
Sistem rekomendasi berbasis fungsionalitas dasar Pandas dan manipulasi string/matriks terbukti efisien untuk melakukan pra-pemrosesan data katalog film berskala menengah. Dengan data yang telah dibersihkan secara konsisten dari kontaminasi nilai kosong (`NULL`), sistem mampu menghasilkan keluaran rekomendasi film yang valid, membantu menghemat waktu pencarian pengguna, dan memberikan pengalaman navigasi konten yang lebih personal.
