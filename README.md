
PCD_UTS_202231072_2024_ITPLN
1. Deteksi Warna Citra
A. Penjelasan Kode Program
Pertama-tama, program mengimpor beberapa pustaka yang diperlukan:
cv2: Ini adalah pustaka OpenCV yang digunakan untuk bekerja dengan gambar.
matplotlib.pyplot: Ini digunakan untuk menampilkan gambar dan plot.
numpy: Ini adalah pustaka Python yang kuat untuk komputasi numerik.

Kemudian, program membaca sebuah gambar dengan menggunakan fungsi cv2.imread(). Gambar ini disimpan dalam variabel citra. Anda perlu pastikan bahwa gambar dengan nama "foto_nama.jpg" ada di direktori yang sama dengan script Python.

Selanjutnya, citra dibalik saluran warnanya dari BGR (Blue-Green-Red) ke RGB (Red-Green-Blue) menggunakan fungsi cv2.cvtColor(). Ini penting karena OpenCV membaca gambar dalam format BGR, sedangkan matplotlib (yang akan kita gunakan untuk menampilkan gambar) mengharapkan format RGB.

Setelah itu, saluran warna dari gambar RGB dipisahkan menggunakan slicing array NumPy. Setiap saluran warna (merah, hijau, dan biru) disimpan dalam variabel terpisah:
red_channel: Saluran warna merah (R)
green_channel: Saluran warna hijau (G)
blue_channel: Saluran warna biru (B)

Program kemudian menggunakan matplotlib.pyplot untuk menampilkan gambar dalam empat subplot:
Subplot pertama menampilkan gambar RGB asli dengan menggunakan plt.imshow() dan menyertakan judul subplot serta menonaktifkan sumbu x dan y dengan plt.title() dan plt.axis('off').
Subplot kedua, ketiga, dan keempat menampilkan saluran warna merah, hijau, dan biru secara berurutan. Pengaturan yang sama dilakukan seperti pada subplot pertama.

Terakhir, panggilan plt.show() digunakan untuk menampilkan semua subplot secara bersamaan.

B. Analisis Citra
Pada tahap pertama dilakukan import library lalu kita dapat melakukan import image.
Karena citra yang dibaca saat dimport masih dalam bentuk BGR(Blue Green Red), kita harus mengubahnya ke dalam bentuk RGB(Red Green Blue) karena Citra dalam format BGR (Blue, Green, Red) umumnya digunakan dalam beberapa framework pengolahan citra seperti OpenCV, sementara kebanyakan aplikasi dan perangkat lunak lainnya menggunakan format RGB (Red, Green, Blue). Sehingga kita harus mengubah citra dari format BGR ke RGB agar terjadi konsistensi dan kesesuaian dengan kebanyakan perangkat lunak dan platform.

Setelah citra diolah menjadi format RGB, citra tersebut dibagi menjadi tiga saluran warna: merah, hijau, dan biru. Kemudian, setiap saluran warna ditampilkan sebagai citra grayscale, yang berarti intensitas warna pada setiap piksel diwakili oleh tingkat kecerahan piksel tersebut.

C. Analisis Histogram
Dari citra yang dihasilkan, Anda dapat melihat dampak kontribusi masing-masing saluran warna terhadap gambar asli. Sebagai contoh, jika citra asli memiliki banyak warna merah, saluran warna merah akan menunjukkan detail yang lebih tinggi dibandingkan dengan saluran warna hijau dan biru.

Analisis histogram untuk setiap saluran warna dapat memberikan pemahaman yang lebih rinci tentang distribusi intensitas piksel dalam gambar. Histogram adalah representasi grafis dari distribusi intensitas piksel di seluruh saluran warna. Histogram yang dihasilkan akan menunjukkan seberapa sering intensitas tertentu muncul dalam saluran warna yang bersangkutan.
Berikut Hasil Analisis Histogram tersebut:
Histogram Saluran Warna Merah: Dapat dilihat pada histogram tersebut intensitas piksel sekitar 20-40 dan 140-160 memiliki frekuensi yang tinggi

Histogram Saluran Warna Hijau: Dapat dilihat pada histogram tersebut intensitas piksel sekitar 10-50 dan 145-155 memiliki frekuensi yang tinggi

Histogram Saluran Warna Biru: Dapat dilihat pada histogram tersebut intensitas piksel sekitar 10-30 dan 130-150 memiliki frekuensi yang tinggi

2. Mencari Nilai Ambang Batas untuk Menampilkan Kategori Warna pada Citra
A. Penjelasan Kode Program
Program di atas melakukan beberapa operasi pemrosesan citra pada citra yang dimuat:
Memuat Citra: Program memuat sebuah citra menggunakan cv2.imread() dan menyimpannya dalam variabel img.

Konversi ke Ruang Warna HSV: Citra diubah ke ruang warna HSV (Hue-Saturation-Value) menggunakan cv2.cvtColor() dengan mode konversi cv2.COLOR_BGR2HSV. Ini memungkinkan pemrosesan warna yang lebih mudah dan lebih intuitif daripada dalam ruang warna RGB.

Pemisahan Saluran Warna: Citra HSV dipisahkan menjadi tiga saluran warna yaitu Hue (H), Saturation (S), dan Value (V), yang masing-masing disimpan dalam hue_channel, saturation_channel, dan value_channel.

Pembuatan Citra Biner untuk Warna Tertentu:
Warna Biru: Nilai ambang batas ditentukan untuk saluran Hue untuk mencari warna biru. cv2.threshold() digunakan untuk membuat citra biner yang hanya menyoroti warna biru.
Warna Merah: Nilai ambang batas ditentukan untuk saluran Hue untuk mencari warna merah. Ini juga menggunakan cv2.inRange() untuk membuat citra biner.
Warna Ungu: Citra biner untuk warna biru dan merah digabungkan menggunakan operasi bitwise OR.
Warna Hijau: Nilai ambang batas ditentukan untuk saluran Hue untuk mencari warna hijau. Citra biner untuk warna hijau juga dibuat.
Warna Putih: Citra biner untuk warna ungu dan hijau digabungkan menggunakan operasi bitwise OR.
Menampilkan Hasil: Citra asli dan citra biner untuk setiap warna (biru, merah, ungu, hijau, dan putih) ditampilkan dalam subplot menggunakan matplotlib.pyplot. Setiap subplot menampilkan citra biner dan diberi judul yang sesuai.


B. Nilai Ambang Batas
Nilai Ambang Batas untuk Warna Biru:
Warna biru dalam ruang warna HSV memiliki nilai Hue (H) sekitar 100.
Dalam kasus ini, nilai ambang batas diterapkan pada saluran Hue untuk mendapatkan piksel yang memiliki nilai Hue mendekati nilai biru.
Nilai ambang batas 100 dipilih berdasarkan estimasi nilai Hue dari warna biru pada citra tertentu. Jika warna biru dalam citra memiliki variasi atau pergeseran yang signifikan dalam nilai Hue, nilai ambang batas mungkin perlu disesuaikan.

Nilai Ambang Batas untuk Warna Merah:
Warna merah dalam ruang warna HSV memiliki nilai Hue (H) yang mendekati 0 atau mendekati 180 (karena batasan nilai Hue dari 0 hingga 180 dalam OpenCV).
Nilai ambang batas rendah 0 dan nilai ambang batas tinggi 20 dipilih untuk menangkap variasi dalam nuansa merah. Ini bisa disesuaikan tergantung pada kecerahan atau intensitas warna merah dalam citra.

Nilai Ambang Batas untuk Warna Hijau:
Warna hijau dalam ruang warna HSV memiliki nilai Hue (H) yang mendekati 60.
Nilai ambang batas rendah 40 dan nilai ambang batas tinggi 80 dipilih untuk menangkap variasi dalam nuansa hijau. Kembali, ini bisa disesuaikan berdasarkan kecerahan atau intensitas warna hijau dalam citra.



