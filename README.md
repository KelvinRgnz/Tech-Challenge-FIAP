# Tech-Challenge-FIAP

Projeto de análise e modelagem para triagem médica com duas frentes:

- **Dados estruturados** (`synthetic_medical_triage.csv`)
- **Dados de imagem** (IDC - classes `0` e `1`)

## Estrutura do projeto

- `data/synthetic_medical_triage.csv`: base tabular de triagem.
- `data/0` e `data/1`: imagens histopatológicas (negativo/positivo).
- `nootebook/data_triagem.ipynb`: EDA, pré-processamento, modelagem e interpretabilidade para dados estruturados.
- `nootebook/image_trial.ipynb`: pipeline de classificação de imagens com **CNN em PyTorch** (EDA, treino, validação, teste e curvas de avaliação).

## Requisitos de ambiente

> Use **Python 3.10 ou 3.11** (recomendado) para combinar com as versões atuais de `torch` e `scikit-learn` nos wheels oficiais.
> O notebook de imagens usa **PyTorch** (CPU por padrão; GPU opcional se você tiver CUDA compatível).
> **Não** é necessário TensorFlow para este repositório.

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
- métricas, matrizes de confusão, gráficos e leitura interpretativa (relatório por classe, árvore da Random Forest e erros na matriz de confusão)

### B) Dados de imagem

Abra e execute:

- `nootebook/image_trial.ipynb`

Conteúdo principal:
- EDA das imagens (contagem e amostras por classe)
- preparação dos dados (split treino/validação/teste)
- treinamento de CNN (PyTorch)
- avaliação com métricas, matriz de confusão, curva ROC e análise de erros

## Dependências

As dependências estão centralizadas em `requirements.txt` e cobrem:

- análise de dados (`pandas`, `numpy`)
- visualização (`matplotlib`)
- modelagem tabular (`scikit-learn`, `imbalanced-learn` para SMOTE)
- imagens e CNN (`pillow`, `torch`, `torchvision`)
- execução de notebooks (`jupyter`, `ipykernel`, `notebook`)

Opcional (não listado no arquivo): `seaborn` para estilos extras em gráficos; `shap` se você adicionar interpretação SHAP ao notebook.

## Observações

- As pastas `data/0` e `data/1` foram reduzidas para facilitar experimentação local.
- Para resultados reprodutíveis, mantenha `random_state`/seed conforme notebooks.
