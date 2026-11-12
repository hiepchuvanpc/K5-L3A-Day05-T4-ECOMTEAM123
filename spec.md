# Bài nộp LAB5 — [T4] · Nhóm [ECOM123]
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]
**Lớp:** L3A · **Bàn / zone:** A2 · **Track:** T4

| Họ và Tên | Mã Học Viên | Việc đã làm |
|---|---|---|
| Nguyễn Tiến Khoa| 2A202603460 |  |
| |  |  |
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

## 3.1. Kịch bản đắt nhất #2: Người mua yêu cầu xử lý nhưng chưa cung cấp đủ thông tin

### Tình huống

Người mua nhắn: “Hàng sai rồi, xử lý đi”.

AI có thể hiểu nhầm rằng người mua đã cung cấp đủ căn cứ và gọi tool `soan_hoan_tien` ngay lập tức. Điều này có thể dẫn đến yêu cầu hoàn tiền sai đơn hàng hoặc gây thiệt hại cho người bán khi chưa xác minh vấn đề.

### Cách xử lý đề xuất

**Phương án được chọn: Hỏi lại (Clarification).**

AI không được tự động tạo yêu cầu hoàn tiền khi chưa xác định được đơn hàng và vấn đề cụ thể. Thay vào đó, AI cần hỏi người mua để thu thập thông tin còn thiếu.

**Câu trả lời mẫu của AI:**

> Mình có thể hỗ trợ bạn kiểm tra và xử lý vấn đề này. Bạn cho mình biết đơn hàng nào đang gặp sự cố và sản phẩm nhận được không đúng ở điểm nào nhé?
>
> Nếu có thể, bạn gửi thêm ảnh sản phẩm hoặc thông tin mô tả sản phẩm tại thời điểm đặt hàng để mình kiểm tra chính xác hơn. Hiện tại mình chưa gửi yêu cầu hoàn tiền vì chưa đủ thông tin để xác minh.

### Người dùng nhìn thấy gì?

- AI thông báo rõ thông tin nào còn thiếu.
- Người mua biết cần cung cấp đơn hàng, mô tả vấn đề hoặc bằng chứng gì.
- Chưa có yêu cầu hoàn tiền nào được gửi đi.
- Người mua không bị hiểu nhầm rằng yêu cầu đã được xử lý thành công.

### Các bước tiếp theo

1. AI xác định đơn hàng mà người mua đang đề cập.
2. AI hỏi rõ điểm khác biệt giữa sản phẩm nhận được và mô tả khi đặt hàng.
3. AI tiếp nhận và kiểm tra bằng chứng người mua cung cấp.
4. AI tóm tắt thông tin đã xác minh để người mua kiểm tra lại.
5. Khi có đủ căn cứ, AI mới hướng dẫn người mua tạo yêu cầu trả hàng hoàn tiền.
6. Nếu không thể xác định đơn hàng hoặc vấn đề vẫn chưa rõ, AI chuyển trường hợp cho nhân viên hỗ trợ.

### Ai được thông báo?

- **Người mua:** Được thông báo về thông tin còn thiếu và bước cần thực hiện.
- **Người bán:** Chỉ được thông báo khi vụ việc đã được xác định và cần phản hồi theo quy trình.
- **Nhân viên hỗ trợ:** Được chuyển trường hợp khi AI không thể xác minh hoặc xử lý an toàn.

AI không tự cam kết thời gian xử lý nếu chưa có SLA chính thức từ hệ thống.

### Vì sao chọn hỏi lại?

- **Không chọn trả lời kèm giới hạn:** Vì AI chưa biết đơn hàng nào và vấn đề cụ thể là gì.
- **Không chuyển nhân viên ngay:** Vì đây có thể chỉ là trường hợp thiếu thông tin, người mua có thể bổ sung nhanh chóng.
- **Không gọi `soan_hoan_tien`:** Vì chưa có đủ căn cứ để tạo yêu cầu hoàn tiền.

### Phân loại nguyên nhân AI có thể sai

- **Lỗi ngữ cảnh:** Tin nhắn quá ngắn, thiếu thông tin về đơn hàng và vấn đề.
- **Lỗi hệ thống:** Nếu hệ thống cho phép AI gọi tool hoàn tiền ngay cả khi chưa đủ dữ liệu đầu vào.

### Nguyên tắc HAX/PAIR được áp dụng

- **HAX G10 – Thu hẹp hành động khi có sự không chắc chắn:** AI phải hỏi lại thay vì tự suy đoán và thực hiện hành động có ảnh hưởng đến quyền lợi.
- **HAX G2 – Làm rõ khả năng của AI:** AI cần nói rõ mình chưa đủ thông tin để xác minh, tránh tạo cảm giác rằng vấn đề đã được xử lý.
- **PAIR – Feedback & Control:** Người mua được bổ sung thông tin và kiểm soát bước tiếp theo trước khi hệ thống thực hiện hành động.

### Vì sao sửa câu chữ chưa đủ?

Nếu chỉ sửa câu trả lời của AI thành “Bạn vui lòng cung cấp thêm thông tin”, hệ thống vẫn có thể gọi tool hoàn tiền ở phía sau.

Do đó, cần có cơ chế kiểm soát ở cấp hệ thống:

- Không cho phép gọi `soan_hoan_tien` khi chưa xác định được đơn hàng.
- Kiểm tra các trường thông tin bắt buộc trước khi thực hiện hành động.
- Yêu cầu AI hỏi lại nếu thiếu dữ liệu.
- Ghi nhận trạng thái bằng chứng đã nhận để tránh hỏi người mua lặp lại.

---

## 3.2. Kịch bản đắt nhất #9: Người bán đã sửa mô tả sản phẩm sau khi người mua đặt hàng

### Tình huống

Người mua phản ánh sản phẩm nhận được không đúng mô tả và cho biết người bán đã sửa nội dung mô tả sau khi đơn hàng được đặt.

AI có thể mắc lỗi khi chỉ đối chiếu sản phẩm thực tế với mô tả hiện tại trên Shopee. Nếu mô tả đã bị thay đổi, AI có thể kết luận sai rằng người bán không vi phạm, dù sản phẩm tại thời điểm đặt hàng thực sự không đúng mô tả.

### Cách xử lý đề xuất

**Phương án được chọn: Trả lời kèm giới hạn (Answer with limits).**

AI cần giải thích rõ rằng việc xác minh phải dựa trên mô tả sản phẩm tại thời điểm người mua đặt hàng, không phải nội dung hiện tại.

**Câu trả lời mẫu của AI:**

> Mình sẽ kiểm tra thông tin mô tả sản phẩm tại thời điểm bạn đặt hàng để đối chiếu với sản phẩm đã nhận.
>
> Nội dung mô tả hiện tại có thể đã thay đổi, vì vậy mình chưa thể kết luận chỉ dựa trên thông tin đang hiển thị.
>
> Mình sẽ kiểm tra lịch sử thông tin sản phẩm và các bằng chứng liên quan. Nếu hệ thống không có dữ liệu lịch sử hoặc chưa đủ căn cứ xác minh, mình sẽ chuyển trường hợp này đến nhân viên hỗ trợ để kiểm tra thêm.

### Người dùng nhìn thấy gì?

- AI giải thích rõ thông tin nào sẽ được dùng để xác minh.
- Người mua biết rằng mô tả hiện tại không phải căn cứ duy nhất để kết luận.
- Người mua được thông báo nếu hệ thống không truy xuất được lịch sử mô tả.
- AI không vội kết luận người mua hoặc người bán đúng khi chưa đủ bằng chứng.

### Các bước tiếp theo

1. AI xác định sản phẩm và đơn hàng đang bị khiếu nại.
2. Hệ thống truy xuất mô tả sản phẩm tại thời điểm người mua đặt hàng.
3. AI đối chiếu mô tả lịch sử với sản phẩm thực tế và bằng chứng của hai bên.
4. AI tóm tắt những điểm đã xác minh và những thông tin còn thiếu.
5. Nếu dữ liệu lịch sử đầy đủ, AI hướng dẫn bước xử lý tiếp theo theo quy trình.
6. Nếu không có lịch sử mô tả hoặc không đủ căn cứ, AI chuyển trường hợp cho nhân viên hỗ trợ.

### Ai được thông báo?

- **Người mua:** Được thông báo về quá trình xác minh và kết quả kiểm tra.
- **Người bán:** Được thông báo khi cần cung cấp thông tin hoặc phản hồi về nội dung khiếu nại.
- **Nhân viên hỗ trợ:** Nhận trường hợp khi dữ liệu lịch sử không có hoặc không đủ để đưa ra kết luận.

Thời gian xử lý cần tuân theo SLA thực tế của Shopee. AI không tự đưa ra thời hạn khi chưa có thông tin chính thức.

### Vì sao chọn trả lời kèm giới hạn?

- **Không tự động kết luận:** Vì mô tả hiện tại có thể khác mô tả tại thời điểm đặt hàng.
- **Không chỉ yêu cầu người mua gửi thêm ảnh:** Vì ảnh sản phẩm không thể thay thế dữ liệu lịch sử mô tả.
- **Không tự động hoàn tiền hoặc bác khiếu nại:** Vì cần đối chiếu thông tin lịch sử trước khi đưa ra kết luận.
- **Chuyển nhân viên khi cần thiết:** Nếu hệ thống không có dữ liệu lịch sử hoặc không thể xác minh đáng tin cậy.

### Phân loại nguyên nhân AI có thể sai

- **Lỗi hệ thống:** Không lưu hoặc không truy xuất được lịch sử mô tả sản phẩm theo thời điểm.
- **Lỗi ngữ cảnh:** AI không phân biệt mô tả hiện tại với mô tả tại thời điểm đặt hàng.

### Nguyên tắc HAX/PAIR được áp dụng

- **HAX G2 – Làm rõ khả năng của AI:** AI phải nói rõ dữ liệu nào có thể và chưa thể kiểm tra.
- **HAX G11 – Giải thích căn cứ:** AI cần cho người mua biết kết luận dựa trên dữ liệu lịch sử nào, thay vì chỉ đưa ra kết quả.
- **PAIR – Explainability:** Quá trình đối chiếu và căn cứ xác minh cần được trình bày minh bạch để người mua và người bán hiểu vì sao có kết quả đó.

### Vì sao sửa câu chữ chưa đủ?

Nếu chỉ yêu cầu AI nói “Tôi sẽ kiểm tra mô tả lúc đặt hàng”, nhưng hệ thống không lưu hoặc không truy xuất được dữ liệu lịch sử, AI vẫn có thể đưa ra kết luận sai.

Do đó, cần thay đổi ở cấp hệ thống:

- Lưu phiên bản mô tả sản phẩm tại thời điểm phát sinh đơn hàng.
- Cho phép truy xuất lịch sử chỉnh sửa mô tả.
- Ghi nhận thời điểm thay đổi nội dung sản phẩm.
- Không cho phép AI kết luận tự động nếu thiếu dữ liệu lịch sử cần thiết.
- Chuyển nhân viên hỗ trợ khi không thể xác minh bằng dữ liệu đáng tin cậy.

---

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
