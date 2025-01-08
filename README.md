import pandas as pd
import requests
from bs4 import BeautifulSoup

url = 'https://en.wikipedia.org/wiki/List_of_largest_companies_in_the_United_States_by_revenue'
page = requests.get(url)
soup = BeautifulSoup(page.text, 'html.parser')
tables = soup.find_all('table')[0]
world_titles = tables.find_all('th')  
world_table = [title.text.strip() for title in world_titles]  
df=pd.DataFrame(columns=world_table)
column_data=tables.find_all('tr')
for row in column_data[1:]:
    row_data=row.find_all('td')
    idividual_row_data=[data.text.strip() for data in row_data ]
    length=len(df)
    df.loc[length]=idividual_row_data
print(df)
df.to_csv(r'C:\Users\M S I\Desktop\datasets\web scarping\companies.csv',index=False)
