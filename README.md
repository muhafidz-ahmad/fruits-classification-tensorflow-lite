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

Model: "sequential_1"
_________________________________________________________________
 Layer (type)                Output Shape              Param #   
=================================================================
 conv2d_3 (Conv2D)           (None, 126, 126, 16)      448       
                                                                 
 max_pooling2d_3 (MaxPooling  (None, 42, 42, 16)       0         
 2D)                                                             
                                                                 
 conv2d_4 (Conv2D)           (None, 40, 40, 64)        9280      
                                                                 
 max_pooling2d_4 (MaxPooling  (None, 10, 10, 64)       0         
 2D)                                                             
                                                                 
 conv2d_5 (Conv2D)           (None, 8, 8, 128)         73856     
                                                                 
 max_pooling2d_5 (MaxPooling  (None, 2, 2, 128)        0         
 2D)                                                             
                                                                 
 flatten_1 (Flatten)         (None, 512)               0         
                                                                 
 dense_3 (Dense)             (None, 128)               65664     
                                                                 
 dense_4 (Dense)             (None, 32)                4128      
                                                                 
 dense_5 (Dense)             (None, 12)                396       
                                                                 
=================================================================
Total params: 153,772
Trainable params: 153,772
Non-trainable params: 0
_________________________________________________________________

Model akan dilatih dengan jumlah epochs sebanyak 45 dengan batch size 128. Optimizer yang digunakan adalah adam optimizer dengan nilai learning rate 0,0008.

Diperoleh akurasi pada data latih di epoch terakhir adalah 88,56%, dan akurasi pada data validasi di epoch terakhir adalah 89,87%. Ini artinya model sudah memiliki performa yang baik.

Karena performa model sudah baik dengan akurasi validasi di 89%, selanjutnya model akan disimpan dalam format TF-Lite untuk dilakukan deployment pada aplikasi android/ios.
