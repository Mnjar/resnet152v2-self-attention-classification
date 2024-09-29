# Proyek Klasifikasi Gambar

## Deskripsi Proyek
Proyek ini bertujuan untuk mengklasifikasikan gambar hewan ke dalam 10 kategori yang berbeda menggunakan model Convolutional Neural Network (CNN). Dataset yang digunakan terdiri dari 26.179 gambar dengan kategori seperti anjing, kucing, kuda, laba-laba, kupu-kupu, ayam, domba, sapi, tupai, dan gajah.

Model yang digunakan adalah **ResNet152V2** sebagai base model yang diikuti oleh beberapa layer tambahan, termasuk **SelfAttention** custom layer, untuk meningkatkan performa klasifikasi.

## Dataset
Dataset ini berisi sekitar 26.179 gambar hewan yang terbagi dalam 10 kategori:
- **dog**
- **cat**
- **horse**
- **spider**
- **butterfly**
- **chicken**
- **sheep**
- **cow**
- **squirrel**
- **elephant**

Dataset diambil dari [Kaggle - Animals10](https://www.kaggle.com/datasets/alessiocorrado99/animals10)

## Arsitektur Model
Model CNN yang dibangun memiliki arsitektur sebagai berikut:
- **Base Model**: ResNet152V2 (pre-trained, frozen)
- **Layer Tambahan**:
  - Conv2D (128 filters, kernel size 3x3, activation 'relu')
  - BatchNormalization
  - MaxPooling2D (pool size 2x2)
  - Dropout (rate 0.5)
  - SelfAttention (num_channels=128)
  - GlobalAveragePooling2D
  - Dense (256 units, activation 'relu')
  - Dropout (rate 0.5)
  - Dense (10 units, activation 'softmax')

Model dilatih dengan **Adam optimizer** dan **categorical_crossentropy** sebagai loss function.

## Proses Pelatihan
Model dilatih menggunakan dataset yang dibagi menjadi train set dan validation set dengan rasio 80:20. Berikut adalah callback yang digunakan selama pelatihan:
- **ReduceLROnPlateau**: Mengurangi learning rate jika val_loss tidak mengalami perbaikan.
- **EarlyStopping**: Menghentikan pelatihan jika val_loss tidak membaik selama 2 epoch.
- **ModelCheckpoint**: Menyimpan model terbaik berdasarkan val_accuracy.

### Format Model yang Disimpan
Model disimpan dalam tiga format berbeda:
- **SavedModel**: Format standar TensorFlow.
- **TF-Lite**: Dioptimalkan untuk perangkat mobile.
- **TFJS**: Untuk dijalankan di browser.