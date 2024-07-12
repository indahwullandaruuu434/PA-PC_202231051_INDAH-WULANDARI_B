# PA-PC_202231051_INDAH-WULANDARI_B
### Deteksi Tepi Pola Objek (⁠・⁠∀⁠・⁠)

Di repository ini, kami mengeksplorasi teknik-teknik untuk mendeteksi tepi pada pola objek dalam gambar.

#### Apa Itu Deteksi Tepi?
Deteksi tepi adalah teknik penting dalam pengolahan gambar yang membantu mengidentifikasi batas-batas objek dalam sebuah gambar. Dalam proyek ini, kami fokus pada menganalisis bagaimana berbagai algoritma dapat digunakan untuk mengenali tepi pada pola objek yang kompleks.

#### Algoritma yang Digunakan
- **Sobel Operator**: Memanfaatkan gradien untuk menyoroti tepi dalam gambar.
- **Canny Edge Detector**: Algoritma multistage yang akurat dalam mengidentifikasi tepi dengan tingkat error rendah.
- **Laplacian of Gaussian (LoG)**: Menggabungkan teknik smoothing Gaussian dengan operator Laplacian untuk deteksi tepi yang lebih tepat.

#### Struktur Proyek
- **`/code`**: Berisi implementasi dari algoritma deteksi tepi.
- **`/images`**: Contoh gambar yang digunakan untuk pengujian.
- **`README.md`**: Dokumentasi utama proyek ini.

#### Cara Penggunaan
Untuk menggunakan algoritma deteksi tepi:
```bash
python detect_edges.py --image nama_gambar.jpg
```
#### penjelasan projek
sebelum memulai projek ini saya mengambil gambar diri saya sendiri untuk bahan yang akan di kelola di projek ini menggunkan berbagai ketentuan yang di buat 
```bash
import cv2
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
import skimage
```
saya mengimpor beberapa pustaka yang umum digunakan untuk memproses dan memvisualisasikan gambar di Python:
1. `cv2` untuk pemrosesan gambar dan komputer vision.
2. `numpy` (alias `np`) untuk komputasi numerik dan manipulasi array.
3. `matplotlib.pyplot` (alias `plt`) untuk visualisasi data dan plot.
4. `%matplotlib inline` untuk menampilkan plot Matplotlib langsung di dalam Jupyter Notebook.
5. `skimage` untuk algoritma pemrosesan gambar dan utilitas tambahan.
   
```bash
image = cv2.imread('1.jpg')

cv2.imshow("indah", image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
Kode yang Anda berikan digunakan untuk membaca dan menampilkan gambar dengan OpenCV di Python. Pertama, gambar "1.jpg" dibaca menggunakan `cv2.imread()` dan disimpan dalam variabel `image`. Kemudian, gambar ditampilkan dalam sebuah jendela dengan judul "indah" menggunakan `cv2.imshow()`. Program akan menunggu hingga pengguna menekan tombol apa pun (`cv2.waitKey(0)`) sebelum menutup jendela. Setelah itu, semua jendela yang dibuat oleh OpenCV dihancurkan dengan `cv2.destroyAllWindows()`, memastikan program keluar dengan bersih setelah gambar ditampilkan.

```bash
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(image, 170, 170)
```
Dalam kode tersebut, `gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)` digunakan untuk mengubah gambar `image` menjadi citra skala abu-abu (grayscale) dengan menggunakan fungsi `cv2.cvtColor()` dari OpenCV. Sedangkan `edges = cv2.Canny(image, 170, 170)` menggunakan metode deteksi tepi Canny untuk menghasilkan citra tepi dari gambar `image`. Parameter 170 dan 170 mengontrol ambang deteksi tepi yang digunakan dalam proses ini.

```bash
cv2.imshow("Gambar indah", edges)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
Kode tersebut menampilkan citra tepi (variabel `edges`) dalam jendela grafis dengan judul "Gambar indah" menggunakan OpenCV di Python. Program menunggu pengguna menekan tombol sebelum menutup jendela dan mengakhiri program dengan bersih.

```bash
ig, axs = plt.subplots(1,2, figsize =(10,10))
ax = axs.ravel()

ax[0].imshow(gray, cmap = "gray")
ax[0].set_title("Gambar Asli")

ax[1].imshow(edges, cmap = "gray")
ax[1].set_title("Gambar Setelah di Olah")
```
Kode ini menggunakan Matplotlib untuk membuat tampilan visual dari dua gambar secara berdampingan dalam satu figur. Pertama, gambar asli ditampilkan dalam skala abu-abu di subplot pertama dengan judul "Gambar Asli". Kemudian, subplot kedua menampilkan gambar hasil olahan menggunakan deteksi tepi Canny, juga dalam skala abu-abu, dengan judul "Gambar Setelah di Olah". Ukuran figur yang dihasilkan adalah 10x10 inci.

```bash
lines = cv2.HoughLinesP(edges, 1, np.pi/250, 20, maxLineGap = -50)
image_line = image.copy()
```
Baris kode ini menggunakan metode Transformasi Hough untuk mendeteksi garis-garis dalam gambar yang telah diolah menjadi tepi (`edges`). Parameter `1` dan `np.pi/250` mengatur resolusi jarak dan resolusi sudut untuk deteksi garis. `20` adalah ambang batas minimum piksel yang diperlukan untuk diterima sebagai garis, sedangkan `maxLineGap = -50` menentukan toleransi maksimum celah dalam piksel antara bagian terputus dari garis yang sama.

```bash
for line in lines:
    x1, y1, x2, y2, = line[0]
    cv2.line(image_line,(x1,y1),(x2,y2),(0,2550, 0), 3)
```
Kode ini iterasi melalui setiap garis yang terdeteksi (`lines`) menggunakan metode Transformasi Hough dan menggambar garis tersebut pada gambar `image_line`. Setiap garis direpresentasikan oleh titik awal `(x1, y1)` dan titik akhir `(x2, y2)`, dengan ketebalan garis sebesar `3` piksel, dan warna garisnya adalah hijau `(0, 255, 0)`.

```bash
import matplotlib.pyplot as plt

fig, axs = plt.subplots(1, 3, figsize=(10, 10))
ax = axs.ravel()

ax[0].imshow(gray, cmap="gray")
ax[0].set_title("Gambar Asli")

ax[1].imshow(edges, cmap="gray")
ax[1].set_title("Canny Edges Image")

ax[2].imshow(image_line, cmap="gray")
ax[2].set_title("Gambar setelah diolah")

plt.show()
```
Kode ini menggunakan `matplotlib` untuk menampilkan beberapa gambar secara bersamaan dalam satu jendela. Gambar asli ditampilkan di subplot pertama (`ax[0]`), tepi-tepi yang dihasilkan oleh detektor Canny ditampilkan di subplot kedua (`ax[1]`), dan gambar hasil deteksi garis dengan metode Hough ditampilkan di subplot ketiga (`ax[2]`). Setiap subplot dilengkapi dengan judul yang sesuai.

#### Penghargaan
saya  mengucapkan terima kasih kepada seluruh kontributor dan pustaka sumber terbuka yang telah membantu dalam pengembangan proyek ini.

Jangan ragu untuk mengadaptasi dan memperluas README ini sesuai dengan kebutuhan proyek mu (⁠・⁠∀⁠・⁠)!
