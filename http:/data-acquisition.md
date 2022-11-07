import requests
from urllib.request import urlopen
from bs4 import BeautifulSoup
import os

def imagedown(url, folder):
    try:
        os.mkdir(os.path.join(os.getcwd(), folder))
    except:
        pass
    os.chdir(os.path.join(os.getcwd(), folder))
    #r = requests.get(url)
    r = urlopen(url)
    #soup = BeautifulSoup(r.text, 'html.parser')
    soup = BeautifulSoup(r, 'html.parser')
    #images = soup.find_all('img')
    images = soup.find_all('img', width=300, height=300)
    #i=1
    for image in images:
        #name = str(i) + 'image'
        #i+=1
        name = image['alt']
        link = image['src']
        #with open(name + '.jpg', 'wb') as f:
        with open(name.replace(' ', '-').replace('/', '').replace('.', '') + '.jpg', 'wb') as f:
            im = requests.get(link)
            f.write(im.content)
            print('Writing: ', name)

imagedown('https://www.homedepot.com/b/Bath-Bathroom-Faucets-Bathroom-Sink-Faucets-Centerset-Bathroom-Faucets/N-5yc1vZbrhk?Nao=48','faucet1')
#replace URL and folder name in the function call line for imagedown function above
