# Modelo de Classificação de Imagens CIFAR-10 com API Flask

Este documento fornece uma visão geral do processo de treinamento de um modelo de classificação de imagens usando a arquitetura ResNet-18 pré-treinada no conjunto de dados CIFAR-10. Além disso, descreve a implementação de uma API Flask para inferência de imagens usando o modelo treinado.

### 1. Treinamento do Modelo

### 1.1 Preparação dos Dados

- Os dados são organizados em classes e divididos em conjuntos de treinamento, validação e teste.
- Uma transformação de pré-processamento é aplicada aos dados, incluindo redimensionamento, recorte aleatório, inversão horizontal e normalização.

### 1.2 Arquitetura do Modelo

- Utilizamos a arquitetura ResNet-18, pré-treinada no conjunto de dados ImageNet, como base.
- A camada totalmente conectada final é substituída para se ajustar ao número de classes do CIFAR-10.

### 1.3 Treinamento

- Um otimizador SGD é usado para ajustar os pesos do modelo.
- O aprendizado é agendado com uma redução de taxa de aprendizado a cada período de épocas.
- Durante o treinamento, a acurácia é monitorada no conjunto de validação para avaliar o desempenho do modelo.

### 1.4 Resultados

### Primeiro teste:

- Epocas: 30
- Taxa de aprendizado: 0.001

### Resultados:

```jsx
loss 1.057, train acc 0.630, valid acc 0.438
286.1 examples/sec on [device(type='cuda', index=0)]
```

![img1](img\1.png)

### Segundo teste:

- Épocas: 30
- Taxa de aprendizado: 0.0001

### Resultados:

```jsx
loss 0.721, train acc 0.767, valid acc 0.525
285.3 examples/sec on [device(type='cuda', index=0)]
```

![img2](img\2.png)

### Terceiro teste:

- Epocas: 50
- Taxa de aprendizado: 0.001

### Resultados:

```jsx
loss 0.546, train acc 0.813, valid acc 0.475
286.9 examples/sec on [device(type='cuda', index=0)]
```

![img3](img\3.png)

### Quarto teste:

- Epocas: 20
- Taxa de aprendizado: 0.001

### Resultados:

```jsx
loss 1.464, train acc 0.477, valid acc 0.537
286.1 examples/sec on [device(type='cuda', index=0)]
```

![img4](img\4.png)

### 2. Implementação da API Flask

### 2.1 Inicialização do Servidor

- A API Flask é configurada para receber solicitações de inferência de imagens.

### 2.2 Carregamento do Modelo

- O modelo treinado é carregado na memória para inferência.

### 2.3 Inferência de Imagens

- Quando uma imagem é enviada para a API, ela é pré-processada e passada para o modelo para inferência.
- O modelo retorna a classe predita da imagem.

### 2.4 Resultado:

- O modelo previu corretamente a categoria cachorro e sapo, porém errou ao prever a categoria cavalo.

```jsx
url = 'http://127.0.0.1:3000/predict'
files = [
    ('file', open('/content/cavalo.jpg', 'rb')),
    ('file', open('/content/cachorro.jpg', 'rb')),
    ('file', open('/content/sapo.jpg', 'rb'))
]
response = requests.post(url, files=files)
print(response.json())
```

```jsx
INFO:werkzeug:127.0.0.1 - - [01/Jun/2024 19:00:51] "POST /predict HTTP/1.1" 200 -
{'predictions': [{'category': 'frog', 'category_index': 6}, 
				{'category': 'dog', 'category_index': 5}, 
				{'category': 'frog', 'category_index': 6}]}
```