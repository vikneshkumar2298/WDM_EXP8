### EX8 Web Scraping On E-commerce platform using BeautifulSoup
### AIM: To perform Web Scraping on Amazon using (beautifulsoup) Python.
### Description: 
<div align = "justify">
Web scraping is the process of extracting data from various websites and parsing it. In other words, it’s a technique 
to extract unstructured data and store that data either in a local file or in a database. 
There are many ways to collect data that involve a huge amount of hard work and consume a lot of time. Web scraping can save programmers many hours. Beautiful Soup is a Python web scraping library that allows us to parse and scrape HTML and XML pages. 
One can search, navigate, and modify data using a parser. It’s versatile and saves a lot of time.
<p>The basic steps involved in web scraping are:
<p>1) Loading the document (HTML content)
<p>2) Parsing the document
<p>3) Extraction
<p>4) Transformation

### Procedure:

1) Import necessary libraries (requests, BeautifulSoup, re, matplotlib.pyplot).
2) Define convert_price_to_float(price) Function: to Remove non-numeric characters from a price string and convert it to a float.
3) Define get_amazon_products(search_query) Function: to Scrape Amazon for product information based on the search query.
4) Fetch and parse the HTML content then Extract product names and prices from the search results and Sort product information based on converted prices in ascending order.
5) Return sorted product data as a list of dictionaries.
6) Call get_amazon_products(search_query) to get product data based on the user's search query.
7) Check if products are found; if not, display "No products found."
8) Visualize Product Data using a Bar Chart

### Program:
```PYTHON
import requests
from bs4 import BeautifulSoup
import time

search_query = input("Enter the book name to search: ").strip().lower()

base_url = "http://books.toscrape.com/catalogue/page-{}.html"
num_pages = 5   # You can increase pages if needed

matched_books = []

for page in range(1, num_pages + 1):
    print(f"Checking page {page}...")
    
    url = base_url.format(page)
    response = requests.get(url)
    
    if response.status_code != 200:
        continue
    
    soup = BeautifulSoup(response.text, "html.parser")
    books = soup.find_all("article", class_="product_pod")
    
    for book in books:
        title = book.h3.a["title"]
        
        # Check if user input matches book title
        if search_query in title.lower():
            
            price = book.find("p", class_="price_color").text.strip()
            availability = book.find("p", class_="instock availability").text.strip()
            rating_class = book.find("p", class_="star-rating")["class"]
            rating = rating_class[1]
            
            matched_books.append({
                "Title": title,
                "Price": price,
                "Availability": availability,
                "Rating": rating
            })
    
    time.sleep(1)

# Display Results
if not matched_books:
    print("\nNo matching books found.")
else:
    print(f"\nFound {len(matched_books)} matching books:\n")
    
    for i, book in enumerate(matched_books, 1):
        print(f"{i}. Title: {book['Title']}")
        print(f"   Price: {book['Price']}")
        print(f"   Availability: {book['Availability']}")
        print(f"   Rating: {book['Rating']}")
        print("-" * 60)
        

```

### Output:

<img width="1653" height="672" alt="image" src="https://github.com/user-attachments/assets/ef4d8ddf-7440-43d7-80d5-08798e8de25c" />


### Result:

Thus,Web Scraping On E-commerce platform using BeautifulSoup is done .
