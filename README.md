# selenium-test
## Yêu cầu môi trường

1.  **Python** (Phiên bản 3.x trở lên).
2.  **Trình duyệt Chrome** đã được cài đặt.

## Cài đặt

1.  **Clone Repository:**
    ```bash
    git clone [https://github.com/Ten_cua_ban/ten-du-an.git](https://github.com/Ten_cua_ban/ten-du-an.git)
    cd ten-du-an
    ```

2.  **Cài đặt các thư viện cần thiết:**
    Sử dụng file `requirements.txt` để cài đặt Selenium và WebDriver Manager.
    ```bash
    pip install -r requirements.txt
    ```
    *Lưu ý: `webdriver-manager` sẽ tự động tải Chrome Driver phù hợp.*

## Cấu hình (RẤT QUAN TRỌNG)

Mở file `test_login_form.py` và thay đổi các giá trị sau:

1.  Thay thế **`BASE_URL`** bằng URL thực tế của Form Đăng nhập.
2.  Thay thế **`VALID_USERNAME`** và **`VALID_PASSWORD`** bằng thông tin đăng nhập hợp lệ.
3.  Cập nhật **`LOCATOR_USERNAME`**, **`LOCATOR_PASSWORD`**, **`LOCATOR_LOGIN_BUTTON`**... bằng các **Locator** (ID, Name, XPATH, CSS Selector) chính xác của form đăng nhập mục tiêu.

## Cách chạy Test

Chạy tất cả các test case bằng lệnh sau trong thư mục dự án:

```bash
python -m unittest tests.test_login_form
