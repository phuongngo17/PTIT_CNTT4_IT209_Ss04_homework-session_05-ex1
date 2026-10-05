# Bài 1: Khôi phục commit đã mất bằng Git Reflog

## 1. Tạo commit

Khởi tạo Git repository:

```bash
git init
```

Tạo file `feature.txt` với nội dung:

```text
Day la tinh nang quan trong
```

Đưa file vào staging và commit:

```bash
git add feature.txt
git commit -m "Them tinh nang quan trong"
```

Sau đó thực hiện chỉnh sửa file và tạo commit cần khôi phục:

```bash
git add feature.txt
git commit -m "Them tinh nang quan trong lan 2"
```

Kiểm tra lịch sử:

```bash
git log --oneline
```

Kết quả:

```text
6108274 (HEAD -> master) Them tinh nang quan trong lan 2
58afa14 Tao commit dau tien
1c5d717 them tinh nang quan trong
```

---

## 2. Làm mất commit bằng `git reset --hard`

Thực hiện:

```bash
git reset --hard HEAD~1
```

Kiểm tra lại lịch sử:

```bash
git log --oneline
```

Kết quả:

```text
58afa14 (HEAD -> master) Tao commit dau tien
1c5d717 them tinh nang quan trong
```

Commit `6108274` không còn xuất hiện trong `git log`.

---

## 3. Tìm commit đã mất bằng Reflog

Sử dụng:

```bash
git reflog
```

Kết quả:

```text
6108274 HEAD@{1}: commit: Them tinh nang quan trong lan 2
```

Mã hash của commit đã mất:

```text
6108274
```

---

## 4. Khôi phục commit

Sử dụng mã hash tìm được từ Reflog:

```bash
git reset --hard 6108274
```

Kết quả:

```text
HEAD is now at 6108274 Them tinh nang quan trong lan 2
```

---

## 5. Kiểm tra kết quả

Kiểm tra lại lịch sử:

```bash
git log --oneline
```

Kết quả:

```text
6108274 (HEAD -> master) Them tinh nang quan trong lan 2
58afa14 Tao commit dau tien
1c5d717 them tinh nang quan trong
```

Commit `6108274` đã được khôi phục thành công.

## 6. Kết luận

Thông qua `git reflog`, có thể tìm lại mã hash của commit đã bị mất sau khi sử dụng `git reset --hard`.

Sau khi xác định được mã hash `6108274`, sử dụng:

```bash
git reset --hard 6108274
```

để khôi phục commit thành công.
