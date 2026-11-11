# Fundamentos de Aprendizagem Profunda

Este projeto reúne **dois dos meus primeiros trabalhos da pós-graduação**. Apresento-os como estudos exploratórios e identifico as limitações encontradas na revisão, em vez de tratar os resultados como uma comparação definitiva.

1. [CIFAR-10: hiperparâmetros de uma ANN](notebooks/01_cifar10_hyperparameters.ipynb) — estudo de configurações de treino para classificação de imagens. O trabalho original foi realizado em grupo.
2. [ECG5000: classificação com CNN, LSTM e GRU](notebooks/02_ecg5000_classification.ipynb) — comparação de três arquiteturas para sequências de ECG.

Os dois notebooks usam PyTorch Lightning, mas abordam conjuntos de dados e tarefas diferentes. As suas métricas não são diretamente comparáveis.

## Ambiente

Recomendo Python 3.11. O notebook CIFAR-10 está configurado para usar GPU; os treinadores do ECG5000 estão configurados para CPU. No Anaconda Prompt ou CMD, a partir da raiz deste projeto:

```cmd
conda create -n dlf python=3.11
conda activate dlf
python -m pip install torch==2.14.1 torchvision==0.29.1 --index-url https://download.pytorch.org/whl/cu130
python -m pip install -r requirements.txt
python -m ipykernel install --user --name dlf --display-name "Python (dlf)"
```

Seleciona o kernel `Python (dlf)` nos dois notebooks. A instalação CUDA acima foi usada com uma NVIDIA RTX 3060 Ti; noutro sistema, escolhe a versão adequada nas [instruções oficiais do PyTorch](https://pytorch.org/get-started/locally/).

## Estrutura e execução

- `notebooks/` contém os dois estudos, pela ordem em que são apresentados.
- `data/` contém os dados locais. O CIFAR-10 é descarregado pelo notebook para `data/cifar10/`; o ECG5000 requer `data/ecg5000/ECG5000_TRAIN.txt` e `data/ecg5000/ECG5000_TEST.txt`.
- `results/` contém CSV de métricas. Os ficheiros históricos foram recuperados dos trabalhos originais e estão separados por estudo.

Abre a pasta do projeto no editor e executa cada notebook com o kernel indicado. Os caminhos funcionam com a raiz do projeto ou `notebooks/` como pasta de trabalho. Os CSV estão incluídos no Git para permitir visualizar os gráficos históricos; dados, logs e checkpoints ficam fora.

## Origem dos dados

- **CIFAR-10:** o notebook descarrega os dados da [página oficial de Alex Krizhevsky](https://www.cs.toronto.edu/~kriz/cifar.html). A página pede a citação do relatório técnico *Learning Multiple Layers of Features from Tiny Images* (Krizhevsky, 2009).
- **ECG5000:** obtém os ficheiros `ECG5000_TRAIN.txt` e `ECG5000_TEST.txt` na [página do ECG5000 no arquivo UCR/UEA](https://www.timeseriesclassification.com/description.php?Dataset=ECG5000) e coloca-os em `data/ecg5000/`. A [página do arquivo UCR](https://www.cs.ucr.edu/~eamonn/time_series_data_2018/) indica a referência académica do conjunto.

Os datasets são publicamente acessíveis, mas não encontrei uma licença explícita que confirme a redistribuição desta cópia do ECG5000. O arquivo CIFAR-10 também ultrapassa o [limite de 100 MiB por ficheiro no GitHub](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github). Por estas razões, os dados permanecem locais e os notebooks foram limpos dos outputs guardados.

## Leitura dos resultados

O notebook CIFAR-10 foi executado nesta estrutura e usa agora uma divisão de validação separada do conjunto de teste. Ainda não apresenta uma avaliação final nesse conjunto de teste. Os CSV antigos foram produzidos quando o conjunto de teste era usado como validação; as suas métricas são exploratórias e não devem ser comparadas diretamente com as da execução recente.

O notebook ECG5000 também foi executado nesta estrutura. No teste final dessa execução, a CNN registou 94,4% de exatidão e a LSTM e a GRU registaram 93,6% cada. Estes valores referem-se a uma execução de cada modelo, sobre uma nova divisão dos ficheiros ECG5000 originais; não constituem uma avaliação clínica nem demonstram superioridade geral. Os gráficos incluem também CSV históricos, sem informação suficiente para identificar todas as configurações anteriores.

## Licença

MIT para o código deste repositório. Consulta [LICENSE](LICENSE). Os conjuntos de dados mantêm as condições das respetivas fontes.
