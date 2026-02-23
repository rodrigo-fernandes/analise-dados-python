# analise-dados-python

1. Criar ambiente e instalar dependências
Shellcd titanic_eda_scpython -m venv .venv# Ativar ambiente:# Windows: .venv\Scripts\activate# macOS/Linux:source .venv/bin/activatepip install -r requirements.txtMostrar mais linhas


2. Adicionar o CSV do Titanic

Coloque o arquivo em: data/raw/ (por exemplo, data/raw/titanic.csv).
Opcional: Se não colocar o arquivo, o script tentará baixar de Google Drive via gdown usando o id fornecido.



3. Executar todos os cenários
Shellpython main.pyMostrar mais linhas
Ou, especificando caminho do CSV e cenário(s):
Shellpython main.py --csv data/raw/titanic.csv --cenarios basico,imputacaoMostrar mais linhas


4. Ver saídas

Relatório: reports/insights.md
Gráficos: outputs/figs/
Dados tratados: data/processed/

strutura criada
titanic_eda_sc/
├─ data/
│  ├─ raw/                # coloque aqui o CSV do Titanic
│  └─ processed/          # saídas (CSV) por cenário
├─ outputs/
│  └─ figs/               # gráficos gerados (PNG)
├─ reports/
│  └─ insights.md         # compilado (Markdown) com os resultados
├─ src/
│  ├─ eda_titanic.py      # funções de EDA e métricas
│  ├─ scenarios.py        # cenários e regras
│  ├─ visualize.py        # gráficos (matplotlib)
│  └─ utils.py            # utilitários (paths, download opcional)
├─ main.py                # ponto de entrada (CLI)
└─ requirements.txt       # dependências mínimas


Explicação das decisões (regras e cenários)

Ajuste de tipos: Survived/Pclass como categóricos; Sex/Embarked como categóricos; Age/Fare como numéricos; textos como string.
Engenharia de atributos:

FamilySize = SibSp + Parch + 1.
IsAlone = 1 quando FamilySize == 1.
Title: extração do título a partir do Name (ex.: Mr, Mrs, Miss).


Imputação:

Age: mediana por (Sex, Pclass) para respeitar perfis socioeconômicos e biológicos distintos.
Fare: mediana (distribuição geralmente assimétrica).
Embarked: moda (valor mais frequente).


Cenários:

básico provê uma limpeza mínima com engenharia de atributos útil para análises.
imputação preserva mais linhas ao tratar os ausentes.
drop_ausentes entrega um subconjunto “limpo” sem ausentes nas colunas-chave.
