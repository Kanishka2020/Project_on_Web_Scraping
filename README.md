# Project_on_Web_Scraping
AGENDA: In this project, we will extract data from IMDB website for top 250 movies with its ratings and released year and save into a csv file.

!pip3 install beautifulsoup4

!pip3 install openpyxl

![image](https://user-images.githubusercontent.com/58786546/186845161-3f793667-5ab2-443d-8c46-d2c06dd9b827.png)

![image](https://user-images.githubusercontent.com/58786546/186846261-d3b14c51-18e5-478a-8841-6d0bc972388a.png)


excel = openpyxl.Workbook()
print(excel.sheetnames)
sheet = excel.active
sheet.title = 'Top Rated Movies'
print(excel.sheetnames)

![image](https://user-images.githubusercontent.com/58786546/186846529-f0dc229a-c3d8-4ec2-9a0c-372a6f564f1d.png)

sheet.append(['Movie Rank', 'Movie Name', 'Year of Release', 'IMDB Rating'])

try:
    source = requests.get('https://www.imdb.com/chart/top/')
    source.raise_for_status()
    
    soup = BeautifulSoup(source.text,'html.parser')
    
    movies = soup.find('tbody', class_="lister-list").find_all('tr')
    
    for movie in movies:
        name = movie.find('td', class_="titleColumn").a.text
        #print(name)
        rank = movie.find('td', class_="titleColumn").get_text(strip=True).split('.')[0]
        #print(rank)
        year = movie.find('td', class_="titleColumn").span.text.strip('()')
        #print(year)
        rating = movie.find('td', class_="ratingColumn imdbRating").strong.text
        #print(rating')
        print(rank, name, year, rating)
        sheet.append([rank, name, year, rating])

except Exception as e:
    print(e)
    
excel.save('IMDB Movie Rating.xlsx')

![image](https://user-images.githubusercontent.com/58786546/186846930-5456e063-c1dc-4d95-9879-a76800f398f6.png)
