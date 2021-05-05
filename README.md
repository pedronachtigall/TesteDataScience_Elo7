# TesteDataScience_Elo7

Esse projeto têm como objetivo desenvolver um pipeline de análise que permita explorar e desenvolver um modelo preditivo para a paltaforma Elo7.

## Descrição do Problema

Durante o dia a dia de trabalho no Elo7 nos deparamos com uma quantidade de produtos únicos da ordem de seis milhões. As informações encontradas na página de um produto são inteiramente inseridas pelo seu vendedor. Sendo assim, existem dados textuais pouco estruturados e dados numéricos que podem ser incoerentes com a prática do mercado. Isso faz com que cada produto seja único, tornando mais difícil a busca por padrões. 

Considerando a interação dos compradores com o site, estes todos os dias utilizam o sistema de busca com dois objetivos principais: encontrar um produto desejado; ou descobrir novos itens que os surpreendam.

O termo de busca (ou query) é a informação que o usuário nos dá sobre a sua intenção e podemos obter informações extras após o usuário visualizar ou comprar algum produto. Será possível identificar algum tipo de intenção do usuário apenas pelo termo de busca?

O projeto aqui apresentado presente utilizar o dataset disponível para atingir três objetivos:

- Criar um sistema supervisionado que classifique os produtos em categorias usando dados rotulados (campo `category`);
- Criar um sistema não supervisionado que utilize os termos de busca para produzir pelo menos duas classes de intenção do usuário;
- Criar um sistema híbrido (utilizando os dois primeiros) que ao receber um termo de busca:
    - Retorne a possível intenção do usuário;
    - Retorne a que categoria este termo pertenceria caso fosse um produto;
    - Recomende os dez produtos mais relevantes dados o termo de busca e a intenção do usuário.


## Dataset

O dataset para esse projeto é composto de uma amostra de dados do Elo7. O dataset pode ser encontrado no presente repositório, no arquivo ["elo7_recruitment_dataset.csv"](https://github.com/pedronachtigall/TesteDataScience_Elo7/blob/main/elo7_recruitment_dataset.csv).

Em resumo, o dataset contém 38.507 registros distribuídos em 6 categorias (`Bebê`, `Bijuterias e Jóias`, `Decoração`, `Lembrancinhas`, `Papel e Cia` e `Outros`). Cada registro corresponde a um clique em um produto a partir de um termo de busca no site. 

Este dataset é composto pelas seguintes colunas:

- `product_id` - identificação de produto
- `seller_id` - identificação do vendedor 
- `query` - termo de busca inserido pelo usuário
- `search_page` - número da página que o produto apareceu nos resultados de busca (mín 1 e máx 5)
- `position` - número da posição que o produto apareceu dentro da página de busca (mín 0 e máx 38)
- `title` - título do produto  
- `concatenated_tags` - tags do produto inseridas pelo vendedor (as tags estão concatenadas por espaço)
- `creation_date` - data de criação do produto na plataforma do Elo7
- `price` - preço do produto em reais  
- `weight` - peso em gramas da unidade do produto reportado pelo vendedor
- `express_delivery` - indica se o produto é pronta entrega (1) ou não (0)
- `minimum_quantity` - quantidade de unidades mínima necessária para compra
- `view_counts` - número de cliques no produto nos últimos três meses  
- `order_counts` - número de vezes que o produto foi comprado nos últimos três meses
- `category` - categoria do produto   

## Solução

A solução está estruturada da seguinte maneira:

1. **Análise exploratória**
2. **Sistema de classificação de produtos**
3. **Sistema de termos de busca**
4. **Avaliação dos sistemas de classificação**
5. **Colaboração entre os sistemas**
6. **Entrega dos sistemas**

A solução pode ser encontrada no arquivo que está em formato jupyter notebbok ["Teste_DataScience_Elo7.ipynb"](https://github.com/pedronachtigall/TesteDataScience_Elo7/blob/main/Teste_DataScience_Elo7.ipynb). Além disso, segue em conjunto o arquivo ["requirements.txt"](https://github.com/pedronachtigall/TesteDataScience_Elo7/blob/main/requirements.txt) (gerado pelo comando `pip freeze > requirements.txt`).

## Parte 1 - Análise exploratória

Nesta etapa foi realizada uma análise explotória dos dados para realização de "limpeza" (i.e., remover/alterar dados com valores nulos, transformação em log, etc) e compreensão dos dados. No intuito de compreender os dados e suas relações, foram análisados valores estatísticos básicos, "plotagem" de gráficos que ajudaram a compreender a distrubuição dos valores de dados específicos e suas possveis relações com outros dados. Além disso, foi aplicada uma análise de correlação entre os dados disponíveis no dataset para detectar padrões relacionais.

Está análise permite identificar variáveis que podem auxiliar no desenvolvimento de um sistema de classificação de produtos com alta performance.

## Parte 2 - Sistema de classificação de produtos
