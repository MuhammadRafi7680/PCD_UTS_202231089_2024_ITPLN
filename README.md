# PCD_UTS_202231089_2024_ITPLN

```python
import cv2
import matplotlib.pyplot as plt 
import numpy as np
```

cv2: Library OpenCV untuk pengolahan citra.
matplotlib.pyplot: Library untuk membuat visualisasi seperti plot.
numpy: Library untuk operasi matematika dan array multidimensi.

```python
img = cv2.imread("AL.jpeg")
```

Membaca citra dengan nama "AL.jpeg" menggunakan OpenCV.

```python
rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

Mengonversi citra dari format BGR (default OpenCV) ke format RGB (digunakan oleh Matplotlib).

```python
beta = 30
citra_cerah = np.zeros((baris, kolom, 3))
for x in range(baris):
    for y in range(kolom):
        gyx = rgb[x, y] + beta
        citra_cerah[x, y] = gyx
citra_cerah = citra_cerah.astype(np.uint8)
```

Menambahkan nilai kecerahan ke seluruh piksel citra dengan nilai beta. Variabel citra_cerah menyimpan citra yang telah diterapkan peningkatan kecerahan.
beta = 30: Variabel beta ditetapkan dengan nilai 30, yang akan digunakan sebagai faktor peningkatan kecerahan.

citra_cerah = np.zeros((baris, kolom, 3)): Membuat matriks berukuran baris x kolom x 3 yang diisi dengan nol. Ini adalah matriks kosong yang akan menyimpan citra hasil peningkatan kecerahan.

for x in range(baris):: Looping melalui setiap baris dalam citra.

for y in range(kolom):: Di dalam loop x, looping melalui setiap kolom dalam citra.

gyx = rgb[x, y] + beta: Mengambil nilai piksel pada posisi (x, y) dari citra rgb (citra asli yang sudah dikonversi ke RGB). Nilai ini kemudian ditambah dengan beta untuk meningkatkan kecerahan.

citra_cerah[x, y] = gyx: Menetapkan nilai piksel yang sudah ditingkatkan kecerahannya ke posisi yang sesuai dalam matriks citra_cerah.

citra_cerah = citra_cerah.astype(np.uint8): Mengonversi tipe data matriks citra_cerah menjadi uint8. uint8 adalah tipe data yang digunakan untuk menyimpan nilai piksel dalam citra dengan rentang 0-255.

```python
fig, axs = plt.subplots(2, 2, figsize=(15, 5))
axs[0, 0].imshow(rgb)
axs[0, 1].hist(img.ravel(), 256, [0, 256])
axs[1, 0].imshow(citra_cerah)
axs[1, 1].hist(citra_cerah.ravel(), 256, [0, 256])
plt.show()
```

Menampilkan citra asli dan histogramnya, serta citra dengan peningkatan kecerahan dan histogramnya.

fig, axs = plt.subplots(2, 2, figsize=(15, 5)): Membuat subplot dengan ukuran 2x2 (total 4 subplot) dengan ukuran gambar 15x5 inci. fig adalah objek yang mewakili gambar utama dan axs adalah larik yang berisi sumbu-sumbu subplot.

axs[0, 0].imshow(rgb): Menampilkan citra rgb (citra asli yang sudah dikonversi ke RGB) pada subplot pertama (indeks baris 0, kolom 0).

axs[0, 1].hist(img.ravel(), 256, [0, 256]): Membuat histogram dari citra asli (img) dengan menggunakan hist() dari Matplotlib. img.ravel() digunakan untuk meratakan matriks citra menjadi larik satu dimensi. Parameter kedua, 256, adalah jumlah bin dalam histogram. Parameter ketiga, [0, 256], adalah rentang nilai untuk histogram (dari 0 hingga 255). Histogram akan ditampilkan di subplot kedua (indeks baris 0, kolom 1).

axs[1, 0].imshow(citra_cerah): Menampilkan citra citra_cerah (citra yang sudah ditingkatkan kecerahannya) pada subplot ketiga (indeks baris 1, kolom 0).

axs[1, 1].hist(citra_cerah.ravel(), 256, [0, 256]): Membuat histogram dari citra yang sudah ditingkatkan kecerahannya (citra_cerah) menggunakan hist(). Histogram ini akan ditampilkan di subplot keempat (indeks baris 1, kolom 1).

plt.show(): Menampilkan gambar beserta histogram yang telah ditambahkan ke subplot sebelumnya.

```python
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
```
Mengonversi citra asli ke citra grayscale.

```python
alpha = 1.5
beta = 30
adjusted = cv2.convertScaleAbs(img, alpha=alpha, beta=beta)
```
Menggunakan convertScaleAbs() untuk menyesuaikan kontras dan kecerahan citra.

alpha = 1.5: Variabel alpha ditetapkan dengan nilai 1.5. Nilai ini akan digunakan sebagai faktor peningkatan kontras.

beta = 30: Variabel beta ditetapkan dengan nilai 30. Nilai ini akan digunakan sebagai faktor peningkatan kecerahan.

adjusted = cv2.convertScaleAbs(img, alpha=alpha, beta=beta): Menggunakan fungsi convertScaleAbs() dari OpenCV untuk menyesuaikan kontras dan kecerahan citra. Fungsi ini mengalikan setiap piksel citra dengan alpha (kontras) dan kemudian menambahkan beta (kecerahan). Hasilnya disimpan dalam variabel adjusted.

```python
plt.figure(figsize=(10, 5))
plt.subplot(1, 2, 1)
plt.title('Original Image')
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.axis('off')

plt.subplot(1, 2, 2)
plt.title('Brightened Image')
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.axis('off')

plt.show()
```
Menampilkan citra asli dan hasil penyesuaian kontras dan kecerahan.

plt.figure(figsize=(10, 5)): Membuat gambar baru dengan ukuran 10x5 inci.

plt.subplot(1, 2, 1): Membagi gambar menjadi satu baris dan dua kolom, dan memilih subplot pertama. Subplot ini akan menampilkan citra asli.

plt.title('Original Image'): Memberikan judul "Original Image" pada subplot pertama.

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)): Menampilkan citra asli yang disimpan dalam variabel img. Karena OpenCV menggunakan urutan warna BGR (Blue-Green-Red), kita perlu mengonversinya ke urutan warna RGB (Red-Green-Blue) menggunakan cv2.cvtColor() untuk memastikan tampilan yang benar di Matplotlib.

plt.axis('off'): Menghilangkan sumbu x dan y pada subplot pertama.

plt.subplot(1, 2, 2): Memilih subplot kedua. Subplot ini akan menampilkan citra yang telah disesuaikan kecerahannya.

plt.title('Brightened Image'): Memberikan judul "Brightened Image" pada subplot kedua.

plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)): Menampilkan citra yang telah disesuaikan kecerahannya yang disimpan dalam variabel adjusted. Seperti sebelumnya, citra dikonversi dari format BGR ke RGB.

plt.axis('off'): Menghilangkan sumbu x dan y pada subplot kedua.

plt.show(): Menampilkan gambar beserta subplotnya. Dua citra akan ditampilkan berdampingan, dengan citra asli di sebelah kiri dan citra yang telah disesuaikan kecerahannya di sebelah kanan.

```python
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB))
plt.title('Original Image')

plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0], cmap="gray")
plt.title('Red')

plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,1], cmap="gray")
plt.title('Green')

plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,2], cmap="gray")
plt.title('Blue')

plt.show()
```
Menampilkan saluran warna (merah, hijau, biru) dari citra hasil penyesuaian.

penjelasan perbarisnya: 

plt.subplot(2, 2, 1): Memilih subplot pertama dalam grid 2x2.

plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)): Menampilkan citra yang disesuaikan kecerahannya dalam format RGB.

plt.title('Original Image'): Memberikan judul "Original Image" pada subplot pertama.

plt.subplot(2, 2, 2): Memilih subplot kedua dalam grid 2x2.

plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,0], cmap="gray"): Menampilkan saluran warna merah dari citra yang disesuaikan kecerahannya dalam skala abu-abu. [:,:,0] digunakan untuk memilih saluran warna merah dari citra RGB.

plt.title('Red'): Memberikan judul "Red" pada subplot kedua.

plt.subplot(2, 2, 3): Memilih subplot ketiga dalam grid 2x2.

plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,1], cmap="gray"): Menampilkan saluran warna hijau dari citra yang disesuaikan kecerahannya dalam skala abu-abu. [:,:,1] digunakan untuk memilih saluran warna hijau dari citra RGB.

plt.title('Green'): Memberikan judul "Green" pada subplot ketiga.

plt.subplot(2, 2, 4): Memilih subplot keempat dalam grid 2x2.

plt.imshow(cv2.cvtColor(adjusted, cv2.COLOR_BGR2RGB)[:,:,2], cmap="gray"): Menampilkan saluran warna biru dari citra yang disesuaikan kecerahannya dalam skala abu-abu. [:,:,2] digunakan untuk memilih saluran warna biru dari citra RGB.

plt.title('Blue'): Memberikan judul "Blue" pada subplot keempat.

plt.show(): Menampilkan semua subplot secara bersamaan. Subplot pertama menampilkan citra asli, sementara subplot yang lain menampilkan saluran warna (merah, hijau, biru) dari citra tersebut dalam skala abu-abu.


```python
merah = citra_cerah[:,:,0]
hijau = citra_cerah[:,:,1]
biru = citra_cerah[:,:,2]
```
Mendapatkan saluran warna merah, hijau, dan biru dari citra yang telah disesuaikan. Lalu, menghitung histogram untuk masing-masing saluran warna dan menampilkannya.

```python
# Ambang batas untuk mendapatkan citra biner (none)
(thresh, binary1) = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY)

# Membuat mask untuk warna biru
mask_blue = cv2.inRange(image_hsv, blue_lower, blue_upper)

# Ambang batas untuk mendapatkan citra biner (red-blue) dan (red-green-blue)
(thresh, binary3) = cv2.threshold(gray, 42, 255, cv2.THRESH_BINARY)
(thresh, binary4) = cv2.threshold(gray, 80, 255, cv2.THRESH_BINARY)
```
Melakukan segmentasi citra dengan menggunakan ambang batas pada citra grayscale dan citra dalam format HSV. Menampilkan hasil segmentasi citra dengan menggunakan metode ambang batas.

(thresh, binary1) = cv2.threshold(gray, 0, 255, cv2.THRESH_BINARY): Pada baris ini, ambang batas diatur pada nilai 0 untuk menghasilkan citra biner menggunakan fungsi threshold() dari OpenCV. Citra yang dihasilkan akan memiliki nilai 255 di mana piksel aslinya memiliki nilai lebih besar dari 0 di citra grayscale gray, dan 0 di tempat lain. Hasilnya disimpan dalam variabel binary1.

mask_blue = cv2.inRange(image_hsv, blue_lower, blue_upper): Fungsi inRange() digunakan untuk membuat masker yang mengandung warna biru dalam citra HSV (image_hsv) dengan rentang warna yang telah ditentukan oleh blue_lower dan blue_upper. Hasilnya disimpan dalam variabel mask_blue.

(thresh, binary3) = cv2.threshold(gray, 42, 255, cv2.THRESH_BINARY): Di sini, ambang batas ditetapkan pada nilai 42 untuk menghasilkan citra biner menggunakan fungsi threshold(). Ini berarti bahwa semua piksel dalam citra grayscale gray yang memiliki nilai lebih besar dari 42 akan menjadi 255, dan sisanya akan menjadi 0. Hasilnya disimpan dalam variabel binary3.

(thresh, binary4) = cv2.threshold(gray, 80, 255, cv2.THRESH_BINARY): Pada baris ini, ambang batas ditetapkan pada nilai 80 untuk menghasilkan citra biner menggunakan fungsi threshold(). Sama seperti sebelumnya, piksel dalam citra grayscale gray yang memiliki nilai lebih besar dari 80 akan menjadi 255, dan sisanya akan menjadi 0. Hasilnya disimpan dalam variabel binary4.
