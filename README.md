# TikTok Performance Analysis 30 Hari (11 Februari 2025 - 13 Februari 2025)

## Analisis Komprehensif Konten untuk Brand Skincare 30 Hari

Proyek ini berisi kumpulan script Python dan notebook Jupyter untuk menganalisis performa konten TikTok brand skincare, dengan fokus pada ekstraksi insight berharga untuk optimasi strategi konten. Dan juga menggunakan AI untuk ekstrak kata penting.

Nantinya kita akan mengimplementasikan AI dan pada project ini saya menggunakan Gemini AI, karena:

Perbandingan Gemini AI vs NLTK dalam Analisis Konten Skincare di TikTok

| **Aspek**                           | **Gemini AI** | **NLTK/Metode Tradisional** |
|--------------------------------------|--------------|----------------------------|
| **Pemahaman Kontekstual**            | Memahami istilah teknis, bahan, dan tren skincare. Mengenali frasa seperti **"skin barrier repair"** sebagai satu konsep utuh. Mampu menginterpretasi bahasa campuran (Indonesia + Inggris). | Mengandalkan frekuensi kata dan TF-IDF. Sulit membedakan makna kata ambigu seperti **"AHA"** (alpha hydroxy acid vs ekspresi). Tidak memahami frasa kompleks, cenderung memecahnya. |
| **Kemampuan Mengidentifikasi Konsep Implisit** | Mengekstrak konsep seperti **"anti-aging"**, meskipun tidak disebutkan eksplisit. Mengenali sinonim seperti **"melembabkan"**, **"hydrating"**, dan **"moisturizing"**. Dapat menyimpulkan hubungan bahan dengan manfaatnya (misal: **"vitamin C"** → **"brightening"**). | Terbatas pada kata eksplisit dalam teks. Tidak mampu melakukan inferensi konsep atau hubungan antar kata. |
| **Penanganan Bahasa Indonesia**      | Memahami slang dan bahasa informal. Mengenali referensi lokal seperti **"kulit kusam"**, **"jerawat batu"**, serta istilah hybrid seperti **"skincare lokal"**. | Dukungan Bahasa Indonesia terbatas. Stopwords tidak lengkap dan stemming kurang akurat. |
| **Hasil untuk Analisis Bisnis**      | Mengekstrak kata kunci yang benar-benar relevan. Dapat mengenali tren baru seperti **"skin cycling"** atau **"skinimalism"**. Mempertimbangkan sentimen dan konteks emosional. | Bias terhadap kata dengan frekuensi tinggi. Sering menghasilkan noise dari kata umum dan sulit mengenali tren baru tanpa pembaruan manual. |
| **Contoh Perbandingan Hasil**        | Mengenali **"tekstur kulit"** sebagai konsep utuh, menambahkan **"skincare malam"** dari konteks **"tiap malam"**, serta mengidentifikasi bahan aktif penting. | Memecah frasa menjadi kata-kata terpisah, menghasilkan banyak kata umum yang kurang bermakna. |
| **Efisiensi dan Skalabilitas**       | Dapat memproses banyak data sekaligus. Konsisten dan adaptif terhadap tren baru tanpa perlu dilatih ulang. | Memerlukan preprocessing intensif (tokenisasi, stemming, stopword removal). Harus diperbarui manual untuk menangkap istilah baru. |

**Kesimpulan**
| **Kriteria**                   | **Gemini AI** | **NLTK/Metode Tradisional** |
|---------------------------------|--------------|----------------------------|
| **Pemahaman Kontekstual**       | ✅ Baik       | ❌ Terbatas                 |
| **Ekstraksi Konsep Implisit**   | ✅ Baik       | ❌ Lemah                     |
| **Dukungan Bahasa Indonesia**   | ✅ Kuat       | ❌ Terbatas                 |
| **Relevansi Bisnis**            | ✅ Tinggi     | ❌ Rendah                   |
| **Adaptabilitas terhadap Tren** | ✅ Adaptif    | ❌ Statis                   |
| **Biaya**                        | ❌ Mahal  | ✅ Gratis  |

Untuk analisis konten skincare di TikTok, **Gemini AI** lebih unggul dalam pemahaman kontekstual, identifikasi konsep implisit, serta relevansi bisnis dibandingkan metode tradisional seperti **NLTK**.

## 📁 Contoh File Hasil Ekstraksi & Analisis dari Gemini AI
Berikut adalah contoh file hasil ekstraksi dan analisis menggunakan Gemini AI dalam project ini:
- **brandskincare_gemini_keywords_final**: Contoh file hasil ekstraksi kata kunci dari deskripsi video menggunakan Gemini AI
- **brandskincare_gemini_post_types_final**: Contoh file hasil klasifikasi jenis konten menggunakan Gemini AI

---

## Business Understanding

### Konteks
Industri skincare lokal Indonesia terus berkembang dengan persaingan ketat di antara merek-merek ternama. Berdasarkan laporan **Tempo** (14 Agustus 2024), **Somethinc, Scarlett Whitening, dan MS Glow Beauty** adalah tiga merek skincare lokal terlaris dengan pencapaian berikut:  

- **Somethinc** (2019) → **Rp53,2 miliar** (peringkat 1)  
- **Scarlett Whitening** → **Rp40,9 miliar** (peringkat 2, April – Juni 2022)  
- **MS Glow** (2013) → **Rp29,4 miliar** (peringkat 3, April – Juni 2022)  

Ketiga brand ini aktif di **TikTok** sebagai strategi pemasaran utama. **TikTok dipilih** karena, meskipun tergolong baru, telah mencapai **70,8% pengguna di Indonesia**, menjadikannya platform ke-4 terbesar setelah **WhatsApp, Instagram, dan Facebook** (sumber: RRI, 23 Desember 2024).  

**Mengapa 30 hari terakhir?** 

Periode **30 hari terakhir** dipilih karena memberikan gambaran terbaru tentang tren engagement dan efektivitas strategi konten masing-masing brand. Dengan data ini, kita dapat mengidentifikasi pola performa terkini, mengetahui perubahan strategi pemasaran, serta melihat dampak dari berbagai kampanye yang baru saja dilakukan.  

Oleh karena itu, analisis ini akan membantu memahami strategi yang paling efektif dalam menarik engagement dan meningkatkan brand awareness di TikTok.

Sumber: 
- [Sumber: RRI - 7 Media Sosial Paling Banyak Digunakan di Indonesia](https://www.rri.co.id/cek-fakta/1209398/7-media-sosial-paling-banyak-digunakan-di-indonesia)  
- [Sumber: Tempo - 10 Merek Skincare Lokal Terlaris di Indonesia](https://www.tempo.co/gaya-hidup/10-merk-skincare-lokal-terlaris-di-indonesia-379732)  

### Problem Statement

Beberapa pertanyaan utama yang ingin dijawab dalam analisis ini:  
1. **Bagaimana performa konten dalam 30 hari terakhir?**  
   - Rata-rata views, likes, comments, shares per hari.  
   - Bagaimana dengan Engagement Rates nya?

2. **Bagaimana perbandingan performa antar brand?**  
   - Brand mana yang paling banyak mendapat views & interaksi dalam sebulan?    

3. **Apa jenis konten dan hashtag yang paling sukses?**  
   - Apakah ada jenis konten (diskon, tutorial, review) yang lebih efektif dalam 30 hari ini?   

Analisis ini bertujuan untuk memberikan **insight actionable** terkait strategi konten TikTok yang dapat diterapkan untuk meningkatkan engagement dan efektivitas pemasaran bagi ketiga brand ini. 

### Tujuan 

Analisis ini bertujuan untuk:  

1. **Mengukur performa konten dalam 30 hari terakhir**  
   - Rata-rata views, likes, comments, shares per hari.  
   - Tren engagement harian/mingguan.  

2. **Membandingkan performa antar brand**  
   - Brand dengan views dan interaksi tertinggi.  

3. **Menemukan konten & hashtag paling efektif**  
   - Jenis konten dengan engagement tertinggi. 

### Pertanyaan Bisnis Utama
- Jenis konten apa yang menghasilkan engagement tertinggi?
- Kata kunci dan tema apa yang paling beresonansi dengan audiens?
- Bagaimana variasi engagement di berbagai kategori konten?
- Strategi konten apa yang dapat memaksimalkan performa di TikTok?

---

## Data Understanding

### Sumber Data
- Video TikTok dari brand skincare populer (Somethinc, MS Glow, Scarlett, dll.)
- Data yang diambil menggunakan scraper TikTok kustom

### Fitur Utama
- **Metrik Engagement**: Views, Likes, Comments, Shares, Total Engagement
- **Data Konten**: Deskripsi video, hashtag, tanggal posting
- **Informasi Video**: URL, durasi, suara

### Proses Pengumpulan Data
Data dikumpulkan menggunakan scraper TikTok berbasis Python yang mengekstrak informasi video, teks deskripsi, dan metrik engagement dari akun brand skincare.

---

## Arsitektur Solusi

### Technology Stack
- **Python**: Bahasa pemrograman utama
- **Pandas & NumPy**: Manipulasi dan analisis data
- **Matplotlib & Seaborn**: Visualisasi data
- **Google Gemini API**: Analisis konten berbasis AI
- **Jupyter Notebook**: Lingkungan pengembangan

### Pendekatan Analisis
1. **Pengumpulan Data**: Scraping video TikTok menggunakan scraper kustom yang saya buat sendiri
2. **Pra-pemrosesan Data**: Membersihkan data teks dan menghitung metrik
3. **Klasifikasi Konten**: Mengkategorikan post ke dalam jenis konten menggunakan AI
4. **Ekstraksi Kata Kunci**: Mengekstrak kata kunci bermakna dari deskripsi
5. **Analisis Engagement**: Menganalisis performa di berbagai jenis konten
6. **Visualisasi**: Membuat visualisasi yang informatif untuk pengambilan keputusan

---

## Fitur Utama

### 1. Analisis Konten Berbasis AI
Kami menggunakan Google Gemini AI untuk:
- Mengklasifikasikan konten ke dalam 4 kategori utama
- Mengekstrak kata kunci bermakna dari deskripsi
- Memberikan pemahaman semantik yang lebih dalam dibandingkan NLP tradisional

### 2. Klasifikasi Jenis Konten
Video diklasifikasikan ke dalam beberapa kategori utama seperti:
- **Produk Baru**: Peluncuran produk, produk baru, ulasan
- **Promo & Diskon**: Diskon, voucher, giveaway
- **Tutorial & Tips**: Video how-to, rutinitas skincare, panduan aplikasi
- **Event & Kolaborasi**: Event brand, kolaborasi dengan influencer

### 3. Analisis Engagement Lanjutan
- Perbandingan metrik engagement di berbagai jenis konten
- Perhitungan engagement rate (engagement relatif terhadap views)
- Korelasi kata kunci dengan metrik engagement

### 4. Insight Visual
- Wordcloud untuk kata kunci paling sering muncul
- Chart distribusi untuk jenis konten
- Perbandingan metrik engagement di berbagai kategori

Contoh hasil ekstrak Gemini AI

---

## Manfaat Utama

### 1. Strategi Konten Berbasis Data
- Mendasarkan keputusan konten pada data performa, bukan intuisi
- Mengidentifikasi jenis konten spesifik yang mendorong engagement
- Memahami efektivitas kata kunci untuk konteks brand spesifik

### 2. Optimasi Waktu & Sumber Daya
- Fokuskan upaya pembuatan konten pada kategori dengan performa tinggi
- Optimalkan deskripsi konten menggunakan kata kunci efektif
- Prioritaskan jenis konten dengan engagement rate tertinggi

### 3. Intelijen Kompetitif
- Bandingkan strategi konten antar brand
- Identifikasi kesenjangan dan peluang dalam lanskap konten

---

## Batasan & Pertimbangan

### 1. Batasan Rate API
- Google Gemini API memiliki batasan rate (50 permintaan/hari untuk tier gratis)
- Implementasi caching dan batch processing untuk mengoptimalkan penggunaan
- Pertimbangkan upgrade ke tier berbayar untuk dataset yang lebih besar

### 2. Akurasi Klasifikasi Konten
- Klasifikasi AI mungkin memiliki keterbatasan untuk konten ambigu
- Verifikasi manual direkomendasikan untuk analisis kritis

### 3. Keterbatasan API TikTok
- Tidak ada API TikTok resmi untuk pengumpulan data komprehensif
- Scraper mungkin terpengaruh oleh perubahan platform TikTok
- Beberapa metrik (misal, video completion rate) tidak dapat diakses

---

## Kesimpulan

### Insight Lintas Brand
- Somethinc unggul di semua aspek utama (views, likes, comments, shares, saves), menunjukkan bahwa brand ini paling menarik perhatian audiens TikTok.
- MS Glow berada di posisi tengah dengan engagement rate tertinggi (0.96%), menandakan bahwa meskipun views lebih sedikit dibandingkan Somethinc, kontennya lebih efektif dalam menarik interaksi.
- Scarlett Whitening memiliki performa engagement paling rendah di seluruh metrik, dengan engagement rate hanya 0.15%, jauh di bawah kompetitor. NAMUN MEMILIKI SATU VIDEO YANG VIEWSNYA MENCAPAI HAMPIR 50 JUTA

Engagement rate di bawah 1% untuk semua brand menunjukkan bahwa performa konten mereka masih kurang baik secara keseluruhan, dan strategi interaksi harus diperbaiki agar lebih menarik audiens.

- Scarlett unggul dalam total views dan jumlah postingan, tetapi engagement rate rendah karena hanya beberapa video yang viral.
- Somethinc memiliki engagement dan median views tertinggi, menunjukkan strategi konten yang konsisten dan menarik audiens.
- MS Glow memiliki engagement rate tertinggi meskipun jumlah views lebih sedikit, menandakan kontennya lebih engaging dibanding pesaingnya.

Strategi terbaik adalah menggabungkan konsistensi Somethinc dengan efektivitas engagement MS Glow untuk meningkatkan performa konten TikTok.

### Rekomendasi Strategi Konten
1. Somethinc  (Konsisten & Engagement Baik)
- Tambah 20-30% konten promo & diskon (2-3x/minggu) → Target: Engagement rate 0.89% → 1.2%
- Gunakan 20-30 influencer mikro per bulan → Target: Share rate 1.2% → 2%
- Buat challenge interaktif (ex: "Somethinc Shade Match") → Target: Komentar 120 → 200/video

2. Scarlett Whitening  (Views Tinggi, Engagement Rendah)
- Buat 50% lebih banyak konten berbasis aroma & storytelling → Target: Like rate 0.8% → 1.5%
- Gunakan 5-7 influencer besar per bulan → Target: Engagement rate 0.15% → 0.6%
- Buat 1 video edukasi keaslian produk per minggu → Target: Share rate 0.5% → 1%

3. MS Glow  (Engagement Tertinggi, Butuh Lebih Banyak Views)
- Optimalkan komunitas reseller (Elite Glowbal) dengan video testimonial → Target: Save rate 0.7% → 1.5%
- Tambah 2-3 video tutorial per minggu dengan influencer → Target: Share rate 1.1% → 2%
- Gunakan UGC (User-Generated Content) untuk meningkatkan trust → Target: Engagement rate 0.96% → 1.3%

---

*Readme ini dibuat untuk proyek TikTok Performance Analysis, berfokus pada optimasi konten brand skincare.*

*Hubungi saya untuk file scrapernya: alfadewa58@gmail.com*
