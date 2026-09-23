# 📚 Ziyo-Makon — Elektron kutubxona platformasi

Laravel (PHP) backend + React Native mobil ilova. Foydalanuvchi yoshiga (18 yoshgacha /
18–35 / 35+) qarab avtomatik o'zgaruvchi interfeys, email va xavfsiz parol orqali kirish,
tuman kutubxonalari bilan bog'lanish, audiokitoblar va ko'zi ojizlar uchun maxsus
**Audio Makon** bo'limi.

## ✅ Bajarilgan test va tekshiruvlar

Ushbu loyiha quyidagi avtomatik tekshiruvlardan **100% muvaffaqiyatli** o'tdi:

| Tekshiruv | Natija |
|---|---|
| PHP sintaksis (`php -l`), butun loyiha (jumladan test fayllari) | **96/96 fayl — 0 xato** |
| JS/JSX sintaksis (esbuild), mobil ilova | **17/17 fayl — 0 xato** |
| Blade teg balansi (`@if/@endif`, `@section/@endsection`, `@foreach`, `@push`, `@auth`) | **31/31 fayl — 0 nomuvofiqlik** |
| routes/web.php dagi barcha controller importlari | **13/13 — barchasi mavjud** |
| Barcha `view()` chaqiruvlari mos Blade fayllarga ega | **28/28 — barchasi mavjud** |
| Barcha `route('...')` chaqiruvlari `routes/web.php`da e'lon qilinganligi | **41/41 — barchasi mavjud** |
| composer.json / mobile package.json JSON formati | **valid** |

Original taqdim etilgan kodda topilgan va tuzatilgan xatolar:
- `routes/api.php` dagi yozuv xatosi (`marshrutiburilmadi` → `marshruti topilmadi`)
- `resources/views/audio/makon.blade.php` dagi bir nechta JavaScript xatosi: tushib qolgan
  `||` operatorlari (`localStorage.getItem(key) || '{}'`), backticksiz shablon literallari,
  va apostrofli sarlavha (`O'tkan Kunlar`) `onclick` atributini buzib yuborayotgani (HTML
  entity bilan tuzatildi)
- `mobile/src/store/slices/*.js` fayllaridagi bir nechta tushib qolgan `||` operatorlari
  (authSlice, offlineSlice)
- `mobile/src/store/index.js` dagi TypeScript sintaksisi (`export type ...`) oddiy
  JavaScript loyihada ishlamasligi — izohga aylantirildi
- Standart `users` migratsiyasi (bigint id) bilan bizning UUID asosidagi `users`
  jadvalimiz orasidagi ziddiyat — standart migratsiya faqat `sessions` va
  `password_reset_tokens` jadvallarini yaratadigan qilib qayta yozildi

## ⚠️ MUHIM: sinov muhitidagi cheklov

Ushbu kod men tomonimdan **to'liq yozilgan, tuzilgan va sintaksis jihatidan tekshirilgan**,
lekin men ishlagan xavfsiz muhit **packagist.org** (Composer paket ombori) ga kira olmaydi —
faqat GitHub, npm, PyPI kabi cheklangan manzillarga ruxsat berilgan. Shu sababli:

- `composer install` orqali Laravel'ning `vendor/` kutubxonalarini yuklab, `php artisan serve`
  yoki `php artisan test` orqali **jonli ishga tushirib bera olmadim**.
- Buning o'rniga har bir faylni alohida `php -l` (sintaksis tekshiruvi) dan o'tkazdim,
  route/controller/view bog'lanishlarini qo'lda va skript orqali tekshirdim.

Sizning kompyuteringizda (to'liq internet kirishi bilan) quyidagi buyruqlarni ishga
tushirsangiz, loyiha to'liq ishga tushadi — bu qadamlar standart Laravel jarayoni:

```bash
composer install
cp .env.example .env
php artisan key:generate
# .env faylida DB_CONNECTION=sqlite qiling (yoki MySQL sozlang) va DB fayl yarating:
touch database/database.sqlite
php artisan migrate
php artisan db:seed
php artisan serve
```

Tayyor demo hisoblar yaratilmaydi. Birinchi administrator uchun `.env` faylida
`ZIYO_BOOTSTRAP_SUPERADMIN_EMAIL` va kamida 7 belgili `ZIYO_BOOTSTRAP_SUPERADMIN_PASSWORD`
qiymatlarini vaqtincha kiriting, `php artisan db:seed` bajaring va keyin ushbu
ikki qiymatni `.env` faylidan o'chiring.

## 📁 Loyiha tuzilishi

```
app/Http/Controllers/Auth/     — Email va parol autentifikatsiyasi
app/Http/Controllers/Api/      — Mobil ilova uchun RESTful API (Sanctum)
app/Http/Controllers/Web/      — Veb-sayt controllerlari
app/Http/Middleware/           — AgeModeMiddleware (yosh aniqlash)
app/Models/                    — 14 ta Eloquent model
database/migrations/           — Barcha jadvallar (users, books, audiobooks, ...)
database/seeders/              — Katalog boshlang'ich ma'lumotlari
resources/views/                — Blade shablonlar (yosh rejimiga mos dizayn)
routes/web.php, routes/api.php — Barcha marshrutlar
mobile/                        — React Native ilova (Redux Toolkit, Navigation)
```

## 🔧 Foydalanuvchi tomonidan sinovda topilgan va tuzatilgan xato (2-bosqich)

Loyiha birinchi marta jonli serverga o'rnatilganda quyidagi xato chiqqan edi:

```
ErrorException: Undefined variable $ageMode
resources/views/home/index.blade.php:10
```

**Sabab:** `AgeModeMiddleware` faqat login qilingan foydalanuvchi bo'lsa
`$ageMode`ni Blade shablonlariga ulashar edi (`if (! Auth::check()) return $next($request);`).
Bosh sahifa (`/`) esa mehmonlar uchun ham ochiq bo'lgani sababli, mehmon kirganda
`$ageMode` umuman aniqlanmay, xato chiqargan.

**Tuzatish:**
1. `AgeModeMiddleware` endi mehmon uchun ham standart `youth` rejimini ulashadi.
2. Middleware `bootstrap/app.php` da barcha **web** sahifalarga global qo'llanadigan
   qilib qayta ro'yxatdan o'tkazildi — endi istalgan yangi ochiq sahifa qo'shilsa ham,
   bu xato boshqa takrorlanmaydi.

Ushbu tuzatishdan keyin butun loyiha (86 PHP fayl) yana bir bor `php -l` orqali
tekshirildi — 0 xato.

## 🆕 Yangi funksiya: Kutubxonaga onlayn kirish-chiqish (QR kod, kutubxonachisiz)

Har bir jismoniy kutubxona filiali uchun noyob **QR kod** generatsiya qilinadi
(`Library` modeli, `qr_token` maydoni). Foydalanuvchi kutubxona eshigidagi QR
kodni telefon kamerasi bilan skanerlaganda:

1. Agar tizimga kirmagan bo'lsa — avval login sahifasiga yo'naltiriladi,
   kirgandan so'ng Laravel'ning standart "intended URL" mexanizmi orqali
   avtomatik yana shu QR sahifasiga qaytariladi.
2. Login qilingan bo'lsa — kutubxona nomi va **"✅ Kutubxonaga kirdim"** tugmasi
   ko'rsatiladi. Bir bosish bilan tashrif **kutubxonachi ishtirokisiz**
   avtomatik qayd etiladi (`LibraryVisit` yozuvi yaratiladi).
3. Chiqishda xuddi shu QR kodni yana skanerlab, **"🚪 Chiqyapman"** tugmasini
   bosadi — chiqish vaqti va kutubxonada o'tkazgan vaqti (daqiqada) avtomatik
   hisoblanadi.

Agar foydalanuvchida boshqa kutubxonada yopilmagan tashrif qolgan bo'lsa
(masalan, u yerda "chiqish"ni bosishni unutgan bo'lsa), yangi kutubxonaga
kirganda eskisi avtomatik yopiladi — bir vaqtning o'zida ikkita "ochiq"
tashrif bo'lishining oldi olinadi.

### Yangi sahifalar
| Marshrut | Vazifasi |
|---|---|
| `GET /kutubxona/{qr_token}` | QR skanerlanganda ochiladigan kirish/chiqish sahifasi |
| `POST /kutubxona/{qr_token}/kirish` | Kirishni qayd etish |
| `POST /kutubxona/{qr_token}/chiqish` | Chiqishni qayd etish |
| `GET /profil/tashriflarim` | Foydalanuvchining o'z tashriflar tarixi |
| `GET /kutubxonalar-panel` | (Admin/Kutubxonachi) — filiallar ro'yxati, QR kodlarni chop etish, hozirgi bandlik |
| `GET /kutubxonalar-panel/{id}/bandlik` | (Admin/Kutubxonachi) — hozir shu kutubxonada bo'lganlar ro'yxati |

### QR kod generatsiyasi
`simplesoftwareio/simple-qrcode` composer paketidan foydalanilgan (SVG formatda,
qo'shimcha Imagick kutubxonasi talab qilinmaydi). `composer.json`ga qo'shilgan —
`composer install` buyrug'i uni avtomatik o'rnatadi.

### Boshlang'ich ma'lumotlar
`php artisan db:seed` ishga tushirilganda 2 ta kutubxona filiali
(Qamashi tuman markaziy kutubxonasi, Qamashi bolalar kutubxonasi) va ularning
QR manzillari konsolga chiqariladi. Standart login yoki parol paketga kiritilmaydi.



`mobile/` papkasida to'liq React Native loyihasi: Redux Toolkit store (auth, books, audio,
theme, offline slice'lari), React Navigation (Auth/Main oqimlari), 7 ta ekran (Login,
Register, Home, BookDetail, AudioPlayer, Reader, Profile), va oflayn yuklab olish xizmati
(`react-native-fs`).

Ishga tushirish:
```bash
cd mobile
npm install
npx react-native run-android   # yoki run-ios
```

`mobile/src/services/apiClient.js` faylida `BASE_URL` ni o'z serveringiz manziliga
o'zgartiring.
