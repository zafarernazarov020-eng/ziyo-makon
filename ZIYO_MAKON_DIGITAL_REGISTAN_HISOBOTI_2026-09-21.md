# Ziyo Makon v1.5.0 — “Digital Registan” dizayn va test hisoboti

Sana: 2026-09-21

## Konsepsiya

Platforma “Ziyo Makon — Raqamli ma’rifat saroyi” konsepsiyasi asosida tubdan yangilandi. Dizayn formulasi: 70% zamonaviy davlat raqamli platformasi, 20% O‘zbekiston milliy me’morchiligi, 10% taqdimot darajasidagi 3D effektlar.

## Amalga oshirilgan ishlar

- Three.js va GSAP asosidagi 6–8 soniyalik ochilish sahnasi yaratildi.
- Qadimiy kitob, moviy-oltin yorug‘lik va Registon peshtoqi asosidagi 3D bilim portali qurildi.
- Introda “Milliy merosdan — raqamli kelajak sari” shiori va “O‘tkazib yuborish” boshqaruvi mavjud.
- Birinchi ekran ortiqcha matndan tozalandi: loyiha ramzi, nomi, shior, katta qidiruv, asosiy tugma va 3D sahna qoldirildi.
- Milliy meros, jahon adabiyoti, bolalar olami, ilm va texnologiya, audiokitoblar hamda yosh ijodkorlar uchun oltita “raqamli zal” yaratildi.
- Rahbariyat paneliga to‘liq ekran “Taqdimot rejimi” qo‘shildi.
- Three.js asosidagi interaktiv O‘zbekiston monitoring xaritasi, faol/o‘rtacha/muammoli holat indikatorlari va hudud kartasi yaratildi.
- “Animatsiyani kamaytirish”, 2D rejim, klaviaturadagi Escape boshqaruvi va WebGL ishlamasa avtomatik zaxira ko‘rinishi qo‘shildi.
- Kuchsiz qurilmalarda 3D avtomatik o‘chib, yengil 2D kompozitsiya ishlaydi.
- Three.js va GSAP dinamik import qilinadi; oddiy sahifalarning boshlang‘ich JavaScript paketi taxminan 9,6 KB.
- Mobil bosh sahifa “Digital Registan” ranglari va milliy oltin aksentlar bilan yangilandi.
- Mobil navigatsiya Bosh sahifa, Katalog, QR-skaner, Kitoblarim va Profil tartibiga o‘tkazildi.
- QR-skaner markazda oltin halqali yirik tugma sifatida joylashtirildi.

## Ranglar

- Chuqur moviy: `#062C4A`
- Koshin moviy: `#087E8B`
- Firuza: `#20C4C7`
- Milliy oltin: `#D8AE5E`
- Oq marmar: `#F7F7F2`
- Tun ko‘ki: `#061725`

## Uch martalik test natijalari

| Tekshiruv | 1-test | 2-test | 3-test |
|---|---:|---:|---:|
| Vite production build | PASS | PASS | PASS |
| Paket xavfsizlik auditi | PASS | PASS | PASS |
| Mobil ESLint, 0 warning | PASS | PASS | PASS |
| Mobil Jest komponent testi | PASS | PASS | PASS |
| Android JavaScript bundle | PASS | PASS | PASS |

## Avtorizatsiya holati

- OneID ulanmagan.
- Kirish email va parol orqali ishlaydi.
- Minimal parol uzunligi 7 belgi.
- Katta harf, kichik harf, raqam va maxsus belgi talabi saqlangan.

## Muhim izoh

PHP CLI mazkur ish muhitida mavjud bo‘lmagani sabab Laravel Feature testlarini jonli bajarish imkoni bo‘lmadi. Ular paketda mavjud va production serverda PHP 8.3+ muhitida `php artisan test` orqali ishga tushirilishi kerak.
