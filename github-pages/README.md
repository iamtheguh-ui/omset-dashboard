# Dashboard Omset — GitHub Pages

Folder ini siap di-upload ke GitHub Pages. Isinya:

- `index.html` — dashboard statis satu file (HTML + CSS + JS)
- `.nojekyll` — agar GitHub Pages tidak memproses file dengan Jekyll
- `README.md` — panduan ini

Tidak ada backend, tidak ada password, tidak perlu domain sendiri.
Dashboard membaca langsung sheet `SCRAPING` dan `MISI HARIAN` dari browser.

## Cara paling mudah (lewat web GitHub)

1. Buat repository baru di GitHub, misalnya `omset-dashboard`.
   Pilih **Public** (GitHub Pages gratis untuk repo public).
2. Di halaman repo, klik **Add file → Upload files**.
3. Upload `index.html` dan `.nojekyll` dari folder ini.
   (File `.nojekyll` tidak terlihat di Explorer; aktifkan “show hidden files”
   atau upload lewat drag-and-drop folder.)
4. Commit ke branch `main`.
5. Buka **Settings → Pages**.
6. Di **Build and deployment → Source**, pilih **Deploy from a branch**.
7. Branch: `main`, folder: `/ (root)`, lalu **Save**.
8. Tunggu 1–2 menit. URL muncul di halaman Pages, bentuknya:

   ```text
   https://<username>.github.io/omset-dashboard/
   ```

Kalau nama repo-nya `<username>.github.io`, URL-nya:

```text
https://<username>.github.io/
```

## Cara lewat GitHub Desktop

1. Buka GitHub Desktop → **File → Add local repository**.
2. Pilih folder `github-pages` ini.
3. Klik **create a repository** / **publish repository**.
4. Setelah ter-push, buka **Settings → Pages** di GitHub dan aktifkan
   branch `main` folder `/ (root)`.

## Cara lewat Git CLI

```bash
cd github-pages
git init
git add .
git commit -m "Dashboard omset statis"
git branch -M main
git remote add origin https://github.com/<username>/<repo>.git
git push -u origin main
```

Lalu aktifkan GitHub Pages di **Settings → Pages**.

## Setelah deploy

Buka URL GitHub Pages, lalu cek:

- KPI Omset, Target, Capaian, DO, dan Customer terisi.
- Badge di kanan atas menunjukkan **LIVE**.
- Kalau muncul **DATA LAMA**, berarti sheet belum diperbarui bot > 25 menit.
- Kalau muncul pesan **Sheet tidak dapat dibaca publik**, ubah sharing sheet
  menjadi **Anyone with the link → Viewer**.

## Kalau ingin mengubah data/config

File `index.html` di folder ini adalah hasil build. Jangan edit langsung.
Edit sumbernya di folder induk:

- `ai_studio/data.js` — ID sheet, nama tab, master salesman, aturan.
- `static/js/app.js` — tampilan/interaksi.
- `static/css/style.css` — CSS.

Lalu jalankan dari folder induk:

```bat
python build_ai_studio.py
```

File `github-pages/index.html` akan ikut diperbarui. Commit dan push lagi.

## Catatan keamanan

- GitHub Pages **publik** dan dashboard **tanpa password**.
- Sheet juga dapat dibaca publik lewat ID sheet yang tertanam di HTML.
- Jangan taruh data customer sensitif di repo/sheet publik.
- Kalau butuh akses terbatas, gunakan versi Flask + password atau proxy
  Google Apps Script; versi statis ini tidak mendukung login.
