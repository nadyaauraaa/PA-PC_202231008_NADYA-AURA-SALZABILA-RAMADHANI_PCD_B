# Teori Tentang Deteksi Tepi Pola Objek

1. Definisi Tepi

Tepi adalah tempat perubahan intensitas yang signifikan dalam gambar terjadi. Tepi biasanya mewakili batas antara objek dan latar belakang atau batas antara dua wilayah dengan intensitas yang berbeda.

2. Pentingnya Deteksi Tepi

Deteksi tepi sangat penting karena:

Mengidentifikasi Struktur: Tepi memberikan informasi penting tentang bentuk dan struktur objek dalam gambar.
Reduksi Data: Deteksi tepi mengurangi jumlah data yang perlu diproses tanpa menghilangkan informasi penting.
Segmentasi: Tepi membantu dalam memisahkan objek dari latar belakang, yang penting untuk segmentasi gambar.

3. Metode Deteksi Tepi

Beberapa metode populer untuk deteksi tepi meliputi:

a. Operator Sobel
Menggunakan dua kernel (horizontal dan vertikal) untuk menghitung gradien intensitas di setiap titik dalam gambar.
Kernel Sobel menggabungkan smoothing dan differentiation.
Menghasilkan peta gradien yang menunjukkan area dengan perubahan intensitas tinggi (tepi).

b. Operator Prewitt
Mirip dengan Sobel tetapi menggunakan kernel yang sedikit berbeda.
Digunakan untuk mendeteksi tepi horizontal dan vertikal.

c. Operator Canny
Salah satu metode deteksi tepi yang paling populer.
Melibatkan beberapa langkah: smoothing dengan Gaussian filter, menghitung gradien, non-maximum suppression, dan penelusuran tepi menggunakan histeresis thresholding.
Hasilnya adalah peta tepi yang lebih bersih dan lebih sedikit noise.

d. Operator Laplacian of Gaussian (LoG)
Menggunakan kombinasi smoothing dengan Gaussian filter dan differentiation dengan operator Laplacian.
Menangkap tepi dengan mendeteksi perubahan kedua intensitas.

4. Aplikasi Deteksi Tepi

Deteksi tepi digunakan dalam berbagai aplikasi seperti:

Pengenalan Objek: Membantu dalam mengenali dan mengidentifikasi objek dalam gambar.

Segmentasi Gambar: Memisahkan objek dari latar belakang untuk analisis lebih lanjut.

Peningkatan Citra: Meningkatkan kualitas gambar dengan menyoroti batas objek.

Pemetaan 3D: Membantu dalam rekonstruksi 3D dengan menemukan batas objek dalam gambar 2D.


# Langkah - Langkah 

- import cv2 : Mengimpor library cv2 (OpenCV) untuk pengolahan citra.

- import matplotlib.pyplot as plt : Mengimpor library cv2 (OpenCV) untuk pengolahan citra.
Mengimpor library matplotlib.pyplot sebagai plt untuk visualisasi gambar.

- image = cv2.imread('aura2.jpg') : Menggunakan fungsi cv2.imread() untuk membaca gambar dengan nama file 'aura2.jpg' dari direktori kerja saat ini dan Variabel image akan berisi data gambar dalam bentuk array Numpy.

- gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY) : gray menunjukkan bahwa gambar akan diubah menjadi skala abu-abu, di mana intensitas piksel hanya direpresentasikan oleh satu saluran warna (intensitas), cv2.cvtColor() adalah fungsi dalam OpenCV yang digunakan untuk mengubah ruang warna atau format warna suatu gambar, image adalah variabel yang berisi gambar dalam format BGR (default format dalam OpenCV setelah membaca gambar dengan cv2.imread()) dan cv2.COLOR_BGR2GRAY adalah konstanta yang menentukan konversi warna dari BGR ke skala abu-abu (grayscale).

- blurred = cv2.GaussianBlur(gray, (5, 5), 1.4) : cv2.GaussianBlur() adalah fungsi dalam OpenCV yang digunakan untuk menerapkan filter Gaussian blur pada gambar, gray adalah variabel yang berisi gambar dalam format skala abu-abu (hasil dari konversi BGR ke skala abu-abu menggunakan cv2.cvtColor()), (5, 5) adalah ukuran kernel filter Gaussian yang akan digunakan. Kernel berukuran (5, 5) berarti filter akan melihat 5x5 piksel di sekitar setiap piksel untuk menghitung nilai rata-rata dan 1.4 adalah sigma, yang mengontrol seberapa tajam atau halus blur yang dihasilkan. Semakin besar nilai sigma, semakin besar efek blur yang dihasilkan.

- edges = cv2.Canny(blurred, 100, 200) : cv2.Canny() adalah fungsi dalam OpenCV yang digunakan untuk melakukan deteksi tepi menggunakan algoritma Canny, blurred adalah variabel yang berisi gambar yang telah diberikan filter Gaussian blur sebelumnya dan 100 dan 200 adalah nilai threshold yang digunakan untuk menentukan intensitas tepi.

- contours, hierarchy = cv2.findContours(edges, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE) : contours adalah daftar dari semua kontur yang ditemukan dalam gambar, hierarchy adalah struktur data yang menggambarkan hubungan parent-child antara kontur. Informasi ini sangat berguna ketika bekerja dengan kontur yang saling berhubungan atau terdapat hierarki di antara objek dalam gambar.cv2.findContours() adalah fungsi dalam OpenCV yang digunakan untuk menemukan kontur atau batas objek dalam gambar biner, edges adalah gambar biner (hasil deteksi tepi menggunakan algoritma Canny) di mana tepi dari gambar asli ditandai dengan piksel putih (nilai tinggi) dan latar belakangnya hitam (nilai rendah), cv2.RETR_TREE adalah mode retrieval hierarchy untuk kontur. Mode ini mengembalikan semua kontur dan menyusunnya dalam struktur pohon yang menggambarkan hubungan parent-child antara kontur dan cv2.CHAIN_APPROX_SIMPLE adalah metode aproksimasi kontur. Metode ini menggabungkan titik-titik yang berdekatan dan lurus untuk mengurangi jumlah titik yang digunakan dalam representasi kontur.

- contour_image = image.copy() : image adalah variabel yang berisi gambar asli yang telah dibaca dan diproses sebelumnya dan image.copy() digunakan untuk membuat salinan dari gambar asli. Ini penting karena kita akan menggambar kontur pada salinan ini tanpa mempengaruhi gambar asli.
  
- cv2.drawContours(contour_image, contours, -10, (0, 255, 0), 5) : adalah fungsi dalam OpenCV yang digunakan untuk menggambar kontur pada gambar, contour_image adalah gambar di mana kontur akan digambar. Dalam konteks ini, ini adalah salinan dari gambar asli, contours adalah daftar dari semua kontur yang ditemukan sebelumnya menggunakan cv2.findContours(), -10 menunjukkan bahwa kita akan menggambar semua kontur yang ditemukan, (0, 255, 0) adalah warna kontur dalam format BGR (di sini, warna hijau yang kuat dengan nilai 255 pada saluran hijau) dan 5 ini adalah ketebalan garis untuk menggambar kontur.

- plt.figure(figsize=(10, 5)) : digunakan untuk membuat gambar plot dengan ukuran tertentu. Di sini, gambar plot akan memiliki lebar 10 inci dan tinggi 5 inci.

- plt.subplot(1, 2, 1) : untuk membuat subplot pertama dalam grid 1x2 (satu baris, dua kolom).

- plt.title('Original Image') : untuk menambahkan judul 'Original Image' pada subplot pertama.

- plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)) : untuk menampilkan gambar dalam format RGB menggunakan cv2.cvtColor() untuk mengonversi dari BGR (format OpenCV) ke RGB (format yang digunakan oleh Matplotlib).

- plt.subplot(1, 2, 2) : untuk membuat subplot kedua dalam grid 1x2.

- plt.title('Canny Edge Detection') : untuk menambahkan judul 'Canny Edge Detection' pada subplot kedua.

- plt.imshow(edges, cmap='gray') : untuk menampilkan gambar edges yang merupakan hasil dari deteksi tepi menggunakan algoritma Canny. Penggunaan cmap='gray' mengonfigurasi colormap agar gambar ditampilkan dalam skala abu-abu.

- plt.show() : digunakan untuk menampilkan semua subplot yang telah didefinisikan sebelumnya dalam satu jendela grafik.


- plt.figure(figsize=(15, 5)) : digunakan untuk membuat gambar plot dengan ukuran tertentu. Di sini, gambar plot akan memiliki lebar 15 inci dan tinggi 5 inci.

- plt.subplot(1, 3, 1) : untuk membuat subplot pertama dalam grid 1x3 (satu baris, tiga kolom).

- plt.title('Original Image') : untuk menambahkan judul 'Original Image' pada subplot pertama.

- plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB)) : untuk menampilkan gambar dalam format RGB menggunakan cv2.cvtColor() untuk mengonversi dari BGR (format OpenCV) ke RGB (format yang digunakan oleh Matplotlib).

- plt.subplot(1, 3, 2) : untuk membuat subplot kedua dalam grid 1x3.

- plt.title('Canny Edge Detection') : untuk menambahkan judul 'Canny Edge Detection' pada subplot kedua.

- plt.imshow(edges, cmap='gray') : untuk menampilkan gambar edges yang merupakan hasil dari deteksi tepi menggunakan algoritma Canny. Penggunaan cmap='gray' mengonfigurasi colormap agar gambar ditampilkan dalam skala abu-abu.


- plt.subplot(1, 3, 3) : untuk membuat subplot ketiga dalam grid 1x3.

- plt.title('Contours Detection') : untuk menambahkan judul 'Contours Detection' pada subplot ketiga.

- plt.imshow(cv2.cvtColor(contour_image, cv2.COLOR_BGR2RGB)) : untuk menampilkan gambar contour_image yang merupakan gambar asli yang telah digambari dengan kontur menggunakan cv2.drawContours(). Kita menggunakan cv2.cvtColor() untuk mengonversi dari BGR ke RGB sebelum menampilkan gambar dengan Matplotlib.

- plt.show() : digunakan untuk menampilkan semua subplot yang telah didefinisikan sebelumnya dalam satu jendela grafik.


