# NetDevOps_Search_Engine_With_Semantic_

İlk önce ilgili git clone:

git clone https://github.com/ErdenizUnvan/NetDevOps_Search_Engine_With_Semantic_

Sonra ilgili kütüphaneleri yükle:

#!pip install transformers==4.25.1

#!pip show transformers

#!pip install sentence-transformers==2.2.2

#!pip show sentence_transformers

#!pip install torch==1.9.0

#!pip show torch

#!pip install requests

#!pip show requests

#!pip install bs4
#!pip show bs4

NetDevOps Search Engine With Semantic Text Matching.ipynb dosyasinda yazmis oldugum gibi once anlamsal metin eşleştirme (semantic textmatching) modelini lokaline download et

#modeli downlad et

from sentence_transformers import SentenceTransformer

model_name = 'paraphrase-multilingual-MiniLM-L12-v2'

model = SentenceTransformer(model_name, device='cpu')

PWD = os.getcwd()

model.save(os.path.join(PWD, model_name))

Lokaline download ettikten sonra modeli yukle. Model referansina degisken olarak ata.

from sentence_transformers import util

import torch

PWD = os.getcwd()

model_name = 'paraphrase-multilingual-MiniLM-L12-v2'

model = SentenceTransformer(os.path.join(PWD, model_name))

BeautifulSoup ve Request kütüphaneleriyle StackOverFlow'dan 2.113.550 soru ve cevabı manuel olarak download edebilirsiniz

import requests

from bs4 import BeautifulSoup

for page in range(1,42271):

    start_url = requests.get(f"https://stackoverflow.com/questions/tagged/python?tab=newest&page={page}&pagesize=15%22")
    
    content = BeautifulSoup(start_url.text, 'lxml')
    
    questions = content.find_all('div', {'class':'s-post-summary js-post-summary' })
    
    for item in questions:
    
        title = item.find('a', {'class': 's-link'}).text

        links = 'https://stackoverflow.com/' + item.find('a', {'class': 's-link'})['href']

        context = {'title': title, 'links':links}

        results.append(context)

        print(f'page scraped: {page}')
    
    print(len(results))
    
    
Downlad edilmiş bu verinin duplicateler temizlendikten sonra sadece network otomasyon içeren soru ve cevapların yer aldığı dosya: 

109036.csv

Network otomasyon konuları: 

nxapi,csv,excel,jinja,regex,textfsm,ansible,yang,http,socket,https,ssh,napalm,pyats,postman,requests,ncclient,netconf,restconf,paramiko,netmiko,json,yaml,xml

Hazırlamış olduğum video: https://www.youtube.com/watch?v=Fp9STz1smuM&ab_channel=KnowledgeClub
