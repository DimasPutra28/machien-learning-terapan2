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
### Solution
- menciptakan sistem rekomendasi makanan dengan memanfaatkan data dan atribut makanan yang tersedia dengan melakukan input makanan dari pengguna dan menghasilkan rekomendasi makanan lainnya yang serupa dari makanan yang diinputkan

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
Pada sistem rekomendasi makanan dengan pendekatan content-based filtering ini menggunakan metrik evaluasi Precision@k untuk metrik pembuktian rekomendasi top-N.
- Precision@5 untuk: Cashew Nut Cookies (Dessert)
- Precision@5: 1.00

Rekomendasi:
| Index | Name                         | C_Type  | Veg_Non |
|-------|------------------------------|---------|---------|
| 202   | banana and chia tea cake     | Dessert | veg     |
| 276   | microwave chocolate cake     | Dessert | veg     |
| 198   | lemon poppy seed cake        | Dessert | veg     |
| 256   | ragi oats ladoo (laddu)      | Dessert | veg     |
| 250   | lemon poppy seed cake        | Dessert | veg     |

- dari hasil evaluasi menggunakan precision@k pada hasil rekomendasi top_n sistem rekomendasi makanan dapat mengatasi kesulitan bagi pengguna dalam menemukan makanan, karena pengguna hanya masukkan makanan yang diinginkan dan menghasilkan rekomendasi makanan lainnya yang serupa. hasil dilihat dengan berdasarkan hasil evaluasi precision@k = 1.00
- dari hasil evaluasi rekomendasi makanan membuktikan rekomendasi makanan berdasarkan kemiripan dari informasi data tiap makanan
- dari solusi yang ada telah diciptakannya sistem rekomendasi makanan dengan memanfaatkan data informasi makanan untuk menghasilkan rekomendasi dan pengguna hanya menginputkan nama makanan yang diinginkan saja, dapat membantu keinginan pengguna.
