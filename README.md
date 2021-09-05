# DQLab: Kelas Penerapan di Industri
## Data Science in Finance: Credit Risk Analysis 
Credit risk analysis merupakan proses penilaian resiko yang dilakukan oleh lembaga peminjam sebelum memberikan pinjaman yang berfungsi untuk memperkecil resiko kredit yang disebut dengan credit scoring dan credit rating terhadap pihak peminjam

# Tahapan Credit Risk Analysis
1. Data preparation
2. Mempersiapkan training set dan testing set
3. Membuat model menggunakan fungsi C5.0
4. Membuat diagram desicion tree
5. Menggunakan model untuk prediksi testing set
6. Evaluasi model 
7. Melakukan prediksi dari data pengajuan pinjaman baru

# Hasil Analisis
## 1. Summary Model
      Class specified by attribute `outcome'

      Read 800 cases (3 attributes) from undefined.data

      Decision tree:

      jumlah_tanggungan > 4:
      :...durasi_pinjaman_bulan <= 24: 4 (98/25)
      :   durasi_pinjaman_bulan > 24: 5 (129/49)
      jumlah_tanggungan <= 4:
      :...jumlah_tanggungan > 2: 3 (219/17)
          jumlah_tanggungan <= 2:
          :...durasi_pinjaman_bulan <= 36: 1 (259/80)
              durasi_pinjaman_bulan > 36:
              :...jumlah_tanggungan <= 0: 2 (37/7)
                  jumlah_tanggungan > 0: 3 (58/2)


      Evaluation on training data (800 cases):

            Decision Tree   
          ----------------  
          Size      Errors  

             6  180(22.5%)   <<


           (a)   (b)   (c)   (d)   (e)    <-classified as
          ----  ----  ----  ----  ----
           179     1     5     5     6    (a): class 1
            80    30    14     3    12    (b): class 2
                   4   258                (c): class 3
                   2          73    31    (d): class 4
                              17    80    (e): class 5


        Attribute usage:

        100.00%	jumlah_tanggungan
         72.62%	durasi_pinjaman_bulan

Berdasarkan output diatas, diperoleh dari 800 cases terdapat 180 jumlah record yang salah klasifikasi dan 620 jumlah record yang diprediksi dengan benar

## 2. Diagram Desicion Tree
![image](https://user-images.githubusercontent.com/86001320/132093498-509632f9-35a6-4681-88db-ad17731b0209.png)
Penjelasan:
* Warna merah menunjukkan node dan penomoran nodenya
* Warna biru menunjukkan kondisi split ke node-node berikutnya
* Warna hijau menunjukkan jumlah data yang telah diklasifikasi
* Warna ungu menunjukkan hasil klasifikasi dan distribusinya (rentang rasio antara 0 dan 1)

## 3. Evaluasi Model: Mengevaluasi kelayakan model
![image](https://user-images.githubusercontent.com/86001320/132116757-6521a4b7-7e73-44ad-a3f3-cdf6d722da99.png)

Berdasarkan gambar diatas, maka dapat disimpulkan persentase prediksi yang benar dengan menjumlahkan posisi diagonal pada confusion matrix. Sehingga diperoleh persentase prediksi yang benar adalah 75% dan persentase yang salah adalah 25%

## 4. Menggunakan Model untuk Prediksi: Melakukan prediksi risk rating dari data pengajuan pinjaman baru
      aplikasi_baru <- data.frame(jumlah_tanggungan = 6, durasi_pinjaman_bulan = 12)
        jumlah_tanggungan durasi_pinjaman_bulan
      1                 6                    12
      predict(risk_rating_model, aplikasi_baru)
      [1] 4
      Levels: 1 2 3 4 5
Berdasarkan output diatas, maka hasil prediksi risk rating untuk untuk data pengajuan baru adalah 4, dari kemungkinan 1,2,3,4, dan 5. 
