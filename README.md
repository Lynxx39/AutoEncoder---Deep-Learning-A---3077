# AutoEncoder---Deep-Learning-A---3077

📁 Dataset
Dataset yang digunakan berupa kumpulan citra lanskap berwarna (RGB). Citra-citra ini kemudian diubah ke format LAB (Lightness, a, b) untuk memisahkan komponen pencahayaan (L) dari informasi warna (a dan b).

Ukuran gambar: 256 × 256 piksel
Jumlah data: 50 gambar
Format gambar: .jpg

🧠 Arsitektur Model Autoencoder
Model terdiri dari dua bagian utama:

🔻 Encoder
Encoder bertugas mengekstraksi fitur dari citra grayscale dan melakukan kompresi spasial:
Conv2D(64)  → MaxPooling2D
Conv2D(128) → MaxPooling2D
Conv2D(256) → MaxPooling2D

🔺 Decoder
Decoder berfungsi merekonstruksi informasi warna dari fitur hasil encoding:
Conv2D(256) → UpSampling2D
Conv2D(128) → UpSampling2D
Conv2D(64)  → UpSampling2D
Conv2D(2, activation='sigmoid')  # Output: 2 channel (a dan b)

⚙️ Training
Model dilatih menggunakan Mean Squared Error (MSE) sebagai fungsi loss dengan optimisasi Adam. Input berupa channel L (grayscale), dan target berupa channel a & b (komponen warna).

model.compile(optimizer=Adam(1e-4), loss='mse')
model.fit(
    x_tr, y_tr,
    validation_data=(x_val, y_val),
    epochs=30,
    batch_size=8,
    shuffle=True
)

