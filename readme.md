# Install TailwindCSS di Android

## Bahan
> - [Termux](https://moneyblink.com/xplljU7Mx7)
> - [Acode Editor]()
> - [Chrome]()
> - [ZArchiver]()

## Buka Aplikasi Termux
- update & upgrade paket
```bash 
pkg update && pkg upgrade
```
- install NodeJs
```bash 
pkg install nodejs
```
- cek apakah NodeJs sudah terinstall
```bash
node -v
```
- cek apakah npm sudah terinstall
```bash
npm -v
```
- install git
```bash
pkg install git
```

## Buat Struktur Direktori Proyek
Contoh:
```bash
-myProjec/
  -public/
    -index.html
    -css/
      -styles.css
    -main/
      -main.js
  -src/
    -routes/
      -router.js
    -css/
      -input.css
    -app.js
```

## Buat Server/Router NodeJs
- install dependensi yang di butuhkan (Express) 
```bash
npm install express body-parser --no-bin-links
```
- isi file src/app.js dengan kode berikut:
```bash 
const express = require('express');
const bodyParser = require('body-parser');
const path = require('path');
const indexRouter = require('./routes/router');

const app = express();

app.use(bodyParser.urlencoded({ extended: true }));
app.use(express.static(path.join(__dirname, '../public')));

app.use('/', indexRouter);

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
    console.log(`Server running on port ${PORT}`);
});
```
- Isi file src/routes/router.js dengan kode berikut: 
```bash
const express = require('express');
const path = require('path');
const router = express.Router();

router.get('/', (req, res) => {
    res.sendFile('index.html', { root: path.join(__dirname, '../../public') });
});

module.exports = router;
```
- isi file public/index.html dengan kode berikut: 
```bash 
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tailwindcss-Android</title>
    <link rel="stylesheet" href="css/styles.css">
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <script src="main/main.js"></script>
   </head>
<body>
    <header class="bg-gray-800 text-white p-4">
        <h1 class="text-2xl">MENGGUNAKAN TAILWINDCSS DI ANDROID</h1>
    </header>
    <main class="p-4">
        <h2 class="text-xl">Contoh menggunakan TailwindCSS pada android</h2>
    </main>
    <footer class="bg-gray-800 text-white p-4 mt-4">
      <p>&copy; Tailwindcss</p>
    </footer>
</body>
</html>
```
- cek apakah server sudah bisa berjalan di localhost
```bash
cd src
```
```bash
node app
```
Jika semua sudah benar, selanjutnya install Tailwindcss

## Install TailwindCSS
- install TailwindCSS versi global
```bash
npm install -g tailwindcss
```
- pastikan tailwindcss terinstall
```bash
tailwindcss
```
- inisialisasi TailwindCSS. Ini akan membuat file tailwind.config.js
```bash
tailwindcss init
```
- pastikan isi file tailwind.config.js seperti berikut: 
```bash
/** @type {import('tailwindcss').Config} */
module.exports = {
    content: [
        "./public/**/*.html",
        "./src/**/*.js",
    ],
    theme: {
        extend: {},
    },
    plugins: [],
}
```
- buat file bernama postcss.config.js di direktori root/utama
- lalu isi file postcss.config.js dengan kode berikut: 
```bash
module.exports = {
plugins: {
    tailwindcss: {},
    autoprefixer: {},
    }
}
```
- isi file src/css/input.css dengan kode berikut: 
```bash
@tailwind base;
@tailwind components;
@tailwind utilities;
```
- kompilasi file input css punya tailwind dari direktori src/css/input.css ke file css utama di public/css/styles.css
```bash
tailwindcss -i src/css/input.css -o public/css/styles.css
```
- tambahkan kode berikut kedalam file package.json di dalam tag <script>. Untuk mempermudah kompilasi
```bash
"compile": "tailwindcss -i src/css/input.css -o public/css/styles.css"
```
- jika ingin kompilasi tinggal ketik kode berikut: 
```bash
npm run compile
```