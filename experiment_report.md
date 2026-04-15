# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 26ai.vinhkq@vinuni.edu.vn
**Name:** Khương Quang Vinh
**Date:** 15/04

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| Clean Data (`processed_data.csv`) | Based on my data, the best choice is Laptop at $1200 | 9 | Du lieu sach, gia va category hop le |
| Garbage Data (`garbage_data.csv`) | Based on my data, the best choice is Nuclear Reactor at $999999. | 2 | Outlier khong bi loai nen Agent tra loi sai |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

Trong file garbage_data.csv, có 4 vấn đề chính gây ra kết quả sai:

Duplicate ID (Trùng lặp mã định danh) — Bản ghi id=1 xuất hiện 2 lần (Laptop và Banana). Điều này khiến Agent có thể xử lý trùng lặp dữ liệu, dẫn đến thống kê sai về số lượng sản phẩm.

Wrong data type (Sai định dạng dữ liệu) — Bản ghi "Broken Chair" có price = 'ten dollars' (chuỗi ký tự thay vì số). Khi Agent cố gắng so sánh hoặc tính toán với giá trị này, nó sẽ bị lỗi hoặc tự động bỏ qua bản ghi, làm mất đi dữ liệu quan trọng.

Extreme Outlier (Giá trị ngoại lai cực đoan) — "Nuclear Reactor" có giá $999,999. Vì Agent chọn sản phẩm có price cao nhất trong nhóm electronics, nó đã chọn Nuclear Reactor thay vì Laptop, dù đây là mức giá phi thực tế. Giá trị ngoại lai này đã làm "độc" kết quả của Agent.

Null values (Giá trị rỗng) — Bản ghi "Ghost Item" có id = None và category = None. Agent không thể phân loại sản phẩm này và các giá trị null có thể gây lỗi khi thực hiện các phép tính toán.

Tóm lại: Vì dữ liệu rác (garbage data) không bước qua khâu kiểm chứng (validate) và làm sạch (clean), Agent đã nhận dữ liệu rác và cho ra kết quả hoàn toàn sai lệch so với thực tế.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Dong y.

Dù prompt có được viết rõ ràng và chính xác đến đâu, nếu dữ liệu đầu vào bị lỗi (outlier, null, wrong type, duplicate), Agent vẫn sẽ trả ra kết quả sai. Thí nghiệm này đã chứng minh một thực tế khách quan:

Bước ETL (Extract - Transform - Load): Đặc biệt là khâu Validate (Kiểm chứng) và Clean (Làm sạch), không phải là một tùy chọn thêm thắt mà là yêu cầu bắt buộc trong bất kỳ pipeline AI nào.

Nguyên tắc "Garbage in, garbage out". Khi Agent phải làm việc với dữ liệu "nhiễu", khả năng suy luận logic của nó không những không phát huy được tác dụng mà còn có thể khuếch đại sai số, dẫn đến những quyết định sai lầm 