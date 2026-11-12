# Bài nộp LAB5 — T4 · Nhóm ECOM123

**Lớp:** L3A · **Bàn / zone:** A2 · **Track:** T4

| Họ và tên | Mã học viên | Việc đã làm |
|---|---|---|
| Chử Văn Hiệp | 2A202603382 | Chưa có thông tin phân công được xác nhận trong tài liệu dự án. |
| Nguyễn Tiến Khoa | 2A202603460 | Chưa có thông tin phân công được xác nhận trong tài liệu dự án. |
| Nguyễn Thanh Liêm | 2A202603358 | Chưa có thông tin phân công được xác nhận trong tài liệu dự án. |
**Căn cứ và giới hạn bài nộp:** Tài liệu này hoàn thiện theo `03-spec-template.md`, bản spec ban đầu và [prototype hiện có](propotype/index.html). Kho mã chưa có README, tài liệu track gốc, `02-guide.md`, `04-rubric.md` hoặc biên bản demo. Vì vậy, không tự bổ sung tên thành viên, ý kiến từng người, dữ liệu track hay kết quả demo. Lát cắt và tên tool được kế thừa từ bản spec ban đầu; cần đối chiếu lại track khi có tài liệu. Các quy tắc vận hành bên dưới là **thiết kế đề xuất của nhóm**, không phải chính sách hoặc SLA đã xác nhận của Shopee. Kết quả kiểm tra prototype được tách rõ khỏi hành vi mong muốn.

## §1. Lát cắt & phạm vi

### Lát cắt

Trong **Trò chuyện với Shopee**, khi **người mua** đang báo “hàng nhận không đúng mô tả”, **AI tự hướng dẫn gửi yêu cầu trả hàng hoàn tiền, xin thêm bằng chứng, hay chuyển nhân viên**, để người mua biết đúng bước tiếp theo, và người bán không bị xử thua khi họ đúng.

Đây là lát cắt kế thừa từ bản spec của nhóm, chưa đối chiếu nguyên văn với track gốc.

### Ba việc tính năng KHÔNG làm

1. **Không tự phán quyết, hoàn tiền hoặc bác khiếu nại:** AI có thể thiếu bằng chứng của một bên; quyết định tài chính phải có người có thẩm quyền duyệt.
2. **Không xử phạt, trừ điểm uy tín hoặc khóa shop:** Chế tài vượt phạm vi hỗ trợ khiếu nại đơn hàng, cần bộ phận chuyên trách kiểm tra độc lập.
3. **Không cung cấp thông tin liên hệ riêng tư của bên kia:** Tránh lộ dữ liệu và quấy rối; hướng dẫn trao đổi trong kênh hỗ trợ của sàn.

## §2. Kịch bản rủi ro (chặng 2)

Do thiếu định nghĩa bốn lớp từ track gốc, bài dùng quy ước làm việc: **① sai/lệch ngữ cảnh hoặc nguồn dữ liệu; ② thiếu thông tin/bằng chứng; ③ vượt phạm vi hoặc thẩm quyền; ④ hậu quả nghiêm trọng về tiền/quyền lợi.** Các lớp có thể giao nhau; cần đối chiếu quy ước với tài liệu lớp trước khi nộp.

Bằng chứng dưới đây trỏ tới tool và các khóa dữ liệu/hàm có thật trong `propotype/index.html`; không coi dữ liệu mock là dữ liệu track hay giao dịch thật.

| ID | Tin người dùng | Lớp | AI có thể sai thế nào và căn cứ cụ thể | Sản phẩm tốt nên làm gì | Nhãn |
|---|---|---|---|---|---|
| KB1 | “Mình đặt áo size L mà nhận size M. Shop nhận gửi nhầm rồi, trả hàng sao?” | ② | Coi lời kể là bằng chứng đã xác minh; `cases.normal.proof` vẫn ghi thiếu ảnh tem và ảnh chat gốc. | Xác nhận đơn; xin đúng ảnh còn thiếu, cho kiểm tra hồ sơ rồi mới soạn đề xuất. | sửa được |
| KB2 | “Hàng sai rồi, xử lý đi.” | ②④ | Đoán đơn rồi gọi `soan_hoan_tien`; `cases.short.proof` chưa có mã đơn, mô tả lúc đặt và loại sai lệch. | Hỏi đơn nào và sai ở đâu; chặn soạn hồ sơ tài chính khi chưa xác định được đơn. | không chấp nhận được |
| KB3 | “Nồi chiên ghi 6 lít mà lòng nồi mình đo chỉ được 5 lít.” | ①④ | Coi hai phép đo là cùng một đại lượng và kết luận shop sai. Dữ liệu `cases.history` không có phương pháp đo hoặc định nghĩa dung tích. | Xin cách đo và mô tả gốc; ghi rõ chưa đủ căn cứ, chuyển chuyên viên nếu cần đánh giá kỹ thuật. | không chấp nhận được |
| KB4 | “Ảnh có tem và đúng mẫu rồi, mình không chụp lại được.” | ② | `yeu_cau_bang_chung` tiếp tục xin ảnh giống hệt hoặc suy diễn không gửi lại là khiếu nại sai. Prototype chỉ có cờ `proofAdded`, chưa có danh mục tệp đã nhận. | Liệt kê bằng chứng đã có, hỏi phần thiếu và cho chuyển nhân viên nếu không thể bổ sung. | sửa được |
| KB5 | “Gửi ảnh rồi mà cứ bị hỏi lại, thiếu gì thì nói rõ!” | ② | `addProof()` đổi cờ nhưng `render()` vẫn lấy nội dung tĩnh từ `c.proof`, nên khung bằng chứng có thể vẫn báo thiếu. | Cập nhật trạng thái theo từng bằng chứng; không yêu cầu lại phần đã nhận. | sửa được |
| KB6 | “Khách dọa bóc phốt để ép shop hoàn tiền ngay.” | ③④ | Dùng lời đe dọa để kích hoạt `soan_hoan_tien` hoặc bỏ qua phản hồi người bán. | Tách lời đe dọa khỏi chứng cứ; chuyển nhân viên và cho hai bên trình bày qua kênh chính thức. | không chấp nhận được |
| KB7 | “Mình nghi hàng giả, khóa shop ngay.” | ③④ | Gọi `phat_shop` dù chưa xác minh. Bảng `cases.*.tools` đã đặt tool này ở mức Cấm. | Ghi nhận phản ánh, chuyển chuyên trách; không hứa khóa hay phạt shop. | không chấp nhận được |
| KB8 | “Không nhớ đơn nào, cũng không rõ khác mô tả chỗ nào.” | ② | Tự chọn đơn hoặc tạo chi tiết sai lệch để đi tiếp; `makeDraft()` hiện không kiểm tra mã đơn hay nội dung bằng chứng. | Hướng dẫn xác định đơn, cho người mua xác nhận; chưa tìm được thì chưa soạn đề xuất. | sửa được |
| KB9 | “Shop sửa mô tả sau khi bán, lúc đặt là 6 lít, giờ chỉ còn 5 lít.” | ①④ | Lấy mô tả hiện tại để gọi `tu_choi_khieu_nai`. `cases.history.proof` có snapshot 6 lít nhưng ghi rõ là mô phỏng và chưa xác minh tính toàn vẹn. | Tách mô tả hiện tại khỏi snapshot lúc đặt; không kết luận, chuyển chuyên viên đối chiếu. | không chấp nhận được |
| KB10 | “Cho tôi số điện thoại và địa chỉ riêng của người bán.” | ③ | Tiết lộ dữ liệu ngoài phạm vi; prototype không có tool hoặc dữ liệu liên hệ riêng tư để đáp ứng. | Không cung cấp dữ liệu riêng tư; chỉ dẫn kênh trao đổi được phép. | không chấp nhận được |

### Quyết định chọn hai kịch bản đắt nhất

- **Chọn KB2:** Thiếu thông tin ngay đầu luồng nhưng có thể dẫn tới quyết định sai đơn. Nếu chỉ sửa câu trả lời mà không chặn hành động thì rủi ro vẫn tồn tại. Hậu quả tài chính khó khắc phục hơn việc hỏi ảnh lặp lại ở KB4–KB5.
- **Chọn KB9:** Có vẻ đủ dữ liệu nhưng nguồn có thể sai thời điểm; người duyệt cũng dễ bị dẫn sai nếu hồ sơ chỉ hiện mô tả hiện tại. Sai lầm có thể làm người mua mất quyền lợi hoặc người bán bị hoàn tiền oan.
- **Suýt chọn KB7:** Thiệt hại khóa shop rất lớn, nhưng có thể loại quyền `phat_shop` khỏi trợ lý và chuyển chuyên trách ngay. KB2 và KB9 khó hơn vì nằm trong luồng hỗ trợ chính, cần vừa giúp người mua đi tiếp vừa kiểm soát bằng chứng.
- Đây là lựa chọn theo mức độ nghiêm trọng và độ khó kiểm soát, không phải xếp hạng theo tần suất; chưa có dữ liệu thực tế để ước lượng xác suất.

## §3. Khi AI sai (chặng 3)

### 3.1. KB2 — Thiếu đơn hàng và nội dung sai lệch

**Câu sai giả định cần ngăn:** “Mình đã gửi yêu cầu hoàn tiền cho đơn hàng của bạn.” Đây là ví dụ lỗi thiết kế, không phải phản hồi đã quan sát từ AI thật.

**Câu đúng hiện có trong `cases.short.reply`:**

> Mình có thể hỗ trợ bạn kiểm tra. Bạn đang nói đến đơn hàng nào và sản phẩm nhận được không đúng ở điểm nào so với mô tả lúc đặt hàng?

- **Người dùng thấy:** Câu hỏi trên và thông báo chưa tạo yêu cầu hoàn tiền, thiếu mã đơn và nội dung sai lệch. Nút “Bổ sung thông tin đơn hàng” và “Chuyển nhân viên” cho biết bước tiếp theo (Ảnh 1).
- **Làm tiếp theo thiết kế:** Người mua chọn/xác nhận đơn và mô tả sai lệch; hệ thống kiểm tra quyền truy cập đơn, tóm tắt phần đã có rồi chỉ xin bằng chứng còn thiếu. Chưa đủ đầu vào thì chưa cho tạo bản nháp. Nếu người mua không thể bổ sung hoặc yêu cầu hỗ trợ, chuyển hồ sơ kèm hội thoại.
- **Ai được báo, khi nào:** Người mua nhận câu hỏi trong lượt trả lời hiện tại. Nhân viên nhận hồ sơ khi thao tác chuyển được hệ thống xác nhận thành công; chỉ sau xác nhận mới hiện “Đã chuyển”. Người bán chỉ được báo khi đã xác định đúng đơn và cần phản hồi. Chưa có SLA nhận việc hoặc thời gian giải quyết được xác nhận; phải hiển thị trạng thái chờ thay vì tự hứa số giờ. Prototype chỉ mô phỏng thông báo trên màn hình.
- **Quyết định:** Chọn **hỏi lại** vì người mua có thể bổ sung ngay. Loại trả lời kèm giới hạn như một kết luận vì chưa biết đang xét đơn nào. Chưa chuyển người ngay mặc định vì làm tăng thời gian chờ cho lỗi thiếu thông tin đơn giản; vẫn giữ quyền yêu cầu chuyển.
- **Loại lỗi:** Thiếu ngữ cảnh là nguyên nhân ban đầu; cho phép hành động khi thiếu trường bắt buộc là lỗi hệ thống. Câu trả lời trung tính, không đổ lỗi cho người mua; cách sửa là giúp bổ sung dữ liệu và chặn hành động không đủ điều kiện.
- **HAX/PAIR áp dụng:** Thu hẹp hành động khi không chắc chắn → câu hỏi mã đơn/điểm sai; làm rõ giới hạn → trạng thái “Chưa tạo yêu cầu hoàn tiền”; phản hồi và kiểm soát → hai nút bổ sung/chuyển nhân viên. Các số 1–3 trong khung chú thích của Ảnh 1 tương ứng ba điểm này.
- **Câu chữ không cứu được:** Nút bổ sung chỉ bật cờ rồi cho tạo bản nháp dù chưa nhập dữ liệu. Cần kiểm tra trường bắt buộc tại nơi thực thi hành động, không chỉ ẩn nút trên giao diện. Đây là yêu cầu thiết kế **chưa được prototype thực thi**.

### 3.2. KB9 — Mô tả thay đổi sau thời điểm đặt hàng

**Câu sai giả định cần ngăn:** “Trang sản phẩm ghi 5 lít nên shop giao đúng, khiếu nại của bạn bị từ chối.”

**Câu đúng hiện có trong `cases.history.reply`:**

> Mình chưa thể kết luận dựa trên mô tả đang hiển thị. Việc xác minh cần dùng phiên bản mô tả tại thời điểm bạn đặt hàng. Hệ thống mô phỏng hiện có bản ghi lịch sử, nhưng cần nhân viên đối chiếu trước khi kết luận.

- **Người dùng thấy:** Mã đơn mock `#SPX-7712`, snapshot mock ghi 6 lít, ghi chú cần xác minh tính toàn vẹn và nút “Chuyển chuyên viên đối chiếu lịch sử” (Ảnh 2).
- **Làm tiếp theo thiết kế:** Giữ riêng lời người mua, mô tả hiện tại và snapshot theo thời điểm. Chuyển chuyên viên kiểm tra nguồn/thời điểm snapshot cùng ảnh sản phẩm và phản hồi người bán. Thiếu snapshot thì ghi “không có dữ liệu lịch sử”, không tạo lại lịch sử bằng suy đoán.
- **Ai được báo, khi nào:** Người mua được báo giới hạn ngay trong lượt trả lời. Chuyên viên nhận hồ sơ khi chuyển thành công; người bán được yêu cầu phản hồi khi chuyên viên cần bằng chứng. Thời hạn xử lý lấy từ cấu hình hàng đợi thực tế; nếu chưa có thì báo đang chờ, không hứa 24/48 giờ. Prototype không có hàng đợi hay thông báo ngoài màn hình.
- **Quyết định:** **Trả lời kèm giới hạn rồi chuyển người trước khi phán quyết.** Loại chỉ hỏi thêm ảnh vì ảnh không xác minh được lịch sử mô tả. Loại trả lời kèm giới hạn rồi tiếp tục tự quyết vì nguồn chưa được xác minh. Không im lặng chuyển người: cần giải thích lý do và hồ sơ được mang theo.
- **Loại lỗi:** Lỗi hệ thống nếu không lưu/truy xuất được snapshot; lỗi ngữ cảnh nếu nhầm mô tả hiện tại với mô tả lúc đặt. Cách nói nêu dữ liệu thiếu, không quy kết shop đã gian lận chỉ từ lời phản ánh.
- **HAX/PAIR áp dụng:** Minh bạch giới hạn → “chưa thể kết luận”; giải thích căn cứ → khung snapshot 6 lít và phần cần xác minh; khả năng kiểm soát → nút chuyển chuyên viên. Xem các chú thích 1–3 trong Ảnh 2.
- **Câu chữ không cứu được:** Cần snapshot gắn với đúng đơn/thời điểm, kiểm tra tính toàn vẹn, nhật ký xét duyệt và quyền phán quyết phía máy chủ. Nếu chưa có dữ liệu thì giữ hồ sơ chờ xác minh. Prototype chưa có các cơ chế này.

## §4. Mức tự chủ (chặng 4)

### 4.1. Quyền của từng tool

`soan_hoan_tien` là tên kế thừa từ spec cũ, chưa có schema tool để xác nhận nó chỉ soạn hay thực sự thực thi. Bài tách rõ **soạn bản nháp** và **duyệt/thực hiện hoàn tiền**. Prototype dùng nhãn `soan_de_xuat_hoan_tien` ở mức “Cần duyệt”; hiểu là kết quả đề xuất phải được duyệt, không phải bản nháp đã làm tiền dịch chuyển.

| Tool / bước | Mức đề xuất | Cost-of-error và chi phí chờ | Phương án đã cân nhắc và loại |
|---|---|---|---|
| `yeu_cau_bang_chung` | **Tự làm có giới hạn**: chỉ xin thông tin liên quan, chưa có; không xin dữ liệu riêng tư không cần thiết. | Xin sai làm người mua/người bán mất công, có thể lộ dữ liệu hoặc lỡ thời hạn; đính chính không xóa hết hậu quả. Duyệt mọi câu hỏi làm chậm thu thập thông tin. | Loại duyệt từng yêu cầu vì quá nhiều bước chờ; dùng danh mục bằng chứng và đường chuyển người cho ca nhạy cảm/bế tắc. |
| `chuyen_truong_nhom` | **Tự làm** khi vượt khả năng hoặc người dùng yêu cầu; kiểm tra đúng nơi nhận. | Chuyển nhầm tăng tải, trì hoãn và có thể chia sẻ hồ sơ sai người; có thể phân tuyến lại nhưng không thu hồi được thời gian đã mất. | Loại yêu cầu duyệt trước khi chuyển vì kéo dài chính bước cần tìm người hỗ trợ; giới hạn dữ liệu người nhận được xem. |
| `soan_hoan_tien` / `soan_de_xuat_hoan_tien` | **Cần người duyệt đối với quyết định cuối**. AI chỉ soạn nháp khi đủ trường, người mua được sửa; không gọi giao dịch tiền. | Sai đơn, số tiền hoặc căn cứ gây thiệt hại hai bên; nháp có thể sửa, giao dịch khó đảo lại. Chờ duyệt kéo dài nhận tiền nhưng cần để kiểm tra quyền lợi. | Loại tự hoàn theo số ảnh hoặc giá trị đơn nhỏ vì bằng chứng có thể sai; loại cấm cả soạn nháp vì làm nhân viên phải nhập lại hồ sơ. |
| `tu_choi_khieu_nai` | **Cần người duyệt**; không đóng hồ sơ chỉ vì thiếu ảnh hoặc hết thời gian chờ. | Từ chối sai làm người mua mất cơ hội xử lý và tốn công khiếu nại lại; người bán phải chờ lâu hơn nếu hồ sơ chưa quyết định. | Loại tự từ chối khi hết hạn vì có thể lỗi tải ảnh; loại cấm hoàn toàn vì chuyên viên vẫn cần xử lý hồ sơ không có căn cứ. |
| `phat_shop` | **Cấm trong trợ lý này**; chỉ chuyển chuyên trách. | Phạt sai ảnh hưởng uy tín và hoạt động kinh doanh, khó phục hồi hoàn toàn; chuyển bộ phận khác làm chậm nhưng phù hợp phạm vi. | Loại cả tự làm và duyệt trong chat vì chế tài shop nằm ngoài lát cắt §1. |

**Quy trình duyệt đề xuất:**

- **Ai duyệt:** Chuyên viên khiếu nại được phân quyền. Phản hồi đồng ý của người bán là một bằng chứng, không mặc nhiên thay thế quyền duyệt của chuyên viên.
- **Người duyệt thấy:** Mã đơn và chủ đơn; số tiền nếu đã có nguồn; mô tả lúc đặt cùng nguồn/thời điểm; mô tả hiện tại tách riêng; bằng chứng của hai bên; phần chưa xác minh; lý do đề xuất; lịch sử chỉnh sửa. Thiếu giá trị đơn thì không tự điền số tiền hay hứa hoàn 100%.
- **Quá hạn:** Hạn duyệt phải lấy từ cấu hình vận hành được phê duyệt. Khi quá hạn, cảnh báo trưởng nhóm và cập nhật trạng thái cho người mua; không tự duyệt, tự từ chối hoặc tự đóng. Nếu chưa cấu hình hạn, hiển thị “Chưa có thời gian xử lý xác nhận” và cho yêu cầu hỗ trợ; đây là việc cần hoàn thiện trước triển khai.
- Prototype chỉ có nút “Nhân viên duyệt (mô phỏng)”, chưa có xác thực vai trò, hồ sơ thật hay bộ đếm quá hạn.

### 4.2. Tool khó xếp nhất

**Chọn `soan_hoan_tien`**, vì tên gọi dễ nhập nhằng giữa chuẩn bị đề xuất và chuyển tiền.

| Phương án cân nhắc | Lợi ích | Cái giá liên hệ §2 |
|---|---|---|
| Tự làm toàn bộ | Ít bước chờ | KB2 có thể sai đơn; KB9 có thể sai căn cứ lịch sử, kéo theo quyết định tài chính sai. |
| Người duyệt từ lúc soạn hồ sơ | Kiểm tra sớm | KB1 cũng phải chờ nhân viên nhập lại dữ liệu; tăng việc thủ công. |
| AI soạn nháp có điều kiện, chuyên viên duyệt quyết định | Giảm nhập liệu, giữ kiểm soát quyết định | Vẫn cần hàng đợi và người duyệt kiểm tra thực chất, không chỉ bấm xác nhận. |

**Phương án chốt trong tài liệu:** Phương án thứ ba. Không coi duyệt thủ công là bảo đảm an toàn tuyệt đối; người duyệt có thể sai nếu hồ sơ trình bày thiếu nguồn.

**Ý kiến từng thành viên:** Chưa có biên bản hoặc thông tin phân công để gán lựa chọn cho từng người. Bảng trên là phân tích phương án, không phải tường thuật một cuộc tranh luận đã diễn ra. Cần nhóm xác nhận phần này trước khi nộp.

### 4.3. Thử mức tự chủ trên ba kịch bản

Kết quả dưới đây là **đối chiếu luồng mã nguồn**, không phải thử nghiệm backend hay AI thật.

| Ca | Theo thiết kế: sai bị chặn thế nào? | Prototype hiện tại | Có chờ vô ích hoặc làm trước khi hỏi? |
|---|---|---|---|
| KB2 | Thiếu đơn/điểm sai thì chỉ hỏi; không tạo nháp. | Màn đầu hỏi đúng. Nhưng `addProof()` chỉ bật cờ, sau đó `makeDraft()` vẫn tạo nháp mà không kiểm tra thông tin. **Chưa đạt chặn đầu vào.** | Không phải chờ nhân viên để được hỏi, nhưng có thể soạn nháp trước khi thật sự nhận thông tin. |
| KB9 | Nguồn lịch sử chưa xác minh thì chuyển người; không duyệt quyết định. | Có nút chuyển đúng. Tuy nhiên “Bổ sung ảnh sản phẩm” → tạo nháp → duyệt mock vẫn đi được, chưa buộc xác minh snapshot. **Chưa đạt chặn luồng thay thế.** | Chờ chuyên viên là có lý do; chưa đo thời gian chờ. Không được coi thêm ảnh là thay thế xác minh lịch sử. |
| KB1 bình thường | Thu thập ảnh tem và ảnh chat, người mua kiểm tra nháp, chuyên viên duyệt. | Có chuỗi xác nhận ảnh → tạo nháp → sửa/duyệt mock. Không tải tệp, kiểm tra ảnh hoặc tạo mã trả hàng thật. | Không phải chờ để xem hướng dẫn; bước duyệt cuối vẫn cần người. Chưa có dữ liệu để nói luồng nhanh hơn bao nhiêu. |

### 4.4. Luật bổ sung và lời hứa

- Tách trạng thái **đang thu thập → đủ đầu vào soạn nháp → chờ chuyên viên → có quyết định**; “đã nhận ảnh” không đồng nghĩa “ảnh đã xác minh”.
- Chặn hành động tại hệ thống thực thi: đúng đơn, quyền truy cập, trường bắt buộc, trạng thái nguồn và quyền người duyệt. Thêm nhật ký, chống xử lý lặp khi tích hợp giao dịch thật.
- Không tự tính tiền hoàn, tạo mã trả hàng miễn phí hay cam kết bảo toàn lịch sử nếu chưa có dữ liệu/công cụ tương ứng.
- **Lời hứa bị loại:** “AI giải quyết tranh chấp và hoàn tiền tức thì.”
- **Lời hứa được chọn:** “AI hỗ trợ thu thập thông tin, nêu rõ dữ liệu còn thiếu và chuẩn bị hồ sơ; chuyên viên có thẩm quyền quyết định hoàn tiền hoặc từ chối.” Việc giới hạn tự chủ đổi kỳ vọng từ nhận tiền ngay sang biết đúng bước tiếp theo.

## §5. Prototype (chặng 5)

### 5.1. File, công cụ và phạm vi mô phỏng

- **File:** [propotype/index.html](propotype/index.html) — giữ đúng tên thư mục hiện tại là `propotype`.
- **Công cụ:** HTML, CSS, JavaScript thuần; mở file bằng trình duyệt, chọn ba tab tình huống.
- **Không gọi AI thật:** Hội thoại và dữ liệu nằm cố định trong đối tượng `cases`; không có kết nối Shopee, thanh toán hoặc truy xuất lịch sử thật.
- **Mock:** Đơn hàng, snapshot, nhận bằng chứng, tạo nháp, duyệt và chuyển nhân viên. Các nút chủ yếu đổi cờ trạng thái rồi gọi `render()`; không thực sự tải ảnh hay gửi hồ sơ ra ngoài.

### 5.2. Hai ảnh và các điểm đánh số

**Ảnh 1 — KB2: thiếu thông tin**

![Ảnh 1 — Ca thiếu thông tin và các chú thích 1–3](prototype/prototype-01.png)

| Số trong khung chú thích | Thể hiện gì | Nguyên tắc | Mức tự chủ liên quan |
|---|---|---|---|
| 1 | AI hỏi đơn hàng và chỗ sai, trạng thái chưa tạo yêu cầu. | Thu hẹp hành động khi không chắc chắn. | Tự hỏi bằng chứng; chưa được soạn đề xuất khi thiếu đầu vào. |
| 2 | Nêu thiếu dữ liệu và giới hạn hỗ trợ. | Làm rõ khả năng/giới hạn. | Không tự hoàn hoặc đóng khiếu nại. |
| 3 | Nút bổ sung và chuyển nhân viên. | PAIR: phản hồi và kiểm soát. | Người mua cung cấp thông tin hoặc yêu cầu chuyển; chuyên viên quyết định cuối. |

**Ảnh 2 — KB9: mô tả thay đổi**

![Ảnh 2 — Ca lịch sử mô tả và các chú thích 1–3](prototype/prototype-02.png)

| Số trong khung chú thích | Thể hiện gì | Nguyên tắc | Mức tự chủ liên quan |
|---|---|---|---|
| 1 | Câu “chưa thể kết luận” từ mô tả hiện tại. | Minh bạch giới hạn. | Không tự kết luận. |
| 2 | Khung bằng chứng nêu snapshot mock 6 lít và cần xác minh tính toàn vẹn. | Giải thích căn cứ. | Dữ liệu chưa xác minh không được dùng để tự bác khiếu nại. |
| 3 | Căn cứ hiện rõ để người xem hiểu vì sao cần đối chiếu. | PAIR: khả năng giải thích. | Chuyển chuyên viên; quyết định hoàn/từ chối cần người duyệt. |

Ảnh thể hiện giao diện và chú thích có sẵn, không chứng minh kiểm soát quyền đã được triển khai. Tên và mã HAX trên giao diện được kế thừa từ prototype; bài diễn giải theo hành vi, chưa xác nhận mã với tài liệu HAX của lớp.

### 5.3. Quyết định trình bày bằng chứng và điều khiển tự chủ

- **Độ chắc chắn:** Cân nhắc phần trăm tự tin, nhãn màu đơn thuần và danh mục dữ liệu có/thiếu. Chọn danh mục có/thiếu kèm nguồn vì người mua biết cần bổ sung gì; loại phần trăm vì không có phép đo hiệu chuẩn, loại chỉ dùng màu vì không giải thích được căn cứ. Snapshot mock phải được ghi rõ là mock, không phải dữ liệu đã xác minh.
- **Điều khiển:** Cân nhắc công tắc cho người mua bật “tự hoàn”, chỉ ghi nhãn quyền, hoặc tách nháp/duyệt/chuyển người. Chọn tách bước vì thể hiện ai chịu trách nhiệm cho từng hành động; loại công tắc vì người mua không có quyền cấp quyền quyết định tiền cho AI, loại nhãn đơn thuần vì nhãn không ngăn được thao tác sai.
- **Giới hạn hiện có:** Nút duyệt nằm cùng màn người mua và ai mở trang cũng bấm được; chỉ dùng trình diễn. Chưa có màn xem hồ sơ đầy đủ, nhập/sửa dữ liệu thật hoặc bảng bằng chứng cập nhật theo trạng thái. Bản triển khai cần phân quyền và kiểm tra phía máy chủ.

## §6. Tốt là gì (chặng 6)

Ba tiêu chí Pass/Fail dưới đây chấm được bằng thao tác hoặc kiểm tra trạng thái. Kết quả hiện tại dựa trên mã nguồn và giao diện mock, chưa có kiểm thử tích hợp.

| Tiêu chí | Cách chấm Pass/Fail | KB2 | KB9 |
|---|---|---|---|
| C1. Không vượt điều kiện hoặc quyền | Pass khi không thể tạo nháp thiếu mã đơn/điểm sai; không thể duyệt quyết định khi thiếu xác minh bắt buộc hoặc quyền chuyên viên. Chỉ cần một đường vượt là Fail. | **Fail:** `addProof()` → `makeDraft()` không kiểm tra trường bắt buộc. | **Fail:** bổ sung ảnh → nháp → `approve()` không xác minh snapshot hay vai trò. |
| C2. Nêu rõ căn cứ và giới hạn ở màn đầu | Pass khi phản hồi/khung bằng chứng cho biết dữ liệu có, thiếu/chưa xác minh và không hứa đã hoàn tiền. | **Pass ở màn đầu:** nêu thiếu mã đơn, điểm sai và chưa tạo yêu cầu. | **Pass ở màn đầu:** nêu snapshot mock và cần đối chiếu trước kết luận. |
| C3. Có đường chuyển người khi chưa quyết định | Pass khi người mua có thể chuyển từ mọi trạng thái trước quyết định và màn hình xác nhận hồ sơ mang theo. Một trạng thái bị mất đường chuyển là Fail. | **Fail toàn luồng:** có nút lúc đầu, nhưng nhánh `proofAdded`/`draft` không còn nút chuyển. | **Fail toàn luồng:** chuyển được lúc đầu, nhưng sau bổ sung ảnh chỉ còn tạo nháp rồi sửa/duyệt. |

**Lỗi còn lại:** `cases.short.order` hiện mã `#SPX-2048` trong khi khung bằng chứng nói chưa có mã đơn; cần đổi thành đơn chưa xác nhận hoặc bỏ mã khỏi màn đầu. `c.proof` và `c.status` không đổi sau khi thêm bằng chứng nên có thể mâu thuẫn với trạng thái thao tác. “Sửa hồ sơ” chỉ đổi cờ, chưa sửa được trường dữ liệu. Không có kiểm tra nguồn, vai trò, hàng đợi, SLA hoặc nhật ký.

**Điều kiện đạt trước triển khai:** Khắc phục C1/C3; đồng bộ bằng chứng theo trạng thái; chạy lại ba ca ở §4.3 và thử đường thao tác thay thế. Không dùng việc prototype không chuyển tiền thật để kết luận hệ thống tài chính đã an toàn.

## §7. Demo

**Tình trạng:** Chưa có ca lạ hoặc biên bản demo do lớp cung cấp trong kho mã. Không ghi một ca tự dựng thành kết quả đã nhận tại demo.

**Ca lạ đề xuất để diễn tập:** “Shop sửa mô tả rồi, mình đã gửi ảnh nhưng không có bản chụp lúc đặt; app cũng không tải thêm ảnh được. Hoàn ngay giúp mình.”

- **Cách diễn tập với prototype:** Chọn tab “Shop sửa mô tả” để đi theo luồng gần nhất. Prototype không có ô chat tự do nên không trực tiếp tiếp nhận và hiểu tin nhắn mới này.
- **Hành vi dự kiến từ mã nguồn:** Màn đầu vẫn dùng kịch bản cố định có snapshot mock 6 lít, dù ca diễn tập nói chưa có snapshot. Bấm chuyển thì hiện xác nhận chuyển mock. Nếu bấm bổ sung ảnh, vẫn có thể tạo nháp và duyệt mock vì các hàm không kiểm tra dữ liệu.
- **Hành vi thiết kế cần đạt:** Ghi rõ chưa có lịch sử được xác minh; không bắt tải lại bằng chứng liên tục; giữ hồ sơ và chuyển chuyên viên, không hứa hoàn hay bác khiếu nại.
- **Điều chỉnh đề xuất từ rà soát này:** Bổ sung nhánh “không có snapshot / lỗi tải ảnh”, giữ nút chuyển ở các trạng thái trước quyết định, chặn duyệt khi nguồn chưa xác minh. Đây là đề xuất sau rà soát mã, chưa phải quyết định của nhóm sau demo thật.
- **Cần ghi nhận khi demo thật diễn ra:** Nguyên văn ca lạ, thứ tự thao tác, trạng thái/ảnh quan sát, tiêu chí C1–C3 đạt hay trượt, quyết định nhóm giữ hoặc đổi và lý do. Thông tin thực tế này cùng phân công thành viên là phần cần nhóm xác nhận để hoàn tất bằng chứng bài nộp.
