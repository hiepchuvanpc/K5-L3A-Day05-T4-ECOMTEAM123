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

### 4.1. Phân mức tự chủ cho từng Tool & Lập luận Cost-of-Error

Dựa trên nguyên tắc không tự ý phán quyết và không tự động hoàn tiền/xử phạt đã chốt ở §1, nhóm phân định mức tự chủ cho 5 tool như sau:

#### 1. `yeu_cau_bang_chung` (Gửi mẫu xin bằng chứng cho người mua hoặc người bán)
- **Mức tự chủ của nhóm:** **Tự làm (Autonomous)**.
- **Lý do theo Cost-of-Error:**
  - *Sai thì ai chịu gì, đảo lại được không:* Nếu AI gửi nhầm mẫu yêu cầu bằng chứng (hoặc gửi thừa), người nhận chỉ mất công đọc hoặc bỏ qua; hệ thống có thể đảo ngược dễ dàng bằng cách gửi tin nhắn đính chính hoặc cập nhật form bổ sung mà không gây thiệt hại tài chính.
  - *Chờ người thì mất gì:* Nếu bắt nhân viên duyệt từng tin nhắn yêu cầu gửi ảnh/video, thời gian phản hồi sẽ bị kéo dài nhiều giờ. Người mua đang nóng lòng sẽ cảm thấy bị bỏ rơi, trong khi thời hạn khiếu nại (SLA) của đơn hàng tiếp tục trôi qua.
- **Phương án đã cân nhắc & vì sao loại:** Cân nhắc mức "Cần người duyệt" cho các đơn giá trị cao hoặc các yêu cầu mơ hồ. Loại vì việc thu thập chứng cứ ban đầu ít rủi ro; giữ luồng tự động giúp hồ sơ sẵn sàng sớm nhất cho nhân viên thẩm định.

#### 2. `chuyen_truong_nhom` (Chuyển hồ sơ cho trưởng nhóm / chuyên viên hỗ trợ)
- **Mức tự chủ của nhóm:** **Tự làm (Autonomous)**.
- **Lý do theo Cost-of-Error:**
  - *Sai thì ai chịu gì, đảo lại được không:* Chuyển nhầm hồ sơ chỉ làm tăng tải nhẹ cho nhân viên tiếp nhận; nhân viên hoàn toàn đảo ngược được bằng cách bấm chuyển trả lại cho bot xử lý tự động tiếp. Không có rủi ro mất tiền hay mất hàng.
  - *Chờ người thì mất gì:* Khi AI phát hiện ca vượt thẩm quyền (như KB 7 nghi hàng giả, KB 6 đe dọa bóc phốt, hoặc KB 9 thiếu dữ liệu lịch sử mô tả). Nếu tool này phải chờ duyệt thì hệ thống sẽ bị tắc nghẽn, triệt tiêu khả năng cứu vãn rủi ro kịp thời.
- **Phương án đã cân nhắc & vì sao loại:** Cân nhắc mức "Cần người duyệt". Loại vì mâu thuẫn logic: không thể bắt người duyệt một hành động mà mục đích của nó là đi gọi người hỗ trợ.

#### 3. `soan_hoan_tien` (Hoàn tiền cho người mua)
- **Mức tự chủ của nhóm:** **Cần người duyệt (Human-in-the-loop) — Tách bước**.
- **Quy định khi cần người duyệt:**
  - *Ai duyệt:* Nhân viên xử lý khiếu nại của sàn Shopee (hoặc Người bán xác nhận đồng ý hoàn tiền).
  - *Người duyệt thấy gì:* Tóm tắt hồ sơ đối chiếu (Snapshot mô tả lúc đặt vs Bằng chứng khách gửi), lịch sử chat giữa 2 bên, và trạng thái xác nhận từ đơn vị vận chuyển (đã nhận hàng hoàn trả hay chưa).
  - *Quá hạn thì sao:* Quá thời hạn quy định (24h kể từ khi đủ bằng chứng hoặc người bán không phản hồi đúng hạn), hệ thống tự động đẩy cảnh báo lên trưởng nhóm trực để quyết định.
- **Lý do theo Cost-of-Error:**
  - *Sai thì ai chịu gì, đảo lại được không:* **Rất khó đảo ngược**. Khi tiền đã hoàn vào Ví ShopeePay/tài khoản của người mua, sàn không thể tự ý thu hồi. Nếu hoàn sai (như trường hợp KB 2, hoặc khách gian lận tráo hàng), người bán mất trắng cả tiền lẫn hàng, sàn gánh chịu khiếu kiện bồi thường.
  - *Chờ người thì mất gì:* Người mua phải chờ thêm thời gian thẩm định (12–24h), nhưng đổi lại sự công bằng tuyệt đối cho người bán và tính toàn vẹn tài chính cho sàn.
- **Phương án đã cân nhắc & vì sao loại:** Cân nhắc mức "Tự làm" cho các đơn hàng giá trị nhỏ (< 50.000 VNĐ). Nhóm quyết định loại vì sẽ tạo lỗ hổng gian lận có hệ thống bòn rút ngân sách sàn.

#### 4. `tu_choi_khieu_nai` (Đóng khiếu nại, tiền về người bán)
- **Mức tự chủ của nhóm:** **Cần người duyệt (Human-in-the-loop)**.
- **Quy định khi cần người duyệt:**
  - *Ai duyệt:* Chuyên viên khiếu nại Shopee.
  - *Người duyệt thấy gì:* Bằng chứng đối soát chứng minh người bán đã giao đúng mô tả lúc đặt (tem niêm phong, video đóng hàng, hóa đơn chính hãng) hoặc biên bản xác nhận người mua không cung cấp bằng chứng sau thời hạn gia hạn.
  - *Quá hạn thì sao:* Sau 48h nếu chưa duyệt từ chối, vụ việc được chuyển lên Trưởng nhóm để tránh đóng đơn treo.
- **Lý do theo Cost-of-Error:**
  - *Sai thì ai chịu gì, đảo lại được không:* **Rất khó đảo ngược**. Khi từ chối khiếu nại, hệ thống sẽ giải phóng tiền thanh toán cho người bán. Nếu AI từ chối sai (đặc biệt ở KB 9 khi shop lén sửa mô tả sau bán), người mua bị ép nhận hàng lỗi/hàng rác, niềm tin vào Shopee sụp đổ hoàn toàn.
  - *Chờ người thì mất gì:* Người bán phải chờ giải phóng tiền thêm 24h, nhưng đảm bảo không có quyết định oan sai cho khách.
- **Phương án đã cân nhắc & vì sao loại:** Cân nhắc mức "Tự làm" khi hết hạn gửi ảnh. Loại vì AI không thể đánh giá được các trường hợp bất khả kháng của khách (như app lỗi không upload được ảnh); cần con người thẩm định lần cuối trước khi đóng vĩnh viễn quyền lợi khiếu nại.

#### 5. `phat_shop` (Trừ điểm uy tín, khoá shop)
- **Mức tự chủ của nhóm:** **CẤM (Forbidden)**.
- **Lý do theo Cost-of-Error:**
  - *Sai thì ai chịu gì, đảo lại được không:* Khóa shop hoặc phạt điểm sao quả tạ sẽ làm giảm uy tín thương hiệu và công việc kinh doanh của cả một cửa hàng; khó khôi phục lại niềm tin và khách quen của shop.
  - *Nguy cơ:* Nếu AI có quyền này, kẻ xấu sẽ dùng các kịch bản đe dọa (như KB 6, KB 7) hoặc đánh giá bẩn có tổ chức để ép AI phạt đối thủ cạnh tranh.
- **Phương án đã cân nhắc & vì sao loại:** Cân nhắc "Cần người duyệt". Loại vì đã quy định dứt khoát tại §1 (Ba việc tính năng KHÔNG làm): Trợ lý chat trong luồng khiếu nại đơn lẻ không được tích hợp công cụ chế tài shop; việc xử phạt phải đi qua hệ thống Kiểm soát Tuân thủ & Gian lận độc lập của sàn.

---

### 4.2. Tool khó xếp nhất & Cách nhóm chốt

- **Tool khó xếp nhất:** `soan_hoan_tien`.
- **Quan điểm tranh luận giữa các thành viên:**
  - *Thành viên ủng hộ "Tự làm":* Cho rằng người dùng kỳ vọng trải nghiệm "Hoàn tiền tức thì" (Instant Refund) khi có bằng chứng rõ ràng. Chờ đợi sẽ làm tăng tỷ lệ gọi hotline phàn nàn.
  - *Thành viên ủng hộ "Cần người duyệt":* Dẫn chứng trực tiếp từ **KB 2 ("hàng sai rồi, xử lý đi")** và **KB 9 ("shop sửa mô tả")**: AI chỉ cần hiểu sai ngữ cảnh một lần là tiền bay khỏi hệ thống, người bán bị mất tiền oan không đòi lại được, vi phạm tính trung lập của sàn.
- **Cái giá của mỗi phía:**
  - Cho AI tự làm: Tốc độ tối đa, nhưng cái giá là rủi ro mất tiền và gian lận bùng phát (Cost-of-Error cực lớn).
  - Bắt người duyệt hoàn toàn: An toàn 100%, nhưng tốn chi phí nhân sự và giảm độ hài lòng của khách.
- **Cách nhóm chốt — Tách tool thành 2 bước (Thiết kế cứu nghiệp vụ):**
  - **Bước 1 (AI tự làm):** `soan_de_xuat_hoan_tien` — AI tự động trích xuất thông tin đơn, tính toán số tiền hoàn dựa trên giá trị lúc mua, đính kèm ảnh bằng chứng thành một bản nháp đề xuất (draft proposal).
  - **Bước 2 (Người duyệt):** Chuyên viên khiếu nại (hoặc Người bán) chỉ cần kiểm tra nhanh bản nháp và bấm nút **"Xác nhận phê duyệt hoàn tiền"**.
  - Nhờ tách bước, AI vẫn giải phóng 80% thời gian soạn hồ sơ thủ công cho con người, trong khi quyền chốt dòng tiền vẫn nằm chắc trong tay con người.

---

### 4.3. Thử nghiệm bộ mức tự chủ trên 3 kịch bản

#### 1. Thử trên Kịch bản đắt nhất #2: *"Hàng sai rồi, xử lý đi"* (KB 2 ở §2 & §3.1)
- **Cái sai có bị chặn không?** **Bị chặn hoàn toàn.** Do `soan_hoan_tien` ở mức "Cần người duyệt" và có điều kiện tiên quyết là phải có mã đơn và bằng chứng, AI không thể tự động bấm hoàn tiền khi tin nhắn chỉ có 6 chữ cụt lủn.
- **Có việc nào AI làm khi lẽ ra phải hỏi không?** **Không.** AI chỉ có quyền thực hiện `yeu_cau_bang_chung` (hỏi lại mã đơn và điểm sai), hoàn toàn đúng theo thiết kế tại §3.1.
- **Người dùng bình thường có bị chờ vô ích không?** **Không.** AI trả lời hỏi lại ngay lập tức, không làm chậm trễ luồng xử lý.

#### 2. Thử trên Kịch bản đắt nhất #9: *"Shop đã sửa mô tả sau khi bán"* (KB 9 ở §2 & §3.2)
- **Cái sai có bị chặn không?** **Bị chặn hoàn toàn.** Do `tu_choi_khieu_nai` ở mức "Cần người duyệt", AI bị tước quyền tự đóng khiếu nại. Khi phát hiện dữ liệu mô tả hiện tại bị lệch hoặc không thể truy xuất lịch sử, AI tự động kích hoạt `chuyen_truong_nhom`.
- **Có việc nào AI làm khi lẽ ra phải hỏi không?** **Không.** AI trả lời kèm giới hạn, minh bạch căn cứ và chuyển chuyên viên thẩm định Snapshot đơn hàng.
- **Người dùng bình thường có bị chờ vô ích không?** **Không.** Thời gian chuyển tiếp được thông báo rõ ràng, người mua được giải thích lý do vì sao cần đối chiếu lịch sử thay vì bị từ chối oan.

#### 3. Thử trên 1 Kịch bản bình thường: Kịch bản 1 (*"Mình đặt áo size L mà nhận size M, shop nhắn nhận gửi nhầm..."*)
- **Cách AI vận hành với bộ mức tự chủ:**
  - AI tự làm (`yeu_cau_bang_chung`): Mở form cho khách đính kèm ảnh chụp tin nhắn shop đã nhận sai và ảnh tem mác size M.
  - AI tự làm (`soan_de_xuat_hoan_tien`): Tạo bản nháp hoàn tiền 100% kèm mã trả hàng miễn phí.
  - Khi bưu tá quét mã nhận hàng hoàn thành công, chuyên viên chỉ cần 1 thao tác click duyệt để giải ngân tiền cho khách.
- **Đánh giá 3 câu hỏi kiểm chứng:**
  - *Cái sai có bị chặn?* Có, tiền chỉ giải ngân khi có bằng chứng shop thừa nhận và hàng đã gửi trả.
  - *Còn làm khi lẽ ra phải hỏi?* Không, AI đã hỏi đúng ảnh chụp tin nhắn xác nhận của shop.
  - *Người dùng bình thường có phải chờ vô ích không?* **Không.** Khách nhận mã gửi hàng ngay lập tức từ AI mà không phải chờ nhân viên vào chat thủ công.

---

### 4.4. Đổi lời hứa với người dùng

- **Lời hứa cũ (thiếu mức tự chủ):** *"Shopee AI tự động giải quyết tranh chấp và hoàn tiền tức thì cho bạn."*  
  *(Hậu quả: Tạo kỳ vọng ảo khiến khách nghĩ chỉ cần nhắn vài chữ là tiền về; đồng thời khiến người bán hoang mang vì sợ bị bot tước đoạt tiền oan).*
- **Lời hứa mới (sau khi đặt mức tự chủ):** *"Shopee AI hỗ trợ bạn thu thập chứng cứ, bảo toàn nguyên vẹn lịch sử đơn hàng và chuẩn bị hồ sơ minh bạch để chuyên viên xử lý công bằng nhất cho cả hai bên."*  
  *(Giá trị mang lại: Khách hàng hiểu rõ vai trò trợ lý thu thập bằng chứng của AI; cả Người mua và Người bán đều an tâm vì phán quyết cuối cùng luôn có sự thẩm định và bảo hộ của con người).*

## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.