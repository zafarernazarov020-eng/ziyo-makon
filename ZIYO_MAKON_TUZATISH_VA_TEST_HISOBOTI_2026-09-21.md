# Ziyo Makon v1.2.1 — tuzatish va test hisoboti

Sana: 2026-09-21

## Bajarilgan tuzatishlar

1. Production paketidan `public/hot` va localhost manzilli development font manifesti olib tashlandi.
2. Vite va React Native npm buyruqlari ZIP ichida buziladigan `.bin` symlinklariga bog‘liq bo‘lmaydigan qilindi.
3. Bootstrap Super Admin uchun birinchi kirishda parolni majburiy almashtirish joriy qilindi.
4. Web va mobil ilovaga parol almashtirish oynasi/API oqimi qo‘shildi.
5. Bootstrap administratorni takroriy seed qilishda uning UUID qiymati almashib ketishi bartaraf etildi.
6. API profilida `district_code` tekshiriladi va `district_id` bilan atomar ravishda moslashtiriladi.
7. A’zolik foydalanuvchilari tuman/kutubxona tenant chegarasi bo‘yicha filtrlandi.
8. Tuman administratori boshqa foydalanuvchiga o‘zicha `district_admin` rolini bera olmasligi ta’minlandi.
9. Production SQLite va SQL snapshotlaridan sessiya, token, cache va navbat vaqtinchalik ma’lumotlari tozalandi.
10. Paketning majburiy fayllari, JSON sintaksisi, build artefaktlari va development izlarini tekshiruvchi `scripts/package_audit.mjs` qo‘shildi.
11. Yangi xavfsizlik PHPUnit testlari: majburiy parol almashtirish hamda tuman kodi/ID mutanosibligi.

## Uch martalik yakuniy testlar

| Test | 1 | 2 | 3 | Natija |
|---|---:|---:|---:|---|
| Vite production build | 1.342 s | 1.294 s | 1.190 s | 3/3 PASS |
| Mobil ESLint (0 warning talabi) | 1.997 s | 1.944 s | 1.964 s | 3/3 PASS |
| Mobil Jest | 6.713 s | 1.282 s | 1.337 s | 3/3 PASS |
| Android JS bundle | 2.446 s | 1.943 s | 1.975 s | 3/3 PASS |
| SQLite integrity/FK | PASS | PASS | PASS | 3/3 PASS |

SQLite 1 000 operatsiyali qayta testda barcha uch urinishda baza yaxlitligi saqlandi. O‘qish 8.267–9.627 ms, yozish 1.539–1.816 ms, 1 000 qator olish 0.395–0.626 ms oralig‘ida bo‘ldi.

## Muhit cheklovi

Tekshiruv konteynerida PHP CLI paketi mavjud emas va paket ombori PHP o‘rnatishga ruxsat bermadi. Shu sabab PHPUnit/Laravel HTTP testlari ushbu muhitda jonli ishga tushirilmadi. Ular loyiha ichida saqlandi va PHP 8.3+ mavjud serverda `php artisan test` orqali bajariladi. Qolgan statik, build, mobil va SQLite testlari real bajarildi.

## Paketlash qarori

Platformaga bog‘liq va ZIP ichida symlinklari buziladigan `node_modules` kataloglari yakuniy paketga kiritilmaydi. Qayta build zarur bo‘lsa, ildiz va `mobile` katalogida `npm ci` bajariladi. Tayyor web build va Android JavaScript bundle paket ichida mavjud.
