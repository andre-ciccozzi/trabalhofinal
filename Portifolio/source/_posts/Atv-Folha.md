---
title: Cálculo  Folha de Árvore
date: 2024-06-21 19:00:00
cover: /img/mt.png
tags:
  - Python
  - programação
  - Math
---

# Medição e Avaliação do Erro Utilizando uma Folha de Árvore

Para esta atividade, coletamos uma folha de árvore, identificamos cinco pontos específicos e empregamos métodos numéricos para avaliar a precisão das medições realizadas. 

## Medições e Cálculos

### Imagem da Folha com as Medições

![](/img/folha.png)


### Código Utilizado

O código abaixo foi utilizado para calcular utilizando o método de Newton com os pontos medidos na folha:

```python
# Código de Interpolação Polinomial usando Newton 

def calcular_diferencas_divididas(x, y):
    n = len(x)
    F = [[0] * n for _ in range(n)]
    for i in range(n):
        F[i][0] = y[i]

    for j in range(1, n):
        for i in range(n - j):
            F[i][j] = (F[i+1][j-1] - F[i][j-1]) / (x[i+j] - x[i])

    return [F[i][i] for i in range(n)]

def calcular_polinomio_interpolador(x, y):
    dif_div = calcular_diferencas_divididas(x, y)
    n = len(x)

    def polinomio_interp(xi):
        resultado = dif_div[0]
        termo = 1
        for i in range(1, n):
            termo *= (xi - x[i-1])
            resultado += dif_div[i] * termo
        return resultado

    return polinomio_interp


x = [1, 2, 3, 4, 5]
y = [2, 3.5, 5, 2, 1.6]


polinomio_interp = calcular_polinomio_interpolador(x, y)


ponto_teste = 3.5
resultado = polinomio_interp(ponto_teste)
print(f"Para x = {ponto_teste}, o valor interpolado é {resultado}")

```
### Resultado no codigo

![Para ver o resultado click na imagem](/img/Refolha.png)