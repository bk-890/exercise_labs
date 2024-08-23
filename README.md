# exercise_labs
Lab exercises from the IBM Coursera courses.

# Exercise: use webscraping to extract stock data
Amazon data: Request, Parse, Extract, and Print.

### Step 1: Send an HTTP request to the web page

url = "https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/netflix_data_webpage.html"

data  = requests.get(url).text
print(data)

### Step 2: Parse the content of the web page

soup = BeautifulSoup(data, 'html.parser')

### Step 3: Create a DataFrame and Print it
amazon_data = pd.DataFrame(columns=["Date", "Open", "High", "Low", "Close", "Volume"])

for row in soup.find("tbody").find_all('tr'):
    col = row.find_all("td")
    date = col[0].text
    Open = col[1].text
    high = col[2].text
    low = col[3].text
    close = col[4].text
    adj_close = col[5].text
    volume = col[6].text
    
    amazon_data = pd.concat([amazon_data,pd.DataFrame({"Date":[date], "Open":[Open], "High":[high], "Low":[low], "Close":[close], "Adj Close":[adj_close], "Volume":[volume]})], ignore_index=True)

amazon_data.head()


#### Question 1: What is the content of the title attribute?
soup.title

#### Question 2: What are the names of the columns in the data frame?
list(amazon_data.columns)

#### Question 3: What is the Open of the last row of the amazon_data data frame?
print(amazon_data['Open'].iloc[4])
