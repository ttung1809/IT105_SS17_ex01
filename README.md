Bài này có **2 việc tách biệt**:

1. Đặt đúng nội dung vào 3 chương của IEEE 830.
2. Sửa REQ-02 và REQ-03 để đạt **Complete + Verifiable**.

## Bước 1 — Xác định vị trí IEEE 830

| Nội dung                                              | Vị trí đề xuất                                              | Đúng/Sai — vị trí đúng nếu sai                                                                             |
| ----------------------------------------------------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Mục A** — định nghĩa “Giỏ hàng”                     | 3.2 Functional Requirements                                 | ❌ **Sai** — đúng là **Chương 1 — Introduction, mục Definitions / Definitions, Acronyms and Abbreviations** |
| **Mục B** — 3 yêu cầu chức năng                       | 3.2 Functional Requirements                                 | ✅ **Đúng**                                                                                                 |
| **Danh sách Actor/Use Case tổng thể**                 | **2.2 Product Functions** / Overall Description             | —                                                                                                          |
| **Sequence Diagram áp mã giảm giá** — minh họa REQ-02 | **3.2 Functional Requirements**, đặt kèm/phụ trợ cho REQ-02 | —                                                                                                          |

### Vì sao?

* **Mục A** là *định nghĩa thuật ngữ*, không phải hành vi hệ thống → không được nhét vào Functional Requirements.
* **Actor + Use Case tổng thể** mô tả hệ thống ở mức overview → thuộc **Overall Description (Chương 2)**.
* **Sequence Diagram áp mã giảm giá** mô tả chi tiết cách một chức năng diễn ra → gắn với **Specific Requirements (Chương 3)**, cụ thể là REQ-02.

> Lưu ý: IEEE 830-1998 có thể được tổ chức thành các mục con khác nhau tùy template. Quan trọng là phân biệt **định nghĩa/overview** với **specific functional requirements**.

---

# Bước 2 — Chuẩn hóa yêu cầu

## REQ-02

Yêu cầu gốc:

> “Khách hàng nhập mã giảm giá hợp lệ thì hệ thống trừ đúng số tiền tương ứng vào tổng hóa đơn.”

### Đặc tính vi phạm: **Complete**

Nó mới mô tả **mã hợp lệ**, nhưng bỏ mất tình huống:

* mã không tồn tại;
* mã hết hạn;
* mã không đủ điều kiện;
* mã không hợp lệ.

Nếu chỉ viết trường hợp thành công thì đặc tả chưa đầy đủ.

### Viết lại

**REQ-02:** Khi khách hàng nhập mã giảm giá, hệ thống phải kiểm tra tính hợp lệ của mã. Nếu mã hợp lệ và còn hiệu lực, hệ thống phải áp dụng mức giảm tương ứng và cập nhật tổng hóa đơn; nếu mã không tồn tại, không hợp lệ hoặc đã hết hạn, hệ thống không áp dụng giảm giá và phải hiển thị thông báo lỗi tương ứng.

Cái này tốt hơn vì đã có **cả success case + failure case**.

---

## REQ-03

Yêu cầu gốc:

> “Hệ thống phải xử lý thanh toán một cách nhanh chóng và ổn định.”

### Đặc tính vi phạm: **Verifiable**

Hai từ **“nhanh chóng”** và **“ổn định”** là vấn đề.

Thằng QA đọc câu này sẽ hỏi:

> “Nhanh chóng là bao nhiêu giây?”
> “Ổn định là bao nhiêu %?”
> “Test trong điều kiện nào?”

Không có con số → **không thể kiểm thử khách quan**.

### Viết lại

**REQ-03:** Hệ thống phải hoàn tất việc xử lý yêu cầu thanh toán trong thời gian **không quá 3 giây đối với ít nhất 95% số yêu cầu**, trong điều kiện tải tối đa **100 yêu cầu thanh toán đồng thời**.

Câu này có:

* **Thời gian:** ≤ 3 giây
* **Tỷ lệ:** ≥ 95%
* **Điều kiện kiểm thử:** 100 request đồng thời

→ QA có thể dựng test và kết luận **Pass/Fail**.

---

# Đáp án hoàn chỉnh để nộp

| Mã         | Đặc tính vàng bị vi phạm | Viết lại đạt chuẩn                                                                                                                                                                                                                                                                                          |
| ---------- | ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **REQ-02** | **Complete**             | Khi khách hàng nhập mã giảm giá, hệ thống phải kiểm tra tính hợp lệ của mã. Nếu mã hợp lệ và còn hiệu lực, hệ thống phải áp dụng mức giảm tương ứng và cập nhật tổng hóa đơn; nếu mã không tồn tại, không hợp lệ hoặc đã hết hạn, hệ thống không áp dụng giảm giá và phải hiển thị thông báo lỗi tương ứng. |
| **REQ-03** | **Verifiable**           | Hệ thống phải hoàn tất việc xử lý yêu cầu thanh toán trong thời gian **không quá 3 giây đối với ít nhất 95% số yêu cầu**, trong điều kiện tải tối đa **100 yêu cầu thanh toán đồng thời**.                                                                                                                  |

### Chốt logic bài này

```text
CHƯƠNG 1 — INTRODUCTION
└── Definitions
    └── "Giỏ hàng" là gì?

CHƯƠNG 2 — OVERALL DESCRIPTION
└── Product Functions
    └── Actor + Use Case tổng thể

CHƯƠNG 3 — SPECIFIC REQUIREMENTS
└── Functional Requirements
    ├── REQ-01
    ├── REQ-02
    │   └── Sequence Diagram áp mã giảm giá
    └── REQ-03
```

**Điểm dễ nhầm nhất:** Actor/Use Case **không phải Functional Requirement**. Nó mô tả **tổng quan hệ thống**, còn REQ-01/02/03 mới là các yêu cầu cụ thể mà hệ thống phải thực hiện.
