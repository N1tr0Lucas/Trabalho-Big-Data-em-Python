# Vacinação contra Influenza em São Gonçalo (RJ): campanha 2025-26

Trabalho Extensionista de **Tópicos de Big Data em Python** (Estácio).

Análise em Python dos registros de vacinação contra a influenza em São Gonçalo (RJ), com limpeza de dados, estatística descritiva, regressão linear e identificação de outliers.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/N1tr0Lucas/Trabalho-Big-Data-em-Python/blob/main/Trabalho_BigDataPython.ipynb)

## Objetivos

1. **Descrever** o perfil dos vacinados (sexo, idade, dose e fabricante).
2. **Ajustar** regressões lineares simples (vacinados por idade e por semana).
3. **Identificar** outliers (idades, dias atípicos e resíduos do modelo).

## Base de dados

- **Fonte:** [Portal de Dados Abertos do SUS](https://dadosabertos.saude.gov.br/dataset?tags=DPNI) (Ministério da Saúde).
- **Arquivo:** `data/25-26_SG_INFLU.xlsx` (aba `25-26_Influ`).
- **Tamanho:** 25 colunas e 280.262 registros após a limpeza. Cada linha é uma dose aplicada.
- **Atenção:** a base não tem identificador do paciente.

## Tratamento dos dados

- Renomeação das 25 colunas (sem acentos e sem espaços).
- Conversão dos códigos para inteiro com suporte a nulos (`Int64`).
- Datas futuras tratadas como dado ausente.
- Remoção de linhas duplicadas.
- Padronização dos fabricantes com `unicodedata` e expressões regulares (Butantan, Sanofi, Serum, Abbott, GlaxoSmithKline, Fiocruz, outros e não informado).
- Criação de faixas etárias: criança (0-9), adolescente (10-17), adulto (18-59) e idoso (60 ou mais).

## Principais resultados

| Análise | Resultado |
|---|---|
| Idade dos vacinados | média de 42,2 anos, mediana de 45, desvio padrão de 26,2 (de 0 a 126 anos) |
| Maior volume por idade | 7.581 vacinados com 0 anos; pico de idosos aos 66 anos (4.807) |
| Sexo | mulheres são maioria entre adultos (65,9%) e idosos (60,5%) |
| Regressão por idade | Vacinados = 4.159 − 29,95 × Idade, com R² de 0,41, p < 0,001 e Durbin-Watson de 0,07 |
| Regressão semanal (fase de queda) | pico em 11/05/2025; −931 vacinados por semana; R² de 0,79 (p = 6,94e-08; 21 semanas) |
| Dias atípicos (IQR) | 50 de 312 dias; maior pico em 10/05/2025, com 14.266 doses |
| Outliers de idade (IQR) | nenhum, mas há registros de até 126 anos, provavelmente erros |
| Resíduos da regressão por idade (\|z\| > 2) | idade 0 e idades de 65 a 69 anos |

## Interpretação

- A vacinação se concentra em **bebês** e em **idosos de 65 a 69 anos**, formando dois picos que uma reta não descreve bem (R² de 0,41).
- Depois do pico de maio de 2025, a campanha **cai em ritmo próximo de linear** (R² de 0,79), mas a reta prevê valores negativos nas últimas semanas.
- O dia 10/05/2025 teve mais de três vezes o segundo maior dia, o que sugere uma ação especial (hipótese a confirmar no calendário da campanha).

## Limitações

- Sem identificador do paciente, doses repetidas legítimas podem ter sido removidas como duplicatas.
- A contagem por idade não considera a população de cada idade, então mistura adesão com tamanho da população.
- Os resíduos da regressão por idade são autocorrelacionados (Durbin-Watson de 0,07), e o p-valor deve ser lido com cautela.
- Idades acima de 110 anos são provavelmente erros de registro e não foram removidas.

## Como executar

1. Clique no botão **Abrir no Colab** acima.
2. Execute as células em ordem (**Ambiente de execução > Executar tudo**). A base é lida direto do GitHub, então é preciso ter internet.

Para executar localmente:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels scipy openpyxl
jupyter notebook Trabalho_BigDataPython.ipynb
```

## Ferramentas

Python, Google Colab, pandas, NumPy, Matplotlib, Seaborn, scikit-learn, statsmodels, SciPy, `re`, `unicodedata` e GitHub.

## Próximos passos

- Calcular **taxas de vacinação** por faixa etária, usando a população de cada idade.
- Testar **modelos não lineares** (polinomial ou logarítmico) e a regressão por faixa etária.
- Cruzar as datas de pico com o calendário oficial da campanha.
  
Roteiro de Extensäo - [Roteiro_Extensao_Lucas (1).docx](https://github.com/user-attachments/files/35245021/Roteiro_Extensao_Lucas.1.docx)

Slides de apresentação - [Apresentacao_Influenza_SaoGoncalo_25-26 (1).pptx](https://github.com/user-attachments/files/35245034/Apresentacao_Influenza_SaoGoncalo_25-26.1.pptx)

## Autor

**Lucas Fernandes Quintanilha**  
Orientação: Prof.ª Simone Gama

