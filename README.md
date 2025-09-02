# A project to pull all the result for Samsung Galaxy S25 Ultra in the Amazon Website with their details for the title, price, date and shipping date
#step 1
#Import Libraries
import requests
from bs4 import BeautifulSoup
import re
import datetime
import csv
import time

#step2
# Connect to the website to extract the data
# Example: Search page for Samsung Galaxy S25 Ultra

URL = "https://www.amazon.com.au/s?k=Samsung+Galaxy+S25+Ultra&ref=mr_direct_us_au_au"

headers = {"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)","Accept-Language": "en-US,en;q=0.9"}

page = requests.get(URL, headers=headers)
soup = BeautifulSoup(page.text, "html.parser")

 for item in items:
        # Title
        title_tag = item.find("h2", class_="a-size-base-plus a-spacing-none a-color-base a-text-normal")
        title = title_tag.get_text(strip=True) if title_tag else "Title not found"
        
        shipping_tag = item.find("span", class_="a-text-bold")
        shipping = shipping_tag.get_text(strip=True) if shipping_tag else "Shipping not found"

        # Price
        price_tag = item.find("span", class_="a-price-whole")
        if not price_tag:
            price_tag = item.find("span", class_="a-offscreen")  # fallback
        price_str = price_tag.get_text(strip=True) if price_tag else "Price not found"

        
 # 🔹 Each search result is inside "div" with class "s-result-item"
    items = soup.find_all("div", {"data-asin": True, "class": "s-result-item"})

    results = []


  # Coversion of the price into float and sorting
price = None
        if price_str != "Price not found":
            price_clean = price_str.replace("$", "").replace(",", "").replace("AUD", "").strip()
            try:
                price = float(price_clean)
            except ValueError:
                price = None

        if price:  # only keep items with valid price
            results.append([title, price, today,shipping])

        results.sort(key=lambda x: x[1])


   # Define a function to pull the Title, Price, Shipping date etc.


def scrape_search_results():
    # Example: Search page for Samsung Galaxy S25 Ultra
    URL = "https://www.amazon.com.au/s?k=Samsung+Galaxy+S25+Ultra&ref=mr_direct_us_au_au"

    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
        "Accept-Language": "en-US,en;q=0.9",
    }

    page = requests.get(URL, headers=headers)
    soup = BeautifulSoup(page.text, "html.parser")

    today = datetime.date.today()

    # 🔹 Each search result is inside "div" with class "s-result-item"
    items = soup.find_all("div", {"data-asin": True, "class": "s-result-item"})

    results = []

    for item in items:
        # Title
        title_tag = item.find("h2", class_="a-size-base-plus a-spacing-none a-color-base a-text-normal")
        title = title_tag.get_text(strip=True) if title_tag else "Title not found"
        #Shipping_date
        shipping_tag = item.find("span", class_="a-text-bold")
        shipping = shipping_tag.get_text(strip=True) if shipping_tag else "Shipping not found"

        # Price
        price_tag = item.find("span", class_="a-price-whole")
        if not price_tag:
            price_tag = item.find("span", class_="a-offscreen")  # fallback
        price_str = price_tag.get_text(strip=True) if price_tag else "Price not found"

        price = None
        if price_str != "Price not found":
            price_clean = price_str.replace("$", "").replace(",", "").replace("AUD", "").strip()
            try:
                price = float(price_clean)
            except ValueError:
                price = None

        if price:  # only keep items with valid price
            results.append([title, price, today,shipping])

        results.sort(key=lambda x: x[1])
        # Save to CSV
    with open("Amazon_Search_Results.csv", "w", newline="", encoding="UTF8") as f:
        writer = csv.writer(f)
        writer.writerow(["Title", "Price", "Date", "Shipping"])
        writer.writerows(results)



    print(f"✅ Saved {len(results)} products to Amazon_Search_Results.csv")

scrape_search_results()


 # Save to CSV
    with open("Amazon_Search_Results.csv", "w", newline="", encoding="UTF8") as f:
        writer = csv.writer(f)
        writer.writerow(["Title", "Price", "Date", "Shipping"])
        writer.writerows(results)



#Final Function

import requests
from bs4 import BeautifulSoup
import re
import datetime
import csv
import time

def scrape_search_results():
    # Example: Search page for Samsung Galaxy S25 Ultra
    URL = "https://www.amazon.com.au/s?k=Samsung+Galaxy+S25+Ultra&ref=mr_direct_us_au_au"

    headers = {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64)",
        "Accept-Language": "en-US,en;q=0.9",
    }

    page = requests.get(URL, headers=headers)
    soup = BeautifulSoup(page.text, "html.parser")

    today = datetime.date.today()

    # 🔹 Each search result is inside "div" with class "s-result-item"
    items = soup.find_all("div", {"data-asin": True, "class": "s-result-item"})

    results = []

    for item in items:
        # Title
        title_tag = item.find("h2", class_="a-size-base-plus a-spacing-none a-color-base a-text-normal")
        title = title_tag.get_text(strip=True) if title_tag else "Title not found"
        
        shipping_tag = item.find("span", class_="a-text-bold")
        shipping = shipping_tag.get_text(strip=True) if shipping_tag else "Shipping not found"

        # Price
        price_tag = item.find("span", class_="a-price-whole")
        if not price_tag:
            price_tag = item.find("span", class_="a-offscreen")  # fallback
        price_str = price_tag.get_text(strip=True) if price_tag else "Price not found"

        price = None
        if price_str != "Price not found":
            price_clean = price_str.replace("$", "").replace(",", "").replace("AUD", "").strip()
            try:
                price = float(price_clean)
            except ValueError:
                price = None

        if price:  # only keep items with valid price
            results.append([title, price, today,shipping])

        results.sort(key=lambda x: x[1])


    # Save to CSV
    with open("Amazon_Search_Results.csv", "w", newline="", encoding="UTF8") as f:
        writer = csv.writer(f)
        writer.writerow(["Title", "Price", "Date", "Shipping"])
        writer.writerows(results)

    print(f"✅ Saved {len(results)} products to Amazon_Search_Results.csv")

scrape_search_results()


# Autosearch within mentioned time(5 sec)
while(True):
    scrape_search_results()
    time.sleep(5)

# Extraction of the Dataframe that saved as CSV file
import pandas as pd

df = pd.read_csv(r'C:\Users\mesag\Amazon_Search_Results.csv')
print(df)    


