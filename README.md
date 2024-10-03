# Web Scraping Project: Largest Companies by Revenue from Wikipedia

## Introduction
This project aims to scrape data from Wikipedia to compile a list of the largest companies by revenue. This method provides a systematic approach to data collection, which is especially useful for academic research, market analysis, or tracking industry trends.

## Tools and Technologies
### Python
Python is used for scripting the web scraping logic due to its rich ecosystem of libraries.
### Selenium
Selenium automates web browser interaction, allowing us to fetch dynamically loaded data.
### BeautifulSoup
BeautifulSoup parses HTML content, enabling us to extract structured data from raw HTML.
### Pandas
Pandas is used for data manipulation and analysis, allowing us to organize data into a readable and analyzable format.

## Environment Setup
### Install Python
Ensure Python is installed on your machine. Download it from [python.org](https://www.python.org/downloads/).
### Install Required Libraries
Install Selenium, BeautifulSoup, and Pandas using pip. Run the following command in your terminal:
```bash
pip install selenium beautifulsoup4 pandas
```

### Step 2: Initialize WebDriver
Set up Selenium WebDriver to control your browser programmatically.

driver = webdriver.Chrome()  # Adjust if using a different browser

### Step 3: Access the Web Page
Direct Selenium to open the Wikipedia page with the list of companies.

url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_by_revenue'
driver.get(url)

### Step 4: Ensure Page Load Completeness
Incorporate a wait function to ensure all components of the page have fully loaded.

driver.implicitly_wait(10)  # Adjust time as necessary

### Step 5: Retrieve HTML Content
Fetch the HTML content of the page from Selenium and then close the browser.

html_content = driver.page_source
driver.quit()

### Step 6: Parse HTML with BeautifulSoup
Utilize BeautifulSoup to parse the HTML content retrieved.

soup = BeautifulSoup(html_content, 'html.parser')

### Step 7: Data Extraction
Locate the table in the HTML and extract relevant data from each row.

table = soup.find('table', {'class': 'wikitable'})
data = []
for row in table.find_all('tr'): \
    cols = row.find_all('td') \
    if cols:
        data.append({
            'Rank': cols[0].text.strip(),
            'Name': cols[1].text.strip(),
            'Industry': cols[2].text.strip(),
            'Revenue (USD billion)': cols[3].text.strip(),
            'Fiscal Year': cols[4].text.strip(),
            'Employees': cols[5].text.strip(),
            'Headquarters': cols[6].text.strip(),
        })
### Step 8: Save Data
Convert the extracted data into a pandas DataFrame and then export it to a CSV file.

df = pd.DataFrame(data)
df.to_csv('largest_companies.csv', index=False)

### Conclusion
The automated web scraping project efficiently compiles critical data from Wikipedia, facilitating easy access to updated and structured information on the world's largest companies by revenue. This method is scalable and can be adapted for various other data extraction tasks.

