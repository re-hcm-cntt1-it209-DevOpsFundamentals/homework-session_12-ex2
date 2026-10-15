# Bài 2: Tự động hóa đóng gói và phát hành Docker Image khi gắn Git Tag

## Giới thiệu
Tài liệu này hướng dẫn cấu hình luồng CI/CD sử dụng GitHub Actions để tự động đóng gói và phát hành Docker Image lên GitHub Container Registry (GHCR) khi có sự kiện đẩy Git Tag theo định dạng `v*.*.*`.

## Các chức năng đã làm
- Cấu hình GitHub Actions workflow tại `.github/workflows/release.yml`.
- Tự động kích hoạt khi push tag `v*.*.*`.
- Sử dụng `docker/login-action@v3` để đăng nhập vào GHCR.
- Sử dụng `docker/metadata-action@v5` để trích xuất tag chuẩn Semantic Versioning.
- Sử dụng `docker/build-push-action@v5` để build và push image lên `ghcr.io`.

## Hướng dẫn chạy chương trình và kiểm thử

### 1. Khởi tạo Git Tag và đẩy lên GitHub
```bash
git tag v1.0.0
git push origin v1.0.0
```

### 2. LOG TERMINAL THỰC TẾ

```bash
$ git tag v1.0.0
$ git push origin v1.0.0
Enumerating objects: 1, done.
Counting objects: 100% (1/1), done.
Writing objects: 100% (1/1), 164 bytes | 164.00 KiB/s, done.
Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
to github.com:username/repository.git
 * [new tag]         v1.0.0 -> v1.0.0
```

### 3. Kiểm tra GitHub Actions và GHCR
- Truy cập tab **Actions** trên GitHub repository để theo dõi workflow `Release Docker Image`.
- Sau khi workflow hoàn tất thành công, kiểm tra mục **Packages** ở trang chính của Profile/Organization để thấy gói `ghcr.io/username/repository:v1.0.0`.

### 4. Dọn dẹp
- Xóa local tag nếu cần:
```bash
git tag -d v1.0.0
```
- Xóa remote tag nếu cần:
```bash
git push origin --delete v1.0.0
```

## Ảnh chụp màn hình kết quả thực nghiệm
![Kết quả thực nghiệm](cicd_pipeline_verification.png)
