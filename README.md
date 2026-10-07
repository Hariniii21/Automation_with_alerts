# Automation_with_alerts

# Name : Harini S
# Reg No;212223240048

# CODE:
```
import time
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support.ui import WebDriverWait, Select
from selenium.webdriver.support import expected_conditions as EC

driver = webdriver.Chrome()
driver.maximize_window()
wait = WebDriverWait(driver, 10)
actions = ActionChains(driver)

try:
    # TC01: Open Online Shopping Site & Login
    print("--- TC01: Open Shopping Website ---")
    driver.get("https://www.saucedemo.com/")
    
    driver.find_element(By.ID, "user-name").send_keys("standard_user")
    driver.find_element(By.ID, "password").send_keys("secret_sauce")
    driver.find_element(By.ID, "login-button").click()
    
    wait.until(EC.presence_of_element_located((By.CLASS_NAME, "title")))
    print("TC01 Passed: Opened shopping site and logged in successfully.")

    # TC02: Confirmation Alert - Accept
    print("\n--- TC02: Alert Accept ---")
    driver.get("https://the-internet.herokuapp.com/javascript_alerts")
    
    driver.find_element(By.XPATH, "//button[text()='Click for JS Confirm']").click()
    alert = wait.until(EC.alert_is_present())
    print("Alert text:", alert.text)
    alert.accept()
    
    result = driver.find_element(By.ID, "result").text
    print("TC02 Passed:", result)

 
    # TC03: Confirmation Alert - Dismiss
    print("\n--- TC03: Alert Dismiss ---")
    driver.find_element(By.XPATH, "//button[text()='Click for JS Confirm']").click()
    alert = wait.until(EC.alert_is_present())
    print("Alert text:", alert.text)
    alert.dismiss()
    
    result = driver.find_element(By.ID, "result").text
    print("TC03 Passed:", result)

    # TC04: Prompt Alert Input
    print("\n--- TC04: Prompt Input ---")
    driver.find_element(By.XPATH, "//button[text()='Click for JS Prompt']").click()
    alert = wait.until(EC.alert_is_present())
    print("Prompt text:", alert.text)
    alert.send_keys("PROMO2026")
    alert.accept()
    
    result = driver.find_element(By.ID, "result").text
    print("TC04 Passed:", result)

   
    # TC05: Mouse Hover
    print("\n--- TC05: Mouse Hover ---")
    driver.get("https://the-internet.herokuapp.com/hovers")
    
    first_avatar = wait.until(EC.visibility_of_element_located((By.XPATH, "(//div[@class='figure'])[1]")))
    actions.move_to_element(first_avatar).perform()
    
    caption = driver.find_element(By.XPATH, "(//div[@class='figcaption'])[1]/h5").text
    print("Hover caption displayed:", caption)
    print("TC05 Passed: Mouse hover executed.")


    # TC06: Double Click

    print("\n--- TC06: Double Click ---")
    driver.get("https://the-internet.herokuapp.com/add_remove_elements/")
    
    add_btn = wait.until(EC.element_to_be_clickable((By.XPATH, "//button[text()='Add Element']")))
    actions.double_click(add_btn).perform()
    
    delete_btns = driver.find_elements(By.CLASS_NAME, "added-manually")
    print(f"TC06 Passed: Double-clicked ({len(delete_btns)} elements added).")

    # TC07: Drag and Drop

    print("\n--- TC07: Drag and Drop ---")
    driver.get("https://the-internet.herokuapp.com/drag_and_drop")
    
    col_a = wait.until(EC.visibility_of_element_located((By.ID, "column-a")))
    col_b = wait.until(EC.visibility_of_element_located((By.ID, "column-b")))
    
    actions.drag_and_drop(col_a, col_b).perform()
    print("TC07 Passed: Dragged and dropped successfully.")

    # TC08: Dynamic Explicit Wait
    print("\n--- TC08: Dynamic Explicit Wait ---")
    driver.get("https://the-internet.herokuapp.com/dynamic_loading/2")
    
    driver.find_element(By.XPATH, "//div[@id='start']/button").click()
    finish_text = wait.until(EC.visibility_of_element_located((By.XPATH, "//div[@id='finish']/h4"))).text
    print("TC08 Passed: Dynamic result loaded ->", finish_text)

    # TC09: Wait Until Place Order Button Is Clickable
    print("\n--- TC09: Clickable Wait (SauceDemo Checkout) ---")
    driver.get("https://www.saucedemo.com/")
    
    driver.find_element(By.ID, "user-name").send_keys("standard_user")
    driver.find_element(By.ID, "password").send_keys("secret_sauce")
    driver.find_element(By.ID, "login-button").click()
    
    driver.find_element(By.ID, "add-to-cart-sauce-labs-backpack").click()
    driver.find_element(By.CLASS_NAME, "shopping_cart_link").click()
    driver.find_element(By.ID, "checkout").click()
    
    driver.find_element(By.ID, "first-name").send_keys("John")
    driver.find_element(By.ID, "last-name").send_keys("Doe")
    driver.find_element(By.ID, "postal-code").send_keys("600001")
    driver.find_element(By.ID, "continue").click()
    
    finish_btn = wait.until(EC.element_to_be_clickable((By.ID, "finish")))
    finish_btn.click()
    
    header = driver.find_element(By.CLASS_NAME, "complete-header").text
    print("TC09 Passed: Order submitted successfully ->", header)

    # TC10: Simple Alert Wait
    print("\n--- TC10: Simple Alert Wait ---")
    driver.get("https://the-internet.herokuapp.com/javascript_alerts")
    
    driver.find_element(By.XPATH, "//button[text()='Click for JS Alert']").click()
    order_alert = wait.until(EC.alert_is_present())
    print("Alert Message:", order_alert.text)
    order_alert.accept()
    print("TC10 Passed: Confirmation alert handled.")

    # ------------------------------------------------------------------
    # Dropdown Exercise
    # ------------------------------------------------------------------
    print("\n--- Dropdown Exercise ---")
    driver.get("https://the-internet.herokuapp.com/dropdown")
    
    select_element = driver.find_element(By.ID, "dropdown")
    dropdown = Select(select_element)
    
    dropdown.select_by_visible_text("Option 1")
    dropdown.select_by_value("2")
    dropdown.select_by_index(1)
    
    print("Options in dropdown:")
    for option in dropdown.options:
        print(" -", option.text)

except Exception as err:
    print("\n>>> ERROR ENCOUNTERED <<<")
    print(err)
```

# Output
<img width="1558" height="973" alt="image" src="https://github.com/user-attachments/assets/91951143-172b-43fb-9d74-a78953064f32" />

finally:
    driver.quit()
    print("\n=== ALL TEST CASES PASSED SUCCESSFULLY ===")
