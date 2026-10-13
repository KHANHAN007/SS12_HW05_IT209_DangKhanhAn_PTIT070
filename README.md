# SS12 EX05 - Chẩn đoán và khắc phục CI/CD

Project riêng của Đặng Khánh An - PTIT070, môn IT209.

Workflow đã sửa nằm ở `.github/workflows/broken-pipeline.yml`. Báo cáo và minh chứng nằm ở `homework/session_12/ex5/`.

## 1. Tạo repository riêng

Chạy trên Mac:

```bash
cd ~/Study/IT209/ss12/ex05
git init
git branch -M main
git config user.name "KHANHAN007"
git config user.email "khanhanke@gmail.com"
git add .
git commit -m "fix: repair Gradle permissions registry login and Docker context"
gh auth switch -u KHANHAN007
gh repo create KHANHAN007/SS12_HW05_IT209_DangKhanhAn_PTIT070 --public --source . --remote origin
```

## 2. Tạo Repository Secret

Trong repository mới: Settings → Secrets and variables → Actions → New repository secret.

- Name: `REGISTRY_TOKEN`.
- Value: PAT classic của KHANHAN007 có quyền `write:packages`.

PAT chỉ có `read:packages` từ EX04 không đủ để push image trong bài này. Token bài SS11 có thể dùng lại nếu còn hạn và có `write:packages`; phải khai báo Secret ở repository mới.

Không đưa token vào README, file workflow hoặc ảnh chụp.

## 3. Push và kiểm tra

```bash
git push -u origin main
```

Vào Actions → Repaired CI Pipeline → job build. Cần thấy test thành công, `Login Succeeded` và build/push image thành công.

Chụp kết quả xanh, lưu `homework/session_12/ex5/pipeline-success.png`. Điền link run thực tế vào troubleshooting.md rồi commit/push báo cáo và ảnh.

Project không triển khai lên VPS nên không cần SSH secrets. Sơ đồ SVG được cung cấp trong thư mục bài nộp.

## 4. Kiểm tra local

```bash
export JAVA_HOME=$(/usr/libexec/java_home -v 17)
chmod +x gradlew
./gradlew test bootJar --no-daemon
```

Đề chưa cung cấp file workflow lỗi gốc; file hiện tại là bản sửa minh họa dựa trên ba loại lỗi được mô tả. Chưa có log thực nghiệm của ba lỗi trong repository mới.
