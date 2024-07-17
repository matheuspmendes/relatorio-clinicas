# [Python - PowerBI] Estudo de Caso - Relatório Clínicas

Nesse estudo de caso, a missão é realizar tratamento dos dados de três arquivos disponibilizados para inserção e 
criação de relatório em BI utilizando o Power BI.
Embora este tratamento possa ser feito diretamente no Power BI, para meios de estudo e portfólio, toda a limpeza 
de dados, manipulação e junção dos arquivos utilizando Python com Pandas através do Jupyter Notebook.
Os dados utilizados neste Estudo de Caso foram cedidos por uma empresa local e 
foram previamente anonimizados, não contendo nenhuma informação sensível.

## Estudo de caso

O proposto para este Case é de gerar um dashboard contendo informações referentes KPI's específicas de médicos e 
especialidades como forma de avaliação de desempenho para a equipe de gestão. Para isto, foram concedidos três arquivos
em planilhas de excel contendo Faltas (informações referentes à agenda médica, remarcação de consultas dentre outras métricas),
Espera (informações geradas na recepção contendo informações sobre consultas realizadas e tempo de espera dos pacientes) e 
Produtividade (contendo número de consultas realizadas e total de horas computadas pelo sistema).

Por ser um projeto de criação de dashboard em BI, o Python foi usado somente 
para **tratamento e manipulação dos dados**, todas as análises e resultados
estarão presentes no Dashboard no Power BI que pode ser acessado por este [link](https://app.powerbi.com/view?r=eyJrIjoiNDA2ZGIyZmEtODZkNy00Y2Y3LWExODYtNTUwNzU3NGUyODVmIiwidCI6IjI1Y2VlODZhLTBmYzUtNDRiNC1iOWQwLWE5NzA4YWVkMjg1MyJ9):
Todo o código e sintaxe utilizada para realização da limpeza e manipulação de dados pode ser acessado pelo arquivo do Jupyter Nutebook.

Para fins de visualização, será anexado uma imagem do Dashboard abaixo:
![Prévia Dashboard](./painel2.png)
