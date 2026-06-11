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
- métricas, matrizes de confusão, comparação entre modelos, interpretabilidade (importância de features, permutação e SHAP) e leitura interpretativa

### B) Dados de imagem

Abra e execute:

- `nootebook/image_trial.ipynb`

Conteúdo principal:
- EDA das imagens (contagem e amostras por classe)
- pré-processamento com **OpenCV** (denoise, Otsu, threshold adaptativo) para **entrada tratada de 3 canais** na CNN; demonstração opcional de OCR com **Tesseract**
- preparação dos dados (split treino/validação/teste)
- treinamento de CNN (PyTorch)
- avaliação com métricas, matriz de confusão, curva ROC, limiar na validação e análise de erros, com **interpretação escrita** dos resultados (métricas, treino vs teste, limiar e erros FP/FN)

> **Reprodutibilidade:** após mudanças no código, use *Kernel → Restart & Run All* no Jupyter para alinhar métricas e figuras a uma única execução (ver também o resumo no próprio notebook).

## Dependências

As dependências estão centralizadas em `requirements.txt` e cobrem:

- análise de dados (`pandas`, `numpy`)
- visualização (`matplotlib`)
- modelagem tabular (`scikit-learn`, `imbalanced-learn` para SMOTE)
- imagens e CNN (`pillow`, `torch`, `torchvision`)
- pré-processamento de imagens no notebook (`opencv-python-headless`; usado na pipeline tratada da CNN)
- OCR no notebook (`pytesseract`; exige também o **executável Tesseract** instalado no sistema — ver abaixo)
- execução de notebooks (`jupyter`, `ipykernel`, `notebook`)

`scipy` e `joblib` entram como dependências transitivas do `scikit-learn` ao instalar com `pip`.

Opcional (não listado no arquivo): `seaborn` para estilos extras em gráficos.

### Tesseract (apenas para a parte de OCR no `image_trial.ipynb`)

O pacote `pytesseract` é instalado pelo `requirements.txt`, mas o motor OCR é **binário externo**:

- **Windows:** instale [Tesseract OCR](https://github.com/UB-Mannheim/tesseract/wiki) (ou build oficial) e garanta que `tesseract.exe` esteja no `PATH`, ou configure `TESSERACT_CMD` na célula do notebook conforme o comentário lá.
- Se você **não** for usar a demonstração de OCR, ainda pode rodar treino/avaliação da CNN desde que `cv2` esteja disponível (`opencv-python-headless` já cobre isso via `pip`).

## Observações

- As pastas `data/0` e `data/1` foram reduzidas para facilitar experimentação local.
- Para resultados reprodutíveis, mantenha `random_state`/seed conforme notebooks.
- O notebook de imagens pode salvar pesos em `cnn_idc_model.pth` na raiz do projeto após o treino (arquivo gerado localmente; não versionar se a política do grupo for ignorar artefatos grandes).
