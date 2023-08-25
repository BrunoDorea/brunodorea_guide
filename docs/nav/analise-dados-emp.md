# Analise de Dados Empresarial

Realizar a analise de dados de PDF com a biblioteca PDF Plumber para extrair e manipular informações de diversos relatórios em pdf ao mesmo tempo.

Vamos utilizar o Google Colab neste projeto.

[Repositório do Github](https://github.com/BrunoDorea/sigmoidal-bootcamp-python)

## Pré-requisitos

- Instalar a biblioteca do PDF Plumber

```bash
!pip install pdfplumber -q
```

## Desenvolvimento

- importando os pacotes necessários

```python
from google.colab import drive
import pdfplumber
import os
```

- mudar para diretório com pdfs da semana

```python
relatorios = '../../docs/modulo_02-projeto/relatorios/'
```

- listar os relatorios

```python
arquivos_semana = os.listdir(relatorios)
print(arquivos_semana)
```

- abrir um relatório de exemplo

```python
relatorio = pdfplumber.open(relatorios + '/20200801.pdf')
pagina = relatorio.pages[0]
```

- extrair o texto da primeira página do primeiro relatório

```python
texto = pagina.extract_text()
print(texto)
```

- buscando o valor da receita

```python
float(texto.split('\n')[3].split('R$')[1])
```

- criando a função para percorrer a lista e buscar os valores

```python
soma = 0

for arquivo in arquivos_semana:
    relatorio = pdfplumber.open(arquivo)
    pagina = relatorio.pages[0]
    texto = pagina.extract_text()
    valor = texto.split('\n')[3].split('R$')[1]
    valor = float(valor)
    soma = soma + valor
    print(arquivo, "--->", valor)
```
