# .md Guide

Khi xem những repository nổi tiếng trên GitHub, gần như sẽ luôn bắt gặp một file tên là `README.md`.

> Vậy `md` là gì, và vì sao nó lại xuất hiện nhiều đến vậy?

---

## Markdown là gì

`md` là viết tắt của **Markdown** — một ngôn ngữ đánh dấu dạng văn bản đơn giản, giúp bạn trình bày nội dung rõ ràng và đẹp mắt mà không cần dùng đến công cụ soạn thảo phức tạp.

Điểm đặc biệt của Markdown là chỉ cần viết bằng văn bản thuần, nhưng khi được hiển thị trên GitHub hoặc các nền tảng hỗ trợ Markdown.

## Tại sao lại chọn Markdown

Bên cạnh đó, còn có những trình soạn thảo kiểu **WYSIWYG** (*What You See Is What You Get*) như Microsoft Word hay Google Docs, nơi có thể bấm nút để định dạng văn bản và nhìn thấy kết quả ngay lập tức.

Tuy nhiên, Markdown vẫn được ưa chuộng trên GitHub và trong giới lập trình vì nhiều lý do:

- **Đơn giản và dễ học**: chỉ với một vài cú pháp cơ bản là đã có thể viết tài liệu rõ ràng, có cấu trúc.
- **Tính di động cao**: file Markdown có thể mở bằng rất nhiều ứng dụng khác nhau, không bị phụ thuộc vào một phần mềm riêng biệt.
- **Độc lập nền tảng**: có thể viết trên macOS, Windows, Linux, iOS hoặc Android.
- **Được hỗ trợ rộng rãi**: GitHub, Reddit và rất nhiều công cụ desktop/web hiện nay đều hỗ trợ Markdown. 

## Khi nào dùng Markdown

Markdown rất linh hoạt và có thể được dùng trong nhiều tình huống khác nhau, chẳng hạn như:

- viết `README.md` cho repository GitHub
- ghi chú học tập
- viết tài liệu kỹ thuật
- tạo nội dung cho website
- soạn email
- làm sách, bài thuyết trình hoặc tài liệu in
- xây dựng trang tài liệu cho dự án

---

## Lưu ý nhỏ

Không phải mọi công cụ đều hỗ trợ Markdown giống hệt nhau. Mỗi ứng dụng có thể hỗ trợ một “phiên bản” hoặc một “flavor” Markdown hơi khác nhau.

Điều đó có nghĩa là có nơi chỉ hỗ trợ cú pháp cơ bản. Vì vậy, khi dùng Markdown trên một nền tảng cụ thể, nên xem kỹ chính nền tảng đó để biết họ hỗ trợ những gì.

---
## Cơ chế hoạt động

Các công cụ biên dịch giúp việc viết bằng Markdown trở nên dễ dàng hơn vì chúng ẩn đi nhiều thao tác diễn ra phía sau. 

Khi bạn viết bằng Markdown, nội dung thực chất được lưu dưới dạng **văn bản thuần** trong một tệp có phần mở rộng như `.md` hoặc `.markdown`. Để nội dung đó xuất hiện dưới dạng một trang web, tài liệu HTML hoặc PDF, bạn cần trình biên dịch xử lý. Markdown thường hoạt động theo 4 bước:

1. Tạo một tệp Markdown bằng text editor hoặc ứng dụng hỗ trợ Markdown.
2. Mở tệp đó bằng một công cụ có khả năng xử lý Markdown.
3. Công cụ sẽ chuyển nội dung Markdown sang HTML.
4. Tệp HTML sau đó có thể được hiển thị trên trình duyệt hoặc tiếp tục xuất sang định dạng khác như PDF.

![Cơ chế hoạt động](./Png/0001.png)