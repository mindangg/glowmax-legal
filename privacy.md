# Chính sách Bảo mật — Glowmax

**Ngày hiệu lực:** 17/05/2026
**Phiên bản:** 1.0

*English version below — [Jump to English](#privacy-policy--glowmax-english)*

---

## 1. Giới thiệu

Glowmax ("ứng dụng", "chúng tôi") là ứng dụng di động phân tích thẩm mỹ khuôn mặt sử dụng trí tuệ nhân tạo. Chính sách này mô tả cách chúng tôi thu thập, sử dụng, và bảo vệ thông tin của bạn khi sử dụng Glowmax trên iOS.

Bằng việc sử dụng Glowmax, bạn đồng ý với các điều khoản trong chính sách này.

## 2. Thông tin chúng tôi thu thập

### 2.1. Thông tin do bạn cung cấp

| Loại dữ liệu | Mục đích | Khi nào thu thập |
|---|---|---|
| **Tên người dùng** (username) | Hiển thị trên bảng xếp hạng | Khi tạo tài khoản |
| **Địa chỉ email** | Xác thực tài khoản, liên hệ hỗ trợ | Khi đăng nhập bằng Google/Apple |
| **Ảnh khuôn mặt** (chính diện + nghiêng) | Phân tích thẩm mỹ bằng AI | Khi thực hiện scan |
| **Câu trả lời onboarding** (chiều cao, cân nặng, mục tiêu, mức độ tự tin) | Cá nhân hoá kết quả + đề xuất | Trong quá trình onboarding |

### 2.2. Thông tin tự động thu thập

| Loại dữ liệu | Mục đích |
|---|---|
| **User ID** (định danh tài khoản) | Đồng bộ dữ liệu giữa các phiên |
| **Device ID** (định danh thiết bị) | Phân biệt người dùng ẩn danh trước khi đăng nhập |
| **Lịch sử mua hàng** (gói subscription) | Xác minh quyền truy cập tính năng Premium |
| **Tương tác trong app** (lượt nhấn, màn hình xem, tính năng sử dụng) | Phân tích hành vi để cải thiện sản phẩm |
| **Dữ liệu lỗi (crash logs)** | Phát hiện và sửa lỗi |
| **Dữ liệu hiệu năng** (thời gian load, độ trễ) | Tối ưu trải nghiệm |

### 2.3. Chúng tôi KHÔNG thu thập

- ❌ Vị trí (location)
- ❌ Danh bạ (contacts)
- ❌ Tin nhắn, email, lịch sử trình duyệt
- ❌ Thông tin tài chính (số thẻ tín dụng, tài khoản ngân hàng) — toàn bộ thanh toán do Apple và RevenueCat xử lý, ứng dụng KHÔNG bao giờ thấy thông tin thẻ của bạn
- ❌ Dữ liệu sinh trắc học (vân tay, Face ID) — Face ID nếu có chỉ dùng để mở khoá thiết bị, do iOS xử lý

## 3. Bên thứ ba xử lý dữ liệu

Để vận hành ứng dụng, chúng tôi sử dụng các dịch vụ bên thứ ba sau:

| Nhà cung cấp | Mục đích | Loại dữ liệu được chia sẻ |
|---|---|---|
| **OpenAI** (openai.com) | Phân tích thẩm mỹ ảnh khuôn mặt bằng GPT-4o | Ảnh khuôn mặt (không kèm User ID), câu trả lời onboarding |
| **Amazon Web Services (AWS S3)** | Lưu trữ ảnh đại diện (avatar) | Ảnh avatar (240×240), User ID |
| **Sentry** (sentry.io) | Báo cáo lỗi và hiệu năng | Crash logs, User ID, thiết bị, OS version |
| **PostHog** (posthog.com) | Phân tích hành vi sản phẩm | Event names, screen views, User ID, Device ID |
| **RevenueCat** (revenuecat.com) | Xử lý subscription | User ID, purchase history |
| **Apple Sign In / Google Sign In** | Xác thực tài khoản | Email, tên (chỉ khi user cấp quyền) |
| **Apple App Store / Google Play** | Xử lý thanh toán | Thông tin giao dịch (chúng tôi KHÔNG nhận thẻ tín dụng) |

Chúng tôi **KHÔNG**:
- ❌ Bán dữ liệu của bạn cho bên thứ ba
- ❌ Sử dụng dữ liệu cho mục đích quảng cáo (không có ads trong app, không tracking ATT)
- ❌ Chia sẻ dữ liệu với data brokers
- ❌ Sử dụng SDK quảng cáo (Facebook SDK, Google Ads, AppsFlyer, Adjust, Branch)

## 4. Ảnh khuôn mặt — chi tiết quan trọng

- Ảnh được **xử lý** (resize, crop) trên thiết bị trước khi upload
- Ảnh được gửi tới backend (Spring Boot trên AWS EC2 Singapore) → forward tới OpenAI để phân tích
- Ảnh **KHÔNG được lưu trữ vĩnh viễn** trên server của chúng tôi — chỉ giữ trong bộ nhớ tạm trong quá trình xử lý (~30 giây)
- **Ảnh đại diện** (avatar) bạn chọn để hiển thị trên bảng xếp hạng sẽ được lưu trên AWS S3 (Singapore) cho đến khi bạn thay đổi hoặc xoá tài khoản
- OpenAI **KHÔNG sử dụng ảnh của bạn để train model** (theo policy của OpenAI dành cho API customers)

## 5. Lưu trữ và bảo mật dữ liệu

- **Vị trí lưu trữ:** AWS EC2 + RDS (PostgreSQL) tại khu vực `ap-southeast-1` (Singapore)
- **Mã hoá truyền tải:** HTTPS/TLS 1.3 trên mọi kết nối
- **Mã hoá lưu trữ:** AES-256 (AWS RDS encryption at rest, S3 server-side encryption)
- **Xác thực:** JWT (JSON Web Token), refresh token rotation
- **Bảo mật token:** lưu trong iOS Keychain (`expo-secure-store`)

## 6. Quyền của bạn

Bạn có các quyền sau với dữ liệu cá nhân:

- **Truy cập:** Xem dữ liệu chúng tôi lưu về bạn trong tab Profile của ứng dụng
- **Chỉnh sửa:** Đổi username, ảnh đại diện trong app
- **Xoá tài khoản:** Vào Profile → "Xoá tài khoản" → toàn bộ dữ liệu (profile, scores, avatar) sẽ bị xoá trong vòng 30 ngày
- **Rút lại đồng ý:** Đăng xuất hoặc xoá app sẽ ngừng thu thập dữ liệu mới
- **Yêu cầu xuất dữ liệu:** Gửi email tới địa chỉ ở mục 10

## 7. Trẻ em dưới 13 tuổi

Glowmax được phân loại **9+ trên App Store**. Chúng tôi **KHÔNG cố ý** thu thập dữ liệu cá nhân của trẻ em dưới 13 tuổi (theo COPPA). Nếu bạn là phụ huynh và phát hiện con mình đã tạo tài khoản, vui lòng liên hệ chúng tôi để xoá.

## 8. Lưu giữ dữ liệu

| Loại dữ liệu | Thời gian lưu |
|---|---|
| Tài khoản và profile | Cho đến khi user xoá tài khoản |
| Ảnh khuôn mặt (scan) | Không lưu (chỉ trong bộ nhớ tạm khi xử lý) |
| Ảnh đại diện | Cho đến khi user thay đổi/xoá |
| Lịch sử scan + điểm số | Cho đến khi user xoá tài khoản |
| Crash logs (Sentry) | 90 ngày |
| Analytics events (PostHog) | 12 tháng |

## 9. Thay đổi chính sách

Chúng tôi có thể cập nhật chính sách này theo thời gian. Phiên bản mới sẽ hiển thị "Ngày hiệu lực" mới ở đầu trang. Thay đổi quan trọng sẽ được thông báo trong app trước khi có hiệu lực.

## 10. Liên hệ

Mọi câu hỏi về chính sách bảo mật hoặc dữ liệu cá nhân:

- **Email:** minhdang875425@gmail.com
- **Đối tượng:** Trần Minh Đăng (cá nhân nhà phát triển)
- **Quốc gia:** Việt Nam

---

# Privacy Policy — Glowmax (English)

**Effective date:** May 17, 2026
**Version:** 1.0

## 1. Introduction

Glowmax ("the app", "we", "us") is a mobile application that performs AI-powered facial aesthetic analysis. This policy describes how we collect, use, and protect your information when using Glowmax on iOS.

By using Glowmax, you agree to the terms of this policy.

## 2. Information we collect

### 2.1. Information you provide

| Data type | Purpose | When collected |
|---|---|---|
| **Username** | Display on leaderboard | Account creation |
| **Email address** | Account authentication, support | When signing in with Google/Apple |
| **Face photos** (front + side) | AI aesthetic analysis | When performing a scan |
| **Onboarding answers** (height, weight, goals, confidence) | Personalize results | During onboarding |

### 2.2. Automatically collected

| Data type | Purpose |
|---|---|
| **User ID** | Sync data across sessions |
| **Device ID** | Identify anonymous users before login |
| **Purchase history** | Verify Premium entitlement |
| **In-app interactions** (taps, screens, features) | Product analytics |
| **Crash logs** | Bug detection |
| **Performance data** (load times, latency) | UX optimization |

### 2.3. We do NOT collect

- ❌ Location
- ❌ Contacts
- ❌ Messages, email, browsing history
- ❌ Financial info (card numbers, bank account) — payment is handled entirely by Apple and RevenueCat; the app never sees your card details
- ❌ Biometric data (fingerprint, Face ID) — Face ID, if used, is only for device unlock and is handled by iOS

## 3. Third-party processors

We use the following third-party services:

| Provider | Purpose | Data shared |
|---|---|---|
| **OpenAI** | Image analysis via GPT-4o | Face photos (without User ID), onboarding answers |
| **Amazon Web Services (AWS S3)** | Avatar storage | Avatar image (240×240), User ID |
| **Sentry** | Error and performance monitoring | Crash logs, User ID, device info |
| **PostHog** | Product analytics | Event names, screen views, User ID, Device ID |
| **RevenueCat** | Subscription management | User ID, purchase history |
| **Apple / Google Sign In** | Authentication | Email, name (only with user consent) |
| **Apple App Store / Google Play** | Payment processing | Transaction info (we never receive card data) |

We do **NOT**:
- ❌ Sell your data to third parties
- ❌ Use data for advertising (no ads, no ATT tracking)
- ❌ Share data with data brokers
- ❌ Use advertising SDKs (Facebook SDK, Google Ads, AppsFlyer, Adjust, Branch)

## 4. Face photos — important details

- Photos are **processed** (resize, crop) on-device before upload
- Photos are sent to our backend (Spring Boot on AWS EC2 Singapore) → forwarded to OpenAI for analysis
- Photos are **NOT permanently stored** on our servers — only kept in memory during processing (~30 seconds)
- **Avatar** you choose for the leaderboard is stored on AWS S3 (Singapore) until you change or delete your account
- OpenAI **does NOT use your photos to train models** (per OpenAI's API customer policy)

## 5. Data storage and security

- **Storage location:** AWS EC2 + RDS (PostgreSQL) in `ap-southeast-1` (Singapore)
- **In-transit encryption:** HTTPS/TLS 1.3 on all connections
- **At-rest encryption:** AES-256 (AWS RDS encryption at rest, S3 server-side encryption)
- **Authentication:** JWT (JSON Web Token), refresh token rotation
- **Token security:** stored in iOS Keychain (`expo-secure-store`)

## 6. Your rights

You have the following rights over your personal data:

- **Access:** View your stored data in the Profile tab
- **Edit:** Change username, avatar in-app
- **Delete account:** Profile → "Delete account" → all data (profile, scores, avatar) deleted within 30 days
- **Withdraw consent:** Sign out or uninstall to stop new data collection
- **Data export:** Email the address in section 10

## 7. Children under 13

Glowmax is rated **9+ on the App Store**. We do **NOT knowingly** collect personal data from children under 13 (per COPPA). If you are a parent and discover your child has created an account, please contact us to delete it.

## 8. Data retention

| Data type | Retention |
|---|---|
| Account and profile | Until user deletes account |
| Face photos (scans) | Not stored (only in-memory during processing) |
| Avatar | Until user changes/deletes |
| Scan history and scores | Until user deletes account |
| Crash logs (Sentry) | 90 days |
| Analytics events (PostHog) | 12 months |

## 9. Policy changes

We may update this policy over time. New versions will show an updated "Effective date" at the top. Material changes will be notified in-app before taking effect.

## 10. Contact

For any questions about this privacy policy or your personal data:

- **Email:** minhdang875425@gmail.com
- **Developer:** Tran Minh Dang (individual developer)
- **Country:** Vietnam
