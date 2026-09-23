# Tuman kutubxonalari va oflayn sinxronlash arxitekturasi

## Tashkiliy iyerarxiya

- Bitta tizim bir yoki bir nechta tumanni boshqara oladi.
- Har bir tuman tarkibida markaziy kutubxona, filiallar va mobil kutubxonalar mavjud.
- Har bir xodim tuman yoki aniq kutubxonaga biriktiriladi.
- Fond kitob nomi bo‘yicha emas, har bir jismoniy nusxaning inventar raqami va shtrix-kodi bo‘yicha yuritiladi.

## Rollar

| Rol | Vakolat doirasi |
|---|---|
| `super_admin` | Butun platforma va barcha tumanlar |
| `district_admin` | O‘z tumani va undagi barcha kutubxonalar |
| `library_admin` | Biriktirilgan kutubxona |
| `librarian` | Fond, a’zolik va kitob berish-qaytarish |
| `operator` | Tashrif, QR va kundalik operatsiyalar |
| `user` | Shaxsiy kabinet va katalog |

## Oflayn ishlash modeli

Filial qurilmasi lokal bazada operatsiyalar navbatini saqlaydi. Internet tiklanganda `push` orqali serverga yuboradi va boshqa qurilmalardagi o‘zgarishlarni `pull` orqali oladi. Har operatsiyada noyob UUID va qurilma ketma-ket raqami bor; shu sababli qayta yuborilgan so‘rov ikki marta bajarilmaydi.

### API

- `POST /api/v1/sync/devices/register` — qurilmani kutubxonaga biriktirish; maxfiy kalit faqat shu javobda qaytariladi.
- `POST /api/v1/sync/push` — ko‘pi bilan 200 ta lokal operatsiyani yuborish.
- `GET /api/v1/sync/pull?device_uuid=...&cursor=...` — keyingi 500 ta server operatsiyasini olish.
- `GET /api/v1/sync/status?device_uuid=...` — aloqa va kursor holatini tekshirish.

Sinxronlash so‘rovlarida Sanctum foydalanuvchi tokeni va `X-Device-Secret` sarlavhasi talab qilinadi. Qurilma faqat o‘zi biriktirilgan kutubxona ma’lumotiga murojaat qiladi.

## Birinchi bosqichda sinxronlanadigan obyektlar

- `inventory_item` — fond nusxasi va holati;
- `loan` — kitob berish, muddat va qaytarish;
- `library_visit` — tashrifchining kirish-chiqishi.

Server har bir qabul qilingan operatsiyani `sync_operations`, muhim boshqaruv hodisalarini esa `audit_logs` jadvalida saqlashga tayyor.
