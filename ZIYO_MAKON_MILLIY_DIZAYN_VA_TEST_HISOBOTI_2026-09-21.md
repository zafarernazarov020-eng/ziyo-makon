# Ziyo Makon v1.4.0 — milliy premium dizayn va yakuniy test hisoboti

Sana: 2026-09-21

## Bajarilgan dizayn ishlari

- Davlat rahbari darajasidagi taqdimot uchun yaxlit “milliy premium” vizual tizim yaratildi.
- O‘zbekiston bayrog‘ining moviy, oq, yashil va qizil ranglari rasmiy to‘q-ko‘k hamda oltin aksentlar bilan uyg‘unlashtirildi.
- Milliy geometrik naqshlar fon elementi sifatida nozik va chalg‘itmaydigan usulda qo‘llandi.
- Yangi ZM belgi tizimi, ikki qavatli rasmiy navigatsiya, davlat platformasi lentasi va premium footer yaratildi.
- Bosh sahifaga “Ma’rifatli jamiyat — buyuk kelajak poydevori” konsepsiyasidagi taqdimot banneri qo‘shildi.
- Kirish va ro‘yxatdan o‘tish oynalari zamonaviy ikki ustunli, mobil moslashuvchan premium kompozitsiyaga o‘tkazildi.
- Boshqaruv paneli rahbariyat uchun real vaqtga yaqin holat, tizim statusi va muhim ko‘rsatkichlarni tez ko‘rsatadigan uslubda yangilandi.
- Mobil ilovaning bolalar, yoshlar va kattalar rejimlari yagona milliy rang tizimiga moslashtirildi.

## Autentifikatsiya talabi

- Minimal parol uzunligi 12 belgidan 7 belgiga tushirildi.
- Xavfsizlikni saqlash uchun parolda katta harf, kichik harf, raqam va maxsus belgi bo‘lishi shart.
- Talab web ro‘yxatdan o‘tish, parol almashtirish, API, mobil ilova va administrator bootstrap jarayonida bir xil qo‘llanadi.
- OneID hozircha ulanmagan; avtorizatsiya email va parol orqali ishlaydi.

## Uch bosqichli tekshiruv natijalari

| Tekshiruv | 1-urinish | 2-urinish | 3-urinish |
|---|---:|---:|---:|
| Vite production build | PASS | PASS | PASS |
| Paket xavfsizlik auditi | PASS | PASS | PASS |
| Mobil ESLint (0 warning) | PASS | PASS | PASS |
| Mobil Jest komponent testi | PASS | PASS | PASS |
| Android JS bundle | PASS | PASS | PASS |

## Muhim izoh

PHP CLI ushbu ish muhitida mavjud emas. Shu sabab Laravel Feature testlarini jonli bajarishning imkoni bo‘lmadi; mavjud testlar paketda saqlangan va serverda PHP 8.3+ muhitida `php artisan test` orqali ishga tushirilishi kerak. Frontend, mobil kod, distributiv build va statik xavfsizlik nazoratlari to‘liq muvaffaqiyatli o‘tdi.
