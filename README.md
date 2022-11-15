# Ecommerce-Customer-Churn-Prediction

Project ini merupakan syarat penyelesaian tugas Capstone Project Modul 3 dari Program Job Connector Video Learning Data Science di Purwadhika.

**Bussiness Context**

E-commerce merupakan sebuah perkembangan teknologi di bidang bisnis yang melibatkan promosi, pembelian dan pemasaran produk melalui media elektronik atau internet. E-commerce merupakan penerapan dari bisnis elektronik yang cukup efisien dengan persaingan yang ketat untuk menawarkan produk yang menarik kepada pelanggan mereka. Bahkan, sering terjadi akuisisi pelanggan antar perusahaan. Pelanggan yang berhenti menggunakan platform e-commerce perusahaan dan beralih ke platform elektronik lainnya dikenal sebagai churn. Pelanggan merupakan aset terpenting bagi perusahaan sebagai sumber keuntungan dari perusahaan. Maka dari itu, perusahaan memerlukan strategi bisnis yang baik untuk mencegah churn.

**Problem Statement**

Proses treatment pelanggan yang akan churn bisa memakan waktu dan sumber daya jika perusahaan menargetkan semua pelanggan tanpa melakukan penyaringan terlebih dahulu. Perusahaan ingin meningkatkan efisiensi promosi dengan mengetahui pelanggan mana yang akan churn sehingga memfokuskan promosi ke mereka. Jika promosi diberikan kepada semua pelanggan, maka biaya promosi tersebut akan menjadi sia-sia jika pelanggan tersebut memang tidak berniat untuk churn.

**Goals**

Maka berdasarkan permasalahan tersebut, perusahaan ingin memiliki kemampuan untuk memprediksi kemungkinan seorang pelanggan untuk churn, sehingga dapat memfokuskan promosi pada pelanggan yang ingin churn saja. Dan juga, perusahaan ingin mengetahui apa/faktor/variabel apa yang membuat seorang pelanggan ingin churn, sehingga mereka dapat membuat strategi bisnis yang lebih baik dalam treatment pelanggan.

**Analytic Approach**

Jadi yang akan kita lakukan adalah menganalisis data untuk menemukan pola yang membedakan pelanggan yang akan churn dan yang tidak akan churn. Kemudian kita akan membangun model klasifikasi yang akan membantu perusahaan untuk dapat memprediksi probabilitas seorang pelanggan akan churn atau tidak.

**Evaluation Metrics**

- *Type I error (False Positive)* mengacu pada pelanggan yang tidak akan churn tetapi diprediksi akan churn. konsekuensinya adalah promosi yang sia-sia.
- *Type II error (False Negative)* mengacu pada pelanggan yang akan churn tetapi diprediksi tidak akan churn. Konsekuensinya adalah kehilangan pelanggan.
- *Akurasi* adalah persentase prediksi yang benar. Rumus akurasi adalah: Accuracy = (TP + TN) / (TP + TN + FP + FN)
- *Recall* adalah seberapa besar persentase kejadian pada kelas positif yang berhasil dideteksi. Rumus recall adalah: Recall = TP / (TP + FN)
- *Presisi* merupakan metrics yang digunakan untuk mengukur ada berapa banyak hasil prediksi suatu kelas yang memang sesuai dengan kenyataan. Rumus presisi adalah: Precision = TP / (TP + FP)
-  F1 score adalah rataan harmonik dari presisi dan recall. Rumus F1 score adalah: F1 Score = 2 x (Precision x Recall) / (Precision + Recall)

## Attibute Information

| Attribute | Data Type, Length | Description |
| --- | --- | --- |
| Tenure | Float | Tenure of customer in ecommerce company |
| WarehouseToHome | Float | Distance in between warehouse to home of customer |
| NumberOfDeviceRegistered | Integer | Total number of devices is registered on particular customer |
| PreferedOrderCat | Text | Preferred order category of customer in last month |
| SatisfactionScore | Integer | Satisfactory score of customer on service |
| MaritalStatus | Text | Marital status of customer |
| NumberOfAddress | Integer | Total number of added added on particular customer |
| Complain | Integer | Any complaint has been raised in last month |
| DaySinceLastOrder | Float | Day Since last order by customer |
| CashbackAmount | Float | Average cashback in last month |
| Churn | Integer | 0 - Not Churn, 1 - Churn|

Dataset memilki 11 kolom dan 5624 baris. Dengan komposisi sebagai berikut:
- 2 data bertipe object
- 4 data bertipe integer
- 4 data bertipe float, dan
- 1 data bertipe boolean. (Churn)

Terdapat beberapa variabel yang memiliki missing value, yaitu:
- Tenure (4.92 %)
- WarehouseToHome (4.29 %)
- DaySinceLastOrder (5.4 %)

## Data Preparation

**Data Duplikat**

![1](https://github.com/BalyaElfata/Ecommerce-Customer-Churn/blob/main/Gambar/Duplicated.png)

Tanpa adanya id transaksi ataupun id pelanggan, kita tidak bisa memastikan data duplikat di atas merupakan data duplikat asli atau hanya transaksi yang diulang pelanggan. Maka dari itu, tidak diperlukan perlakuan khusus terhadap data duplikat.

**Data Kosong**

![2](https://github.com/BalyaElfata/Ecommerce-Customer-Churn/blob/main/Gambar/missing_value.png)

Data kosong diisi dengan median dari statistik fitur lainnya dari data kosong masing-masing fitur.

**Outliers**

![3](https://github.com/BalyaElfata/Ecommerce-Customer-Churn/blob/main/Gambar/Outliers.png)

Dengan melihat grafik box plot, terlihat bahwa fitur WarehouseToHome, DaySinceLastOrder, NumberOfAddress, dan Tenure memiliki outliers yg cukup ekstrem nilainya dibanding data yang lain. Maka hanya data tersebut yang akan kita hilangkan, sedangkan untuk outliers lainnya kita biarkan.

![4](https://github.com/BalyaElfata/Ecommerce-Customer-Churn/blob/main/Gambar/splitting_and_encoder.png)

Fitur yang merupakan fitur kategorikal diubah menggunakan one hot encoder dengan argument drop=First.

## Modelling and Evaluation

**Modelling**

![5](https://github.com/BalyaElfata/Ecommerce-Customer-Churn/blob/main/Gambar/model.png)

6 Model yang dipilih akan dibandingkan nilai F1 Scorenya lalu diambil model dengan performa terbaik.

![6](https://github.com/BalyaElfata/Ecommerce-Customer-Churn/blob/main/Gambar/models_performance.png)

Menggunakan K Fold, LightGBM dipilih sebagai model untuk dataset ini karena memiliki performa terbaik di antara model lainnya.

**Oversampling**

Oversampling dilakukan menggunakan RandomOversampler(). Akan tetapi, dipilih model tanpa oversampling untuk mempertahankan nilai presisi yang tinggi karena resiko False Positive lebih besar daripada False Negative.

**Hyperparameter Tuning**

![7](https://github.com/BalyaElfata/Ecommerce-Customer-Churn/blob/main/Gambar/hyperparameter.png)

Hyperparameter space dari LightGBM yang divariasikan adalah max_bin, num_leaves, min_data_in_leaf, num_iterations, learning_rate, dan random_state.

![8](https://github.com/BalyaElfata/Ecommerce-Customer-Churn/blob/main/Gambar/hyperparameter_tuning_score.png)

Setelah dilakukan hyperparameter tuning, didapatkan nilai F1 Score yang lebih tinggi yaitu 0.82. Model inilah yang disimpan sebagai model terbaik untuk prediksi kasus E-Commerce Customer Churn.

## Conclusion and Recommendation

**Conclusion**

Berdasarkan hasil classification report dari model, dapat disimpulkan bahwa; bila seandainya nanti digunakan model ini untuk memfilter list pelanggan yang akan coba ditawarkan promosi, maka model ini dapat mengurangi 97% kandidat yang tidak churn untuk tidak di-approach, dan model ini dapat menangkap 79% pelanggan yang churn dari seluruh kandidat yang tertarik.

Model ini memiliki ketepatan prediksi pelanggan yang churn sebesar 84%. Artinya, setiap model ini memprediksi bahwa seorang pelanggan akan churn, maka kemungkinan tebakannya benar itu sebesar 84% kurang lebih. Masih akan ada pelanggan yang tidak akan churn tetapi diprediksi sebagai pelanggan yang akan churn sekitar 3% dari keseluruhan pelanggan yang tidak churn.

**Recommendation**

Hal-hal yang bisa dilakukan untuk mengurangi masalah customer churn antara lain:
- Memberikan promo khusus kepada pelanggan yang memiliki masa tenure rendah untuk mencegah potensi churn terhadap pelanggan baru.
- Membuka cabang warehouse lebih banyak sehingga lebih dekat ke pemukiman rumah-rumah pelanggan.
- Mengoptimalkan harga cashback untuk meningkatkan customer retention tanpa resiko kerugian yang besar.
- Mengoptimalkan user experience dan customer service dari aplikasi atau website e-commerce untuk dapat melayani complain pelanggan dengan baik.
- Memberikan promo khusus kepada pelanggan yang sudah lama tidak bertransaksi.

Hal-hal yang dapat dilakukan untuk mengembangkan model agar lebih baik lagi, seperti:
- Penghapusan fitur kategorikal untuk pemodelan ulang tanpa fitur yang tidak terlalu berpengaruh ke model.
- Penggunaan grid search karena grid search menjamin hasil yang terbaik saat melakukan hyperparameter tuning dengan hyperparameter yang lebih banyak.
- Menambahkan fitur-fitur baru yang dapat berguna untuk analisis dan pemodelan seperti lama penggunaan aplikasi atau website, jumlah produk yang berada dalam keranjang pelanggan, dan sebagainya.
