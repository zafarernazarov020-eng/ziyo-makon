# Ziyo Makon — yakuniy yig‘ish hisoboti

Sana: 2026-09-21

> v1.2.1 yakuniy tuzatishlar va uch martalik test tafsilotlari `ZIYO_MAKON_TUZATISH_VA_TEST_HISOBOTI_2026-09-21.md` faylida.

## Tuman miqyosidagi oflayn arxitektura

- Tuman → markaziy kutubxona → filial iyerarxiyasi qo‘shildi.
- `super_admin`, `district_admin`, `library_admin`, `librarian`, `operator`, `user` rollari joriy qilindi.
- A’zolik kartalari, inventar nusxalari va kitob berish-qaytarish jadvallari yaratildi.
- Kutubxonaga bog‘langan qurilmalar va maxfiy qurilma kaliti bilan himoyalangan push/pull API qo‘shildi.
- Operatsiya UUID-si orqali takroriy sinxronlashdan himoya qilindi.
- Bo‘sh SQLite bazadan barcha migratsiya va seederlar muvaffaqiyatli bajarildi.
- PHP sintaksis tekshiruvi: 82 fayl — PASS.
- Integratsion smoke-test: 15 tekshiruv — PASS.

## 2026-09-19 — production tayyorgarligi bo‘yicha tuzatishlar

- Tumanlararo kutubxona ro‘yxati va bandlik sahifasidagi tenant izolyatsiyasi yopildi.
- 6 rol permission modeli, administrator dashboardi va ruxsatlarni boshqarish oynasi qo‘shildi.
- Inventar, a’zolik, a’zolik to‘lovi va QR/shtrix-kod orqali berish-qaytarish modullari yaratildi.
- Tuman kodi qo‘lda yozilmaydi: web va mobil ilovada server katalogidan tanlanadi.
- Mobil menyuga kitoblar, yangi/ommabop/o‘qilayotgan kitoblar, katalog, audio, QR, yuklanganlar, a’zolik/to‘lov va sinxronlash markazi qo‘shildi.
- Sanctum tokeni AsyncStorage’dan Android Keystore/iOS Keychain saqloviga ko‘chirildi.
- Oflayn operatsiya navbati, internet holati, push/pull, konflikt va qayta yuborish holati qo‘shildi.
- React Native 0.87.1 va React Navigation 7 ga yangilandi; high/moderate audit zaifliklari 0 ga tushirildi.
- Jest ESM muammosi tuzatildi va mobil test ishga tushdi.
- 198 inline style’dan 174 tasi design-system utility sinflariga ko‘chirildi; qolganlari dinamik yoki alohida accessibility sahifasiga tegishli.
- Responsiv hamburger menyu, dashboard kartalari, jadvallar, formalar va reduced-motion qo‘llab-quvvatlandi.

## Bajarilgan ishlar

1. React Native 0.75.4 Android/iOS native scaffold, Metro, Babel, Jest va lock-fayl qo‘shildi.
2. `react-native-track-player` orqali ko‘p trekli audio, fon boshqaruvi, trek tanlash va progress sinxronizatsiyasi qo‘shildi.
3. Native PDF reader haqiqiy sahifa/jami sahifa qiymatlarini kuzatadi; soxta 100% progress bloklandi.
4. Bola foydalanuvchiga har bir tugallangan kitob uchun XP faqat bir marta beriladi.
5. Audiokitoblarning yosh cheklovi ro‘yxat, detail va progress API darajasida tekshiriladi.
6. `database/snapshots/ziyo_makon_final.sqlite` va `.sql` nusxalari yaratildi.
7. Standart demo hisoblar/parollar olib tashlandi; bootstrap admin faqat muhit o‘zgaruvchilari orqali yaratiladi.
8. Composer, veb npm va mobil npm paketlari o‘rnatildi; Vite va Metro production build bajarildi.
9. Migratsiya, DB, ro‘yxatdan o‘tish, login, Sanctum, rol, yosh filtri, PDF va XP bo‘yicha 10 ta smoke check PASS.
10. PHP sintaksisi (73 fayl), JSON fayllar va mobil ESLint tekshirildi; ESLintda 0 xato.

## Muhit bo‘yicha eslatma

Android JavaScript production bundle yaratildi. Ushbu Linux ish muhitida Android SDK mavjud bo‘lmagani va Gradle distributiviga tarmoq kirishi cheklangani sabab APK fayli kompilyatsiya qilinmadi. Android Studio o‘rnatilgan kompyuterda `mobile` katalogidan `npm run android` yoki `android/gradlew assembleRelease` bajariladi.

Haqiqiy `.env` fayli va `APP_KEY` xavfsizlik sabab ZIP paketga kiritilmagan. O‘rnatishda `.env.example` nusxalanadi va yangi `APP_KEY` yaratiladi.
