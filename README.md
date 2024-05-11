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

```python
fig, axs = plt.subplots(2, 2, figsize=(15, 5))
axs[0, 0].imshow(rgb)
axs[0, 1].hist(img.ravel(), 256, [0, 256])
axs[1, 0].imshow(citra_cerah)
axs[1, 1].hist(citra_cerah.ravel(), 256, [0, 256])
plt.show()
```

Menampilkan citra asli dan histogramnya, serta citra dengan peningkatan kecerahan dan histogramnya.

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
