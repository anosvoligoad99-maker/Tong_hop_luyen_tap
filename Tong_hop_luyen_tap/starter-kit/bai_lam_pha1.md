## 4.1. Bảo vệ dữ liệu và chống ảo giác

### a) Ghi chú đã ẩn danh hoá

**GHI CHU DA AN DANH**

```text
Khán giả [TEN_KHACH],số điện thoại [SO_DIEN_THOAI],số CCCD [SO_DINH_DANH_CA_NHAN],email [TEN_EMAIL],đặt 3 vé gói SVT trận bán kết Cúp Sao Vàng ngày 18/12/2026 cho 2 người lớn và 1 trẻ em 9 tuổi. Khán giả đã chuyển khoản đặt cọc 1.500.000 đồng. Khán giả yêu cầu 3 ghế ngồi cạnh nhau gần lối đi.
```

### b) Hai câu lệnh chống ảo giác

**CAU LENH**

```text
Câu 1: Dựa trên file chính sách hoàn/hủy vé mà tôi gửi hãy trả lời câu hỏi trên của tôi.Nếu các thông tin không có trong chính sách thì không được bịa mà trả lời rằng điều khoản này không tồn tại.
Câu 2:Khi bạn trả lời cho tôi thì bạn trả lời theo mục nào và điều khoản nào trong file 
```

## 4.2. Trích xuất tin nhắn đặt vé ra JSON

**PROMPT**

```text
[CONTEXT]:Bạn một chuyên gia tư vấn khách hàng , bạn có nhiệm vụ chuyển các tin nhắn thành định dạng JSON
[REQUETS]:Bạn hãy chuyển TN1, TN2, TN3 trong thẻ <tin_nhan> thành một mảng JSON 3 đối tượng, đúng thứ tự, đúng 6 trường như tin nhắn mẫu.
Đúng 6 trường lớn như sau:"ma_goi","VIP", "ngay_su_kien","nguoi_lon", "tre_em", "loai_ve"
[EXPLANTION]: Khi chuyển hóa thành JSON bạn cần bám theo quy tắc chuẩn hóa trong thẻ <quy_chuan> .Bạn có thể xem qua 2 ví dụ mẫu
<quy_chuan>
    BẢNG MÃ GÓI
    SVT – Sân Vận Động: vé trận đấu
    FZ – Fan Zone: khu cổ vũ
    VIP – Khán đài VIP
    QUY TẮC CHUẨN HOÁ (5 quy tắc)
    1. ma_goi lấy theo bảng mã gói.
    2. ngay_su_kien dạng YYYY-MM-DD; tin nhắn không ghi năm thì lấy năm 2026; không có ngày cụ thể thì null.
    3. Khách không nhắc trẻ em thì tre_em là 0 và mọi khách là người lớn.
    4. loai_ve chỉ nhận "thuong", "vip" hoặc null.
    5. ghi_chu chỉ ghi yêu cầu đặc biệt về chỗ ngồi, hỗ trợ di chuyển hoặc ăn uống; không có thì null.
    Câu trả lời không chào hỏi dài dòng không giải thích.
</quy_chuan>
<vi_du>
    Tin nhắn mẫu 1:
    Đặt giúp mình 2 vé VIP trận chung kết ngày 15/11/2026, 2 người lớn và 1 bé. Cần chỗ ngồi cạnh lối đi.
    Kết quả đúng:
    {"ma_goi": "VIP", "ngay_su_kien": "2026-11-15", "nguoi_lon": 2, "tre_em": 1, "loai_ve": "vip", "ghi_chu": "chỗ ngồi cạnh lối đi"}

    Tin nhắn mẫu 2:
    Cho mình một vé Fan Zone, ngày nào cũng được, mình đi một mình.
    Kết quả đúng:
    {"ma_goi": "FZ", "ngay_su_kien": null, "nguoi_lon": 1, "tre_em": 0, "loai_ve": "thuong", "ghi_chu": null}
</vi_du>
<tin_nhan>
TN1: Mình muốn đặt gói Sân Vận Động trận tứ kết ngày 20/12 nha, 2 người lớn với 1 bé 8 tuổi, vé thường.

TN2: Cho 3 người đi Fan Zone trận ngày 05/01/2027 ạ. Một người cần hỗ trợ xe lăn.

TN3: Trận chung kết Cúp Sao Vàng tháng 12 còn vé không ạ? Nhà em 4 người lớn, có một người khiếm thị cần hỗ trợ tìm chỗ, lấy vé VIP.
</tin_nhan>


[ACTION]:Đọc dữ liệu tin nhắn của khách hàng mà tôi đưa ra, sau đó chuẩn hóa về đúng các trường dữ liệu rồi trả đúng về định dạng JSON.
[TONE]:Giọng điệu nghiêm túc , chuyên nghiệp , lịch sự , ngắn gọn dễ hiểu 
[EXTRA] Định dạng dữ liệu đầu ra là định dạng JSON 


```

## 4.3. Báo giá vé bằng Chain-of-Thought

### a) Prompt

**PROMPT**

```text
Bạn là một chuyên gia soát vé , hãy đọc thẻ <bang_gia> và tính tổng tiền cho yêu cầu báo giá 
<bang_gia>
BẢNG GIÁ VÉ (đồng/người lớn)
SVT – Sân Vận Động: 1.200.000
FZ – Fan Zone: 800.000
VIP – Khán đài VIP: 2.500.000
</bang_gia>
<quy_chuan>
QUY TẮC TÍNH GIÁ
1. Trẻ em từ 5 đến 11 tuổi tính 70% giá người lớn. Trẻ dưới 5 tuổi miễn phí.
2. Nhóm từ 5 người lớn trở lên được giảm 5% trên tiền vé (tiền người lớn + tiền trẻ em).
3. Phụ thu khu ghế ưu tiên: 300.000 đồng/người. Phụ thu không được giảm giá.
4. Tổng tiền = tiền vé sau giảm + phụ thu.
</quy_chuan>
<yeu_cau>
YÊU CẦU BÁO GIÁ
Nhóm cổ động viên đi xem trận bán kết, mua gói SVT, gồm 5 người lớn, 2 trẻ em (8 tuổi và 10 tuổi) và 1 bé 3 tuổi. Có 1 người lớn chọn khu ghế ưu tiên.
 đưa bảng giá, quy tắc và yêu cầu báo giá vào cặp dấu phân tách; yêu cầu suy luận từng bước theo thứ tự tiền người lớn → tiền trẻ em → tiền vé → giảm giá nhóm → phụ thu → tổng tiền, mỗi bước ghi phép tính; dòng cuối có dạng [RESULT: <tổng tiền> đồng].
</yeu_cau>
```

## 4.4. Dây chuyền xử lý khiếu nại (Prompt Chaining)

### a) Prompt Trạm 1

**PROMPT**

```text
[CONTEXT]:Bạn là nhân viên chăm sóc khách hàng đang đọc email khiếu nại , bạn có nhiệm vụ đọc email, trả về chỉ một đối tượng JSON gồm đúng 4 trường
[REQUETS]:Bạn hãy chuyển Trạm 1 trong thẻ <tram_1> thành một đối tượng JSON gồm đúng 4 trường.
4 trường như sau:"loai_su_co", "so_khach","so_hiep_bi_anh_huong","tom_tat"
[EXPLANTION]: Khi chuyển hóa thành JSON bạn cần bám theo quy tắc chuẩn hóa trong thẻ <chinh_sach> , bạn có thể xem qua ví dụ mẫu.
<chinh_sach>
- tran_gio: trận đấu bắt đầu trễ trên 2 giờ do ban tổ chức: tặng voucher 200.000 đồng/khách.
- sai_khu_vuc: khán giả bị xếp sang khu vực thấp hơn quyền lợi đã cam kết: hoàn 500.000 đồng/khách cho mỗi hiệp bị ảnh hưởng.
- nhan_vien: khiếu nại về thái độ nhân viên: tặng voucher 300.000 đồng/khách.
- khac: chuyển bộ phận Chăm sóc khán giả xem xét, chưa đề xuất mức đền bù.
- Tổng mức đền bù trên 1.500.000 đồng phải được Trưởng ban Chăm sóc khán giả duyệt trước khi gửi khách.
</chinh_sach>
<vi_du>
Trạm 1 – đọc email, trả về chỉ một đối tượng JSON gồm đúng 4 trường:
{"loai_su_co": một trong"loai_su_co" | "sai_khu_vuc" | "nhan_vien" | "khac", "so_khach": số nguyên, "so_hiep_bi_anh_huong": số nguyên hoặc null, "tom_tat": "không quá 20 từ"}
</vi_du>
<tin_nhan_khieu_nai>
Tôi là khán giả mua vé gói SVT trận Cúp Sao Vàng ngày 02/11/2026, đi 2 người lớn. Ban tổ chức cam kết khu khán đài có mái che nhưng trong 2 hiệp đầu chúng tôi bị xếp sang khu không mái, trời mưa và ghế ướt. Nhân viên soát vé rất nhiệt tình, tôi không có gì phàn nàn về nhân viên. Tôi đề nghị ban tổ chức giải quyết thỏa đáng.
</tin_nhan_khieu_nai>
[ACTION]:Đọc dữ liệu tin nhắn khiếu nại của khách hàng mà tôi đưa ra, sau đó chuẩn hóa về đúng các trường dữ liệu rồi trả đúng về định dạng JSON.
[TONE]:Giọng điệu nghiêm túc , chuyên nghiệp , lịch sự , ngắn gọn dễ hiểu 
[EXTRA] Định dạng dữ liệu đầu ra là định dạng JSON


```

### b) Hai điều cần kiểm tra ở JSON đầu ra của Trạm 1

1. Đúng định dạng JSON

2. Kiểm tra lại các chính sách

### c) Câu lệnh viết tiếp

**CAU LENH**

```text
Bạn đang dừng ở chỗ " …Ban tổ chức Cúp Sao Vàng xin hoàn lại Quý khán giả khoản" hãy viết tiếp
```
