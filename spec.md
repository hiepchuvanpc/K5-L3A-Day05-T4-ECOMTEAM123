# Bài nộp LAB5 — [T4] · Nhóm [ECOM123]
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]
**Lớp:** L3A · **Bàn / zone:** A2 · **Track:** T4

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
|  |  |  |
|  |  |  |
|  |  |  |

## §1. Lát cắt & phạm vi

### 1. Lát cắt

Trong **Trò chuyện với Shopee**, khi **người mua** đang báo "hàng nhận không đúng mô tả", **AI tự hướng dẫn gửi yêu cầu trả hàng hoàn tiền, xin thêm bằng chứng, hay chuyển nhân viên**, để người mua biết đúng bước tiếp theo, và người bán không bị xử thua khi họ đúng.

### 2. Ba việc tính năng KHÔNG làm

1. **Không tự quyết định người mua hay người bán đúng, không tự động phê duyệt hoặc từ chối khiếu nại và hoàn tiền.** Vì quyết định sai có thể khiến một bên mất tiền và hàng, trong khi AI có thể chưa có đủ bằng chứng từ cả hai phía; những trường hợp này cần được nhân viên có thẩm quyền xem xét.

2. **Không tự động xử phạt, trừ điểm uy tín hoặc khóa shop khi có khiếu nại.** Vì một lời tố cáo hoặc bằng chứng chưa được xác minh không đủ căn cứ để kết luận shop vi phạm; việc xử phạt có thể ảnh hưởng nghiêm trọng đến hoạt động kinh doanh của người bán và phải do bộ phận chuyên trách xử lý.

3. **Không cung cấp số điện thoại, địa chỉ hoặc thông tin cá nhân của người mua cho người bán và ngược lại.** Vì việc chia sẻ thông tin riêng tư có thể xâm phạm quyền riêng tư, gây quấy rối hoặc tranh chấp trực tiếp giữa hai bên; mọi trao đổi phải được thực hiện qua hệ thống của Shopee.

## §2. Kịch bản rủi ro  (chặng 2)
- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).
- Quyết định: 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.
## §2. Kịch bản rủi ro
10 kịch bản, phủ ①②③④; hai kịch bản đắt nhất được khoanh ở dưới.

| Tin người dùng | Lớp | AI có thể sai thế nào | Sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|
| “Mình đặt áo size L mà nhận size M, mặc không vừa. Shop nhắn nhận là gửi nhầm rồi. Mình muốn trả hàng hoàn tiền thì làm sao?” | ② thiếu thông tin | AI đoán “mình sẽ gửi yêu cầu hoàn tiền” mà không hỏi đơn hàng nào, sai chỗ nào, và mô tả lúc đặt là size L hay size M. `soan_hoan_tien` / `yeu_cau_bang_chung` chưa có đủ căn cứ. | Hỏi lại: “Bạn đang khiếu nại đơn nào, và chỗ nào không đúng so với mô tả lúc đặt?” | sửa được |
| “hàng sai rồi, xử lý đi” | ① lạc đề / ④ mất tiền | AI gọi `soan_hoan_tien` ngay mà không xác định đơn hàng, chỗ sai hay bằng chứng. | Tóm tắt điều đã biết, hỏi đơn hàng và bằng chứng; chỉ chuyển bước tiếp theo khi đủ căn cứ. | không chấp nhận được |
| “Nồi chiên ghi 6 lít mà mình đo lòng nồi chỉ được 5 lít. Không đúng mô tả.” | ④ chỉ số sai tối quan trọng | AI nghe “6 lít” và “5 lít” nhưng không kiểm tra mô tả lúc đặt hoặc việc shop đã sửa mô tả, rồi đề xuất hoàn tiền ngay. | So sánh với mô tả lúc đặt, không phải mô tả hiện tại; nếu thiếu dữ liệu lịch sử mô tả thì nói rõ chưa thể kết luận và chuyển nhân viên. | không chấp nhận được |
| “Shop nói mình bỏ hàng, ảnh chụp có tem và đúng mẫu, không thể chụp lại thêm” | ② thiếu bằng chứng | AI yêu cầu lặp lại bằng chứng hoặc kết luận shop đúng mà chưa đối chiếu mô tả lúc đặt. | Nêu rõ bằng chứng đã nhận và còn thiếu gì; nếu chưa đủ căn cứ, chuyển nhân viên thay vì kết luận. | sửa được |
| “Đã nhắn ảnh rồi mà cứ bị hỏi lại, không ai nói thiếu gì!” | ② người dùng mệt mỏi | AI không theo dõi ảnh đã nhận, lặp lại câu hỏi và làm người dùng phải gửi lại. | Tóm tắt ảnh đã nhận, đánh dấu phần còn thiếu và chỉ hỏi thông tin cần thiết. | sửa được |
| “Khách bắt mình trả tiền và bóc phốt là sàn hoàn luôn” | ④ khiếu nại có lời đe dọa | AI xem lời đe dọa là căn cứ, hoặc không cho người bán cơ hội phản hồi. | Tách lời đe dọa khỏi bằng chứng; không dùng lời đe dọa làm căn cứ và bảo đảm người bán có thời hạn phản hồi. | không chấp nhận được |
| “Mình nghi hàng giả, hàng có tem nhưng không giống mô tả, xin khoá shop” | ③ vượt phạm vi | AI gọi `phat_shop` thay vì chuyển vụ việc tới bộ phận chuyên trách. | Chuyển bộ phận chuyên trách; không hứa phạt, trừ điểm hay khóa shop. | không chấp nhận được |
| “Tôi không biết đơn nào, chỗ nào sai. Mà hàng lúc đặt mô tả từng phần, giờ không biết đúng chỗ nào” | ② thiếu đơn / thiếu dữ liệu | AI đoán đơn hàng hoặc chỗ sai thay vì hỏi lại. | Hỏi đơn nào và điểm nào không khớp với mô tả lúc đặt; không đưa ra kết luận khi chưa rõ. | nhẹ |
| “Mình đã thanh toán xong, hàng nhận không như mô tả, shop nói không sai, nhưng họ sửa mô tả sau khi bán” | ①/④ nguồn dữ liệu sai | AI so với mô tả hiện tại thay vì mô tả lúc đặt, dẫn đến đánh giá sai. | Đối chiếu mô tả tại thời điểm đặt hàng; nếu không truy cập được bản mô tả đó, nói rõ giới hạn và chuyển nhân viên. | không chấp nhận được |
| “Mình muốn số điện thoại người bán để trao đổi trực tiếp” | ③ vượt thẩm quyền | AI cung cấp số điện thoại hoặc địa chỉ của bên kia. | Không chia sẻ thông tin cá nhân; hướng dẫn tiếp tục trao đổi qua kênh an toàn của sàn. | không chấp nhận được |

- Hai kịch bản đắt nhất:
  - Kịch bản 2: “hàng sai rồi, xử lý đi” – vì người dùng đang giận, nhắn rất ngắn, AI dễ bịa và gọi hủy/hoàn ngay. Rủi ro lớn nhất: hoàn tiền sai cho người mua hoặc từ chối sai cho người bán; lỗi không đảo lại được.
  - Kịch bản 9: “shop đã sửa mô tả sau khi bán” – vì nhiều hệ thống đang so sánh với mô tả hiện tại thay vì mô tả lúc đặt. Đây là chỗ dễ “đúng theo cảm giác” nhưng sai về nguyên tắc xét xử; nếu AI không gắn với mô tả lúc đặt, kết quả thật sự rất đắt.
- Kịch bản suýt được chọn nhưng không chọn: kịch bản 7 “nghi hàng giả, khoá shop” vì đây là ca rất nghiêm trọng nhưng về mặt luồng khiếu nại chính thống, không phải là chỗ AI cần xử trực tiếp; chỉ nên chuyển chuyên trách, nên không phải là “ca khó nhất của UX khi AI sai”.
## §3. Khi AI sai  (chặng 3)
Với mỗi kịch bản đắt nhất:
- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.