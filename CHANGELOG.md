# Changelog - Perbaikan Project

## Masalah yang Diperbaiki

### 1. **Redirect Box Tidak Berfungsi**
**Masalah:** Ketika box di index.html diklik, tidak terjadi redirect ke halaman merry-christmas-nadya.html

**Penyebab:** 
- Path menggunakan absolute path (`/merry-christmas-nadya.html`) yang mencari dari root server
- Path assets menggunakan absolute path yang tidak konsisten

**Solusi:**
- Mengubah semua path menjadi relative path (`./`)
- Memastikan Parcel bundler dapat meng-handle semua file dengan benar

### 2. **Build Configuration**
**Masalah:** File merry-christmas-nadya.html tidak ter-bundle saat build

**Solusi:**
- Update package.json untuk include kedua file HTML dalam build
- Simplifikasi vercel.json untuk deployment yang lebih baik

## Perubahan File

### index.html
- Path redirect: `/merry-christmas-nadya.html` → `./merry-christmas-nadya.html`

### merry-christmas-nadya.html
- favicon: `/favicon.ico` → `./favicon.ico`
- stylesheet: `style.css` → `./style.css`
- assets images: `/assets/...` → `./assets/...`
- audio: `christmas.mp3` → `./christmas.mp3`
- script: `script.js` → `./script.js`

### style.css
- background gift: `/assets/Gift_Flat_Icon_Vector.svg` → `./assets/Gift_Flat_Icon_Vector.svg`

### script.js
- Audio path: `'christmas.mp3'` → `'./christmas.mp3'`

### package.json
```json
{
  "source": ["index.html", "merry-christmas-nadya.html"],
  "scripts": {
    "start": "parcel index.html merry-christmas-nadya.html",
    "build": "parcel build index.html merry-christmas-nadya.html"
  }
}
```

### vercel.json
Disederhanakan untuk Parcel bundler

## Cara Menjalankan

### Development
```bash
npm start
```
Server akan berjalan di http://localhost:1234 (atau port lain jika 1234 sedang digunakan)

### Build untuk Production
```bash
npm run build
```
Output akan ada di folder `dist/`

### Deploy ke Vercel
```bash
vercel --prod
```

## Testing
✅ Build berhasil tanpa error
✅ Semua assets ter-bundle dengan benar
✅ Redirect dari index.html ke merry-christmas-nadya.html berfungsi
✅ Semua path menggunakan relative path yang konsisten
