# Um Bilhão de Linhas: Desafio de Processamento de Dados com Python

## Controle de Versão

### Histórico de Atualizações

| Versão | Data       | Alterações                                     | Autor     |
|:------:|:----------:|:---------------------------------------------- |:---------:|
| 1.0    | 2024-04-10 | Projeto clonado.                                           | 1brc               |
| 1.1    | 2024-04-10 | Projeto clonado.                                           | lvgalvao e ArthurJ |
| 1.2    | 2025-04-05 | Melhorias gerais.                                          | diegobarbosaa      |

## Introdução

O objetivo deste projeto é demonstrar como processar eficientemente um arquivo de dados massivo contendo 1 bilhão de linhas (~14GB), especificamente para calcular estatísticas (Incluindo agregação e ordenação que são operações pesadas) utilizando Python. 

Este desafio foi inspirado no [The One Billion Row Challenge](https://github.com/gunnarmorling/1brc), originalmente proposto para Java.

O arquivo de dados consiste em medições de temperatura de várias estações meteorológicas. Cada registro segue o formato `<string: nome da estação>;<double: medição>`, com a temperatura sendo apresentada com precisão de uma casa decimal.

Aqui estão dez linhas de exemplo do arquivo:

```
Hamburg;12.0
Bulawayo;8.9
Palembang;38.8
St. Johns;15.2
Cracow;12.6
Bridgetown;26.9
Istanbul;6.2
Roseau;34.4
Conakry;31.2
Istanbul;23.0
```

O desafio é desenvolver um programa Python capaz de ler esse arquivo e calcular a temperatura mínima, média (arredondada para uma casa decimal) e máxima para cada estação, exibindo os resultados em uma tabela ordenada por nome da estação.

| station      | min_temperature | mean_temperature | max_temperature |
|--------------|-----------------|------------------|-----------------|
| Abha         | -31.1           | 18.0             | 66.5            |
| Abidjan      | -25.9           | 26.0             | 74.6            |
| Abéché       | -19.8           | 29.4             | 79.9            |
| Accra        | -24.8           | 26.4             | 76.3            |
| Addis Ababa  | -31.8           | 16.0             | 63.9            |
| Adelaide     | -31.8           | 17.3             | 71.5            |
| Aden         | -19.6           | 29.1             | 78.3            |
| Ahvaz        | -24.0           | 25.4             | 72.6            |
| Albuquerque  | -35.0           | 14.0             | 61.9            |
| Alexandra    | -40.1           | 11.0             | 67.9            |
| ...          | ...             | ...              | ...             |
| Yangon       | -23.6           | 27.5             | 77.3            |
| Yaoundé      | -26.2           | 23.8             | 73.4            |
| Yellowknife  | -53.4           | -4.3             | 46.7            |
| Yerevan      | -38.6           | 12.4             | 62.8            |
| Yinchuan     | -45.2           | 9.0              | 56.9            |
| Zagreb       | -39.2           | 10.7             | 58.1            |
| Zanzibar City| -26.5           | 26.0             | 75.2            |
| Zürich       | -42.0           | 9.3              | 63.6            |
| Ürümqi       | -42.1           | 7.4              | 56.7            |
| İzmir        | -34.4           | 17.9             | 67.9            |

## Dependências

Para executar os scripts deste projeto, você precisará das seguintes bibliotecas:

* Polars: `0.20.3`
* DuckDB: `0.10.0`
* Dask[complete]: `^2024.2.0`

## Resultados

Os testes foram realizados em um laptop equipado com um processador M1 da Apple e 8GB de RAM. As implementações utilizaram abordagens puramente Python, Pandas, Dask, Polars e DuckDB. Os resultados de tempo de execução para processar o arquivo de 1 bilhão de linhas são apresentados abaixo:

| Implementação | Tempo |
| --- | --- |
| Bash + awk | 25 minutos |
| Python | 20 minutos |
| Python + Pandas | 263 sec |
| Python + Dask | 155.62 sec  |
| Python + Polars | 33.86 sec |
| Python + Duckdb | 14.98 sec |

## Agradecimentos
[Koen Vossen](https://github.com/koenvo) pela implementação em Polars.
[Arthur Julião](https://github.com/ArthurJ) pela implementação em Python e Bash.
[Luciano Galvão](https://github.com/lvgalvao) pelo clone do repositório.

## Conclusão

Este desafio destacou claramente a eficácia de diversas bibliotecas Python na manipulação de grandes volumes de dados. Métodos tradicionais como Bash (25 minutos), Python puro (20 minutos) e até mesmo o Pandas (5 minutos) demandaram uma série de táticas para implementar o processamento em "lotes", enquanto bibliotecas como Dask, Polars e DuckDB provaram ser excepcionalmente eficazes, requerendo menos linhas de código devido à sua capacidade inerente de distribuir os dados em "lotes em streaming" de maneira mais eficiente. O DuckDB se sobressaiu, alcançando o menor tempo de execução graças à sua estratégia de execução e processamento de dados.

Esses resultados enfatizam a importância de selecionar a ferramenta adequada para análise de dados em larga escala, demonstrando que Python, com as bibliotecas certas, é uma escolha poderosa para enfrentar desafios de big data.

Duckdb vence tambem com 1 milhao de linhas, realmente é o melhor

## Como Executar

Para executar este projeto e reproduzir os resultados:

1. Clone esse repositório
2. Deletar o .python-version.
3. Verificar as versões intaladados do python no pyenv.
4. Definir a versao do Python usando o `pyenv local 3.13.2`. Indico verificar a versão mais recente a partir da data que visualiza esse projeto.
5. Na sequência rodar: `poetry env use 3.13.2`, `poetry lock` e `poetry install --no-root`
6. Execute o comando `python src/create_measurements.py` para gerar o arquivo de teste (foi diminuido o tamanho de linhas para caber no github).
7. Tenha paciência e vá fazer um café, vai demorar uns 10 minutos para gerar o arquivo
8. Certifique-se de instalar as versões especificadas das bibliotecas Dask, Polars e DuckDB
9. Execute os scripts `python src/using_python.py`, `python src/using_pandas.py`, `python src/using_dask.py`, `python src/using_polars.py` e `python src/using_duckdb.py` através de um terminal ou ambiente de desenvolvimento que suporte Python.

Este projeto destaca a versatilidade do ecossistema Python para tarefas de processamento de dados, oferecendo valiosas lições sobre escolha de ferramentas para análises em grande escala.

Neste exemplo, apenas as primeiras 1000 linhas serão processadas.

Ao executar o script, você verá a barra de progresso (se pv estiver instalado corretamente) e, eventualmente, a saída esperada no terminal ou em um arquivo de saída, se você decidir modificar o script para direcionar a saída.