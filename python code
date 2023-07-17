"""
Automated program to play https://gabrielecirulli.github.io/2048/
"""

# import required modules
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.desired_capabilities import DesiredCapabilities
from time import sleep

# open a new csv or wipe the existing one
filename = open("play_2048_high_scores.csv", "w")
filename.close()

# open the game in browser
# bypass the endless loading once the html shows on screen
capa = DesiredCapabilities.CHROME
capa["pageLoadStrategy"] = "none"
driver = webdriver.Chrome(desired_capabilities=capa)

wait = WebDriverWait(driver, 10)
driver.get("https://gabrielecirulli.github.io/2048/")
driver.maximize_window()
wait.until(EC.presence_of_element_located((By.XPATH, "//html")))

# wait for the endless loading to resolve itself then game commences
sleep(3)

# find the game board and repeatedly press up, right, down, left in that order
buttons = driver.find_element(By.XPATH, "//html")

count = 1
while count <= 1000:
    try:
        # code will crash when game is done
        # check for the try again button
        # save the current high score to a csv file
        driver.find_element(By.XPATH, "/html/body/div[1]/div[3]/div[1]/div/a[2]").click()
        high_score = driver.find_element(By.CSS_SELECTOR, ".best-container")

        with open("play_2048_high_scores.csv", "a") as f:
            f.write(f"The high score as of game {count} is {str(high_score.text)}.\n")

        count += 1
    except Exception as ex:
        buttons.send_keys(Keys.UP)
        buttons.send_keys(Keys.RIGHT)
        buttons.send_keys(Keys.DOWN)
        buttons.send_keys(Keys.LEFT)
