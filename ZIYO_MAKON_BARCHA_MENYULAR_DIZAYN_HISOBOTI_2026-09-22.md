# Ziyo Makon v1.6.0 — barcha menyular dizayn hisoboti

Sana: 2026-09-22

## Natija

Platformadagi 37 ta Blade ko‘rinish va 65 ta web marshrut uchun “Digital Registan” dizayn tizimi umumlashtirildi. Bosh sahifadagi milliy-zamonaviy vizual til katalog, audio, hamjamiyat, profil, kutubxona, QR va boshqaruv sahifalariga yoyildi.

## Yangilangan bo‘limlar

- Kitoblar katalogi, kitob tafsiloti, onlayn o‘qish va tuman fondi.
- Audiokitoblar katalogi, audio tafsiloti va inklyuziv Audio Makon.
- Kitob klublari va guruh muhokamalari.
- G‘oyalar markazi, yangi g‘oya va ovoz berish sahifalari.
- Profil, o‘qilgan kitoblar, bronlar, tashriflar, oila va sozlamalar.
- Kutubxona filiallari, yangi filial, bandlik va QR kirish-chiqish.
- Administrator dashboardi, foydalanuvchilar, fond, a’zolik va QR aylanma.
- Kirish, ro‘yxatdan o‘tish, parol almashtirish va farzand profili.
- Loyiha haqida va yordam bo‘limlari.

## Yagona dizayn komponentlari

- Kutubxona, Hamjamiyat va Platforma guruhlariga ajratilgan ochiluvchi navigatsiya.
- Mobil qurilmalarda klaviatura va sensor orqali boshqariladigan menyu.
- Har bo‘lim uchun mavzuga mos “Digital Registan” ichki sahifa banneri.
- Chuqur moviy, koshin moviy, firuza, milliy oltin va oq marmar palitrasi.
- Bir xil shakldagi kartochka, forma, tugma, jadval va bo‘sh holat komponentlari.
- Maxsus ZM raqamli kitob muqovalari.
- Profil uchun yagona shaxsiy kabinet kompozitsiyasi.
- Administrator sahifalari uchun rasmiy to‘q-ko‘k boshqaruv sarlavhalari.
- Audio Makonda inklyuzivlik va katta shrift imkoniyatlari saqlangan.
- Responsive telefon, planshet va katta ekran ko‘rinishlari.
- Reduced-motion sozlamasi va 2D zaxira rejimi saqlangan.

## Test natijalari

| Tekshiruv | 1-test | 2-test | 3-test |
|---|---:|---:|---:|
| Vite production build | PASS | PASS | PASS |
| Paket xavfsizlik auditi | PASS | PASS | PASS |
| Mobil ESLint, 0 warning | PASS | PASS | PASS |
| Mobil Jest | PASS | PASS | PASS |
| Android JavaScript bundle | PASS | PASS | PASS |

## Izoh

Three.js sahnasi dinamik yuklanadi. Oddiy ichki sahifalarda og‘ir 3D modul yuklanmaydi, shu sabab yangi yagona dizayn asosiy xizmatlarning tezligiga xalaqit bermaydi. PHP CLI ish muhitida mavjud emasligi sabab Laravel Feature testlari production serverda PHP 8.3+ bilan bajarilishi kerak.
