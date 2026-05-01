---
name: tech-news
description: Lấy tin tức công nghệ từ các trang uy tín trong và ngoài nước. Dùng khi user yêu cầu "tin công nghệ", "tech news", "AI news", "tin IT", hoặc tóm tắt diễn biến công nghệ hôm nay/tuần này.
---

# Tech News Fetcher

Mục tiêu: lấy và tóm tắt tin công nghệ mới nhất từ các nguồn uy tín, trả về danh sách có nguồn rõ ràng.

## Nguồn ưu tiên

**Quốc tế (tiếng Anh)**
- TechCrunch — https://techcrunch.com/
- The Verge — https://www.theverge.com/
- Ars Technica — https://arstechnica.com/
- Wired — https://www.wired.com/
- MIT Technology Review — https://www.technologyreview.com/
- Hacker News (front page) — https://news.ycombinator.com/

**Việt Nam**
- VnExpress Số hóa — https://vnexpress.net/so-hoa
- GenK — https://genk.vn/
- Tinhte — https://tinhte.vn/
- ICTNews — https://ictnews.vietnamnet.vn/

## Quy trình thực hiện

1. **Xác định phạm vi**: hỏi/đoán user muốn nguồn VN hay quốc tế, chủ đề cụ thể (AI, mobile, startup, security…) hay tổng quan, khoảng thời gian (hôm nay / 24h / tuần).
2. **Fetch song song**: dùng `WebFetch` cho 3–5 nguồn phù hợp nhất cùng lúc trong một message. Lấy trang chủ hoặc trang chuyên mục.
3. **Lọc tin**: ưu tiên tin có ngày đăng trong khung thời gian user yêu cầu, bỏ tin quảng cáo/sponsored, bỏ tin trùng chủ đề.
4. **Tóm tắt mỗi tin** bằng 1–2 câu tiếng Việt, giữ nguyên tên riêng/sản phẩm bằng tiếng Anh.
5. **Trả về theo định dạng** bên dưới.

## Định dạng output

```
📰 Tin công nghệ — <khung thời gian>

1. <Tiêu đề ngắn gọn tiếng Việt>
   <1–2 câu tóm tắt>
   Nguồn: <tên trang> — <URL>

2. ...
```

Mặc định trả 5–8 tin, sắp xếp theo độ quan trọng (không theo thứ tự nguồn).

## Lưu ý

- **Luôn kèm URL** để user verify được. Không bịa link.
- Nếu `WebFetch` trả về nội dung thiếu, thử `WebSearch` với query cụ thể.
- Nếu user yêu cầu chủ đề hẹp (vd "AI hôm nay"), thêm `WebSearch` với từ khóa + `after:<date>` để lấy tin mới nhất.
- Không tóm tắt tin quá cũ (>7 ngày) trừ khi user hỏi rõ.
- Nếu không lấy được tin từ một nguồn, ghi rõ "không truy cập được" thay vì bỏ qua âm thầm.
