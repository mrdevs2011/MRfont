# MRnotes — 6 ta yaxshilanish uchun reja

Maqsad: `index.html` ga quyidagi 6 ta qo'shimcha imkoniyatlarni kiritish, mavzor, uslub va arxitekturani saqlab qolgan holda.

## 1. Qaydlar qidiruvi
- **Joylashuv**: `notes-view` sarlavha qismiga qo'shiladi.
- **UI**: `note-title-input` uslubidagi kichik `<input type="search">`.
- **Mantiq**: `notesList` massivini sarlavha (`title`) va matn (`content`) bo'yicha filtrlash; natijani `renderNotesList()` ga moslashtirish.
- **Hususiyat**: bo'sh qidiruvda barcha qaydlar ko'rinadi; qidiruv natijasi bo'sh bo'lsa "Topilmadi" holati ko'rsatiladi.

## 2. Qorong'u mavzu (dark mode)
- **Qo'llash**: `:root` ga dark-uchun CSS o'zgaruvchilarini qo'shish va `body.dark` sinfi bilan almashtirish.
- **Tugma**: hisob/account modaliga yoki sozlamalar ko'rinishiga quyosh/oy piktogrammasi tugmasi qo'shiladi.
- **Saqlash**: `settings.theme = 'light' | 'dark'` shaklida `localStorage`/cloud ga saqlanadi.
- **Sistema**: `prefers-color-scheme: dark` ni initsializatsiya vaqtida inobatga olish.
- **Qo'shimcha**: Firebase Google logotipi va onboarding rasmlari quyosh/o'g'irlangan holatda ko'rinishi uchun invert/shadow uslublari qo'llaniladi.

## 3. PWA / Service Worker
- **Fayllar**:
  - `manifest.json` — ilova nomi, piktogramma, `start_url`, `display: standalone`.
  - `service-worker.js` — statik fayllarni keshga olish va offline da `index.html` ni qaytarish.
- **Integratsiya**: `index.html` head ga `<link rel="manifest">` va `<script>` da `navigator.serviceWorker.register()`.
- **Ikonka**: SVG ni turli o'lchamlarga aylantirish yoki mavjud SVG ni manifest piktogrammasi sifatida ishlatish.

## 4. Accessibility (foydalanish imkoniyati)
- **Tugmalar**: barcha `icon-only` va `icon-btn` lar uchun `aria-label` qo'shiladi.
- **Klaviatura**: global klaviatura parchalari:
  - `Ctrl/Cmd + S` — qaydni saqlash.
  - `Ctrl/Cmd + N` — yangi qayd.
  - `Escape` — modal va yozish fullscreendan chiqish (allaqachon bor, kengaytirish).
  - `Ctrl/Cmd + K` — qidiruv maydoniga fokus.
- **Skip link**: asosiy tarkibga o'tish uchun "Skip to content" havolasi.
- **Modal**: modal ochilganda fokusni birinchi focusable elementga o'tkazish, yopilganda oldingi elementga qaytarish.

## 5. Ma'lumotlarni eksport/import qilish
- **Joylashuv**: account modaliga "Zaxira yuklash" va "Zaxiradan tiklash" tugmalari qo'shiladi.
- **Format**: JSON fayl — ichida `manifest`, `glyphsData`, `notesList`, `notes`, `settings`.
- **Eksport**: barcha cloud/local ma'lumotlarni to'plash, JSON ga aylantirish, `download` atributli havola yaratish.
- **Import**: fayl tanlash `<input type="file">` orqali JSON ni o'qish, ma'lumotlar strukturasi tekshiriladi, tasdiqlash modalidan keyin saqlanadi.
- **Xavfsizlik**: import qilingan ma'lumotlar to'liq eskisini almashtirmaydi, balki birlashtiriladi (ixtiyoriy).

## 6. Qo'lyozma chiziqlarini optimallashtirish
- **Muammo**: har bir harf chizilganda juda ko'p nuqta yig'ilishi mumkin, natijada shrift hajmi va ishlashi sekinlashadi.
- **Yechim**: chiziq nuqtalarini saqlashdan oldin Ramer–Douglas–Peucker (RDP) yoki oddiy burchak/piksel masofasi bo'yicha soddalashtirish.
- **Integratsiya**: `computeBBox` dan oldin `simplifyStrokes()` chaqiriladi; variantning `strokes` maydoniga saqlanadi.
- **Foydasi**: kesh hajmi, Firestore yozuvlari va render tezligi yaxshilanadi.

## Implementatsiya tartibi
1. HTML/CSS qismini kengaytirish: dark mode o'zgaruvchilari, qidiruv input, PWA meta, accessibility tugmalar.
2. JavaScript da qidiruv, dark mode, klaviatura parchalari, eksport/import.
3. PWA fayllarini yaratish va ulash.
4. Qo'lyozma optimallashtirish funksiyasini qo'shish.
5. Kichik sinovlar: modallar, dark mode almashish, qidiruv, eksport/import.

## Tahminiy fayllar
- `index.html` — asosiy o'zgartirishlar.
- `manifest.json` — yangi.
- `service-worker.js` — yangi.
- `PLAN.md` — ushbu reja.
