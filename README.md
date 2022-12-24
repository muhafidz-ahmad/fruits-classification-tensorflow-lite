# Klasifikasi Buah Segar dan Busuk Menggunakan Tensorflow

## Rumusan Masalah
* Banyaknya buah-buahan yang masuk ke toko menjadikan pekerja harus lebih bekerja keras untuk memisahkan tiap buahnya serta memisahkan antara buah yang masih segar dan buah yang telah busuk. 

* Machine learning diharapkan dapat membantu untuk memisahkan buah-buahan tersebut sehingga dapat disimpan pada tempatnya.

<p align="center">
  <img src="https://www.eitfood.eu/files/_1200x590_crop_center-center_none/fruits.jpg" alt="Buah-buahan" width="500">
</p>

Data akan diambil dari [kaggle](https://www.kaggle.com/datasets/raghavrpotdar/fresh-and-stale-images-of-fruits-and-vegetables?select=ImageLabels.txt).

Data terdiri dari beberapa jenis gambar buah-buahan yang segar dan juga yang busuk. Tiap gambar telah dipisahkan dalam foldernya masing-masing sesuai dengan jenis buah dan kesegarannya.

## Augmentasi Gambar
Dilakukan augmentasi gambar untuk melakukan transformasi pada gambar data latih sehingga akan membuat variasi yang lebih banyak pada data latih. Hal ini dilakukan untuk mengurangi overfitting ketika proses pelatihan.

Augmentasi yang dilakukan adalah:
1. Rescale nilai vektor gambar menjadi antara 0 hingga 1.
2. Memutar atau merotasi gambar hingga 20 derajat.
3. Membalikkan gambar secara horizontal maupun vertikal.
4. Mengisi bagian gambar yang kosong dengan warna yang ada didekatnya.

## Model Machine Learning
Model machine learning akan dibuat menggunakan Convolutional Neural Networks dengan lapisan sebagai berikut.

![image](https://user-images.githubusercontent.com/115754250/209429812-dc3a7bdf-8842-4515-9d93-8f1725ce055f.png)

Model dilatih dengan hyperparameter sebagai berikut:
* Epochs: 45
* Batch size: 128
* Optimizer: Adam
* Learning rate: 0,0008

Diperoleh akurasi ketika pelatihan (training) pada data latih di epoch terakhir adalah **88,56%**, dan akurasi pada data validasi di epoch terakhir adalah **89,87%. Ini artinya model sudah memiliki performa yang baik.

Karena performa model sudah baik dengan akurasi validasi di 89%, selanjutnya model akan disimpan dalam format TF-Lite untuk dilakukan deployment pada aplikasi android/ios.
