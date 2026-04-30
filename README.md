# Tech-Challenge-FIAP

Projeto de análise e modelagem para triagem médica com duas frentes:

- **Dados estruturados** (`synthetic_medical_triage.csv`)
- **Dados de imagem** (IDC - classes `0` e `1`)

## Estrutura do projeto

- `data/synthetic_medical_triage.csv`: base tabular de triagem.
- `data/0` e `data/1`: imagens histopatológicas (negativo/positivo).
- `nootebook/data_triagem.ipynb`: EDA, pré-processamento, modelagem e interpretabilidade para dados estruturados.
- `nootebook/image_trial.ipynb`: pipeline de classificação de imagens com CNN (EDA, treino, validação e teste).
- `main.py`: script auxiliar do projeto.

## Requisitos de ambiente

> Para rodar a parte de **imagens com TensorFlow**, use **Python 3.11** (recomendado).
> Python 3.14 não é suportado pelo TensorFlow no momento.

### 1) Criar e ativar ambiente virtual

Windows (PowerShell):

```powershell
py -3.11 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 2) Kernel para notebooks (opcional, recomendado)

```powershell
python -m ipykernel install --user --name tc-fiap --display-name "Python (tc-fiap)"
```

No Jupyter/VS Code, selecione o kernel `Python (tc-fiap)`.

## Como executar

### A) Dados estruturados

Abra e execute:

- `nootebook/data_triagem.ipynb`

Conteúdo principal:
- análise exploratória (EDA)
- limpeza e tratamento de dados
- modelos de classificação (Decision Tree e Random Forest)
- métricas, gráficos e interpretabilidade (feature importance e SHAP)

### B) Dados de imagem

Abra e execute:

- `nootebook/image_trial.ipynb`

Conteúdo principal:
- EDA das imagens (contagem e amostras por classe)
- preparação dos dados (split treino/validação/teste)
- treinamento de CNN
- avaliação com métricas, matriz de confusão e curva ROC

## Dependências

As dependências estão centralizadas em `requirements.txt` e cobrem:

- análise de dados (`pandas`, `numpy`)
- visualização (`matplotlib`, `seaborn`)
- modelagem clássica (`scikit-learn`, `imbalanced-learn`)
- interpretabilidade (`shap`)
- imagens e deep learning (`pillow`, `tensorflow`)
- execução de notebooks (`jupyter`, `ipykernel`, `notebook`)

## Observações

- As pastas `data/0` e `data/1` foram reduzidas para facilitar experimentação local.
- Para resultados reprodutíveis, mantenha `random_state`/seed conforme notebooks.
