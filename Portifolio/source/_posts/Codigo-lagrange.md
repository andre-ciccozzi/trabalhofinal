---
title: Interpolação de Lagrange
date: 2024-06-21 12:00:00
cover: /img/lagrange.png
tags:
  - Python
  - programação
  - Math
---


# Código de Interpolação de Lagrange em Python
# Introdução
A interpolação de Lagrange é outra técnica fundamental na matemática e na computação, utilizada para encontrar um polinômio que passe por um conjunto específico de pontos de dados. Este método é eficaz na reconstrução de funções contínuas a partir de valores discretos, sendo amplamente aplicado em diversas áreas da ciência e engenharia.
## Código em Python

```python


def lagrange_basis(x, x_points, j):
    l_j = 1
    for m in range(len(x_points)):
        if m != j:
            l_j *= (x - x_points[m]) / (x_points[j] - x_points[m])
    return l_j


def lagrange_interpolator(x, x_points, y_points):
    L_x = 0
    for j in range(len(x_points)):
        L_x += y_points[j] * lagrange_basis(x, x_points, j)
    return L_x

# Ex 1
x1_points = [-1, 0, 1, 2]
y1_points = [1, 3, 1, 1]
x1_eval = 1.5
y1_interpolated = lagrange_interpolator(x1_eval, x1_points, y1_points)
print(f"Exercício 1: O valor interpolado de f(1.5) é: {y1_interpolated}")

# Ex 2
tempo = [1, 3, 5, 7, 13]
velocidade = [800, 1310, 2090, 2340, 3180]
tempo_eval = 10
velocidade_interpolada = lagrange_interpolator(tempo_eval, tempo, velocidade)
print(f"Exercício 2: A velocidade de queda do paraquedista ao fim de 10 segundos é: {velocidade_interpolada} cm/s")

# Ex 3
x3_points = [11, 12, 13, 14, 15]
y3_points = [2.397895, 2.484907, 2.564949, 2.639057, 2.708050]
x3_eval = 12.3
y3_interpolated = lagrange_interpolator(x3_eval, x3_points, y3_points)
print(f"Exercício 3: A aproximação para ln(12.3) é: {y3_interpolated}")


def show_lagrange_details(x_eval, x_points, y_points):
    L_x_calc = 0
    for j in range(len(x_points)):
        l_j = lagrange_basis(x_eval, x_points, j)
        print(f"l_{j}({x_eval}) = {l_j}")
        L_x_calc += y_points[j] * l_j
        print(f"Termo {j}: y_{j} * l_{j}({x_eval}) = {y_points[j]} * {l_j} = {y_points[j] * l_j}")
    print(f"Polinômio interpolador L({x_eval}) = {L_x_calc}")


print("\nDetalhes dos cálculos para o Exemplo 1:")
show_lagrange_details(x1_eval, x1_points, y1_points)

print("\nDetalhes dos cálculos para o Exemplo 2:")
show_lagrange_details(tempo_eval, tempo, velocidade)

print("\nDetalhes dos cálculos para o Exemplo 3:")
show_lagrange_details(x3_eval, x3_points, y3_points)


```
## Resultado do codigo acima


![Para ver o resultado  click na imagem](/img/rela.png)
