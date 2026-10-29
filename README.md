# FB Text Fixer

Ứng dụng desktop Python/Tkinter hỗ trợ quản lý một số thao tác Facebook qua trình duyệt Chrome do Selenium điều khiển. Giao diện có các công cụ sửa nội dung bài đăng, bình luận, lập lịch đăng bài, quản lý bài chờ duyệt và đăng bài vào nhóm.

> Đây là công cụ tự động hóa giao diện, không phải API chính thức của Meta. Hãy chỉ sử dụng trên tài khoản và nhóm bạn có quyền quản lý, tuân thủ Điều khoản dịch vụ và quy định cộng đồng của Meta/Facebook, cũng như quy định riêng của từng nhóm. Luôn kiểm tra nội dung và hành động trước khi chạy; không dùng để gửi spam, lặp nội dung không mong muốn hoặc né giới hạn của nền tảng.

## Tính năng

### 1. Đăng nhập và sửa bài viết

- Mở Chrome và truy cập Facebook để đăng nhập.
- Tải một số lượng bài viết đã chọn trên trang cá nhân.
- Áp dụng các cặp quy tắc tìm/thay thế văn bản cho bài viết.
- Có tùy chọn quét đến hết trang, thanh tiến trình, nhật ký hoạt động và nút dừng.

### 2. Bình luận trong nhóm

- Tải danh sách nhóm mà tài khoản có thể truy cập, tìm kiếm và chọn nhóm.
- Soạn tối đa năm mẫu bình luận; có thể đính kèm một ảnh hoặc danh sách ảnh.
- Chọn xử lý tuần tự hoặc song song qua nhiều tab.
- Có tùy chọn bình luận trên bài cũ, theo dõi bài mới, chọn khoảng nghỉ và giới hạn nhóm mỗi phiên.
- Có tùy chọn biến thể nội dung. Hãy dùng nội dung phù hợp, có liên quan và được nhóm cho phép.

### 3. Lập lịch đăng bài trên trang cá nhân

- Cấu hình tối đa ba nội dung, mỗi nội dung có thể bật/tắt riêng.
- Lịch đăng hằng ngày hoặc theo một ngày trong tuần; hỗ trợ nhiều mốc giờ.
- Nội dung có thể gồm văn bản và ảnh.
- Có nút bắt đầu/dừng lịch và lưu cấu hình.

### 4. Quản lý bài chờ duyệt trong nhóm

- Tải và chọn các nhóm bạn quản trị.
- Quét bài đang chờ duyệt theo lịch một lần hoặc định kỳ.
- Dùng từ khóa để nhận diện nội dung cần từ chối; có tùy chọn tự phê duyệt bài không khớp từ khóa.
- Có thể dừng tác vụ và lưu thiết lập.

**Lưu ý:** lọc theo từ khóa không hiểu đầy đủ ngữ cảnh và có thể phân loại sai. Không bật tự phê duyệt nếu chưa kiểm tra kỹ tiêu chí; thường xuyên xem lại quyết định trong giao diện Facebook.

### 5. Đăng bài vào nhóm

- Tải danh sách nhóm, tìm kiếm và chọn nhóm đích.
- Soạn tối đa ba mẫu bài, kèm ảnh tùy chọn.
- Chạy theo chu kỳ hoặc lịch hằng ngày/hằng tuần; chọn mẫu tuần tự hoặc ngẫu nhiên.
- Cấu hình giới hạn bài mỗi nhóm/ngày, giới hạn nhóm mỗi phiên và thời gian nghỉ.
- Có thiết lập đánh dấu nhóm cần kiểm duyệt hoặc bỏ qua nhóm đó.

## Yêu cầu

- Windows 10/11 khuyến nghị.
- Python 3.9 trở lên.
- Google Chrome được cài đặt.
- Kết nối Internet khi khởi động lần đầu để `webdriver-manager` tải ChromeDriver phù hợp.
- Tkinter (thường có sẵn trong bộ cài Python trên Windows).

## Cài đặt và chạy

Mở PowerShell tại thư mục dự án:

```powershell
py -3 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
python -m pip install selenium webdriver-manager pillow
python fb_text_fixer.py
```

`pillow` chỉ được dùng để hiển thị logo trong giao diện; nếu không cần phần đó, có thể bỏ gói này. Repo hiện chưa có `requirements.txt` hoặc bộ kiểm thử tự động.

Khi ứng dụng mở, Chrome có thể được khởi chạy tự động. Đăng nhập trong cửa sổ Chrome nếu được yêu cầu rồi quay lại ứng dụng. Chọn đúng tab, cấu hình nội dung/nhóm, lưu thiết lập và kiểm tra lại trước khi bấm **Bắt đầu**. Dùng **Dừng** để kết thúc tác vụ đang chạy.

### Chạy nhiều profile

```powershell
python fb_text_fixer.py --profile acc2
```

Mỗi tên profile tạo một phiên Chrome và bộ cấu hình riêng. Dùng tên đơn giản, không có dấu cách. Profile `default` có logic thử sao chép dữ liệu phiên từ Chrome mặc định khi khởi tạo lần đầu; các profile có tên khác được tạo riêng và cần đăng nhập thủ công. Dữ liệu phiên trình duyệt tương đương thông tin đăng nhập: không gửi thư mục profile cho người khác, không đưa lên GitHub và chỉ chạy ứng dụng trên máy tin cậy.

## Cấu hình và dữ liệu cục bộ

- Cấu hình được lưu trong `FBTextFixerData/` cạnh chương trình; khi dùng profile có tên, tên file được gắn thêm hậu tố profile.
- Danh sách nhóm được tải và lưu vào các file cache trong cùng thư mục.
- Phiên Chrome của ứng dụng nằm trong các thư mục `fb_chrome_profile...` cạnh chương trình.
- Đường dẫn ảnh được lưu nguyên dạng. Nếu chuyển máy hoặc thư mục, hãy chọn lại ảnh có trên máy mới.
- Các file JSON mẫu/đang dùng trong repo có thể chứa nội dung bài, số liên hệ, URL nhóm, ID tài khoản hoặc đường dẫn cục bộ. Hãy rà soát và thay bằng dữ liệu mẫu trước khi chia sẻ repo công khai. Thêm một mẫu mới vào `.gitignore` không xóa dữ liệu đã được Git theo dõi hoặc lịch sử commit trước đó.

## Giới hạn và an toàn vận hành

- Facebook thường xuyên thay đổi giao diện; các thao tác Selenium có thể ngừng hoạt động hoặc cần đăng nhập lại.
- Tác vụ điều khiển giao diện là best-effort. Ứng dụng không thể đảm bảo bài đăng/bình luận/duyệt đã hoàn tất chỉ dựa trên thao tác click; hãy xác minh trực tiếp trên Facebook.
- Tự động hóa có thể bị giới hạn hoặc không được phép theo chính sách nền tảng hoặc quy định nhóm. Không tăng tốc hay chạy hàng loạt để vượt giới hạn.
- Không chia sẻ cookie, profile Chrome, cấu hình cá nhân hoặc log có thông tin nhận dạng.
- Dừng tác vụ nếu xuất hiện cảnh báo, giới hạn thao tác hoặc hành vi bất thường.

## Xử lý sự cố

- **`ModuleNotFoundError: webdriver_manager`**: kích hoạt môi trường ảo rồi chạy `python -m pip install selenium webdriver-manager`.
- **Chrome/ChromeDriver không khởi động**: cập nhật Chrome, kiểm tra Internet và thử lại để `webdriver-manager` tải driver tương thích.
- **Facebook yêu cầu đăng nhập**: đăng nhập thủ công trong cửa sổ Chrome do ứng dụng mở. Với profile phụ, mỗi profile có phiên đăng nhập riêng.
- **Không tìm thấy nhóm hoặc bài viết**: tải lại danh sách, kiểm tra quyền truy cập/quyền quản trị và xác nhận giao diện Facebook đã tải xong.
- **Ảnh không được đính kèm**: kiểm tra đường dẫn và quyền đọc file; chọn lại ảnh từ máy hiện tại.

## Cấu trúc chính

```text
fb_text_fixer.py       Ứng dụng Tkinter và các tác vụ Selenium
logo.ico, logo.jpg     Biểu tượng ứng dụng
FBTextFixerData/       Cấu hình và cache theo phiên bản hiện tại
fb_*_config.json       Một số file cấu hình cũ ở thư mục gốc
```

## Giấy phép

Repo hiện chưa khai báo giấy phép sử dụng. Hãy hỏi chủ sở hữu trước khi phân phối lại hoặc sử dụng mã nguồn ngoài phạm vi được cho phép.