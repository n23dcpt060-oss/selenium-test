import unittest
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
import time

# Giả định thông tin đăng nhập hợp lệ và URL
VALID_USERNAME = "testuser"
VALID_PASSWORD = "Password123"
BASE_URL = "http://your-website-url/login" # THAY THẾ BẰNG URL THỰC TẾ

class TestLoginForm(unittest.TestCase):

    def setUp(self):
        # Thiết lập WebDriver (sử dụng ChromeDriverManager để tự động quản lý driver)
        self.driver = webdriver.Chrome(service=Service(ChromeDriverManager().install()))
        self.driver.get(BASE_URL)
        self.driver.implicitly_wait(10) # Chờ ngầm 10 giây

    def tearDown(self):
        # Đóng trình duyệt sau mỗi test case
        self.driver.quit()

    # --- Locators (2 điểm) ---
    # Viết gọn, chính xác (Cần thay thế các giá trị XPATH/ID thực tế)
    LOCATOR_USERNAME = (By.NAME, "username") # Giả định: dùng NAME
    LOCATOR_PASSWORD = (By.ID, "password")    # Giả định: dùng ID
    LOCATOR_LOGIN_BUTTON = (By.XPATH, "//button[text()='LOGIN']") # Giả định: dùng XPATH
    LOCATOR_FORGOT_LINK = (By.LINK_TEXT, "Forgot password?")
    LOCATOR_SIGNUP_LINK = (By.LINK_TEXT, "SIGN UP")
    LOCATOR_ERROR_MESSAGE = (By.CLASS_NAME, "alert-error") # Giả định class hiển thị lỗi
    LOCATOR_DASHBOARD_TITLE = (By.TAG_NAME, "h1") # Giả định title trên trang Dashboard

    # --- 6 Test Case (6 điểm) ---

    # 1. Đăng nhập thành công
    def test_01_successful_login(self):
        """Nhập username/password hợp lệ và kiểm tra chuyển trang/thông báo thành công."""
        self.driver.find_element(*self.LOCATOR_USERNAME).send_keys(VALID_USERNAME)
        self.driver.find_element(*self.LOCATOR_PASSWORD).send_keys(VALID_PASSWORD)
        self.driver.find_element(*self.LOCATOR_LOGIN_BUTTON).click()
        
        # Kiểm tra điều hướng (Kiểm tra URL hoặc một phần tử trên trang Dashboard)
        # Cách 1: Kiểm tra URL sau khi đăng nhập
        # self.assertIn("dashboard", self.driver.current_url.lower(), "Không chuyển đến trang Dashboard.")
        # Cách 2: Kiểm tra thông báo thành công (nếu không chuyển trang)
        # self.assertEqual(self.driver.find_element(By.ID, "success-msg").text, "Login success")
        
        # CHỤP ẢNH MÀN HÌNH KẾT QUẢ CHẠY (1 điểm)
        self.driver.save_screenshot("test_01_success_screenshot.png")

    # 2. Sai thông tin đăng nhập (Username đúng, Password sai)
    def test_02_invalid_password(self):
        """Kiểm tra hiển thị thông báo lỗi khi nhập sai mật khẩu."""
        self.driver.find_element(*self.LOCATOR_USERNAME).send_keys(VALID_USERNAME)
        self.driver.find_element(*self.LOCATOR_PASSWORD).send_keys("WrongPassword")
        self.driver.find_element(*self.LOCATOR_LOGIN_BUTTON).click()
        
        # Kiểm tra thông báo lỗi xuất hiện
        error_element = self.driver.find_element(*self.LOCATOR_ERROR_MESSAGE)
        self.assertTrue(error_element.is_displayed(), "Thông báo lỗi không hiển thị.")
        
        self.driver.save_screenshot("test_02_invalid_password_screenshot.png")

    # 3. Bỏ trống trường (Để trống Password)
    def test_03_empty_password(self):
        """Kiểm tra cảnh báo khi bỏ trống trường Password."""
        self.driver.find_element(*self.LOCATOR_USERNAME).send_keys(VALID_USERNAME)
        # Bỏ trống Password
        self.driver.find_element(*self.LOCATOR_LOGIN_BUTTON).click()
        
        # Kiểm tra cảnh báo (ví dụ: HTML5 required attribute) hoặc thông báo lỗi
        # Sử dụng thuộc tính validationMessage nếu là HTML5 form validation
        password_field = self.driver.find_element(*self.LOCATOR_PASSWORD)
        
        # Kiểm tra xem có thông báo lỗi hiển thị không
        error_element = self.driver.find_element(*self.LOCATOR_ERROR_MESSAGE)
        self.assertTrue(error_element.is_displayed(), "Cảnh báo/Thông báo lỗi không hiển thị.")
        
        self.driver.save_screenshot("test_03_empty_password_screenshot.png")


    # 4. Link Forgot password?
    def test_04_forgot_password_link(self):
        """Kiểm tra sự tồn tại và khả năng click của link Forgot password?."""
        forgot_link = self.driver.find_element(*self.LOCATOR_FORGOT_LINK)
        self.assertTrue(forgot_link.is_displayed(), "Link Forgot password? không hiển thị.")
        forgot_link.click()
        
        # Kiểm tra điều hướng sang trang quên mật khẩu
        self.assertIn("forgot", self.driver.current_url.lower(), "Không chuyển sang trang quên mật khẩu.")
        
        self.driver.save_screenshot("test_04_forgot_link_screenshot.png")


    # 5. Link SIGN UP
    def test_05_signup_link(self):
        """Kiểm tra sự tồn tại và khả năng click của link SIGN UP."""
        signup_link = self.driver.find_element(*self.LOCATOR_SIGNUP_LINK)
        self.assertTrue(signup_link.is_displayed(), "Link SIGN UP không hiển thị.")
        signup_link.click()
        
        # Kiểm tra điều hướng sang trang đăng ký
        self.assertIn("signup", self.driver.current_url.lower(), "Không chuyển sang trang đăng ký.")
        
        self.driver.save_screenshot("test_05_signup_link_screenshot.png")

    # 6. Nút social login
    def test_06_social_buttons_exist(self):
        """Kiểm tra sự tồn tại và khả năng click của 3 nút Social Login (F, T, G)."""
        # Giả định locators cho các nút Social Login
        facebook_btn = self.driver.find_element(By.CLASS_NAME, "fa-facebook")
        twitter_btn = self.driver.find_element(By.CLASS_NAME, "fa-twitter")
        google_btn = self.driver.find_element(By.CLASS_NAME, "fa-google")

        self.assertTrue(facebook_btn.is_displayed() and facebook_btn.is_enabled(), "Nút Facebook không hợp lệ.")
        self.assertTrue(twitter_btn.is_displayed() and twitter_btn.is_enabled(), "Nút Twitter không hợp lệ.")
        self.assertTrue(google_btn.is_displayed() and google_btn.is_enabled(), "Nút Google không hợp lệ.")
        
        # Thêm kiểm tra click (tùy chọn, vì thường sẽ chuyển sang domain khác)
        # google_btn.click()
        
        self.driver.save_screenshot("test_06_social_buttons_screenshot.png")


if __name__ == "__main__":
    unittest.main(warnings='ignore')
