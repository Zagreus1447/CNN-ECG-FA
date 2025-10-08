Projeto CNN: Detecção de Fibrilação Atrial (FA) em ECG Vestível
Visão Geral do Projeto

Este projeto implementa uma Rede Neural Convolucional (CNN) com arquitetura de kernels grandes e reduzidos, focada na extração de características de baixa frequência (como as da FA). O objetivo principal é a classificação de Fibrilação Atrial (FA) utilizando sinais de Eletrocardiograma (ECG) de uma única derivada, simulando dados coletados por dispositivos vestíveis (wearables).

O trabalho utiliza uma variedade de datasets para garantir a robustez contra diferentes tipos de FA e ruídos, e é estritamente dividido em dois ambientes Python separados para gerenciar as dependências de GPU/CUDA e de processamento de sinal.
💾 Bases de Dados Utilizadas (5 Datasets)

Seu projeto utiliza 5 datasets do PhysioNet, agrupados por função:
1. Dados de Fibrilação Atrial (FA)

Dataset
	

Código PhysioNet
	

Propósito no Projeto

AF Termination Challenge (2017)
	

af-termination-challenge-database-1.0.0
	

Principal fonte de registros de FA paroxística e persistente para treino e rótulos de ritmo normal.

PhysioNet/CinC Challenge 2017
	

physionet-computing-in-cardiology-challenge-2017
	

Dataset com 4 classes de FA (Simulando wearables), essencial para simular a variabilidade e classificação encontrada em dispositivos vestíveis.

PTB-XL (ECG Dataset)
	

ptb-xl-a-large-publicly-available-electrocardiography-dataset-1.0.3
	

Dataset ECG grande utilizado para obter grande volume de exemplos de FA e outras arritmias, além de ser usado como fonte de ritmo normal.
2. Dados de Ruído (Noise)

Dataset
	

Código PhysioNet
	

Propósito no Projeto

Motion Artifacts (Ruídos)
	

motion-artifact-contaminated-ecg-database-1.0.0
	

Utilizado para treinar o modelo contra artefatos de movimento, comuns em wearables, aumentando a robustez.

MIT-BIH Noise Stress Test Database
	

mit-bih-noise-stress-test-database-1.0.0
	

Fonte adicional de ruídos (músculo, eletrodo, etc.) para injeção e aumento da capacidade de generalização do modelo.

Localização: Todos esses datasets devem ser baixados e colocados na pasta basededados/ na raiz do seu projeto. Esta pasta deve ser ignorada pelo Git.
⚙️ Configuração dos Ambientes Virtuais

O projeto utiliza pip e Jupyter Notebook como ferramentas principais.

ATENÇÃO: Os nomes dos ambientes são cruciais para a organização:
Ambiente 1: Pré-Processamento (preprocessamento)

    Foco: Leitura de sinais (wfdb), filtragem, resampling e normalização.

    Notebook Correspondente: notebooks/01_Pre_processamento.ipynb (Deverá ser executado primeiro).

# Crie e ative o ambiente
conda create --name preprocessamento python=3.x  # OU crie usando venv/pip
conda activate preprocessamento

# Instale as dependências usando PIP
pip install -r environments/requirimentspreprocessamentosbs2.txt 


Ambiente 2: Modelo CNN (bs2+)

    Foco: Treinamento, validação e uso do modelo CNN (TensorFlow/Keras ou PyTorch).

    Requisito: Necessita de suporte CUDA/GPU para aceleração do treinamento.

    Notebook Correspondente: notebooks/02_Treinamento_CNN.ipynb

# Crie e ative o ambiente
conda create --name bs2+ python=3.x
conda activate bs2+

# Instale as dependências usando PIP (incluindo as bibliotecas GPU)
pip install -r environments/requirimentscnnNovaB.txt 


📝 Guia de Execução dos Notebooks

    Notebook 01_Pre_processamento.ipynb (Use o ambiente preprocessamento):

        Carrega, limpa e padroniza os dados dos 5 datasets.

        Realiza a segmentação dos sinais em janelas (e.g., 30 segundos) e aplica as rótulos de FA e Ruído.

        Salva o dataset final processado no disco (fora do Git) para o próximo passo.

    Notebook 02_Treinamento_CNN.ipynb (Use o ambiente bs2+):

        Carrega o dataset processado.

        Define e treina a arquitetura CNN com kernels grandes para detecção de FA.

        Realiza a avaliação de desempenho e salva o modelo final em disco.
