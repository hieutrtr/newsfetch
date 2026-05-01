---
name: stock-news
description: Lấy tin tức chứng khoán Việt Nam và thế giới từ các trang tài chính uy tín. Dùng khi user yêu cầu "tin chứng khoán", "thị trường", "VN-Index", "tin tài chính", "stock news", hoặc tổng hợp diễn biến phiên/tuần.
---

# Stock & Finance News Fetcher

Mục tiêu: lấy tin chứng khoán, vĩ mô, doanh nghiệp niêm yết từ nguồn uy tín; trả về danh sách có nguồn và kèm số liệu chính khi có.

## Nguồn ưu tiên

**Việt Nam**
- CafeF — https://cafef.vn/ (chứng khoán, vĩ mô, doanh nghiệp)
- VietStock — https://vietstock.vn/
- NDH (Người Đồng Hành) — https://ndh.vn/
- VnExpress Kinh doanh — https://vnexpress.net/kinh-doanh
- Đầu Tư Chứng Khoán — https://www.tinnhanhchungkhoan.vn/
- FiinGroup / FiinPro insights — https://fiingroup.vn/

**Quốc tế**
- Bloomberg — https://www.bloomberg.com/markets
- Reuters Markets — https://www.reuters.com/markets/
- Financial Times — https://www.ft.com/markets
- WSJ Markets — https://www.wsj.com/news/markets
- CNBC — https://www.cnbc.com/markets/

## Quy trình thực hiện

1. **Xác định phạm vi**:
   - Thị trường: VN (HOSE/HNX/UPCoM) hay quốc tế (US/Asia)?
   - Loại tin: tổng quan phiên, mã cụ thể (VD: HPG, FPT), ngành (ngân hàng, BĐS niêm yết, dầu khí), hay vĩ mô (lãi suất, tỷ giá, CPI)?
   - Khung thời gian: phiên hôm nay / hôm qua / tuần.
2. **Fetch song song**: 3–5 nguồn phù hợp qua `WebFetch`. Với mã cụ thể, ưu tiên trang chi tiết của CafeF/VietStock.
3. **Trích số liệu chính**: VN-Index, thanh khoản, top mua/bán ròng khối ngoại, các mã tăng/giảm mạnh — nếu có.
4. **Lọc tin**: bỏ tin nhận định cá nhân/PR môi giới, ưu tiên tin sự kiện (ĐHCĐ, KQKD, M&A, thay đổi chính sách).
5. **Trả về theo định dạng** bên dưới.

## Định dạng output

```
📈 Tin chứng khoán — <khung thời gian>

[Tóm tắt phiên — nếu user hỏi tổng quan]
VN-Index: <điểm> (<+/-%>) | Thanh khoản: <giá trị>
Khối ngoại: <mua/bán ròng>

Tin nổi bật:
1. <Tiêu đề>
   <1–2 câu tóm tắt + số liệu chính>
   Nguồn: <tên trang> — <URL>

2. ...
```

Mặc định 5–8 tin. Nếu user hỏi 1 mã cụ thể, trả 3–5 tin liên quan tới mã đó.

## Lưu ý

- **Không đưa khuyến nghị mua/bán**. Chỉ tóm tắt thông tin có trong nguồn.
- **Luôn kèm URL** và tên nguồn.
- Số liệu phải khớp với nguồn — không làm tròn sai, không bịa.
- Phân biệt rõ "tin sự kiện" (KQKD, M&A) với "tin nhận định" (góc nhìn chuyên gia) — ghi tag nếu cần.
- Với tin quốc tế ảnh hưởng VN (Fed, giá dầu, USD/VND), ghi rõ tác động dự kiến nếu nguồn có nêu.
- Nếu nguồn paywall (Bloomberg/FT/WSJ), thử tìm bản tóm tắt qua `WebSearch` hoặc dùng nguồn thay thế.
