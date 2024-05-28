# Modelo de Classificação de Imagens CIFAR-10 com Fine-Tuning e API Flask

Este documento fornece uma visão geral do processo de treinamento de um modelo de classificação de imagens usando a arquitetura ResNet-18 pré-treinada no conjunto de dados CIFAR-10. Além disso, descreve a implementação de uma API Flask para inferência de imagens usando o modelo treinado.

### 1. Treinamento do Modelo

### 1.1 Preparação dos Dados

- Os dados são organizados em classes e divididos em conjuntos de treinamento, validação e teste.
- Uma transformação de pré-processamento é aplicada aos dados, incluindo redimensionamento, recorte aleatório, inversão horizontal e normalização.

### 1.2 Arquitetura do Modelo

- Utilizamos a arquitetura ResNet-18, pré-treinada no conjunto de dados ImageNet, como base.
- A camada totalmente conectada final é substituída para se ajustar ao número de classes do CIFAR-10.

### 1.3 Treinamento

- O modelo é treinado usando a técnica de Fine-Tuning.
- Um otimizador SGD é usado para ajustar os pesos do modelo.
- O aprendizado é agendado com uma redução de taxa de aprendizado a cada período de épocas.
- Durante o treinamento, a acurácia é monitorada no conjunto de validação para avaliar o desempenho do modelo.

### 1.4 Resultados

- O treinamento é avaliado em termos de perda e acurácia.
- Após o treinamento, o modelo é salvo para uso posterior.

### 2. Implementação da API Flask

### 2.1 Inicialização do Servidor

- A API Flask é configurada para receber solicitações de inferência de imagens.

### 2.2 Carregamento do Modelo

- O modelo treinado é carregado na memória para inferência.

### 2.3 Inferência de Imagens

- Quando uma imagem é enviada para a API, ela é pré-processada e passada para o modelo para inferência.
- O modelo retorna a classe predita da imagem.

### 2.4 Encerramento do Servidor

- Um endpoint especial `/shutdown` é fornecido para encerrar o servidor Flask de forma controlada.

### Conclusão

Este processo fornece uma solução completa para treinar um modelo de classificação de imagens usando Fine-Tuning e implementar uma API Flask para inferência de imagens. A API Flask oferece uma maneira conveniente de fazer predições usando o modelo treinado, permitindo integração em diferentes aplicativos e serviços.
