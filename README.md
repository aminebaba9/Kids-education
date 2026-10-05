# Little Lingua — Website song ngữ Việt / Anh cho trẻ học tiếng Anh 🎈

*(English summary at the bottom of this file.)*

Trang giới thiệu lớp học tiếng Anh trực tuyến cho bé 4–12 tuổi, làm **riêng cho phụ huynh Việt Nam**: mặc định hiển thị **tiếng Việt**, có nút chuyển sang **tiếng Anh** chỉ với một cú nhấp. Toàn bộ nội dung **chỉ tập trung vào thị trường Việt Nam**.

Toàn bộ website nằm trong **một file `index.html`** — không cần cài đặt, không cần server, mở là chạy.

---

## 1. Điểm chính của website

| Hạng mục | Nội dung |
|---|---|
| Ngôn ngữ | **Tiếng Việt mặc định + tiếng Anh** (`VI` / `EN`), nhớ lựa chọn của khách, có link `?lang=en` |
| Thị trường | **Chỉ Việt Nam**: giờ GMT+7, Zalo, VNĐ, 34 tỉnh/thành, hotline Việt Nam |
| Nội dung | Dải cam kết, **lộ trình Cambridge (Starters – Movers – Flyers)**, khối "Bố mẹ không biết tiếng Anh vẫn theo dõi được con", đội ngũ giáo viên, bảng học phí, 3 đánh giá phụ huynh, **8 câu hỏi thường gặp** |
| Chuyển đổi | Nút **Zalo** nổi, thanh gọi/Zalo dính đáy trên điện thoại, form đăng ký (tên, SĐT/Zalo, tuổi, tỉnh/thành, khung giờ) |
| SEO | `lang="vi"`, `hreflang` vi/en, mô tả, Open Graph cho Zalo/Facebook, dữ liệu có cấu trúc FAQ + EducationalOrganization |
| Trải nghiệm | Nút bỏ qua tới nội dung, `aria-*` đầy đủ, khoá tiêu điểm trong hộp thoại, tôn trọng `prefers-reduced-motion` |

---

## 2. Cần thay gì trước khi chạy quảng cáo

Mở `index.html` và tìm các vị trí sau (dùng `Ctrl/Cmd + F`):

1. **`window.CONTACT`** (gần cuối file) — thay số Zalo, hotline, email, Facebook/TikTok/YouTube thật.
   ```js
   window.CONTACT = {
     zalo: "https://zalo.me/0900000000",   // ← số Zalo thật
     phone: "tel:+84900000000",            // ← hotline
     email: "mailto:hello@littlelingua.vn",
     facebook: "https://facebook.com/…",
     tiktok: "https://tiktok.com/@…",
     youtube: "https://youtube.com/@…"
   };
   ```
   > Hiện tại các link này đang là **số giả**: khi khách bấm, website hiện thông báo "đây là bản demo, hãy thay link thật". Sau khi bạn điền link thật, thông báo sẽ tự mất.
2. **`SUBMIT_ENDPOINT`** (đầu khối `<script>` thứ hai) — nơi nhận đăng ký của phụ huynh.
   * Để trống: chạy chế độ demo, dữ liệu chỉ hiện trong Console, vẫn hiện màn hình cảm ơn.
   * Dán link **Google Apps Script** (đẩy về Google Sheet) hoặc **Formspree / Getform / API riêng** vào đây để nhận dữ liệu thật. Form gửi bằng `POST` JSON:
     ```json
     { "parentName": "…", "phone": "…", "childAge": "6-8", "city": "Hà Nội",
       "timePreference": "18:30 – 20:00 (giờ VN)", "email": "…", "note": "…",
       "language": "vi", "page": "…", "submittedAt": "…" }
     ```
3. **Học phí** — sửa trong khối `"vi"` / `"en"` của `window.I18N`: `price.p2.unit`, `price.p2.save`, `price.p3.*`. (Hiện là giá tham khảo: 1.190.000₫ lớp nhóm, 2.990.000₫ lớp 1-1.)
4. **Zalo OA** (khuyến nghị): tạo Zalo Official Account, sau đó dán đoạn script widget của Zalo ngay trước `</body>` — đã có ghi chú trong file.
5. **Số liệu xã hội** trong phần thống kê (`10+`, `2.500+`, `25+`, `4.9/5`) — thay bằng số thật để tránh quảng cáo sai sự thật.
6. **Tên miền** trong thẻ `canonical` / `hreflang` / `og:image` (đầu file) — đổi thành tên miền thật.

> ⚠️ Lưu ý pháp lý: website thu thập số điện thoại của phụ huynh. Nên có **trang chính sách bảo mật** và **sự đồng ý của phụ huynh** (Nghị định 13/2023/NĐ-CP về bảo vệ dữ liệu cá nhân). Nếu dùng hình ảnh/giọng nói của trẻ (video buổi học), cần sự đồng ý bằng văn bản của phụ huynh.

---

## 3. Cách sửa chữ (không cần biết lập trình)

Mọi câu chữ nằm trong khối `window.I18N` ở cuối `index.html`:

```js
window.I18N = {
  vi: { "hero.title": "Tiếng Anh thật vui cho những em nhỏ tỏa sáng!", … },
  en: { "hero.title": "Big English fun for little bright minds!", … }
};
```

Sửa trực tiếp phần chữ (giữ nguyên khoá như `"hero.title"`), lưu file và tải lại trang. Phần HTML phía trên không cần đụng tới.

**Lưu ý:** hai khối `vi` và `en` phải có **đủ các khoá giống nhau** (hiện là 291 khoá mỗi khối). Nếu thêm câu mới, thêm vào cả hai khối rồi dùng `data-i18n="khoá"` trong HTML.

Danh sách tỉnh/thành trong form đã cập nhật theo **34 tỉnh, thành phố** (sau sáp nhập từ 01/07/2025), gồm cả lựa chọn "Tỉnh/thành khác".

---

## 4. Đưa lên mạng

| Cách | Các bước | Ghi chú |
|---|---|---|
| **Netlify Drop** (nhanh nhất) | Kéo thả thư mục chứa `index.html` vào netlify.com/drop | Miễn phí, có HTTPS, gắn tên miền riêng trong 2 phút |
| **GitHub Pages** | Settings → Pages → Deploy from branch `main` → `/ (root)` | Miễn phí, phù hợp repo này |
| **Vercel / Cloudflare Pages** | Import repo GitHub, framework: **Other**, không cần build | Miễn phí, tốc độ tốt ở Việt Nam |
| **Hosting Việt Nam** (PA Vietnam, Tino, Mắt Bão…) | Upload `index.html` qua FTP/cPanel | Chọn nếu cần hoá đơn VAT và hỗ trợ tiếng Việt |

Sau khi có tên miền, nhớ cập nhật `canonical`, `hreflang` và `og:image` trong `<head>`.

---

## 5. Kiểm thử nhanh

```bash
python3 -m http.server 8080     # mở http://localhost:8080
```
Checklist:
- [ ] Mở trang thấy tiếng Việt, bấm `EN` → toàn bộ chữ đổi sang tiếng Anh, tải lại trang vẫn giữ tiếng Anh.
- [ ] Mở `?lang=vi` → quay về tiếng Việt.
- [ ] Trong form: chọn tỉnh/thành thấy đủ 34 tỉnh thành; thử bỏ trống / SĐT sai → có thông báo lỗi tiếng Việt; điền đủ → hiện màn hình cảm ơn.
- [ ] Trên điện thoại: thanh "Gọi / Zalo" + "Học thử miễn phí" dính đáy, nút Zalo nổi không che nội dung.
- [ ] Kiểm tra trên cả Safari iOS và Chrome Android.

---

## English summary

A single-file bilingual (Vietnamese-first + English) landing page for Little Lingua — online English classes for kids aged 4–12, built **exclusively for the Vietnamese market**. Vietnamese is the default language; the `VI`/`EN` toggle swaps every string on the page (including form options, meta title/description and image `alt` text) and remembers the choice via `localStorage`, with `?lang=vi|en` deep links. Sections: trust strip, Cambridge roadmap (Starters → Movers → Flyers), a "you don't need English to follow their progress" panel for parents, teacher profiles, transparent pricing in VND, three parent testimonials and eight FAQs written for Vietnamese families. Vietnam-specific touches: Zalo links and floating button, a sticky mobile "Call/Zalo + Free trial" bar, VN time slots and a province/city picker covering Vietnam's current **34 provinces and cities** (post-July-2025 merger). SEO includes `hreflang`, Open Graph and FAQ/Organization structured data. To go live: fill in `window.CONTACT`, set `SUBMIT_ENDPOINT` (Google Apps Script, Formspree or your API), update the real prices and the domain in `<head>`. Everything else is plain HTML/CSS/JS — no build step, no dependencies.
