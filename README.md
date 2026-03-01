# Mini Project Pemrograman Berbasis Web
## Teknologi yang digunakan dalam membangun halaman portofolio meliputi:
1) HTML untuk membuat struktur halaman web. pada project ini dihunakan struktur dasar HTML yaitu  !DOCTYPE html, html, head, dan body. HTML digunakan untuk membuat kerangka semua section seperti navbar, hero, about, galeri, sertifikat, footer, dan lightbox.
2) CSS, digunakan untuk mengatur tampilan visual seluruh halaman. pada project ini CSS digunakan untuk membuat variabel warna dengan :root, layout masonry dengan columns, animasi dengan transition dan @keyframes, efek hover, pseudo-element :before untuk garis warna card sertifikat, glassmorphism navbar dengan backdrop-filter: blur, dan responsive design dengan @media query.
3) Bootstrap 5, merupakan framework CSS yang membantu proses layouting dan styling secara cepat. pada project portofolio ini bootstrap 5 digunakan untuik:
   * Navbar, dimana digunakan navbar, navbar-expand-lg, navbar-toggler, navbar-collapse
   * Grid System yaitu container, row, col-lg-4, col-lg-7, col-md-6 untuk layout responsif
   * Utilities yaitu d-flex, gap-2, flex-wrap, justify-content-center, text-center, mb-1, mt-4.
   * Progress Bar antara lain progress, progress-bar untuk skill bar di section About.
   * Responsive Breakpoints, layout otomatis menyesuaikan ukuran layar (desktop, tablet, HP).
   kemudian Bootstrap 5 diimpor melalui CDN:
```index.HTML
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"/>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
```
4) Bootstrap Icons, library icon dari Bootstrap yang digunakan untuk menampilkan berbagai icon di seluruh halaman seperti icon hamburger menu, icon zoom galeri, icon building, icon calendar, icon sosial media (Instagram, LinkedIn), icon centang sertifikat, dan lain-lain. Dipakai dengan tag <i class="bi bi-namaicon"></i>.
5) Vue JS, framework JavaScript untuk membuat tampilan web lebih interaktif. Meskipun data di project ini bersifat statis, Vue JS digunakan untuk
6) Google Fonts digunakan untuk mengimport dua jenis font:
   * Playfair Display, font serif elegan untuk heading, judul section, dan nama di navbar serta footer
   * Inter, font sans serif modern dan bersih untuk teks biasa seperti bio, deskripsi, dan label
```index.HTML
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,700;1,400&family=Inter:wght@300;400;500&display=swap" rel="stylesheet"/>
```
7) JavaScript (Vanilla), JavaScript digunakan langsung di dalam tag <script> untuk beberapa fungsi, yaitu:
   * Scroll effect navbar untuk menambah class scrolled saat halaman di-scroll lebih dari 50px
   * Keyboard navigation lightbox → menutup dengan Escape, navigasi dengan tombol panah
   * IntersectionObserver untuk mendeteksi saat section About terlihat di layar lalu menjalankan animasi progress bar skill

## Penjelasan Kode
### HTML:
#### Navbar
```index.HTML
<nav class="navbar navbar-expand-lg fixed-top" id="nav">
        <div class="container">
        <a class="navbar-brand" href="#home">Nova.</a>
        <button class="navbar-toggler border-0" type="button" data-bs-toggle="collapse" data-bs-target="#menu">
            <i class="bi bi-list fs-4"></i>
        </button>
        <div class="collapse navbar-collapse justify-content-end" id="menu">
            <ul class="navbar-nav gap-1">
            <li v-for="n in nav" :key="n.id">
                <a class="nav-link" :href="'#'+n.id">{{ n.label }}</a>
            </li>
            </ul>
        </div>
        </div>
    </nav>
```
Navbar merupakan menu navigasi yang letaknya di atas halaman. fixed-top dari Bootstrap membuat navbar tidak ikut scroll ke bawah. navbar-expand-lg membuat menu tampil horizontal di layar besar dan berubah menjadi tombol hamburger (tombol garis tiga bersusun ke bawah) di HP/mobile. Saat pengguna scroll lebih dari 50px, JavaScript menambahkan class scrolled yang membuat navbar lebih kecil dan menambahkan bayangan. Di CSS, navbar diberi warna krem coklat semi transparan dengan efek blur.
#### Home
```index.HTML
<section id="home" class="hero d-flex align-items-center">
        <div class="container">
        <div class="row align-items-center g-5">
            <div class="col-lg-7">
            <p class="text-rose mb-2">✦ Hi Everyone, saya</p>
            <h1 class="hero-name">Nova<br/><em>Rasyadina</em></h1>
            <p class="hero-sub mt-3">Digital Artist · artist · Undergraduate<br/>
                Mahasiswi Sistem Informasi - Fakultas Teknik - Universitas Mulawarman, Samarinda</p>
            <div class="d-flex gap-2 flex-wrap mt-4">
                <span class="chip" v-for="t in tags" :key="t">{{ t }}</span>
            </div>
            <div class="mt-4 d-flex gap-3 flex-wrap">
                <a href="#galeri" class="btn-rose">Lihat Galeri</a>
                <a href="#about" class="btn-ghost">Tentang Saya</a>
            </div>
            </div>
            <div class="col-lg-5 text-center">
            <div class="hero-photo-wrap">
                <img src="foto2.jpeg"
                    alt="Nova Rasyadina" class="hero-photo"/>
                <div class="hero-badge">📍 Samarinda, Kaltim</div>
            </div>
            </div>
        </div>
        </div>
    </section>
```
section digunakan untuk mengelompokan konten berdasarkan bagiannya. id="Home" digunakan sebagai target link navbar. layout dibagi dua kolom menggunakan Bootstrap grid, col-lg-7 untuk teks di kiri dan col col-lg-5 untuk foto di kanan, keduanya hanya berlaku di layar besar (lg ke atas), di HP otomatis menjadi satu kolom penuh. g-5 adalah gap atau jarak antar kolom. Tag h1 untuk nama utama, em membuat teks miring sekaligus berwarna rose dari CSS. Chip tags dibuat otomatis dengan v-for="t in tags". Dua tombol menggunakan class custom btn-rose dan btn-ghost. Foto menggunakan tag img biasa dengan alt untuk aksesibilitas. Badge lokasi adalah div biasa yang diposisikan absolute di atas foto menggunakan CSS.

#### About Me
```index.HTML
    <section id="about" class="section">
        <div class="container">
        <div class="text-center mb-5">
            <span class="sec-label">01 — About</span>
            <h2 class="sec-title">Tentang <em>Saya</em></h2>
        </div>
        <div class="row g-5 align-items-start">

            <div class="col-lg-4">
            <div class="info-card">
                <div class="info-row" v-for="i in info" :key="i.label">
                <span class="info-label">{{ i.label }}</span>
                <span class="info-val">{{ i.val }}</span>
                </div>
            </div>
            </div>

            <div class="col-lg-8">
            <p class="bio">Saya Nova Rasyadina yang biasa disapa Nova, mahasiswi semester 4 Sistem Informasi Fakultas Teknik
                Universitas Mulawarman. Saya sangat condong di bidang seni, khususnya gambar, lukisan, dan musik. sangat sangat menyukai 
                berkebun dan bermain game untuk mengisi waktu luang.Pernah aktif sebagai pengurus organisasi Inforsa (Information System Association) pada periode 2024-2025. saat ini sedang fokus mengembangkan skill di bidang digital art,
                UI/UX, serta web development, dan tentunya fokus terhadap akademik. saya telah menjual beberapa produk digital di sela waktu luang, diantara nya adalah undangan digital dan open commis digital art.</p>

            <h5 class="block-title mt-4 mb-3">Skills</h5>
            <div class="mb-3" v-for="s in skills" :key="s.name">
                <div class="d-flex justify-content-between mb-1">
                <small class="text-mid">{{ s.name }}</small>
                <small class="text-rose fw-500">{{ s.val }}%</small>
                </div>
                <div class="progress" style="height:6px; background:#ede4d3; border-radius:10px">
                <div class="progress-bar skill-bar" role="progressbar"
                    :style="'width:'+s.val+'%'" :aria-valuenow="s.val"></div>
                </div>
            </div>

            <h5 class="block-title mt-4 mb-3">Hobi</h5>
            <div class="d-flex flex-wrap gap-2">
                <span class="chip" v-for="h in hobbies" :key="h">{{ h }}</span>
            </div>

            <h5 class="block-title mt-4 mb-3">Pengalaman</h5>
            <div class="exp-item" v-for="e in exp" :key="e.role">
                <div class="d-flex justify-content-between flex-wrap gap-1">
                <div>
                    <div class="fw-500 text-dark">{{ e.role }}</div>
                    <small class="text-rose">{{ e.org }}</small>
                </div>
                <small class="text-muted">{{ e.year }}</small>
                </div>
                <p class="small text-muted mt-1 mb-0">{{ e.desc }}</p>
            </div>
            </div>

        </div>
        </div>
    </section>
```
secion dibagi duya kolom, yaitu col-lg-4 untuk info card di kiri dan col-lg-8 untuk konten utama di kanan. Info card menggunakan v-for="i in info" untuk menampilkan data diri secara otomatis, setiap baris berisi label di kiri dan nilai di kanan. Progress bar skill menggunakan komponen Bootstrap progress dan progress-bar, lebar bar diisi dinamis dari data menggunakan :style="'width:'+s.val+'%'", nilai aria-valuenow disimpan untuk dibaca JavaScript saat animasi dijalankan. Hobi ditampilkan sebagai chip badge dengan v-for="h in hobbies". Pengalaman menggunakan v-for="e in exp" yang menampilkan role, organisasi, tahun, dan deskripsi dalam card atau kotak putih.

#### Galeri Karya
```index.HTML
<section id="galeri" class="section bg-warm">
        <div class="container">
        <div class="text-center mb-5">
            <span class="sec-label">02 — Galeri</span>
            <h2 class="sec-title">Galeri <em>Karya</em></h2>
            <p class="text-muted small mt-1">Klik gambar untuk melihat lebih detail ✨</p>
        </div>

        <div class="d-flex flex-wrap justify-content-center gap-2 mb-4">
            <button class="chip-btn" :class="{active: filter===f.key}"
                    @click="filter=f.key" v-for="f in filters" :key="f.key">
            {{ f.emoji }} {{ f.label }}
            </button>
        </div>

        <div class="masonry">
            <div class="m-item" v-for="(g,i) in shown" :key="g.id" @click="open(i)">
            <img :src="g.img" :alt="g.title" loading="lazy"/>
            <div class="m-hover">
                <span class="m-cat">{{ g.cat }}</span>
                <i class="bi bi-zoom-in m-icon"></i>
            </div>
            </div>
        </div>

        <p v-if="shown.length===0" class="text-center text-muted py-5">
        </p>
        </div>
    </section>
```
tombol filter dibuat denggan v-for="f in filters", saat diklik @click="filter=f.key" mengubah nilai filter di Vue, lalu :class="{active: filter===f.key}" otomatis menambah class active pada tombol yang sedang aktif. gambar galeri di tampilkan dari shown yang merupakan computed property Vue hasil penyaringan berdasarkan filter aktif. Setiap item galeri menggunakan @click="open(i)" untuk membuka lightbox. loading="lazy" membuat gambar hanya dimuat saat akan terlihat di layar sehingga halaman lebih cepat. Overlay hover .m-hover berisi kategori dan icon zoom yang muncul saat mouse di atas gambar terlihat seperti sedkiti bergerak zoom ketika disentuh kursor dan muncul tandah +.

#### Section Sertificate
```index.HTML
 <section id="sertifikat" class="section">
        <div class="container">
        <div class="text-center mb-5">
            <span class="sec-label">03 — Sertifikat</span>
            <h2 class="sec-title">Sertifikat &amp; <em>Penghargaan</em></h2>
        </div>
        <div class="row g-4">
            <div class="col-md-6 col-lg-4" v-for="c in certs" :key="c.id">
            <div class="cert-card" :class="'ct-'+c.type.toLowerCase()">
                <div class="cert-top">
                <div class="cert-icon"><i :class="c.icon"></i></div>
                <span class="chip small">{{ c.type }}</span>
                </div>
                <h6 class="cert-name">{{ c.title }}</h6>
                <p class="small text-muted mb-1"><i class="bi bi-building me-1"></i>{{ c.issuer }}</p>
                <p class="small text-muted mb-2"><i class="bi bi-calendar3 me-1"></i>{{ c.year }}</p>
                <p class="small text-muted mb-3">{{ c.desc }}</p>
                <div class="cert-foot">
                <span class="small text-success"><i class="bi bi-patch-check-fill me-1">

                </i>Resmi</span >
                </div>
            </div>
            </div>
        </div>
        </div>
    </section>
```
Card sertifikat dibuat otomatis dengan v-for="c in certs" dari array data certs. Layout menggunakan Bootstrap grid col-md-6 col-lg-4 sehingga tampil 3 kolom di desktop, 2 kolom di tablet, dan 1 kolom di HP. Class warna card ditentukan dengan :class="'ct '+c.type.toLowerCase()" yang menghasilkan class seperti ct-uiux, ct-organisasi, ct-seni, ct-prestasi. Icon menggunakan Bootstrap Icons yang dirender dari data dengan :class="c.icon". &amp; adalah karakter HTML untuk menampilkan simbol &. .cert-foot selalu berada di bawah card berkat margin-top: auto di bagian CSS nya.

#### Section Footer/Paling bawah halaman portofolio
```index.HTML
 <footer class="footer">
        <div class="container text-center">
        <div class="footer-name mb-1">Nova.</div>
        <p class="small text-muted mb-3">🌸</p>
        <div class="d-flex justify-content-center gap-3 mb-3">
            <a href="https://www.instagram.com/nva_ras/" class="soc"><i class="bi bi-instagram"></i></a>
            <a href="https://www.linkedin.com/in/nova-rasyadina-anwar-8a88bb323/" class="soc"><i class="bi bi-linkedin"></i></a>
        </div>
        <small class="text-muted">© 2024 Nova Rasyadina</small>
        </div>
    </footer>
```
tag "footer" adalah elemen HTML untuk bagian bawah halaman yang berisi nama, emoji, dua link sosial media yang langsung mengarah ke instragram dan linkedin menggunakan href yang berisi URL lengkap, dan teks copyright. Icon sosmed menggunakan Bootstrap Icons bi-instagram dan bi-linkedin.

#### Overlay yang muncul/Lightbox
```index.HTML
 <div class="lb-bg" :class="{show:lb}" @click.self="close">
        <div class="lb-box" :class="{show:lb}" v-if="lb && cur">
        <button class="lb-close" @click="close"><i class="bi bi-x-lg"></i></button>
        <button class="lb-prev"  @click="prev"><i class="bi bi-chevron-left"></i></button>
        <button class="lb-next"  @click="next"><i class="bi bi-chevron-right"></i></button>
        <img :src="cur.img" :alt="cur.title" class="lb-img" :key="cur.id"/>
        <div class="lb-info">
            <div class="d-flex justify-content-between align-items-center mb-1">
            <span class="chip small">{{ cur.cat }}</span>
            <small class="text-muted">{{ idx+1 }} / {{ shown.length }}</small>
            </div>
            <div class="fw-500">{{ cur.title }}</div>
            <small class="text-muted d-block mt-1">{{ cur.desc }}</small>
            <div class="d-flex gap-1 flex-wrap mt-2">
            <span class="chip small" v-for="t in cur.tags" :key="t">{{ t }}</span>
            </div>
        </div>
        <div class="lb-thumbs">
            <img v-for="(g,i) in shown" :key="g.id" :src="g.img"
                :class="{active:i===idx}" @click="idx=i" class="lb-thumb"/>
        </div>
        </div>
    </div>
```
Lightbox adalah overlay yang muncul saat gambar galeri diklik. :class="{show:lb}" menambah class show saat lb bernilai true di Vue. @click.self="close" menutup lightbox hanya saat klik area background, bukan saat klik konten di dalamnya (.self memastikan event hanya dari elemen itu sendiri). v-if="lb && cur" memastikan konten lightbox hanya dirender saat lightbox aktif dan ada gambar yang dipilih. :key="cur.id" pada <img> memaksa Vue me-render ulang gambar setiap kali gambar berganti sehingga animasi fadeIn berjalan setiap pergantian. idx+1 / shown.length menampilkan posisi gambar saat ini dari total gambar. Thumbnail strip di bawah menampilkan semua gambar, klik thumbnail mengubah idx sehingga gambar utama berganti.

#### Vue JS & JavaScript
```indeks.HTML
  </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <script>
    Vue.createApp({
    data: () => ({
        lb: false, idx: 0, filter: 'all',
```
Vue.createApp() adalah cara membuat aplikasi Vue JS 3. data() adalah fungsi yang mengembalikan semua data reaktif yang digunakan di seluruh halaman. lb adalah boolean untuk status lightbox (true = terbuka, false = tertutup). idx adalah index gambar yang sedang aktif di lightbox. filter menyimpan kategori filter galeri yang aktif, defaultnya 'all' untuk menampilkan semua gambar.
```indeks.HTML
       nav: [
        { id:'home',       label:'Home' },
        { id:'about',      label:'About' },
        { id:'galeri',     label:'Galeri' },
        { id:'sertifikat', label:'Sertifikat' },
        ],

        tags: ['🎨 Digital Art/artist', '🖥️ IT Student', '🎵 Music', '✂️ DIY'],
```
Array nav berisi data link navbar. Setiap objek punya id sebagai target anchor link (home, about, dll) dan label sebagai teks yang ditampilkan. Data ini dirender di HTML menggunakan v-for="n in nav". kemudian Array tags berisi chip/badge yang ditampilkan di hero section. Cukup tambah atau hapus item di array ini untuk mengubah chip yang tampil tanpa perlu menyentuh HTML.

```indeks.HTML
   info: [
        { label:'Nama',        val:'Nova Rasyadina Anwar' },
        { label:'Tempat Lahir', val:'Balikpapan' },
        { label:'Universitas', val:'Universitas Mulawarman Samarinda' },
        { label:'Prodi',       val:'Sistem Informasi' },
        { label:'Semester',    val:'4 (Aktif)' },
        { label:'Organisasi',  val:'Inforsa 2024-2025' },
        ],

        skills: [
        { name:'Digital Art & Ilustrasi', val:85 },
        { name:'UI/UX Design (Figma)',    val:80 },
        { name:'Seni Lukis & Gambar',     val:98 },
        { name:'HTML & CSS',              val:50 },
        { name:'Vokal & Gitar',           val:95 },
        { name:'Game',             val:70 },
        { name:'Gardening',      val:90 },
        ],

        hobbies: ['✏️ Menggambar','🎨 Melukis','✂️ DIY','🎤 Bernyanyi','🎸 Gitar','🎮 Game', '🥬 Gardenig'],
```
Array skills berisi skill yang dimiliki beserta persentasenya. name adalah nama skill yang ditampilkan sebagai label, val adalah angka 0-100 yang menentukan lebar progres bar. nilai ini juga disimpan di aria-valuenow untuk dibaca oleh javascript saat animasi dijalankan. kemudian ada Array hobbies dimana berisi dafar hobu yang ditampilkan sebagai chip badge di section about. setiap item ya langsung berupa string teks beserta emot.

```indeks.HTML
 exp: [
        { role:'Anggota Organisasi', org:'Inforsa, Unmul', year:'2024-2025',
            desc:'Pernah Aktif sebagai pengurus/anggota, MC & Panitia Kegiatan Proker Bureau EDEN Akseleraasi Karir(AKSA).' },
        { role:'Kepanitiaan Makrab', org:'Makrab Sistem Informasi Unmul', year:'2024',
            desc:'Menjadi panitian di bagian keamanan.' },
        { role:'Digital Artist', org:'Freelance / Personal', year:'2024–Sekarang',
            desc:'Mengerjakan digital art, open commis character, Undangan Digital.' },
        ],

        filters: [
        { key:'all',     label:'Semua',          emoji:'✨' },
        { key:'digital', label:'Digital Art',    emoji:'🎨' },
        { key:'uiux',    label:'UI/UX',          emoji:'🖥️' },
        { key:'lukis',   label:'Lukis & Gambar', emoji:'🖌️' },
        { key:'diy',     label:'DIY & Craft',    emoji:'✂️' },
        { key:'musik',   label:'Musik',          emoji:'🎵' },
        ],
```
kode di atas dalaha Array exp yang berisi data pengalaman saya. setiap objek memiliki role (jabatan), org(nama organisasi/tempat), year (tahun), dan desc (deskripsi singkat). Dirender otomatis menjadi card pengalaman di section About. selanjutnya terdapat kode Array filters yang berisi data tombol filter galeri yang sudah dijelaskan sebelumnya mengenai galeri. key adalah nilai yang disimpan ke filter saat tombol diklik dan dicocokkan dengan type di array gallery. label adalah teks tombol dan emoji adalah icon di depan teks.

```indeks.HTML
gallery: [
        { id:1, type:'digital', cat:'Digital Art',    title:'Character Hanwool Phi',      desc:'karakter dari webtoon Study Group.',   tags:['Digital Art'],    img:'gambar_sketsa_nova1.jpeg' },
        { id:2, type:'uiux',    cat:'UI/UX',           title:'Marketing Web Design', desc:'Desain UI Web Marketing.',              tags:['Figma'],      img:'webdesign.jpeg' },
        { id:3, type:'lukis',   cat:'Lukis & Gambar',  title:'Fuji Mountain', desc:'Lukisan gunung fuji bernuansa vintage effect.',                tags:['Painting','Nature'], img:'lukisan.jpeg' },
        { id:4, type:'diy',     cat:'DIY & Craft',     title:'Paper Basket',       desc:'I made this stationery Basket with unused newspaper.',                 tags:['Hand Craft','DIY'],        img:'basket.jpeg' },
        { id:5, type:'digital', cat:'Digital Art',     title:'Cool Boy',    desc:'I drew this when i remember some of my friend from high school.',             tags:['Digital Art'],     img:'gambar_sketsa_nova2.jpeg' },
        { id:6, type:'musik',   cat:'Musik',           title:'Song Cover on BandLab',    desc:'some of my song cover on BandLab.',               tags:['Song Cover','Music'],      img:'musik.jpeg' },
        { id:8, type:'diy',     cat:'DIY & Craft',     title:'Crochet',       desc:'I made some crochet for me and my grandma on this pict.',                    tags:['Crochet','Yarn'],    img:'crochet1.jpeg' },
        { id:9, type:'lukis',   cat:'Lukis & Gambar',  title:'The Lonely Horse',    desc:'Sketsa potret Seekor Kuda Yang Kesepian.',              tags:['Hatching/Crosshatcing','Sketch'],      img:'sketsakuda.jpeg ' },
        ],

        certs: [
        { id:1, type:'UI/UX',     title:'UI/UX Design Study Club',       issuer:'Information System Association',        year:'2024',      desc:'Dasar desain antarmuka, wireframing dan prototyping.',         icon:'bi bi-vector-pen' },
        { id:2, type:'Organisasi',title:'Sertifikat Kepengurusan Inforsa',  issuer:'Inforsa ',           year:'2024-2025', desc:'Dedikasi sebagai pengurus organisasi mahasiswa Inforsa di bidang wirausaha.',      icon:'bi bi-people-fill' },
        { id:3, type:'Seni',      title:'Piagam Penghargaan Murid Berprestasi Dalam Bidang Seni Seni',          issuer:'SMPN 11 Balikpapan',    year:'2019',      desc:'Prestasi dalam bidang seni rupa dan musik.',     icon:'bi bi-trophy-fill' },
        { id:6, type:'Prestasi',  title:'Runner Up Cerdas Cermat PKLH Balikpapan',  issuer:'Dinas Lingkungan Hidup With Bank Kaltim Event',year:'2014',     desc:'Partisipasi cerdas cermat menganai Pendidikan Lingkungan Hidup.',    icon:'bi bi-award-fill',},
        ],
    }),
```
