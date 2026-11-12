# Bài nộp LAB5 — T4 · Thương mại điện tử (Shopee) · Nhóm [Tên Nhóm]

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| [Thành viên 1] | [Mã HV 1] | Dựng prototype, kịch bản demo |
| [Thành viên 2] | [Mã HV 2] | Viết kịch bản rủi ro, phân loại lỗi HAX/PAIR |
| [Thành viên 3] | [Mã HV 3] | Thiết lập mức tự chủ, lập luận cost-of-error |

---

## §1. Lát cắt & phạm vi

### 1.1 Lát cắt (từ Track 4)
Trong **Trò chuyện với Shopee**, khi **người mua** đang báo "hàng nhận không đúng mô tả", **AI tự hướng dẫn gửi yêu cầu trả hàng hoàn tiền, xin thêm bằng chứng, hay chuyển nhân viên**, để người mua biết đúng bước tiếp theo, và người bán không bị xử thua khi họ đúng.

### 1.2 Ba việc tính năng KHÔNG LÀM
1. **Không tự ý can thiệp xử phạt hoặc khóa shop (`phat_shop`):** Việc trừ điểm sao quả tạ hay khóa shop thuộc thẩm quyền của bộ phận kiểm soát gian lận độc lập; trợ lý khiếu nại đơn lẻ không được đe dọa hay áp đặt chế tài này.
2. **Không chia sẻ thông tin liên lạc cá nhân giữa người mua và người bán:** Tuyệt đối không cung cấp SĐT, địa chỉ riêng hay tài khoản ngân hàng để các bên tự giải quyết ngoài sàn, nhằm ngăn chặn quấy rối và đảm bảo giao dịch được bảo hộ.
3. **Không tự động phán quyết hoàn tiền ngay lập tức khi chưa có đối chứng 2 chiều:** Khiếu nại sai mô tả luôn cần bằng chứng đối chiếu (ảnh/video đóng - mở hàng, tem nhãn). AI không được hoàn tiền chỉ dựa trên lời khai 1 chiều của người mua.

---

## §2. Kịch bản rủi ro (chặng 2)

### 2.1 Bảng 3 kịch bản rủi ro đã chọn

| # | Tin người dùng nhắn | Lớp chỗ khó | AI có thể sai thế nào | Một sản phẩm tốt nên làm gì | Nhãn mức hại |
|---|---|:---:|---|---|:---:|
| **KB3** | *"Nồi chiên ghi 6 lít mà mình đo lòng nồi chỉ được 5 lít. Không đúng mô tả."* | ① Nguồn sự thật | AI chỉ đọc mô tả sản phẩm hiện tại (lỡ khách hàng đặt nhầm phiên bản 5L), phải đối chiếu với đơn hàng của khách. | Truy xuất **Snapshot chi tiết đơn hàng lúc đặt** để xem khách đặt phân loại 5L hay 6L:<br>- Nếu khách chọn 5L: Chỉ rõ cho khách thấy họ đã đặt phiên bản 5L.<br>- Nếu khách đặt 6L mà lòng nồi 5L: Yêu cầu khách gửi ảnh chụp thước đo lòng nồi làm căn cứ đối soát. | Sửa được |
| **KB4** | *"Mình đặt áo size L mà nhận được size M, mặc không vừa. Shop cũng nhắn nhận là gửi nhầm rồi. Mình muốn trả hàng hoàn tiền thì làm sao?"* | ① Nguồn sự thật | AI vội tin lời khách và tự động gọi `soan_hoan_tien` ngay lập tức khi chưa có ảnh chụp tin nhắn xác nhận của shop hoặc mã vận đơn hoàn trả hàng. | Hướng dẫn tạo yêu cầu Trả hàng - Hoàn tiền; yêu cầu đính kèm ảnh chụp màn hình tin nhắn shop thừa nhận gửi nhầm để đưa vào diện xét duyệt nhanh; cấp mã gửi trả hàng. | Sửa được |
| **KB11** | *"Hàng đúng là mẫu tôi đặt, nhưng hộp méo mó rách nát hết, sản phẩm bên trong xước xát như đồ cũ đã qua sử dụng. Shop bán đồ cũ lừa khách à?"* | ④ Đặc thù domain | AI có thể gắn nhãn "sai mô tả" cho shop mặc dù lỗi có thể do đơn vị vận chuyển, tự động mở tranh chấp giữa Khách và Shop. | Đối chiếu ảnh/video lúc shop gửi hàng, lúc shipper giao hàng và lúc khách mở hàng. Xác định chính xác lỗi do Đơn vị vận chuyển (để bảo hiểm bồi thường), do shop (giao đồ cũ) hay do khách. | **Không chấp nhận được** |

### 2.2 Quyết định: 2 kịch bản đắt nhất

1. **KB11 (Lỗi vận chuyển vs Sai mô tả - Tranh chấp 3 bên):**
   - **Vì sao đắt nhất:** Nếu AI gán nhầm nhãn "Sai mô tả", Shop bị quy trách nhiệm oan, bị phạt sao quả tạ và mất tiền hàng, trong khi Đơn vị vận chuyển (bên trực tiếp làm hỏng hàng) thoát trách nhiệm bồi thường bảo hiểm. Đây là lỗi **sai bản chất sự việc**, tiền đã xuất thì không đòi lại được từ shipper.
2. **KB3 (Sai lệch dung tích - Đối soát Snapshot đơn hàng):**
   - **Vì sao đắt nhì:** Nếu AI chỉ đọc mô tả hiện tại mà bỏ qua Snapshot đơn hàng của khách, AI sẽ phán quyết sai: hoặc hoàn tiền oan của shop (khi khách mua nhầm bản 5L), hoặc bác bỏ khiếu nại chính đáng của khách (khi shop sửa lại bài viết sau khi bán).
- **Kịch bản suýt được chọn:** **KB4 (Shop đã thừa nhận trong chat):** Bị loại khỏi top 2 vì kịch bản này hai bên đã có sự đồng thuận sơ bộ, rủi ro thấp hơn nhiều so với việc tranh chấp 3 bên (KB11) hoặc sai lệch thông số kỹ thuật (KB3).

---

## §3. Khi AI sai (chặng 3)
*(Sẽ thực hiện tiếp ở chặng 3)*

## §4. Mức tự chủ (chặng 4)
*(Sẽ thực hiện tiếp ở chặng 4)*

## §5. Prototype (chặng 5)
*(Sẽ thực hiện tiếp ở chặng 5)*

## §6. Tốt là gì (chặng 6)
*(Sẽ thực hiện tiếp ở chặng 6)*

## §7. Demo
*(Sẽ thực hiện tiếp ở phần demo)*
