import csv
from selenium import webdriver
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.chrome.service import Service
from time import sleep
from selenium.webdriver.common.by import By

servico = Service(ChromeDriverManager().install())   #Tira a necessidade de baixar e atualizar o chromedriver.exe manualmente
tela_maxima = webdriver.ChromeOptions() 
tela_maxima.add_argument("--start-maximized") #Faz com que o navegador inicie com a tela cheia

navegador = webdriver.Chrome(service=servico, options=tela_maxima)

navegador.get("https://gizmodo.uol.com.br/")
sleep(3)                                             #Tempo de espera para o site carregar completamente

titulos = '//*[@id="mdContent"]/div[{}]/article/header/h3/a'

lista_titulos = {}

for i in range(1, 11):                                #Repetição para deixar o codigo mais "limpo" e automatizado
    xpath_titulos = titulos.format(i)
    titulos_posts = navegador.find_element(By.XPATH, xpath_titulos)
    
    lista_titulos[i] = titulos_posts.text    

datas = '//*[@id="mdContent"]/div[{}]/article/div[3]/div[1]/div/div/span/abbr'

lista_datas = {}

for i in range(1, 11):
    xpath_datas = datas.format(i)
    datas_posts = navegador.find_element(By.XPATH, xpath_datas)    
    
    lista_datas[i] = datas_posts.text

resumo = '//*[@id="mdContent"]/div[{}]/article/div[3]/div[2]/div/p'

lista_resumo = {}

for i in range(1, 11):
    xpath_resumo = resumo.format(i)
    resumo_posts = navegador.find_element(By.XPATH, xpath_resumo)    
    
    lista_resumo[i] = resumo_posts.text

juncao_listas = [lista_titulos, lista_datas, lista_resumo]      #Junção dos dicionários para ter uma exportação correta
chaves = set().union(*juncao_listas) #União das chaves dos dicionários

with open('desafio-parvi.csv', 'w', newline='') as arquivo_csv: #criação e exportação do arquivo csv com os dados
    writer = csv.writer(arquivo_csv)
    writer.writerow(['Chave', 'Titulo', 'Data', 'Resumo'])
    
    for chave in chaves:
        conteudo = [materias.get(chave, '') for materias in juncao_listas]
        writer.writerow([chave] + conteudo)
