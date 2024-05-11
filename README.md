# PCD_UTS_202231053_2024_ITPLN
# LAPORAN <br>
## SOAL NO.1
1.	Import Library<br>
Untuk melakukan deteksi warna citra disini saya mengimport library yang dibutuhkan menggunakan script berikut :
```python
import cv2 # untuk pengolahan citra atau video
import matplotlib.pyplot as plt # untuk memvisualisasi data
import numpy as np # untuk komputasi numerik
```
2.	Membaca Data Gambar/Citra<br>
Setelah mengimport library yang dibutuhkan maka langkah selanjutnya adalah membaca data gambar yang akan digunakan untuk deteksi citra menggunakan fungsi imread dari library openCV dengan gambar yang sudah diupload ke dalam satu folder yang sama dengan folder file .ipynb kemudian gambar disimpan dalam variabel img.
```python
img = cv2.imread("20240511_010046.jpg")
```
3.	Membuat Baris dan Kolom<br>
Langkah selanjutnya adalah membuat baris dan kolom menggunakan script ‘img.shape’ sehinggan menampilkan output (1973, 3330, 3) yang berarti terdapat 1973 baris, 3330 kolom dan 3 saturasi warna selanjutnya pada cell 4 script ‘[baris, kolom] = img.shape[:2]’ dijalankan untuk membuat variabel baris dan kolom yang akan menyimpan 2 nilai pertama output dari img.shape yaitu jumlah baris dan jumlah kolom.
```python
img.shape # membuat variabel dalam baris dan kolom dalam shape citra
[baris, kolom] = img.shape[:2]
```
4.	Mengkonversi Gambar dari BGR ke RGB
```python
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```
Script tersebut menggunakan fungsi ‘cvtColor’ dari library openCV dengan paramater gambar yang akan diubah adalah img dan ‘cv2.COLOR_BGR2RGB’ sebagai fungsi untuk merubah format warna dari BGR ke RGB dimana kita mengubah gambar yang sebelumnya sudah kita simpan dalam variabel img.<br>
Konversi ini perlu dilakukan karena secara default library openCV menggunakan format BGR sedangkan library matplotlib menggunakan format RGB maka gambar/citra harus diubah menjadi format RGB
5.	Menampilkan Gambar Yang Sudah Dikonversi<br>
Setelah dilakukan konversi warna pada citra maka kita akan cek apakah warna dari citra sudah sesuai dengan format warna RGB dengan menampilkan gambar dalam hal ini variabel img menggunakan fungsi imshow dari library matplotlib dengan script berikut :
```python
plt.imshow(img)
```
6.	Melakukan Operasi Gabungan Piksel Untuk Meningkatkan Kecerahan dan Kontras<br>
Sebelum melakukan deteksi warna pada citra dilakukan operasi gabungan piksel untuk meningkatkan kecerahan dan kontras karena citra asli terlihat kurang jelas kontras warnanya dan kecerahannya.
```python
alpa = 1.2
beta = 10

citra_gabungan = np.zeros((baris, kolom, 3))

for x in range (baris) :
    for y in range (kolom) :
        gcx = (img[x, y] * alpa) + beta
        citra_gabungan[x, y] = gcx

citra_gabungan = citra_gabungan.astype(np.uint8)

# menampilkan
fig, axs = plt.subplots(2, 2, figsize = (15, 5))
axs[0, 0].imshow(img)
axs[0, 1].hist(img.ravel(), 256, [0, 256])
axs[1, 0].imshow(citra_gabungan)
axs[1, 1].hist(citra_gabungan.ravel(), 256, [0, 256])
plt.show()
```
```python
alpa = 1.2
beta = 10
```
alpa disini menunjukan faktor kontras warna dimana disini kita beri nilai 1.2
beta disini menunjukan faktor kecerahan yang akan ditambahkan dimana disini kita beri nilai 10 ke setiap piksel


```python
citra_gabungan = np.zeros((baris, kolom, 3))
```
pada program ini kita membuat sebuah citra baru dengan nama citra_gabungan yang seukuran dengan citra asli.

```python
for x in range(baris):
    for y in range(kolom):
        gcx = (img[x, y] * alpa) + beta
        citra_gabungan[x, y] = gcx
```
looping ini melakukan tugas untuk mengambil nilai piksel dari citra asli, kemudian diubah sesuai dengan faktor alpa dan beta.

```python
citra_gabungan = citra_gabungan.astype(np.uint8)
```
setelah penyesuaian selesai tipe data dari variabel citra_gabungan dirubah dari float64 karena sebelumnya menggunakan np.zeros menjadi tipe data uint8 yang lebih umum digunakan untuk pemrosesan citra.

```python
fig, axs = plt.subplots(2, 2, figsize=(15, 5))
axs[0, 0].imshow(img)
axs[0, 1].hist(img.ravel(), 256, [0, 256])
axs[1, 0].imshow(citra_gabungan)
axs[1, 1].hist(citra_gabungan.ravel(), 256, [0, 256])
plt.show()
```
setelah operasi piksel dilakukan maka kita tampilkan citra asli dan citra_gabungan yang sudah disesuaikan kecerahan dan kontrasnya bersamaan dengan histogramnya untuk melihat perbedaan dengan lebih jelas<br><br>
7.	Deteksi Warna Pada Citra<br>
Selanjutnya adalah melakukan pendeteksian warna dari citra yang sudah kita sesuaikan kontras dan kecerahannya dimana kita akan mendeteksi warna Red, Green, Blue menggunakan program berikut :
```python
# gambar citra kontras (citra_gabungan)
plt.subplot(2, 2, 1)
plt.imshow(citra_gabungan)
plt.title('Citra Kontras')

# warna merah
plt.subplot(2, 2, 2)
plt.imshow(citra_gabungan[:,:,0], cmap="gray")
plt.title('RED')

# warna hijau
plt.subplot(2, 2, 3)
plt.imshow(citra_gabungan[:,:,1], cmap="gray")
plt.title('GREEN')

# warna biru
plt.subplot(2, 2, 4)
plt.imshow(citra_gabungan[:,:,2], cmap="gray")
plt.title('BLUE')

plt.show()
```
* penjelasan
```python
plt.subplot(2, 2, 1)
```
menentukan layout subplot menjadi grid 2x2 dan memilih subplot pertama untuk menampilkan citra yang telah disesuaikan kecerahan dan kontras.

```python
plt.imshow(citra_gabungan)
```
menampilkan citra yang telah disesuaikan kecerahan dan kontras pada subplot pertama dengan citra yang ditampilkan diambil dari variabel citra_gabungan.

```python
plt.title('Citra Kontra')
```
memberi judul "Citra Kontras" pada subplot pertama

```python
plt.subplot(2, 2, 2)
```
Langkah ini memilih subplot kedua untuk menampilkan deteksi warna merah dari citra yang telah disesuaikan.

```python
plt.imshow(citra_gabungan[:,:,0], cmap="gray")
plt.title('RED')
```
hasil deteksi warna merah dari citra yang telah disesuaikan ditampilkan dalam grayscale pada subplot kedua dengan pengindeksan [:,:,0] untuk menyeleksi warna merah dari citra. Selanjutnya memberi judul tampilan pada subplot 2 dengan judul RED


langkah pada deteksi warna merah digunakan lagi untuk deteksi warna lainnya dangan pengindeksan [:,:,1] untuk warna hijau dan pengindeksan [:,:,2] untuk warna biru

```python
plt.show()
```
menampilkan seluruh subplot yang sudah tulis sebelumnya.

Pada output dari program diatas dapat dilihat pada warna yang kita seleksi maka akan memudar dan nampak tidak terlalu jelas sedangkan warna lain yang tidak terseleksi akan tetap ditampilkan dengan skala grayscale.


8.	Menampilkan Histogram Pada Setiap Kategori Warna Citra<br>
Setelah berhasil melakukan deteksi warna pada citra maka kita akan melihat histogram dari setiap deteksi warnanya menggunakan script berikut :
```python
# Menghitung histogram untuk citra_gabungan
hist = cv2.calcHist([citra_gabungan], [0], None, [256], [0, 256])

fig, axs = plt.subplots(4, 2, figsize=(15, 15))

# citra_kontras(citra_gabungan) dan histogramnya
axs[0, 0].imshow(citra_gabungan)
axs[0, 0].set_title('Citra Kontras')
axs[0, 1].plot(hist)
axs[0, 1].set_title('Citra Kontras Histogram')

# RED
red = citra_gabungan[:, :, 0]
redHist = cv2.calcHist([red], [0], None, [256], [0, 256])
axs[1, 0].imshow(red, cmap='gray')
axs[1, 0].set_title('RED')
axs[1, 1].plot(redHist, color='r')
axs[1, 1].set_title('RED HISTOGRAM')

# GREEN
green = citra_gabungan[:, :, 1]
greenHist = cv2.calcHist([green], [0], None, [256], [0, 256])
axs[2, 0].imshow(green, cmap='gray')
axs[2, 0].set_title('GREEN')
axs[2, 1].plot(greenHist, color='g')
axs[2, 1].set_title('GREEN HISTOGRAM')

# BLUE
biru = citra_gabungan[:, :, 2]
hist_biru = cv2.calcHist([biru], [0], None, [256], [0, 256])
axs[3, 0].imshow(biru, cmap='gray')
axs[3, 0].set_title('Biru')
axs[3, 1].plot(hist_biru, color='b')
axs[3, 1].set_title('Histogram Biru')

plt.tight_layout()
plt.show()
```
* penjelasan
```python
hist = cv2.calcHist([citra_gabungan], [0], None, [256], [0, 256])
fig, axs = plt.subplots(4, 2, figsize=(15, 15))
```

digunakan fungsi cv2.calcHist() untuk menghitung histogram dari _gabungan dan dihitung untuk dalam skala grayscale dengan menentukan jumlah bin histogram (256) serta rentang nilai (0 sampai 256). Setelah menghitung histogram output akan ditampilkan dalam subplot dengan plt.subplots(4, 2, figsize=(15, 15)) dimana akan terbentuk subplot 4 baris dan 2 kolom jadi total 8 subplot.

```python
axs[0, 0].imshow(citra_gabungan)
axs[0, 0].set_title('Citra Kontras')
axs[0, 1].plot(hist)
axs[0, 1].set_title('Citra Kontras Histogram')
```
menampilkan gambar citra_kontras dari citra_gabungan dan memberi judul subplot dengan judul Citra Kontras pada subplot pertama kemudian menampilkan histogram dari citra_kontras yang sudah dihitung sebelumnya pada subplot kedua dan memberi judul subplotnya 'Citra Kontras Histogram'


```python
red = citra_gabungan[:, :, 0] 
```
membuat variabel bernama red untuk menyimpan citra warna merah

```python
redHist = cv2.calcHist([red], [0], None, [256], [0, 256])
```
membuat histogram dari citra warna merah dan disimpan dalam variabel `redHist` menggunakan fungsi cv2.calcHist dari library openCV.

```python
axs[0, 0].imshow(red, cmap='gray')
axs[0, 0].set_title('RED')
```
citra warna merah ditampilkan pada subplot 2, dalam skala grayscale dan memberi judul plotnya dengan judul RED

```python
axs[0, 1].plot(redHist, color='r')
```
menampilkan

```python
axs[0, 1].set_title('RED HISTOGRAM')
```
Subplot kedua diberi judul "RED HISTOGRAM" untuk mengidentifikasi konten subplot tersebut.

-	Untuk menampilkan gambar citra hijau dan biru sama dengan cara menampilkan citra merah hanya dirubah variabel dan pengindeksannya

```python
plt.tight_layout()
```
memastikan tata letak subplot yang rapi.

```python
plt.show()
```
menampilkan semua subplot dalam satu jendela tampilan. Sehingga menampilkan histogram setiap gambar sebagai berikut.

Berdasarkan program diatas terdapat tiga histogram yang menunjukkan distribusi frekuensi warna pada gambar "DWITIAN TANGGUH EDINUGRAHA". Histogram tersebut berwarna merah, hijau, dan biru, sesuai dengan warna primer yang digunakan dalam gambar.

Perbedaan utama antara ketiga histogram tersebut adalah distribusi frekuensi warna yang berbeda.

- Histogram merah menunjukkan bahwa warna merah adalah warna yang paling dominan dalam gambar, dengan frekuensi tertinggi pada rentang nilai 1500-2000.
- Histogram hijau menunjukkan bahwa warna hijau adalah warna yang paling dominan kedua dalam gambar, dengan frekuensi tertinggi pada rentang nilai 1000-1500.
- Histogram biru menunjukkan bahwa warna biru adalah warna yang paling dominan ketiga dalam gambar, dengan frekuensi tertinggi pada rentang nilai 1500-2000.

9. mencari dan mengurutkan nilai ambang batas
```python
def find_threshold(hist):
    peaks = []
    threshold = []
    
    for i in range(1, len(hist)-1):
        if hist[i] > hist[i-1] and hist[i] > hist[i+1]:
            peaks.append(i)
    
    # Mengambil nilai tengah antara dua puncak histogram sebagai ambang batas
    for i in range(len(peaks) - 1):
        threshold.append((peaks[i] + peaks[i+1]) // 2)
    
    return threshold
```
Program ini berfungsi untuk mengidentifikasi ambang batas pada histogram setiap warna dalam sebuah citra. Pertama, program menghitung histogram untuk setiap saluran warna (merah, hijau, dan biru) menggunakan fungsi cv2.calcHist. Kemudian, dengan menggunakan fungsi find_threshold, program menemukan nilai ambang batas berdasarkan puncak-puncak dalam histogram. Ambang batas ini diurutkan dari nilai terkecil hingga terbesar untuk memudahkan penggunaan selanjutnya menggunakan fungsi .sort(). Sehingga program mencetak nilai ambang batas yang telah ditemukan

10. menampilkan kategori warna pada citra dengan nilai ambang batas metode 1

```python
gray = cv2.cvtColor(citra_gabungan, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots(2, 2, figsize=(10, 10))

# Ambang batas none
(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)  
axs[0, 0].imshow(binary1, cmap='gray')
axs[0, 0].set_title('NONE')

# Ambang warna blue
(thresh, binary2) = cv2.threshold(gray, 70, 255, cv2.THRESH_BINARY)  
axs[0, 1].imshow(binary2, cmap='binary')
axs[0, 1].set_title('BLUE')

# Ambang warna red-blue
(thresh, binary3) = cv2.threshold(gray, 100, 255, cv2.THRESH_BINARY)
axs[1, 0].imshow(binary3, cmap='binary')
axs[1, 0].set_title('RED-BLUE')

# Ambang warna red-green-blue
(thresh, binary4) = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)
axs[1, 1].imshow(binary4, cmap='binary')
axs[1, 1].set_title('RED-GREEN-BLUE')

plt.tight_layout()
plt.show()
```
Program tersebut melakukan pemrosesan pada citra untuk menampilkan empat versi citra dengan ambang batas yang berbeda. Berikut adalah penjelasan detailnya:

1. Pertama, citra digunakan untuk membuat citra skala abu-abu (`gray`) menggunakan fungsi `cv2.cvtColor` dengan parameter `cv2.COLOR_RGB2GRAY`.

2. Kemudian, program membuat sebuah subplot dengan 2 baris dan 2 kolom menggunakan `plt.subplots(2, 2, figsize=(10, 10))`.

3. Ambang batas yang digunakan dalam proses binerisasi (mengubah citra menjadi citra biner) ditentukan dalam empat langkah berikut:
   - Langkah pertama (`binary1`): Ambang batas 0 digunakan untuk membuat citra biner, yang artinya semua piksel dengan intensitas lebih tinggi dari 0 akan menjadi putih, sedangkan yang lainnya hitam. Ini menghasilkan citra yang sama dengan citra skala abu-abu.
   - Langkah kedua (`binary2`): Ambang batas 70 digunakan untuk menghasilkan citra biner di mana piksel dengan intensitas lebih tinggi dari 70 akan menjadi putih, sedangkan yang lainnya hitam. Ini bertujuan untuk menyoroti bagian citra yang cenderung berwarna biru.
   - Langkah ketiga (`binary3`): Ambang batas 100 digunakan untuk menciptakan citra biner di mana piksel dengan intensitas lebih tinggi dari 100 akan menjadi putih, sedangkan yang lainnya hitam. Ini bertujuan untuk menyoroti bagian citra yang cenderung berwarna merah dan biru.
   - Langkah keempat (`binary4`): Ambang batas 150 digunakan untuk menciptakan citra biner di mana piksel dengan intensitas lebih tinggi dari 150 akan menjadi putih, sedangkan yang lainnya hitam. Ini bertujuan untuk menyoroti bagian citra yang cenderung memiliki semua warna (merah, hijau, dan biru).

4. Setiap citra biner kemudian ditampilkan dalam subplot yang sesuai dengan judul yang sesuai.

5. Terakhir, `plt.tight_layout()` digunakan untuk memastikan layout subplot terlihat rapi, dan `plt.show()` untuk menampilkan gambar-gambar tersebut.

alasan mengapa menggunakan ambang 70 untuk blue, 120 untuk red-blue, dan 150 untuk red-green-blue karena setelah mencari dan mengurutkan nilai ambang batas pada program sebelumnya angka ini berada diantara nilai minimum dan maksimum ambang batas dan setelah dilakukan berbagai percobaan angka tersebut menghasilkan tampilan kategori warna yang paling mendekati, namun dengan program tersebut hasil terasa kurang memuaskan, oleh karena itu disini digunakan program lain untuk menampilkan kategori warna berdasarkan nilai ambang batasnya

11. menampilkan kategori warna pada citra dengan nilai ambang batas metode 2

```python
hsv_image = cv2.cvtColor(citra_gabungan, cv2.COLOR_RGB2HSV)

# Definisikan rentang warna untuk setiap warna
lower_blue = np.array([100, 100, 100])
upper_blue = np.array([140, 255, 255])

# Gunakan ambang batas untuk warna hijau yang telah Anda temukan
lower_green = np.array([20, 100, 100])
upper_green = np.array([250, 255, 255])

lower_red1 = np.array([0, 100, 100])
upper_red1 = np.array([10, 255, 255])
lower_red2 = np.array([160, 100, 100])
upper_red2 = np.array([180, 255, 255])

# Deteksi warna merah
mask_red1 = cv2.inRange(hsv_image, lower_red1, upper_red1)
mask_red2 = cv2.inRange(hsv_image, lower_red2, upper_red2)
mask_red = np.maximum(mask_red1, mask_red2)

# Deteksi warna hijau
mask_green = cv2.inRange(hsv_image, lower_green, upper_green)

# Deteksi warna biru
mask_blue = cv2.inRange(hsv_image, lower_blue, upper_blue)

# Deteksi warna red-green-blue
mask_red_green_blue = np.maximum(np.maximum(mask_red, mask_green), mask_blue)

# subplot 1
gray = cv2.cvtColor(citra_gabungan, cv2.COLOR_RGB2GRAY)
fig, axs = plt.subplots (2, 2, figsize=(10,10))

(thresh, binary1) = cv2.threshold(gray, 0, 0, cv2.THRESH_BINARY)
axs[0,0].imshow(binary1, cmap = 'gray')
axs[0,0].set_title('NONE')

# subplot 2
plt.subplot(2, 2, 2)
plt.imshow(mask_blue, cmap='gray')
plt.title('Blue')
plt.xticks(np.arange(0, mask_blue.shape[1]+1, 800))
plt.yticks(np.arange(0, mask_blue.shape[0]+1, 500))
plt.axis('on')

# subplot 3
plt.subplot(2, 2, 3)
plt.imshow(np.maximum(mask_red, mask_blue), cmap='gray')
plt.title('reed-blue')
plt.xticks(np.arange(0, mask_green.shape[1], 800))
plt.yticks(np.arange(0, mask_green.shape[0], 500))
plt.axis('on')

# subplot 4
plt.subplot(2, 2, 4)
plt.imshow(mask_red_green_blue, cmap='gray')
plt.title('Red-Green-Blue')
plt.xticks(np.arange(0, mask_green.shape[1], 800))
plt.yticks(np.arange(0, mask_green.shape[0], 500))
plt.axis('on')

# menampilkan output
plt.tight_layout()
plt.show()
```

* penjelasan

1. Citra awal dikonversi ke ruang warna HSV menggunakan fungsi `cv2.cvtColor`.

2. Rentang warna untuk setiap warna (biru, hijau, merah) ditentukan. Setiap warna didefinisikan oleh batas bawah (`lower`) dan batas atas (`upper`) dalam ruang warna HSV. Misalnya, untuk warna biru, rentang warna ditentukan dari nilai Hue (H) sekitar 100-140 dan untuk warna merah Sebenarnya, kita hanya memerlukan dua masker untuk warna merah. Namun, dalam ruang warna HSV, nilai hue (H) yang menunjukkan warna merah memiliki rentang dari 0-10 dan 160-180. Karena nilai hue ini dapat melintasi batas 0-180, kita perlu membagi rentang menjadi dua bagian dan mendeteksi warna merah dalam dua rentang tersebut. Oleh karena itu, kita menggunakan dua masker untuk mendeteksi warna merah: satu untuk rentang 0-10 dan satu lagi untuk rentang 160-180. Setelah itu, kedua masker tersebut digabungkan menggunakan operasi np.maximum() untuk mendapatkan masker akhir yang menunjukkan wilayah yang berwarna merah.

3. Deteksi warna dilakukan untuk setiap warna (biru, hijau, merah) menggunakan fungsi `cv2.inRange`. Fungsi ini menghasilkan citra biner di mana piksel yang berada dalam rentang warna akan menjadi putih, sedangkan yang lainnya hitam. Untuk warna merah, karena rentang warnanya melintasi nilai H yang meliputi 0 dan 180, dua rentang (merah ke oranye dan merah muda ke magenta) diambil terpisah dan digabungkan dengan menggunakan operasi `np.maximum`.

4. Subplot dibuat untuk menampilkan empat versi citra dengan deteksi warna yang berbeda:
   - Subplot pertama menampilkan citra awal dalam skala abu-abu.
   - Subplot kedua menampilkan citra biner yang menyoroti piksel yang sesuai dengan warna biru.
   - Subplot ketiga menampilkan citra biner yang menyoroti piksel yang sesuai dengan warna merah dan biru.
   - Subplot keempat menampilkan citra biner yang menyoroti piksel yang sesuai dengan warna merah, hijau, dan biru.

5. Setiap subplot diberi judul yang sesuai.

6. Terakhir, menggunakan `plt.tight_layout()` untuk memastikan layout subplot terlihat rapi, dan `plt.show()` untuk menampilkan gambar-gambar tersebut.
7. Untuk alasan mengapa menggunakan angka tersebut sebagai ambang batas karena angkka tersebut berada diantara batas minimum dan maksimum setiap warna dan menghasilkan tampilan kategori warna yang paling mendekati sempurna

# Teori Pendukung
## Library yang digunakan

1.	OpenCV (Open Source Computer Vision Library)

 Adalah sebuah library open source  yang memiliki fokus pada pengolahan gambar dan pengenalan pola. Library ini berfungsi unruk membaca serta memanipulasi gambar atau video dan melakukan operasi pemrosesan citra seperti deteksi objek, segmentasi dll. Library ini memiliki keunggulan dalam menyediakan fungsi untuk berbagai macam tugas pengolahan citra dan visi komputer.

2.	Matplotlib

Adalah suatu library dalam python untuk membuat visualisasi data seperti grafik, plot, diagram  dll serta berfungsi untuk membuat plot 2D dan 3D dari data numerik dalam array. Keunggulan library ini adalah adanya dukungan yan g luas untuk berbagai jenis plot serta fleksibel dan mudah digunakan.

3. NumPy

NumPy adalah library untuk mengolah dan memanipulasi data dalam bentuk array. Melalui berbagai fungsi matematika yang terintegrasi sampai kemudahan dalam pembuatan dan manipulasi array, NumPy memastikan kita dapat fokus pada penggalian informasi daripada terhambat oleh keterbatasan teknis.

## Representasi Pengolahan Citra dalam Kehidupan Nyata

1.	Pengolahan Citra Dalam Bidang Medis

Penerapan pengolahan citra digital dalam dunia medis membantu analisis dan diagnosa medis dengan cara mengidentifikasi area patologis dalam tubuh menggunakan sinar-X, CT scan, dan lainnya seperti deteksi tumor pada pasien dengan melakukan segmentasi untuk mengidentifikasi bagian mana yang organ dan bagian mana yang merupakan tumor.

2.	Pengolahan Citra Satelit

Pengolahan Citra Digital juga digunakan dalam Pengolahan citra satelit dimana pengolahan citra satelit adalah aplikasi pengolahan citra yang digunakan untuk menganalisis gambar dari satelit atau pesawat terbang yang digunakan untuk memantau permukaan bumi dari ruang angkasa. Salah satu contohnya adalah Pemantauan Perubahan Lahan, yang memungkinkan untuk memantau perubahan lahan seperti urbanisasi, perubahan penggunaan lahan, atau dampak lingkungan dari pembangunan infrastruktur. Ini membantu pemantauan lingkungan dan perencanaan kota.

3.	Pengolahan Citra Keamanan

Pengaplikasin pengolahan citra digital ini digunakan untuk menganalisis gambar dari sistem keamanan seperti kamera CCTV, sensor pengawasan, dan lainnya. Contohnya adalah Deteksi Wajah, yang dapat diidentifikasi melalui pengolahan citra. Ini memungkinkan pemantauan dan keamanan di tempat umum seperti bandara, stasiun kereta, atau pusat perbelanjaan, sehingga jika terdapar seorang DPO yang melarikan diri dan tertangkap kamera pengawas maka akan langsung terdeteksi karena adanya pengolahan citra dari potret dirinya sebelum ia melarikan diri.

Pada program project ini memiliki beberapa langkah dalam memproses citra. Pertama, citra dimuat dan dikonversi ke dalam format RGB untuk mempermudah analisis. Selanjutnya, dilakukan penyesuaian terhadap kontras dan kecerahan citra agar gambar lebih terang dan detailnya lebih terlihat. Setelah itu, dilakukan analisis histogram untuk memahami sebaran warna dalam gambar. Informasi ini penting dalam menentukan langkah-langkah selanjutnya. Kemudian, dilakukan deteksi warna untuk menemukan area dengan warna tertentu, seperti merah, hijau, dan biru. Ambang batas juga ditentukan berdasarkan histogram untuk setiap warna yang dideteksi. Ini membantu dalam memisahkan elemen berwarna dalam citra. Citra hasil proses dan histogramnya ditampilkan dalam subplot secara terpisah, memudahkan untuk melihat efek dari setiap langkah proses pengolahan citra. Selain itu, program ini memanfaatkan teknik-teknik dasar dalam pengolahan citra, seperti konversi warna, analisis histogram, dan deteksi warna, yang merupakan langkah awal dalam banyak aplikasi yang lebih kompleks dalam pengolahan citra, seperti pengenalan objek, deteksi wajah, dan lainnya.

# Jurnal Terkait

PENGOLAHAN CITRA DIGITAL DAN HISTOGRAM DENGAN PHYTON DAN TEXT EDITOR PHYCHARM


https://ojs.uniska-bjm.ac.id/index.php/JIT/article/view/3294

Deteksi Warna Manggis Menggunakan Pengolahan Citra dengan Opencv Python

https://doi.org/10.24036/voteteknika.v9i4.114251
