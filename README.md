# PA-PC_202231074_DITO_IMANUEL_ARMINTO_A
# GEOMETRIX CITRA
---
## Dito Imanuel Arminto
## 20231074
## Pengolahan Citra Digital - A
---
# Pendahuluan
Dalam dunia digital, kita banyak dipertemukan dengan banyak gambar dengan beragam ukuran, intensitas, maupun keunikannya masing-masing ada yang jelas, ada yang buram, ada juga yang terpotong. Sebagian besar dari kita pasti sudah sering melihat gambar entah itu dari media sosial ataupun dari media lainnya. namun, sebagian besar dari orang yang melihat gambar-gambar tersebut belum tentu paham proses komputasi apa yang terjadi sehingga sebuah gambar dapat berukuran, berposisi terbalik, ataupun bercitra seperti berkaca. Pada kesempatan kali ini, pada bagian ini akan dijelaskan beberapa teknik **Geometrix Citra** yang menjadi dasar sebuah gambar dapat kita manipulasi secara fleksibel di berbagai platform pengeditan citra, berikut 5 teknik untuk merubah **Geometrix Citra** dari sebuah gambar:
1. Rotated
2. Rezised
3. Cropped
4. Flipped
5. Translated

Adapula beberapa tahapan dalam pengolahannya, adalah sebagai berikut:
1. Penentuan gambar (dalam kasus ini gambar diri sendiri)
2. Penentuan library
3. Penentuan alur dari program, berikut alur yang direncanakan:<br>

   a. Import library<br>
   b. Penambahan gambar ke variable<br>
   c. Penampilan gambar asli dengan pixelnya (sebagai patokan penentuan parameter)<br>
   d. Operasi Geometrix Citra<br>
   e. Tampilan perbandingan semua hasil operasi<br>
4. Implementasi

## Penjelasan Program
***Import Library***<br>
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
```
- **cv2**: Merupakan modul pada library OpenCV yang kurang lebih memiliki fungsi untuk memanipulasi gambar, deteksi objek, dan lainnya. Kali ini implementasinya untuk manipulasi Geometrix dari gambar.
- **numpy (np)**: NumPy adalah pustaka Python yang digunakan untuk komputasi numerik. Penggunaannya kali ini yakni untuk membuat larik NumPy.
- **matplotlib.pyplot as plt**: Matplotlib adalah pustaka untuk visualisasi data atau menampilkan gambar dalam bentuk plot.
  
***Membaca Citra & Konversi RGB ke GBR***<br>
```
original_image = cv2.imread("dito.jpg")
original_image_rgb = cv2.cvtColor(original_image, cv2.COLOR_BGR2RGB)
```
- Dengan perintah diatas kita dapat membaca sebuah citra lalu menampungnya dalam sebuah variable, dalam konteks program diatas citranya **dito.jpg** dan variabelnya **original_image**.
- Ada juga proses konversi RGB ke BGR yang ditampung dalam variabel **original_image_rgb**.

***Menampilkan Gambar Asli dengan Parameter Dalam Satuan Pixel***<br>
```
plt.figure(figsize=(8, 6))
plt.imshow(image_rgb)
plt.title("Gambar Asli")
plt.axis('on')  # Tampilkan axis untuk menunjukkan koordinat pixel
plt.show()
```
- **plt.figure()**: Mengatur ukuran figur yang akan digunakan untuk menampilkan gambar.
- **plt.imshow()**: Mengambil gambar (image_rgb) dan menampilkannya dalam figur menggunakan Matplotlib.
- **plt.title()**: Mengatur judul plot
- **plt.axis('on')**: Argumen 'on' di sini digunakan untuk mengaktifkan tampilan sumbu. Sumbu akan menunjukkan koordinat piksel di sekitar gambar.
- **plt.show()**: Menampilkan figur lengkap dengan gambar, judul, dan sumbu yang sudah dikonfigurasi sebelumnya.
***Rotasi Gambar Sebesar 45 Derajat***
```
(h, w) = original_image.shape[:2]
center = (w // 2, h // 2)
M = cv2.getRotationMatrix2D(center, 45, 1.0)
rotated_image = cv2.warpAffine(original_image_rgb, M, (w, h))
```
- **(h, w) = original_image.shape[:2]**: Mendapatkan tinggi (h) dan lebar (w) dari gambar asli (original_image). Dengan memanfaatkan atribut .shape untuk mendapatkan dimensi gambar lalu mengambil dua nilai pertama dari atribut shape itu yakni tinggi dan lebar gambar.
- **center = (w // 2, h // 2)**:Menentukan titik pusat rotasi dengan memanfaatkan setengah dari lebar dan tinggi gambar yang mana jadi pusat rotasi.
- **M = cv2.getRotationMatrix2D(center, 45, 1.0)**: Menggunakan cv2.getRotationMatrix2D() untuk menghasilkan matriks transformasi dengan parameter seperti titik pusat rotasi, sudut rotasi, dan skala ukuran gambar setelah rotasi.
- **rotated_image = cv2.warpAffine(original_image_rgb, M, (w, h))**: Menggunakan cv2.warpAffine() untuk menerapkan transformasi ke gambar.

***Mengubah ukuran gambar dengan cv2***
```
resized_image = cv2.resize(original_image_rgb, (95, 127))
```
- Mengubah ukuran gambar menjadi ukuran yang lebih kecil atau lebih besar dengan memanfaatkan fungsi bawahan dari opencv yakni **cv2.resize()**, gambar akan diubah berdasarkan parameter yakni 95 x 237 yang mana merupakan resolusi dari gambarnya.


***Crop Gambar***
```
cropped_image = original_image_rgb[1500:4000, 1000:2000]
```
- Operasi crop pada gambar menggunakan NumPy adalah dengan menggunakan slicing pada larik pixel gambar untuk memilih area tertentu dan menyimpannya ke dalam variabel baru. Simpelnya dengan mengambil bagian tertentu dari larik pixel, lalu ditampung ke variabel gambar dapat terpotong pada bagian yang diambil saja.

***Flip Gambar***
```
flipped_image = cv2.flip(original_image_rgb, 1)
```
- **cv2.flip(original_image_rgb, 1)** digunakan untuk membalik (flip) gambar secara horizontal menggunakan library opencv-python (cv2). Argumen yang mengatur apakah flip akan dilakukan secara horizontal atau flip vertikal adalah angkanya (1 untuk flip horizontal, 0 untuk flip vertikal, dan -1 untuk flip horizontal dan vertikal).

***Menampilkan hasil perubahan gambar***
1. **fig, axes = plt.subplots(2, 3, figsize=(15, 10))**:

  - Tujuan: Membuat sebuah figur (figure) dengan subplot (multiplot) berukuran 2 baris dan 3 kolom.
  - Fungsi: **plt.subplots()** digunakan untuk membuat subplot, di mana 2, 3 menunjukkan ukuran grid (2 baris, 3 kolom).
  - Parameter: **figsize=(15, 10)** menentukan ukuran figur dalam satuan inci (lebar 15 inci, tinggi 10 inci).

2. List gambar dan titlenya:

  - **images = [original_image_rgb, rotated_image, resized_image, cropped_image, flipped_image, translated_image]**: List ini berisi gambar-gambar yang akan ditampilkan dalam subplot.
  - **titles = ["Citra Asli", "Citra Rotasi", "Citra Rezise", "Citra Crop", "Citra Flip", "Citra Translate"]**:List ini berisi judul-judul untuk setiap gambar yang akan ditampilkan.

3. Plot gambarnya:

  - **for ax, img, title in zip(axes.flatten(), images, titles)**: Melalui loop ini, setiap gambar dan judulnya dipasangkan dengan subplot yang sesuai.
  - **axes.flatten()** digunakan untuk meratakan array dari subplot menjadi satu dimensi, mempermudah iterasi.
  - **ax.imshow(img)** digunakan untuk menampilkan gambar img di subplot ax.
  - **ax.set_title(title)** digunakan untuk menambahkan judul title pada subplot ax.
  - **ax.axis('off')** menghilangkan sumbu pada subplot, sehingga hanya gambar yang ditampilkan tanpa sumbu.

4. **plt.tight_layout()**:Fungsi ini digunakan untuk menyesuaikan layout subplot secara otomatis agar sesuai dengan ukuran dan konten yang ditampilkan.
   
5. **plt.show()**: Menampilkan figur lengkap yang sudah disiapkan dengan semua subplot, gambar, dan judulnya.



# Referensi
Devi, Assistant Professor, Department of Electronic and Communication Engineering, Saranathan College of Engineering, Trichy, India. "Geometric Transformations and Thresholding of Images using Opencv-Python." GRD Journal for Engineering, Volume 2, Issue 11, October 2017, ISSN: 2455-5703. Available at: www.grdjournals.com
