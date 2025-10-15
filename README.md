# 🩺 Projeto kb2s+: Detecção de Fibrilação Atrial

## 🚀 Visão Geral
CNN especializada para detecção de FA em ECGs de wearables com robustez a ruídos.

----

## 💾 Bases de Dados

**ECG:**
- AF Termination Challenge
- CODE-15

**Ruído:**
- Motion Artifacts
- MIT-BIH Noise Stress Test  
- Mobile ECG Challenge

----

## ⚙️ Configuração dos Ambientes

### Ambiente 1: Pré-processamento
*python -m venv preprocessamento*  
*source preprocessamento/bin/activate*  
*pip install -r requirements/preprocessamento.txt*

**Funções:**
- Leitura sinais WFDB
- Filtragem e reamostragem
- Normalização inicial
- Notebook: `preprocessamento.ipynb`

----

### Ambiente 2: Processamento
*python -m venv processamento*  
*source processamento/bin/activate*  
*pip install -r requirements/processamento.txt*

**Funções:**
- Aumento de dados
- Balanceamento classes
- Preparação datasets
- Notebook: `processamento.ipynb`

----

### Ambiente 3: Treinamento
*python -m venv treinamento*  
*source treinamento/bin/activate*  
*pip install -r requirements/treinamento.txt*

**Requisitos:**
- GPU CUDA
- TensorFlow/Keras
- Notebooks: `modelo_cnn.ipynb`, `teste_modelo.ipynb`

----

## 🔄 Fluxo de Execução

### Fase 1: Pré-processamento
**Ambiente:** preprocessamento  
**Arquivo:** `preprocessamento.ipynb`  
**Ações:**
- Carregar 5 datasets originais
- Salvar arquivos .npy em `data/processed/`

----

### Fase 2: Processamento  
**Ambiente:** processamento  
**Arquivo:** `processamento.ipynb`  
**Ações:**
- Carregar arquivos .npy processados
- Aplicar filtros digitais
- Segmentar sinais em janelas
- Adicionar ruídos artificiais
- Aplicar data augmentation
- Realizar undersampling das classes
- Preparar datasets finais

----

### Fase 3: Treinamento
**Ambiente:** treinamento  
**Arquivo:** `modelo_cnn.ipynb`  
**Ações:**
- Carregar datasets aumentados
- Definir arquitetura CNN
- Treinar modelo
- Salvar pesos treinados

----

### Fase 4: Teste
**Ambiente:** treinamento  
**Arquivo:** `teste_modelo.ipynb`  
**Ações:**
- Carregar modelo treinado
- Realizar inferência
- Avaliar performance

----

## 🧪 Metodologia de Ruído

**Técnica de Síntese:**
1. Costura de dois sinais ECG diferentes
2. Adição flutuação linha base  
3. Injeção ruído alta frequência

----

## 📂 Organização do Projeto

**Pasta de Dados** - basededados/  
**Pasta de Notebooks** - notebooks/  
**Pasta de Requisitos** - requirements/  
**Pasta de Modelos** - modelos/  
**Pasta de Resultados** - resultados/  

----

## 📋 Arquivos Principais

**Pré-processamento** - preprocessamento.ipynb  
**Processamento** - processamento.ipynb  
**Modelo CNN** - modelo_cnn.ipynb  
**Testes** - teste_modelo.ipynb

----

## ⚠️ Instruções Iniciais

1. Criar diretório basededados/
2. Incluir no .gitignore
3. Obter datasets do PhysioNet
4. Executar notebooks na ordem correta