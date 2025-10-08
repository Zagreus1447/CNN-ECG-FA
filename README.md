# 🩺 Projeto CNN: Detecção de Fibrilação Atrial (FA) em ECG Vestível

## 🚀 Visão Geral do Projeto

Este projeto implementa uma **Rede Neural Convolucional (CNN)** com uma arquitetura de kernels grandes e reduzidos, otimizada para a extração de características de baixa frequência, como as presentes na Fibrilação Atrial (FA). O objetivo principal é classificar a FA a partir de sinais de Eletrocardiograma (ECG) de derivação única, simulando dados coletados por dispositivos vestíveis (*wearables*).

Para garantir a reprodutibilidade e gerenciar dependências complexas, o trabalho é estritamente dividido em dois ambientes Python isolados: um para o processamento de sinais e outro para o treinamento do modelo com suporte a GPU/CUDA.

---

## 💾 Bases de Dados Utilizadas (5 Datasets)

O projeto utiliza 5 datasets do PhysioNet. É necessário baixá-los e armazená-los na pasta `basededados/` na raiz do projeto. Esta pasta deve ser incluída no seu arquivo `.gitignore`.

### 1. Dados de Fibrilação Atrial (FA)

| Dataset                               | Código PhysioNet                                                              | Propósito no Projeto                                                                                                 |
| ------------------------------------- | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| AF Termination Challenge (2017)       | `af-termination-challenge-database-1.0.0`                                     | Principal fonte de registros de FA paroxística e persistente para treino e rótulos de ritmo normal.                  |
| PhysioNet/CinC Challenge 2017         | `physionet-computing-in-cardiology-challenge-2017`                            | Dataset de curta duração (simulando *wearables*) com 4 classes, essencial para o treinamento da classificação final. |
| PTB-XL (ECG Dataset)                  | `ptb-xl-a-large-publicly-available-electrocardiography-dataset-1.0.3`         | Utilizado para obter grande volume de exemplos de FA, outras arritmias e como fonte de ritmo normal.                |

### 2. Dados de Ruído (Noise)

| Dataset                           | Código PhysioNet                                  | Propósito no Projeto                                                                                             |
| --------------------------------- | ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| Motion Artifacts (Ruídos)         | `motion-artifact-contaminated-ecg-database-1.0.0` | Utilizado para treinar o modelo contra artefatos de movimento, comuns em *wearables*.                              |
| MIT-BIH Noise Stress Test Database| `mit-bih-noise-stress-test-database-1.0.0`        | Fonte adicional de ruídos (músculo, eletrodo, etc.) para injeção e aumento da capacidade de generalização do modelo. |

---

## ⚙️ Configuração dos Ambientes Virtuais (Usando PIP)

Você deve criar dois ambientes virtuais distintos a partir dos arquivos de requisitos fornecidos.

### Ambiente 1: Pré-Processamento (`preprocessamento`)

-   **Foco**: Leitura de sinais (`wfdb`), filtragem, reamostragem e normalização.
-   **Notebook Correspondente**: `notebooks/01_Pre_processamento.ipynb` (deve ser executado primeiro).

**Passos para configuração:**

1.  **Crie e ative o ambiente:**
    ```bash
    # Para macOS/Linux
    python -m venv preprocessamento
    source preprocessamento/bin/activate

    # Para Windows (CMD)
    python -m venv preprocessamento
    preprocessamento\Scripts\activate
    ```

2.  **Instale as dependências:**
    ```bash
    pip install -r environments/requirimentspreprocessamentosbs2.txt
    ```

### Ambiente 2: Modelo CNN (`bs2+`)

-   **Foco**: Treinamento, validação e inferência do modelo CNN (TensorFlow/Keras ou PyTorch).
-   **Requisito**: Suporte a **CUDA/GPU** para aceleração do treinamento.
-   **Notebook Correspondente**: `notebooks/02_Treinamento_CNN.ipynb`

**Passos para configuração:**

1.  **Crie e ative o ambiente:**
    ```bash
    # Para macOS/Linux
    python -m venv bs2+
    source bs2+/bin/activate

    # Para Windows (CMD)
    python -m venv bs2+
    bs2+\Scripts\activate
    ```

2.  **Instale as dependências (incluindo bibliotecas de GPU):**
    ```bash
    pip install -r environments/requirimentscnnNovaB.txt
    ```

---

## 📝 Guia de Execução dos Notebooks

1.  **`01_Pre_processamento.ipynb`**:
    -   **Ambiente**: `preprocessamento`
    -   **Ação**: Carrega os 5 datasets, limpa e segmenta os sinais, e salva o dataset final processado (que não deve ser versionado pelo Git).

2.  **`02_Treinamento_CNN.ipynb`**:
    -   **Ambiente**: `bs2+`
    -   **Ação**: Carrega os dados processados pelo notebook anterior, define a arquitetura da CNN, treina o modelo, avalia sua performance e salva o modelo final.
