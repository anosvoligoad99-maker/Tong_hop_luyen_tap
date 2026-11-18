## 4.2. Trích xuất tin nhắn đặt vé ra JSON

**KET QUA AI**

```text
[
  {
    "ma_goi": "SVD",
    "VIP": false,
    "ngay_su_kien": "2026-12-20",
    "nguoi_lon": 2,
    "tre_em": 1,
    "loai_ve": "thuong"
  },
  {
    "ma_goi": "FZ",
    "VIP": false,
    "ngay_su_kien": "2027-01-05",
    "nguoi_lon": 3,
    "tre_em": 0,
    "loai_ve": "thuong"
  },
  {
    "ma_goi": "CSV",
    "VIP": true,
    "ngay_su_kien": "2026-12-01",
    "nguoi_lon": 4,
    "tre_em": 0,
    "loai_ve": "vip"
  }
]
```

**Link trò chuyện:https://share.gemini.google/sbHajCZtPI5E**

## 4.3. Báo giá vé bằng Chain-of-Thought

**KET QUA AI**

```text
<bang_gia>
BẢNG GIÁ VÉ (đồng/người lớn)
SVT – Sân Vận Động: 1.200.000
FZ – Fan Zone: 800.000
VIP – Khán đài VIP: 2.500.000
</bang_gia><quy_chuan>
QUY TẮC TÍNH GIÁTrẻ em từ 5 đến 11 tuổi tính 70% giá người lớn. Trẻ dưới 5 tuổi miễn phí.Nhóm từ 5 người lớn trở lên được giảm 5% trên tiền vé (tiền người lớn + tiền trẻ em).Phụ thu khu ghế ưu tiên: 300.000 đồng/người. Phụ thu không được giảm giá.Tổng tiền = tiền vé sau giảm + phụ thu.
</quy_chuan><yeu_cau>
YÊU CẦU BÁO GIÁ
Nhóm cổ động viên đi xem trận bán kết, mua gói SVT, gồm 5 người lớn, 2 trẻ em (8 tuổi và 10 tuổi) và 1 bé 3 tuổi. Có 1 người lớn chọn khu ghế ưu tiên.
</yeu_cau>Chi tiết các bước tính giá véTiền người lớn:Số lượng người lớn: 5 ngườiGiá vé SVT người lớn: 1.200.000 đồng/ngườiPhép tính: $5 \times 1.200.000 = 6.000.000$ đồngTiền trẻ em:Trẻ 8 tuổi và 10 tuổi (từ 5 đến 11 tuổi): 2 trẻ, tính 70% giá người lớn ($1.200.000 \times 70\% = 840.000$ đồng/trẻ)Phép tính: $2 \times 840.000 = 1.680.000$ đồngTrẻ 3 tuổi (dưới 5 tuổi): 1 trẻ, miễn phí ($0$ đồng)Tổng tiền trẻ em: $1.680.000 + 0 = 1.680.000$ đồngTiền vé (trước giảm giá):Phép tính: $6.000.000 + 1.680.000 = 7.680.000$ đồngGiảm giá nhóm:Nhóm có 5 người lớn (đạt điều kiện từ 5 người lớn trở lên, được giảm 5% trên tổng tiền vé)Phép tính giảm giá: $7.680.000 \times 5\% = 384.000$ đồngTiền vé sau giảm: $7.680.000 - 384.000 = 7.296.000$ đồngPhụ thu:Có 1 người lớn chọn khu ghế ưu tiên, mức phụ thu 300.000 đồng/ngườiPhép tính: $1 \times 300.000 = 300.000$ đồngTổng tiền:Phép tính: $7.296.000 + 300.000 = 7.596.000$ đồng[RESULT: 7.596.000 đồng]
```

**Link trò chuyện:https://share.gemini.google/vzqHPbLEsekC**

### b) Kiểm tra kết quả AI
Kết quả cuối cùng do AI đưa ra không có sai sót hay lỗi ở đâu


## 4.4. Dây chuyền xử lý khiếu nại – kết quả Trạm 1

**KET QUA AI**

```text
{
  "loai_su_co": "sai_khu_vuc",
  "so_khach": 2,
  "so_hiep_bi_anh_huong": 2,
  "tom_tat": "Khán giả bị xếp sang khu không mái che trong 2 hiệp đầu, yêu cầu đền bù."
}
```

**Link trò chuyện:https://share.gemini.google/Sca8j4vVokcP**
