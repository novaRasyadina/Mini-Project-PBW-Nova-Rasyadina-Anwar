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
Array gallery berisi semua data karya. id adalah identitas unik tiap karya. type digunakan untuk filter dan harus sesuai dengan key di array filters. cat adalah label kategori yang ditampilkan di overlay dan lightbox. title dan desc adalah judul dan deskripsi karya. tags adalah array chip kecil di lightbox. img adalah nama file gambar yang harus ada di folder project. kemudian pada baris kode "certs" dimana Array certs berisi data sertifikat. type menentukan warna garis atas card melalui class dinamis Vue. title adalah nama sertifikat, issuer adalah penerbit, year adalah tahun, desc adalah deskripsi singkat, dan icon adalah class Bootstrap Icons yang dirender sebagai icon di pojok kiri atas card.

```indeks.HTML
computed: {
        shown() { return this.filter==='all' ? this.gallery : this.gallery.filter(g=>g.type===this.filter); },
        cur()   { return this.shown[this.idx] || null; }
    },
```
computed adalah properti Vue yang dihitung ulang otomatis setiap kali data yang digunakan berubah. shown() menyaring array gallery berdasarkan nilai filter yang aktif. Jika filter 'all' maka tampilkan semua, jika tidak maka filter berdasarkan type. cur() mengembalikan objek gambar yang sedang aktif di lightbox berdasarkan idx, atau null jika tidak ada.

```indeks.HTML
methods: {
        open(i) { this.idx=i; this.lb=true;  document.body.style.overflow='hidden'; },
        close()  { this.lb=false;            document.body.style.overflow=''; },
        next()   { this.idx=(this.idx+1) % this.shown.length; },
        prev()   { this.idx=(this.idx-1+this.shown.length) % this.shown.length; },
    },
```
methods berisi semua fungsi yang bisa dipanggil dari HTML maupun JavaScript. open(i) membuka lightbox dengan mengubah lb menjadi true dan menyimpan index gambar yang diklik, lalu mengunci scroll halaman agar tidak bisa scroll saat lightbox terbuka. close() menutup lightbox dan mengaktifkan kembali scroll halaman. next() berpindah ke gambar berikutnya menggunakan operator modulo % agar setelah gambar terakhir kembali ke gambar pertama. prev() berpindah ke gambar sebelumnya, ditambah this.shown.length sebelum modulo agar tidak bernilai negatif.

```indeks.HTML
mounted() {
        window.addEventListener('scroll', () =>
        document.getElementById('nav').classList.toggle('scrolled', scrollY > 50));
        document.addEventListener('keydown', e => {
        if (!this.lb) return;
        if (e.key==='ArrowRight') this.next();
        if (e.key==='ArrowLeft')  this.prev();
        if (e.key==='Escape')     this.close();
        });
```
mounted() adalah lifecycle hook Vue yang dijalankan otomatis satu kali saat halaman selesai dimuat. Kode ini menambahkan event listener scroll pada window. Setiap kali halaman di-scroll, classList.toggle('scrolled', scrollY > 50) akan menambah class scrolled ke navbar jika posisi scroll lebih dari 50px, dan menghapusnya jika kurang dari 50px. Kemudian adapun Event listener keyboard ini aktif di seluruh halaman. if (!this.lb) return memastikan fungsi hanya berjalan saat lightbox sedang terbuka. Jika lightbox terbuka, tombol ArrowRight memanggil next(), ArrowLeft memanggil prev(), dan Escape memanggil close() untuk menutup lightbox.

```indeks.HTML
const aboutEl = document.getElementById('about');
        new IntersectionObserver(([entry]) => {
        if (entry.isIntersecting)
            aboutEl.querySelectorAll('.skill-bar').forEach(b =>
            (b.style.width = b.getAttribute('aria-valuenow') + '%'));
        }, { threshold: 0.2 }).observe(aboutEl);
    }
```
IntersectionObserver merupakan API browser untuk mendeteksi saat suatu elemen masuk ke area tampilan layar. Di sini digunakan untuk mengamati section About. threshold: 0.2 artinya callback dijalankan saat 20% dari section About terlihat di layar. Saat terlihat, semua elemen .skill-bar dicari lalu lebar masing-masing diubah ke nilai aria-valuenow yang sudah disimpan dari data Vue, sehingga progress bar beranimasi dari 0% ke nilai sebenarnya.

```indeks.HTML
 }).mount('#app');
    </script>
    </body>
    </html>
```
.mount('#app') adalah perintah terakhir yang menghubungkan seluruh aplikasi Vue ke elemen HTML dengan id="app". Semua fitur Vue seperti v-for, {{ }}, @click, dan lainnya hanya aktif di dalam elemen tersebut.

### CSS
#### WarnA dan Riset
```style.CSS
:root {
    --cream:    #faf6f0;
    --warm:     #f3ece0;
    --border:   rgba(124,92,62,.15);
    --rose:     #c4796b;
    --brown:    #7c5c3e;
    --brown2:   #a07850;
    --dark:     #2d2018;
    --mid:      #5a3e28;
    --light:    #9a7e68;
    --shadow:   rgba(45,32,24,.12);
    --r:        14px;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }
    body { background: var(--cream); color: var(--dark); font-family: 'Inter', sans-serif; font-weight: 300; line-height: 1.7; overflow-x: hidden; }
    ::-webkit-scrollbar { width: 5px; }
    ::-webkit-scrollbar-thumb { background: var(--brown2); border-radius: 4px; }
```
kode :root adalah selector khusus CSS untuk menyimpan variabel global yang bisa dipakai di seluruh file CSS. Variabel dipanggil menggunakan var(--nama). semua warna menggunakan palet coklat hangat dan krem agar tampilan terasa elegan dan natural. --r adalah variabel untuk border-radius yang dipakai berulang di berbagai elemen. Selanjutnya ada barisan kode box-sizing: border-box membuat padding dan border dihitung di dalam ukuran elemen, bukan di luar. margin: 0; padding: 0 menghapus jarak bawaan browser. scroll-behavior: smooth membuat scroll antar section terasa halus. overflow-x: hidden mencegah scroll horizontal. Scrollbar dikustomisasi menjadi tipis 5px berwarna coklat.
```style.CSS
h1, h2, h3, h4, h5 { font-family: 'Playfair Display', serif; }
    em { font-style: italic; color: var(--rose); }
    strong { color: var(--dark); font-weight: 600; }
    .text-rose  { color: var(--rose); }
    .text-mid   { color: var(--mid); }
    .text-dark  { color: var(--dark); }
    .fw-500     { font-weight: 500; }
```

Semua heading menggunakan font Playfair Display yang berkesan elegan dan artistik. Tag em diberi warna rose agar teks italic terlihat menonjol seperti pada judul section "Tentang Saya". Utility class warna memudahkan pemberian warna teks tanpa menulis CSS baru setiap saat.

```style.CSS
#nav {
    padding: 1.1rem 0;
    background: rgba(200, 185, 162, 0.92);
    transition: all .35s;
    }
    #nav.scrolled {
    padding: .7rem 0;
    background: rgba(200, 185, 162, 0.92);
    backdrop-filter: blur(5px);
    box-shadow: 0 2px 20px var(--shadow);
    border-bottom: 1px solid var(--border);
    }
    .navbar-brand {
    font-family: 'Playfair Display', serif;
    font-size: 1.5rem;
    font-weight: 700;
    color: var(--dark) !important;
    text-decoration: none;
    }
    .nav-link {
    font-size: .82rem;
    font-weight: 500;
    text-transform: uppercase;
    letter-spacing: 1.5px;
    color: var(--mid) !important;
    padding: 7px 14px !important;
    border-radius: 100px;
    text-decoration: none;
    transition: all .2s;
    }
    .nav-link:hover { background: var(--warm); color: var(--brown) !important; }
```
Navbar awalnya memiliki padding besar dan background semi-transparan krem coklat. Saat di-scroll, JavaScript menambah class .scrolled yang memicu CSS mengecilkan padding dan menambahkan efek blur di belakang navbar sehingga terlihat seperti kaca (glassmorphism). transition: all .35s membuat perubahan ini terasa halus. Link navbar dibuat uppercase dengan letter-spacing besar agar terlihat rapi dan elegan. Hover mendapat background hangat dengan border-radius bulat.

```style.CSS
 .btn-rose {
    background: var(--brown);
    color: var(--cream);
    padding: 11px 26px;
    border-radius: 100px;
    text-decoration: none;
    font-size: .85rem;
    font-weight: 500;
    transition: all .3s;
    box-shadow: 0 4px 16px rgba(124,92,62,.25);
    }
    .btn-rose:hover { background: var(--rose); transform: translateY(-2px); box-shadow: 0 8px 24px rgba(196,121,107,.35); color: #fff; }

    .btn-ghost {
    color: var(--mid);
    padding: 11px 26px;
    border-radius: 100px;
    border: 1.5px solid var(--border);
    text-decoration: none;
    font-size: .85rem;
    font-weight: 500;
    transition: all .3s;
    }
    .btn-ghost:hover { background: var(--warm); border-color: var(--brown2); color: var(--brown); transform: translateY(-2px); }
```
.btn-rose adalah tombol solid berwarna coklat, saat hover berubah menjadi rose dan naik 2px ke atas dengan translateY(-2px) serta bayangan membesar. .btn-ghost adalah tombol transparan hanya dengan border tipis, saat hover mendapat background hangat. Keduanya menggunakan border-radius: 100px agar berbentuk pill/pil yang modern.

```style.CSS
.chip {
    background: var(--warm);
    border: 1px solid var(--border);
    color: var(--mid);
    padding: 5px 13px;
    border-radius: 100px;
    font-size: .78rem;
    font-weight: 400;
    display: inline-block;
    }
    .chip.small { font-size: .68rem; padding: 3px 10px; }
    .chip-btn {
    background: var(--cream);
    border: 1.5px solid var(--border);
    color: var(--light);
    padding: 7px 18px;
    border-radius: 100px;
    font-size: .78rem;
    font-weight: 500;
    cursor: pointer;
    transition: all .2s;
    }
    .chip-btn:hover { border-color: var(--brown2); color: var(--brown); }
    .chip-btn.active { background: var(--brown); border-color: var(--brown); color: var(--cream); }
```
.chip adalah label kecil berbentuk pil untuk tags dan kategori. .chip.small adalah versi lebih kecil untuk badge di card sertifikat. .chip-btn adalah chip yang bisa diklik sebagai tombol filter galeri, bedanya dari .chip adalah ada cursor: pointer dan efek hover. Saat filter aktif, Vue menambah class .active yang mengubah chip menjadi coklat solid dengan teks krem.

```style.CSS
    .section { padding: 100px 0; }
    .bg-warm  { background: var(--warm); }
    .sec-label {
    display: inline-block;
    font-size: .7rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 3px;
    color: var(--brown2);
    margin-bottom: 10px;
    }
    .sec-title {
    font-size: clamp(2rem, 5vw, 3rem);
    font-weight: 700;
    letter-spacing: -1px;
    color: var(--dark);
    }
```
Setiap section diberi padding: 100px 0 agar konten tidak terlalu rapat antar section. .bg-warm memberi background krem hangat untuk section Galeri. .sec-label adalah label kecil di atas judul seperti "01 — About" yang dibuat sangat kecil, uppercase, dan letter-spacing besar agar terkesan premium. clamp(2rem, 5vw, 3rem) pada .sec-title membuat ukuran judul responsif otomatis, minimum 2rem di HP dan maksimum 3rem di desktop.

```style.CSS
  .hero {
    min-height: 100vh;
    background: #fdfaf5;
    padding-top: 90px;
    }
    .hero-name {
    font-size: clamp(3.5rem, 9vw, 6.5rem);
    font-weight: 700;
    line-height: .95;
    letter-spacing: -3px;
    color: var(--dark);
    }
    .hero-sub { font-size: .95rem; color: var(--light); line-height: 1.8; }

    .hero-photo-wrap { position: relative; display: inline-block; }
    .hero-photo {
    width: 320px;
    height: 400px;
    object-fit: cover;
    object-position: top;
    border-radius: 24px 24px 80px 24px;
    box-shadow: 0 24px 60px var(--shadow);
    transition: transform .4s;
    }
    .hero-photo:hover { transform: scale(1.02); }
    .hero-badge {
    position: absolute;
    bottom: -12px; left: 20px;
    background: rgba(250,246,240,.95);
    border: 1px solid var(--border);
    backdrop-filter: blur(8px);
    padding: 6px 14px;
    border-radius: 100px;
    font-size: .75rem;
    color: var(--mid);
    box-shadow: 0 4px 14px var(--shadow);
    }
```
min-height: 100vh memastikan hero memenuhi seluruh tinggi layar. padding-top: 90px memberi ruang agar konten tidak tertutup navbar. Nama menggunakan clamp() agar responsif di semua ukuran layar. line-height: .95 membuat baris nama sangat rapat sehingga terlihat besar dan dramatis. Foto menggunakan border-radius: 24px 24px 80px 24px yang membuat hanya pojok kanan bawah melengkung sangat besar, menciptakan bentuk unik. Badge lokasi menggunakan position: absolute dengan bottom: -12px agar menggantung sedikit di bawah foto.

```style.CSS
 .info-card {
    background: #fff;
    border: 1px solid var(--border);
    border-radius: var(--r);
    padding: 16px 20px;
    box-shadow: 0 4px 18px var(--shadow);
    }
    .info-row {
    display: flex;
    justify-content: space-between;
    padding: 8px 0;
    border-bottom: 1px solid var(--border);
    font-size: .82rem;
    }
    .info-row:last-child { border: none; }
    .info-label { color: var(--light); font-size: .72rem; text-transform: uppercase; letter-spacing: .5px; }
    .info-val   { color: var(--dark);  font-weight: 500; text-align: right; }

    .bio { font-size: .93rem; color: var(--mid); line-height: 1.9; text-align: justify; }
    .block-title { font-size: .85rem; text-transform: uppercase; letter-spacing: 1.5px; color: var(--light); font-family: 'Inter', sans-serif; font-weight: 600; }

    .skill-bar {
    background: linear-gradient(90deg, var(--rose), var(--brown2));
    border-radius: 10px;
    width: 0;
    transition: width 1.2s cubic-bezier(.22,1,.36,1);
    }

    .exp-item {
    background: #fff;
    border: 1px solid var(--border);
    border-radius: var(--r);
    padding: 14px 18px;
    margin-bottom: 12px;
    transition: border-color .3s;
    }
    .exp-item:hover { border-color: rgba(196,121,107,.35); }
```
Info card menggunakan display: flex dengan justify-content: space-between agar label di kiri dan nilai di kanan secara otomatis. :last-child menghapus border bawah pada baris terakhir. .bio menggunakan text-align: justify agar teks rata kiri kanan. Skill bar dimulai dari width: 0 lalu dianimasikan ke lebar sebenarnya oleh JavaScript, cubic-bezier(.22,1,.36,1) membuat gerakan terasa natural seperti melambat di akhir. Card pengalaman saat hover menampilkan border rose tipis.

```style.CSS
   .masonry {
    columns: 3;
    column-gap: 16px;
    }
    @media (max-width: 900px) { .masonry { columns: 2; } }
    @media (max-width: 540px) { .masonry { columns: 1; } }

    .m-item {
    break-inside: avoid;
    margin-bottom: 16px;
    border-radius: var(--r);
    overflow: hidden;
    cursor: pointer;
    position: relative;
    box-shadow: 0 4px 18px var(--shadow);
    transition: transform .35s, box-shadow .35s;
    }
    .m-item:hover { transform: translateY(-5px); box-shadow: 0 16px 40px rgba(45,32,24,.18); }
    .m-item img { width: 100%; display: block; transition: transform .5s; }
    .m-item:hover img { transform: scale(1.04); }

    .m-hover {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(45,32,24,.75) 0%, transparent 55%);
    border-radius: var(--r);
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    padding: 14px;
    opacity: 0;
    transition: opacity .3s;
    }
    .m-item:hover .m-hover { opacity: 1; }
```
Layout masonry menggunakan CSS columns: 3 bukan grid, sehingga gambar dengan tinggi berbeda-beda otomatis tersusun rapi tanpa celah seperti Pinterest. break-inside: avoid mencegah satu card terpotong ke kolom berikutnya. Media query mengubah jumlah kolom menjadi 2 di tablet dan 1 di HP. Saat hover card naik dan bayangan membesar, gambar sedikit zoom dengan scale(1.04). Overlay gelap gradient muncul dari bawah ke atas saat hover menggunakan perubahan opacity dari 0 ke 1.


```style.CSS
   .cert-card {
    background: var(--cream);
    border: 1.5px solid var(--border);
    border-radius: var(--r);
    padding: 22px;
    height: 100%;
    display: flex;
    flex-direction: column;
    transition: all .3s;
    box-shadow: 0 3px 16px var(--shadow);
    position: relative;
    overflow: hidden;
    }
    .cert-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 3px;
    }
    .cert-card:hover { transform: translateY(-5px); box-shadow: 0 16px 40px rgba(45,32,24,.16); }

    .ct-ui\/ux::before,
    .ct-uiux::before     { background: linear-gradient(90deg, var(--rose), #b07db0); }
    .ct-organisasi::before { background: linear-gradient(90deg, #7a9b7e, #aac2ad); }
    .ct-seni::before     { background: linear-gradient(90deg, #c9a84c, var(--rose)); }
    .ct-prestasi::before { background: linear-gradient(90deg, var(--brown2), var(--brown)); }

    .cert-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 14px;
    }
    .cert-icon {
    width: 44px; height: 44px;
    background: var(--warm);
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.2rem;
    color: var(--rose);
    }
    .cert-name {
    font-size: 1rem;
    font-weight: 700;
    color: var(--dark);
    margin-bottom: 8px;
    line-height: 1.35;
    }
    .cert-foot {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: auto;
    padding-top: 12px;
    border-top: 1px solid var(--border);
    }
    .text-rose { color: var(--rose) !important; }
```
Card menggunakan display: flex; flex-direction: column agar .cert-foot selalu berada di paling bawah card meskipun panjang konten berbeda-beda, ini dicapai dengan margin-top: auto pada .cert-foot. garis warna di atas card menggunakan pseudo-element ::before yang diposisikan absolute di atas card dengan tinggi hanya 3px dan warna gradient berbeda tiap tipe sertifikat. overflow: hidden memastikan garis tidak keluar dari area card.

```style.CSS
.footer {
    background: var(--dark);
    padding: 50px 0 30px;
    }
    .footer-name {
    font-family: 'Playfair Display', serif;
    font-size: 2.2rem;
    font-weight: 700;
    color: var(--cream);
    }
    .soc {
    width: 38px; height: 38px;
    border-radius: 50%;
    border: 1px solid rgba(250,246,240,.12);
    background: rgba(250,246,240,.06);
    color: rgba(250,246,240,.55);
    display: inline-flex;
    align-items: center;
    justify-content: center;
    text-decoration: none;
    transition: all .25s;
    }
    .soc:hover { background: var(--rose); border-color: var(--rose); color: #fff; transform: translateY(-2px); }
```
Footer menggunakan background coklat gelap var(--dark). Ikon sosmed berbentuk lingkaran sempurna dengan border-radius: 50%, border dan background sangat transparan agar terkesan subtle di atas background gelap. display: inline-flex dengan align-items dan justify-content: center membuat icon selalu tepat di tengah lingkaran. Saat hover berubah penuh menjadi warna rose dan naik sedikit ke atas.

```style.CSS
    .lb-bg {
    position: fixed; inset: 0;
    background: rgba(20,10,5,.9);
    backdrop-filter: blur(10px);
    z-index: 2000;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 16px;
    opacity: 0;
    pointer-events: none;
    transition: opacity .3s;
    }
    .lb-bg.show { opacity: 1; pointer-events: all; }

    .lb-box {
    background: var(--cream);
    border-radius: 20px;
    width: 100%;
    max-width: 860px;
    max-height: 90vh;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    transform: scale(.94);
    transition: transform .35s cubic-bezier(.22,1,.36,1);
    box-shadow: 0 32px 80px rgba(0,0,0,.5);
    position: relative;
    }
    .lb-box.show { transform: scale(1); }

    .lb-img { width: 100%; max-height: 50vh; object-fit: cover; display: block; animation: fadeIn .3s ease; }
    @keyframes fadeIn { from { opacity: 0; transform: scale(.98); } to { opacity: 1; transform: none; } }

    .lb-close, .lb-prev, .lb-next {
    position: absolute;
    z-index: 5;
    background: var(--cream);
    border: 1.5px solid var(--border);
    border-radius: 50%;
    width: 38px; height: 38px;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer;
    font-size: .9rem;
    color: var(--mid);
    transition: all .2s;
    }
    .lb-close { top: 12px; right: 12px; }
    .lb-prev  { top: 45%; left: 10px; transform: translateY(-50%); }
    .lb-next  { top: 45%; right: 10px; transform: translateY(-50%); }
    .lb-close:hover, .lb-prev:hover, .lb-next:hover { background: var(--rose); color: #fff; border-color: var(--rose); }

    .lb-info { padding: 14px 18px 10px; }

    .lb-thumbs {
    display: flex;
    gap: 7px;
    padding: 10px 18px 14px;
    overflow-x: auto;
    border-top: 1px solid var(--border);
    background: var(--warm);
    }
    .lb-thumbs::-webkit-scrollbar { height: 3px; }
    .lb-thumbs::-webkit-scrollbar-thumb { background: var(--brown2); }

    .lb-thumb {
    width: 50px; height: 50px;
    object-fit: cover;
    border-radius: 8px;
    cursor: pointer;
    opacity: .5;
    border: 2px solid transparent;
    flex-shrink: 0;
    transition: all .2s;
    }
    .lb-thumb:hover { opacity: .8; }
    .lb-thumb.active { opacity: 1; border-color: var(--rose); transform: scale(1.08); }
```
Lightbox menggunakan position: fixed; inset: 0 agar menutupi seluruh layar di atas semua elemen lain dengan z-index: 2000. Awalnya opacity: 0 dan pointer-events: none agar tidak terlihat dan tidak bisa diklik. Saat aktif class .show mengubah keduanya. backdrop-filter: blur(10px) mengaburkan konten di belakang overlay. Box muncul dengan animasi scale dari 0.94 ke 1 dengan cubic-bezier yang terasa elastis. Setiap gambar baru dianimasikan dengan @keyframes fadeIn. Thumbnail aktif diberi border rose dan diperbesar dengan scale(1.08).

```style.CSS
 @media (max-width: 768px) {
    .section { padding: 70px 0; }
    .hero-photo { width: 240px; height: 300px; }
    .hero-name { letter-spacing: -2px; }
    }
```
kode di atas yaitu Media ini aktif saat lebar layar di bawah 768px yaitu ukuran HP. Padding section dikurangi dari 100px menjadi 70px agar tidak boros ruang di layar kecil. Foto hero diperkecil dari 320x400px menjadi 240x300px. Letter-spacing nama dikurangi dari -3px menjadi -2px karena di layar kecil teks besar dengan spasi terlalu lebar bisa keluar dari layar.

## Dokumentasi Tampilan Setiap Section dan Fitur
