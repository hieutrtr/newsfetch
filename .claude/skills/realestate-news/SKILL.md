---
name: realestate-news
description: Lấy tin bất động sản Việt Nam (chính sách, dự án, giá, phân khúc) từ các trang uy tín. Dùng khi user yêu cầu "tin bất động sản", "BĐS", "tin nhà đất", "thị trường địa ốc", hoặc cập nhật khu vực/dự án cụ thể.
---

# Real Estate News Fetcher

Mục tiêu: lấy tin bất động sản — chính sách, quy hoạch, dự án, biến động giá, phân khúc — từ nguồn uy tín. Trả về danh sách có nguồn và phân loại rõ.

## Nguồn ưu tiên

**Việt Nam (chính)**
- CafeLand — https://cafeland.vn/
- Batdongsan.com.vn (tin tức) — https://batdongsan.com.vn/tin-tuc
- CafeF Bất động sản — https://cafef.vn/bat-dong-san.chn
- VnExpress Bất động sản — https://vnexpress.net/kinh-doanh/bat-dong-san
- Báo Đầu Tư BĐS — https://baodautu.vn/bat-dong-san-d6/
- Reatimes — https://reatimes.vn/

**Báo cáo thị trường (chuyên sâu)**
- Savills Vietnam — https://www.savills.com.vn/research/
- CBRE Vietnam — https://www.cbrevietnam.com/research-and-reports
- JLL Vietnam — https://www.jll.com.vn/vi/xu-huong-va-nghien-cuu

## Quy trình thực hiện

1. **Xác định phạm vi**:
   - Khu vực: HCM, Hà Nội, tỉnh (Bình Dương, Đồng Nai, Long An…), hay toàn quốc?
   - Phân khúc: căn hộ, đất nền, nhà phố, BĐS công nghiệp, BĐS nghỉ dưỡng, văn phòng cho thuê?
   - Loại tin: chính sách/luật (Luật Đất đai, Luật Nhà ở, tín dụng), dự án mới, biến động giá, M&A doanh nghiệp BĐS niêm yết?
   - Khung thời gian: tuần / tháng / quý.
2. **Fetch song song**: 3–5 nguồn phù hợp qua `WebFetch`. Với báo cáo thị trường (Savills/CBRE/JLL), fetch trang research mới nhất.
3. **Phân loại tin** thành nhóm: Chính sách | Dự án | Giá & giao dịch | Doanh nghiệp.
4. **Lọc tin**: bỏ tin quảng cáo dự án/sponsored content, ưu tiên tin có số liệu hoặc nguồn chính thức (Bộ Xây dựng, Sở TN-MT, NHNN).
5. **Trả về theo định dạng** bên dưới.

## Định dạng output

```
🏘️ Tin bất động sản — <khu vực> — <khung thời gian>

📋 Chính sách & Pháp lý
1. <Tiêu đề>
   <1–2 câu tóm tắt>
   Nguồn: <tên trang> — <URL>

🏗️ Dự án & Nguồn cung
2. ...

💰 Giá & Giao dịch
3. ...

🏢 Doanh nghiệp & M&A
4. ...
```

Bỏ nhóm nào không có tin. Mặc định 5–8 tin tổng cộng.

## Lưu ý

- **Cảnh giác với tin PR dự án** — nhiều bài trên báo lớn vẫn là dạng booking content. Dấu hiệu: chỉ ca ngợi 1 dự án, không có số liệu so sánh, không có ý kiến độc lập. Bỏ hoặc gắn tag "[PR]" nếu phải đưa.
- **Luôn kèm URL** và nguồn.
- Số liệu giá/diện tích/tỷ lệ hấp thụ phải khớp nguồn.
- Phân biệt rõ "giá rao bán" vs "giá giao dịch thực" — nguồn batdongsan.com.vn thường là giá rao.
- Với chính sách, ghi rõ trạng thái: dự thảo / đã ban hành / hiệu lực từ ngày…
- Nếu user hỏi khu vực hẹp (1 quận/1 dự án), thêm `WebSearch` với địa danh + thời gian.
