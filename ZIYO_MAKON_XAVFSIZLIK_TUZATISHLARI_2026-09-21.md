# Ziyo Makon v1.3.0 — xavfsizlik tuzatishlari

Sana: 2026-09-21

## Autentifikatsiya

- OneID integratsiyasi hozircha to‘liq o‘chirildi: controller, marshrut, interfeys tugmasi, konfiguratsiya va muhit kalitlari olib tashlandi.
- Kirish faqat email va parol orqali amalga oshiriladi.
- Login 5 urinish/daqiqa, ro‘yxatdan o‘tish 3 urinish/daqiqa bilan cheklandi.
- Yangi parol kamida 7 belgi, katta-kichik harf, raqam va maxsus belgidan iborat bo‘lishi shart.
- Birinchi kirishda parol almashtirish talabi saqlandi.

## Ma’lumot va media himoyasi

- PDF, EPUB va audio fayllar to‘g‘ridan-to‘g‘ri `public/storage` orqali berilmaydi.
- Kontent private diskdan muddati cheklangan imzolangan URL orqali uzatiladi.
- Audio Makon statik ochiq MP3 manzillaridan dinamik, imzolangan katalogga o‘tkazildi.
- Security headers: CSP, HSTS (HTTPSda), X-Frame-Options, nosniff, Referrer-Policy va Permissions-Policy qo‘shildi.
- Production sessiyasi uchun secure, HttpOnly, SameSite va session encryption sozlamalari kiritildi.

## IDOR, tenant va parallel so‘rovlar

- Kitob klubi show/join/message amallari foydalanuvchi tumani bilan cheklandi.
- Klubga a’zo bo‘lmagan foydalanuvchi xabar yubora olmaydi.
- Klubga qo‘shilish transaction va row-lock orqali himoyalandi.
- Bron yaratish/bekor qilish transaction va row-lock orqali himoyalandi; boshqa tumandan bron qilish bloklandi.
- Sync API faqat `sync.manage` ruxsatiga ega Super Admin, District Admin va Library Admin uchun qoldirildi.
- Sync qurilma secretini almashtirish uchun amaldagi secret talab qilinadi; eskirgan sequence rad etiladi.
- Web profilidagi tuman kodi va ID bir vaqtda yangilanadi; farzand profiliga ham district_id yoziladi.
- API `per_page` maksimal 50 qilib cheklandi.
- Web o‘qish progressida soxta sahifa soni va takroriy XP olish yopildi.
- QR kirish/chiqish amallari rate-limit bilan himoyalandi.

## Test natijalari

- Paket auditi: PASS.
- Vite production build: 3/3 PASS.
- Mobil ESLint, 0 warning: 3/3 PASS.
- Mobil Jest: 3/3 PASS.
- Android JS bundle: 3/3 PASS.
- SQLite integrity va foreign keys: 3/3 PASS.
- OneID qoldiq marshrut/kalit tekshiruvi: PASS.
- Ochiq media yo‘llari tekshiruvi: PASS.

PHP CLI ushbu muhitda mavjud emasligi sabab yangi Laravel Feature testlari paketga qo‘shildi, ammo jonli `php artisan test` serverda PHP 8.3+ bilan bajarilishi kerak.
