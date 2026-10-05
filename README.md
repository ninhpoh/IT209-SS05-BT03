# Bài 3: Xử lý xung đột phức tạp trong quá trình Rebase

## 1. Mục tiêu

Thực hiện rebase nhánh `feature-api` lên `main` và xử lý conflict thủ công từng chặng.

## 2. Các commit

### Main

```text
init config
update port on main
add env config
```

### Feature-api

```text
feat: change port
feat: enable debug
```

## 3. Thực hiện Rebase

Chuyển sang nhánh `feature-api`:

```bash
git checkout feature-api
```

Thực hiện:

```bash
git rebase main
```

## 4. Conflict lần 1

Conflict xảy ra tại `config.json` khi áp dụng commit:

```text
feat: change port
```

Main có:

```json
"port": 8081
```

Feature có:

```json
"port": 9000
```

Đã giải quyết thủ công và giữ `port: 9000`, đồng thời giữ `env: production` của main.

Sau đó:

```bash
git add config.json
git rebase --continue
```

## 5. Conflict lần 2

Conflict tiếp tục xảy ra tại `config.json` khi áp dụng commit:

```text
feat: enable debug
```

Đã giải quyết thủ công và kết quả cuối cùng:

```json
{
  "port": 9000,
  "debug": true,
  "env": "production"
}
```

Sau đó:

```bash
git add config.json
git rebase --continue
```

Rebase hoàn tất thành công.

## 6. Kiểm tra

### Kiểm tra trạng thái

```bash
git status
```

Kết quả:

```text
On branch feature-api
nothing to commit, working tree clean
```

### Kiểm tra lịch sử

```bash
git log --graph --oneline --all
```

Kết quả:

```text
* a3a6e2d (HEAD -> feature-api) feat: enable debug
* be0e297 feat: change port
* d058f92 (main) add env config
* d13d459 update port on main
* 56df06b init config
```

## 7. Kết luận

Đã hoàn thành bài Rebase và xử lý thành công 2 lần conflict.

Lịch sử sau rebase được sắp xếp thẳng hàng, không có merge commit phụ.
