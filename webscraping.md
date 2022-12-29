# codechunks-
#code for web scraping 
import requests
from bs4 import BeautifulSoup
import bs4
url='https://www.flipkart.com/search?q=tv&as=on&as-show=on&otracker=AS_Query_TrendingAutoSuggest_8_0_na_na_na&otracker1=AS_Query_TrendingAutoSuggest_8_0_na_na_na&as-pos=8&as-type=TRENDING&suggestionId=tv&requestId=9c9fa553-b7e5-454b-a65b-bbb7a9c74a29'
link=requests.get(url)
raw_data=link.content
soup=BeautifulSoup(raw_data,'html.parser')
name=soup.find('div',class_="_4rR01T")
price=soup.find('div',class_="_30jeq3 _1_WHN1")

print(name.text)
print(price.text)

spec=soup.find('div',class_="fMghEO")
for i in spec:
    speci=i.find_all('li',class_="rgWa7D")
    print(speci[0].text)
    print(speci[1].text)
    print(speci[2].text)
    

1 Year Warranty on Product and 2 Years Warranty on Panel. OEM warranty activation starts from the date of delivery.
products=[]              #List to store the name of the product
prices=[]                #List to store price of the product         
os = []                  #List to store operating system
hd = []                  #List to store resolution
for data in soup.findAll('div',class_='_3pLy-c row'):
        names=data.find('div', attrs={'class':'_4rR01T'})
        price=data.find('div', attrs={'class':'_30jeq3 _1_WHN1'})
        specification = data.find('div', attrs={'class':'fMghEO'})
        
        for each in specification:
            col=each.find_all('li', attrs={'class':'rgWa7D'})
            os_ = col[0].text
            hd_ = col[1].text
        products.append(names.text) # Add product name to list
        prices.append(price.text) # Add price to list
        os.append(os_) # Add operating system specifications to list
        hd.append(hd_) # Add resolution specifications to list
  
import pandas as pd
df=pd.DataFrame({'Product Name':products,'OS':os,"Resolution":hd,'Price':prices})
df.head(10)

#Author Sameep Kumar Gupta  
