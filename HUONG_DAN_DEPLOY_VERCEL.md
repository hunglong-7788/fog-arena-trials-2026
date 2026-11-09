# FSC x Flame — Hướng dẫn đưa FOG Arena Trials lên Vercel (không dùng terminal)

**Phạm vi:** minigame gian 2 (6 thử thách) có website và bảng xếp hạng RIÊNG. **Không** chỉnh sửa project FSC x Flame Club Portal hoặc Glitch Raid.

## 1. Chuẩn bị

Giải nén `FOG-Arena-Trials-Club-Day-2026.zip`. Các file web nằm ngay trong thư mục giải nén:

- `index.html` — trang chính
- `app.js` — gameplay / kết nối bảng xếp hạng
- `styles.css` — giao diện PC / mobile
- `favicon.svg` — biểu tượng web
- `vercel.json` — cấu hình Vercel

Các file `README.md`, `QA_REPORT.md`, và hướng dẫn này để tham khảo. **Không upload mỗi file ZIP vào repo**: hãy upload *các file bên trong ZIP*.

## 2. Đưa mã nguồn lên GitHub

1. Đăng nhập https://github.com (nếu có phiên đăng nhập sẵn thì không cần nhập mật khẩu).
2. Vào https://github.com/new, đặt **Repository name**: `fog-arena-trials-2026`.
3. Có thể chọn **Private**; chọn **Create repository**. Không cần nhập gì trong ô Description.
4. Trong repository mới, chọn **uploading an existing file** (hoặc **Add file → Upload files**).
5. Kéo thả `index.html`, `app.js`, `styles.css`, `favicon.svg`, `vercel.json` và các file hướng dẫn vào trang upload. Kiểm tra file `index.html` nằm ngay **gốc repository**, không nằm trong một thư mục lồng.
6. Nhấn **Commit changes**.

## 3. Tạo web riêng trên Vercel

1. Vào https://vercel.com/new (hoặc Vercel Dashboard → **Add New... → Project**).
2. Chọn workspace `hunglong-7788s-projects`.
3. Chọn **Import Git Repository**, tìm repo `fog-arena-trials-2026` vừa tạo và nhấn **Import**.
4. **Project Name**: `fog-arena-trials-2026` (nếu tên đã có người dùng, đặt `fscxflame-arena-trials-2026`).
5. **Framework Preset**: **Other**. **Root Directory**: `./`. Không đặt Build Command, không đặt Output Directory, không cần cấu hình biến môi trường cho bản thử nghiệm hiện tại.
6. Nhấn **Deploy**. Vercel cấp một URL dạng `https://fog-arena-trials-2026.vercel.app` nếu tên miền còn trống (không phải URL đã được xác minh).

Nếu không thấy repository trong Vercel: vào phần cấu hình GitHub integration từ Vercel, cho phép Vercel truy cập repo mới, rồi quay lại Import. **Không** cần công khai mật khẩu hoặc API keys.

## 4. Kiểm tra TRƯỚC KHI IN QR

Dùng URL thật Vercel đã cấp, mở bằng **điện thoại và laptop**:

- Trang chủ tải đúng logo, font, màu và sáu loại thử thách.
- Nhập nickname (2–16 ký tự) và bấm **Bắt đầu thử thách**.
- Hoàn tất đủ **6 trạm**. Kiểm tra màn **Mission Complete**, số điểm và thời gian phản hồi.
- Mở **Bảng xếp hạng**, xác nhận điểm đã lên, rồi mở link đó trên điện thoại khác và kiểm tra cùng một bảng điểm.
- Mở **Màn hình BTC** trên laptop, thử toàn màn hình; xác nhận BXH cập nhật.
- Kiểm tra mở trên Wi-Fi trường và trên 4G; thử đường dẫn QR ở chế độ ẩn danh.
- Thử trên iOS Safari / Android Chrome / Windows Chrome nếu có.
- Không sử dụng kết quả để trao thưởng trước khi kiểm thử ghi điểm và xác nhận BTC thành công.

**Đường dẫn tiện dùng** (thay `TEN-MIEN-CUA-BAN` bằng URL Vercel thật):

- Chơi game: `https://TEN-MIEN-CUA-BAN/#home`
- BXH: `https://TEN-MIEN-CUA-BAN/#leaderboard`
- Màn hình BTC: `https://TEN-MIEN-CUA-BAN/#spectator`

## 5. Backend đã nối sẵn — CHỈ CHO THỬ NGHIỆM

Bản web trong ZIP hiện trỏ tới Supabase thử nghiệm có sẵn:

`https://sjwyrtgyuwqhhkpcsbuj.supabase.co/functions/v1/arena-trials`

Không cần tạo database hoặc nhập key để nhìn thấy giao diện / test lần đầu. Bảng điểm của Arena Trials là riêng với Glitch Raid. **Tuy nhiên** backend này đang ở dự án Supabase non-production và chưa vượt qua kiểm thử gửi điểm + nhiều thiết bị thực. Bản Vercel vừa deploy từ ZIP là một **bản thử nghiệm công khai**, chưa được bảo đảm để tổ chức sự kiện trao giải chính thức. Khi chạy Club Day đông người, cần chuyển backend sang hệ thống production chuyên biệt, thử tải, đối soát dữ liệu và cách BTC xác minh người thắng.

Nếu mất mạng, có chế độ luyện tập offline, **không ghi vào BXH**.

## 6. Cập nhật web sau này

Sửa file trên GitHub → Commit changes → Vercel tự triển khai lại project riêng này; không ảnh hưởng website FSC x Flame Club Portal hay Glitch Raid.

**Không gửi** mật khẩu, mã OTP, token, service-role key cho người hỗ trợ qua chat.
