---
title: Interpolação de Newton
date: 2024-06-21 12:00:00
cover: /img/lagrange.png
tags:
  - Python
  - programação
  - Math
---

# Código de Interpolação de Newton em Python

#### Código em Python para resolver os 3 exercícios com Newton.

## Introdução

A interpolação de Newton é uma técnica matemática empregada para encontrar um polinômio que atravessa todos os pontos de um conjunto de dados. Este método é especialmente útil para aproximar funções complexas a partir de dados discretos, garantindo precisão na interpolação numérica.

## Código em Python

```python
def divided_differences(x_points, y_points):
    n = len(x_points)
    F = [0] * n
    for i in range(n):
        F[i] = y_points[i]
    
    for j in range(1, n):
        for i in range(n-1, j-1, -1):
            F[i] = (F[i] - F[i-1]) / (x_points[i] - x_points[i-j])
    
    return F


def newton_interpolator(x_eval, x_points, y_points):
    F = divided_differences(x_points, y_points)
    n = len(x_points)
    p = F[0]
    for j in range(1, n):
        term = F[j]
        for i in range(j):
            term *= (x_eval - x_points[i])
        p += term
    return p

# Ex 1
x1_points = [-1, 0, 1, 2]
y1_points = [1, 3, 1, 1]
x1_eval = 1.5
y1_interpolated = newton_interpolator(x1_eval, x1_points, y1_points)
print(f"Exemplo 1: O valor interpolado de f(1.5) é: {y1_interpolated}")

# Ex  2
tempo = [1, 3, 5, 7, 13]
velocidade = [800, 1310, 2090, 2340, 3180]
tempo_eval = 10
velocidade_interpolada = newton_interpolator(tempo_eval, tempo, velocidade)
print(f"Exemplo 2: A velocidade de queda do paraquedista ao fim de 10 segundos é: {velocidade_interpolada} cm/s")

# Ex 3
x3_points = [11, 12, 13, 14, 15]
y3_points = [2.397895, 2.484907, 2.564949, 2.639057, 2.708050]
x3_eval = 12.3
y3_interpolated = newton_interpolator(x3_eval, x3_points, y3_points)
print(f"Exemplo 3: A aproximação para ln(12.3) é: {y3_interpolated}")


def show_newton_details(x_eval, x_points, y_points):
    F = divided_differences(x_points, y_points)
    n = len(x_points)
    
    print("Tabela de diferenças divididas:")
    for i in range(n):
        print(f"f[{i},0] = {F[i]}")
    
    p_x = F[0]
    termos = [f"f[0,0] = {F[0]}"]
    
    for i in range(1, n):
        termo = ""
        for j in range(i):
            termo += f"(x - {x_points[j]})"
        termo = f"f[{i},{i}] * {termo}"
        termos.append(termo)
        p_x += F[i] * (x_eval - x_points[i-1])
    
    print("\nPolinômio interpolador de Newton:")
    print("P(x) =", " + ".join(termos))
    print(f"P({x_eval}) = {p_x}")

print("\nDetalhes dos cálculos para o Exemplo 1:")
show_newton_details(x1_eval, x1_points, y1_points)

print("\nDetalhes dos cálculos para o Exemplo 2:")
show_newton_details(tempo_eval, tempo, velocidade)

print("\nDetalhes dos cálculos para o Exemplo 3:")
show_newton_details(x3_eval, x3_points, y3_points)

```

## Resultado do código acima

![Para ver o resultado  click na imagem](/img/renw.png)
