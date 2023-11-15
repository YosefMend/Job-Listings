# Job-Listings
# Scrape main website to compile all job titles and their corresponding links relating to professions of Data or Biology.

from bs4 import BeautifulSoup
import requests

url = 'https://www.cytoreason.com/career/'
response = requests.get(url)
soup = BeautifulSoup(response.content, 'html.parser')
job_string = str(soup.find_all('div', 'comeet-position-name'))
job_listings = job_string.split('<div class="comeet-position-name">')[1:-1]


def career_list(job_listings):
    job_dict = {}
    for job in range(len(job_listings)):
        title = soup.find_all('a', 'comeet-position')[job].text.replace('\n', '').strip().split('  ')[0]
        link = soup.find_all('a', 'comeet-position')[job]['href']
        job_dict[title] = link

    return job_dict


job_dict = career_list(job_listings)
print(job_dict)
