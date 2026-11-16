Đề bài / Yêu cầu

1. Mục tiêu

- Giải thích bản chất của Context Window như một "chiếc cốc nước" có dung lượng RAM giới hạn.

- Diễn giải hiện tượng Truncation (cắt gọt dữ liệu cũ) khi phiên chat quá dài.

2. Bối cảnh

Nhân viên CSKH MartX tư vấn cho khách hàng trên 1 phiên chat ChatGPT duy nhất qua 45 lượt liên tục.

3. Vấn đề hiện tại

Nhật ký hội thoại bị nhầm lẫn thông tin được ghi nhận như sau:

Lượt Chat	Nội dung Khách hàng cung cấp / Hỏi	Phản hồi của AI	Trạng thái Bộ nhớ RAM (Context Window)

Lượt 1	"Tôi tên Trần Văn B, mã đơn hàng #MTX-9988, mua tại MartX Q1"	"Chào anh B, em đã ghi nhận thông tin đơn #MTX-9988 ạ."	Cốc còn trống 95% (Chứa lượt 1)

...	(Tư vấn kéo dài 40 lượt về chi tiết các mặt hàng rau củ...)	(AI trả lời dông dài làm tích lũy 32.000 Tokens)	Cốc đầy 100% (Token mới tràn vào)

Lượt 42	"Vậy đơn hàng của tôi có được miễn phí hoàn tiền không?"	"Chào chị Mai, chị cho em xin lại mã đơn hàng với ạ?"	Bị Truncation: Lượt 1 bị đẩy văng khỏi cốc!

Thắc mắc của nhân viên: "Tại sao mới nói lúc đầu phiên chat mà AI đã bị trí nhớ ngắn hạn quên mất?"

4. Yêu cầu đầu ra

- Phần 1: Giải thích hình tượng Chiếc cốc nước  

Dùng hình ảnh ẩn dụ "Chiếc cốc nước" giải thích cho nhân viên lý do AI quên thông tin ở Lượt 1.

Bộ nhớ tạm của AI (Context Window) giống như một chiếc cốc có dung tích cố định (chứa tối đa 32.000 Tokens).

Lượt 1: Thông tin "Anh Trần Văn B - Đơn #MTX-9988" được đổ vào và nằm dưới đáy cốc.

40 lượt tiếp theo: Hội thoại tư vấn rau củ dông dài làm nước dâng lên đầy 100% miệng cốc.

Lượt 42: Câu hỏi mới đổ thêm vào khiến chiếc cốc bị quá tải, buộc phải đẩy phần nước cũ nhất ở đáy cốc tràn ra ngoài (hiện tượng Truncation).

Vì dữ liệu ở Lượt 1 đã bị tràn khỏi cốc và biến mất khỏi bộ nhớ hiện tại nên AI hoàn toàn quên mất thông tin khách hàng.

- Phần 2: Phương án quản lý RAM bộ nhớ  

Đề xuất 2 phương án (thao tác người dùng & thiết kế hệ thống) để luồng tư vấn không bị tràn cốc.

1. Thao tác người dùng (Nhân viên CSKH)

Tóm tắt và mở chat mới: Sau 15–20 lượt, yêu cầu AI tóm tắt ngắn nội dung chính rồi copy sang phiên chat mới để làm sạch bộ nhớ.

Nhắc lại thông tin cốt lõi: Đính kèm tên khách và mã đơn (VD: "Đơn #MTX-9988 của anh B...") ngay trong các câu hỏi quan trọng phía sau.

2. Thiết kế hệ thống (Kỹ thuật)

Ghim thông tin cố định (Pinned Context): Lưu tên khách, mã đơn vào System Prompt để luôn gửi kèm ở mọi lượt chat, không bao giờ bị đẩy ra ngoài.

Tóm tắt cuốn chiếu tự động (Rolling Summary): Cấu hình hệ thống tự động nén các hội thoại cũ thành đoạn tóm tắt ngắn để liên tục giải phóng dung lượng cốc.

