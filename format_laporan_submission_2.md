# Laporan Proyek Machine Learning - Sistem Rekomendasi Makanan pendekatan Content-Based Filtering - Dimas Meidiansyah Putra

## Project Overview
    Pemilihan makanan menjadi aspek penting dalam kebutuhan makanan maupun bidang industri kuliner. Pengguna sering kali kesulitan menemukan makanan yang sesuai preferensi, baik dari sisi tipe makanan, kandungan vegan/non-vegan, maupun deskripsi hidangan. oleh karena itu, diadakannya sistem rekomendasi membantu pengguna mendapatkan saran makanan berdasarkan preferensi yang diinginkan atau variasi makanan lainnya yang sejenis dengan makanan yang diinginkan. 
    Dengan demikian, dikembangkan proyek sistem rekomendasi makanan berbasis pendekatan content-based filtering ini penting untuk diselesaikan dalam menghasilkan atau merekomendasikan makanan yang mirip berdasarkan jenis, preferensi vegan/non-vegan, dan deskripsi makanan. Dataset yang digunakan berisi informasi mengenai berbagai makanan, termasuk nama, tipe, deskripsi, dan label vegan/non-vegan.
    
sumber referensi: [Sistem Rekomendasi Wisata Kuliner Madura Menggunakan Content Based Filtering](https://jurnal.yudharta.ac.id/v2/index.php/EXPLORE-IT/article/view/5366)

## Business Understanding    
### Problem Statements
- Pengguna sering kesulitan menemukan makanan yang sesuai dengan preferensi mereka karena banyaknya pilihan makanan yang tersedia tanpa sistem penyaringan yang efektif.
- Tidak adanya sistem rekomendasi yang memanfaatkan informasi konten makanan (seperti jenis makanan, status vegan/non-vegan, dan deskripsi) untuk memberikan saran makanan yang relevan.
### Goals
- Membangun sistem rekomendasi makanan berbasis content-based filtering yang mampu menyarankan makanan serupa dari inputan makanan dari pengguna yang dicocokkan berdasarkan deskripsi dan atribut makanan.
- Meningkatkan pengalaman pengguna dalam menjelajahi makanan dengan memberikan top-N rekomendasi yang relevan dan personal.

## Data Understanding
Dataset yang dipilih adalah dataset sistem rekomendasi makanan yang dalam dataset menampilkan nama makanan dan detail dari makanan tersebut:
Sumber dataset: [Food Recommendation System](https://www.kaggle.com/datasets/schemersays/food-recommendation-system)
Jumlah Baris Data: 400 baris data
Jumlah Kolom Data: 5 kolom Data
Kondisi Data:
- Missing Value: Tidak ditemukan nilai kosong pada dataset (hasil dari kode `data.isnull().sum()` manghasilkan nol untuk semua fitur pada dataset).
- Data Duplikat: Tidak terdapat duplikat dalam dataset (hasil dari kode `data.duplicated().sum()` = 0).
  
Variabel-variabel pada Dataset sistem rekomendasi makanan adalah sebagai berikut:
- Food_ID: merukapan nomor Unique ID dari tiap makanan.
- Name: merupakan nama-nama makanan dari dataset tersebut.
- C_Type: merupakan kategori dari makanan tersebut.
- Veg_Non: merupakan tipe makanan tersebut antara tergolong vegetarian atau non vegetarian.
- Describe: merupakan bahan bahan-bahan atau isian dari makanan tersebut.

**teknik visualisasi data dalam menganalisis dataset**
- Identifikasi distribusi variabel kategori tipe makanan disajikan dalam bar plot
![distribusi tipe makanan)](https://github.com/user-attachments/assets/4fc70d03-7a09-440d-b4cf-a2d834840254)
- Identifikasi distribusi variabel tipe makanan vegan/non vegan disajikan dalam bar plot
![distribusi tipe makanan vegan/non egan](https://github.com/user-attachments/assets/866d36b2-eaab-4d08-bb31-d2cb025f4f35)

## Data Preparation
1. pemilihan variabel fitur yang akan digunakan sebagai pertimbangan hasil rekomendasi:
   - kolom variabel C_Type
   - kolom variabel Veg_Non
   - kolom variabel Describe
2. Penggabungan variabel fitur yang dipilih
   - penggabungan dilakukan agar mempermudah sebelum melakukan teknik vektorisasi TF-IDF vectorizer dan sebelum melakukan rekomendasi
3. Melakukan teknik vektorisasi menggunakan TF-IDF vectorizer:
   - tujuan melakukan teknik ini `TfidfVectorizer()` untuk mengubah penggabungan variabel tersebut dari kata menjadi bentuk vektor numerik
   - menggunakan stop_words='english' karenakan dataset menggunakan bahasa Inggris.


## Modeling
cara kerja sistem rekomendasi ini dengan menggunakan pendekatan content-based Filtering menghitung hasil kesamaan tiap makanan menggunakan teknik cosine similarity dari hasil penggabungan fitur yang di proses vektorisasi menggunakan TF-IDF. dan menghasilkan rekomendasi makanan teratas berdasarkan hasil kemiripan tertinggi
- kelebihan:
  - Hanya membutuhkan informasi dari makanan tersebut untuk menghasilkan rekomendasi makanan lainnya
  - dapat menghasilkan rekomendasi makanan lainnya dengan memasukkan nama makanan yang diinginkan
- kekurangan:
  - terbatas dengan data yang ada
  - tidak dapat mempertimbangkan rekomendasi makanan dari pengguna lainnya.

Berikut Top_n=5 sebagai output untuk sistem rekomendasi makanan
recommend_food("cashew nut cookies", top_n=5)
| Name	                                                   | C_Type                        | Veg_Non         |
| -------------------------------------------------------- | ----------------------------- | --------------- |
| banana and chia tea cake                                 | Dessert                       | veg             |
| microwave chocolate cake                                 | Dessert                       | veg             |
| lemon poppy seed cake                                    | Dessert                       | veg             |
| ragi oats ladoo (laddu)                                  | Dessert                       | veg             |
| lemon poppy seed cake                                    | Dessert                       | veg             |


## Evaluation
Pada bagian ini Anda perlu menyebutkan metrik evaluasi yang digunakan. Kemudian, jelaskan hasil proyek berdasarkan metrik evaluasi tersebut.

Ingatlah, metrik evaluasi yang digunakan harus sesuai dengan konteks data, problem statement, dan solusi yang diinginkan.

**Rubrik/Kriteria Tambahan (Opsional)**: 
- Menjelaskan formula metrik dan bagaimana metrik tersebut bekerja.

**---Ini adalah bagian akhir laporan---**

_Catatan:_
- _Anda dapat menambahkan gambar, kode, atau tabel ke dalam laporan jika diperlukan. Temukan caranya pada contoh dokumen markdown di situs editor [Dillinger](https://dillinger.io/), [Github Guides: Mastering markdown](https://guides.github.com/features/mastering-markdown/), atau sumber lain di internet. Semangat!_
- Jika terdapat penjelasan yang harus menyertakan code snippet, tuliskan dengan sewajarnya. Tidak perlu menuliskan keseluruhan kode project, cukup bagian yang ingin dijelaskan saja.
