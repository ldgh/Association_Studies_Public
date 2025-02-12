# **Association Studies**

- [Introdução](#introdução)
- [Bibliotecas](#bibliotecas)
- [Explicação e Arquivos de Input](#explicação-e-arquivos-de-input)
- [Exemplo de Análise](#exemplo-de-análise)



## Introdução
Este repositório contém um conjunto de scripts desenvolvidos por **LUCCA V. AGUIAR** e **MARCUS V. G. ANTUNES**, com o objetivo de:

- Auxiliar e padronizar a saída dos testes de associação genética.
- Automatizar a plotação de imagens para análise de associação (Manhattan e QQ plots).
- Padronizar a busca e comparação com o banco de dados GWAS Catalog, identificando variantes próximas fisicamente.

A filtragem e organização dos resultados são realizadas em Python, enquanto a plotação é feita em R devido à qualidade gráfica e disponibilidade de pacotes especializados. Para eficiência computacional, apenas variantes com p-valor menor ou igual ao limite estabelecido no config.ini serão processadas na plotação e comparação com o GWAS Catalog.



## Bibliotecas

Python:
- pandas
- configparser (ConfigParser)
- os
- glob

R:
- parallel
- qqman
- data.table


  
## Explicação e Arquivos de Input

Configuração do config.ini

O arquivo config.ini deve ser configurado antes da execução do script. Os seguintes parâmetros precisam ser definidos:

```
[Filter]
DIRECTORY_ASSOC = <diretório_com_os_testes_de_associação>
FILTER_OUTPUT_PATH = <diretório_para_os_resultados_filtrados>
P_VALUE = <p-valor_desejado_para_filtragem>  # Padrão: 1e-06

[Search]
GWAS_CATALOG = <caminho_para_o_banco_GWAS_Catalog>
SEARCH_OUTPUT_PATH = <diretório_de_saida_dos_resultados>
SIZE_OF_WINDOW = <tamanho_da_janela_em_bp>  # Padrão: 25000 (upstream e downstream)
```

Atenção:
O cabeçalho dos arquivos de entrada deve estar corretamente nomeado. Em algumas saídas do PLINK, o cabeçalho pode aparecer com formatação inadequada, como:

```
X10  X48486  X10.48486_C.T  C  T  T.1  ADD  X679  X.0.0139651  X0.0540564  X.0.258344  X0.796221
```

Certifique-se de padronizar os nomes das colunas antes de executar o script.



## Exemplo de Análise
Execução do Script:


Execute o script R para gerar as imagens de plotação.

Se a execução for bem-sucedida, os gráficos serão gerados e salvos no diretório de saída:

![Test_file_Manhattan](https://github.com/user-attachments/assets/b8325a9d-a3cc-49da-bcfe-a5312e7a479d)

Manhattan plot

![Test_file_QQplot](https://github.com/user-attachments/assets/f567b0e1-7c7c-4802-a014-12f0cf50e251)

QQ plot

Execute o script Python:

Verifique se os arquivos estão corretamente organizados.

Ajuste o arquivo config.ini com os caminhos corretos (Teste de associação e Banco de dados GWAS Catalog).

Execute o script Python para filtragem: 
O script Python gera dois arquivos principais:
  - filtered_pvalues.txt: Contém as variantes que passaram pelo critério de filtragem do p-valor. No exemplo abaixo, com P_VALUE = 1e-03, foram selecionadas 9 variantes.
  - SNPs_GWAS_Catalog.tsv: Lista as variantes filtradas que foram comparadas com o GWAS Catalog, buscando variantes próximas (exemplo: 25.000 pb). O resultado inclui 3.958 variantes associadas a fenótipos próximos.

