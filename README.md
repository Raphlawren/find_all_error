# find_all_error
# Attribute error in webscraping
url = 'https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/amazon_data_webpage.html.'


html_data = requests.get(url).text
soup = BeautifulSoup(html_data, 'html5lib')

amazon_data = pd.DataFrame(columns=["Date", "Open", "High", "Low", "Close", "Volume"])

for row in soup.find("tbody").find_all("tr"):
    col = row.find_all("td")
    date = cell[0].text
    Open =  cell[1].text
    high = cell[2].text
    low = cell[3].text
    close = cell[4].text
    adj_close = cell[5].text
    volume = cell[6].text
    
    amazon_data = amazon_data.append({"Date":date, "Open":Open, "High":high, "Low":low, "Close":close, "Adj Close":adj_close, "Volume":volume}, ignore_index=True)
