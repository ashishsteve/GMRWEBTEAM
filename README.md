# GMRWEBTEAM
Verification of contact form

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.action_chains import ActionChains
import time

# Set up the WebDriver (Make sure to provide the correct path to your WebDriver)
driver = webdriver.Chrome(executable_path="path_to_chromedriver")  # Replace with your chromedriver path

# Open the website with the contact form
driver.get("http://example.com/contact")  # Replace with the actual URL of the page

# Find the form elements (make sure to use the correct locators based on the HTML of the form)
name_field = driver.find_element(By.NAME, "name")  # Use the correct name or ID attribute of the name input field
email_field = driver.find_element(By.NAME, "email")  # Use the correct name or ID attribute of the email input field
message_field = driver.find_element(By.NAME, "message")  # Use the correct name or ID attribute of the message input field
submit_button = driver.find_element(By.ID, "submit")  # Use the correct ID or another locator for the submit button

# Fill in the form with test data
name_field.send_keys("John Doe")
email_field.send_keys("johndoe@example.com")
message_field.send_keys("This is a test message to verify the contact form functionality.")

# Submit the form (simulating clicking the submit button)
submit_button.click()

# Wait for the response (e.g., success message or confirmation)
time.sleep(3)  # Wait for 3 seconds to allow the page to load or display the success message

# Verify if the success message appears (you can customize the locator as per the HTML of your success message)
try:
    success_message = driver.find_element(By.ID, "success_message")  # Adjust the ID as needed
    if success_message.is_displayed():
        print("Form submitted successfully!")
    else:
        print("Success message not displayed.")
except Exception as e:
    print("Error: ", str(e))

# Optionally: Check if any validation error message is shown for empty fields
try:
    error_message = driver.find_element(By.CLASS_NAME, "error")  # Adjust to the error class or locator used in the form
    if error_message.is_displayed():
        print("Form submission failed due to validation errors.")
except Exception as e:
    print("No error message detected.")

# Close the browser after the test
driver.quit()

