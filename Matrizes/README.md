# Matrizes em Programação C

# Motivação do Problema

Até agora aprendemos vetores.

Um vetor permite armazenar vários valores do mesmo tipo.

Exemplo:

```c
int notas[5];
```

Representação:

| Índice | Valor |
|---|---:|
| 0 | 10 |
| 1 | 20 |
| 2 | 30 |
| 3 | 40 |
| 4 | 50 |

Mas imagine situações como:

- armazenar notas de vários alunos;
- representar um tabuleiro de jogo;
- armazenar pixels de uma imagem;
- trabalhar com planilhas;
- organizar linhas e colunas.

Por exemplo:

Uma turma com 3 alunos e 4 notas.

| Aluno | Nota 1 | Nota 2 | Nota 3 | Nota 4 |
|---|---:|---:|---:|---:|
| João | 8 | 7 | 9 | 10 |
| Maria | 10 | 9 | 8 | 10 |
| Pedro | 6 | 7 | 8 | 9 |

Usar vários vetores seria confuso.

Exemplo ruim:

```c
int aluno1[4];
int aluno2[4];
int aluno3[4];
```

Para resolver isso usamos:

```txt
Matrizes
```

---

# O Que é uma Matriz?

Uma matriz é um:

```txt
vetor de vetores
```

Ou seja:

```txt
linhas × colunas
```

Uma matriz armazena elementos do mesmo tipo organizados em forma de tabela.

Representação:

```txt
1 2 3
4 5 6
7 8 9
```

---

# Estrutura de uma Matriz

## Sintaxe

```c
tipo nome[linhas][colunas];
```

---

## Exemplo

```c
int numeros[3][4];
```

Significa:

```txt
3 linhas
4 colunas
```

Representação:

| Linha/Coluna | 0 | 1 | 2 | 3 |
|---|---:|---:|---:|---:|
| 0 | | | | |
| 1 | | | | |
| 2 | | | | |

---

# Índices da Matriz

Assim como vetores:

```txt
índices começam em 0
```

Temos:

```txt
matriz[linha][coluna]
```

Exemplo:

```c
matriz[1][2]
```

Significa:

```txt
linha 1
coluna 2
```

---

# Declarando uma Matriz

```c
int matriz[3][3];
```

Representação:

| Linha/Coluna | 0 | 1 | 2 |
|---|---:|---:|---:|
| 0 | | | |
| 1 | | | |
| 2 | | | |

---

# Inicializando Matrizes

## Inicialização completa

```c
int matriz[2][3] = {

    {1,2,3},
    {4,5,6}

};
```

Representação:

| Linha | Coluna 0 | Coluna 1 | Coluna 2 |
|---|---:|---:|---:|
| 0 | 1 | 2 | 3 |
| 1 | 4 | 5 | 6 |

---

## Outra forma

```c
int matriz[2][3] = {

    1,2,3,
    4,5,6

};
```

---

# Acessando Elementos

Sintaxe:

```c
matriz[linha][coluna]
```

Exemplo:

```c
printf("%d", matriz[0][1]);
```

Saída:

```txt
2
```

---

# Alterando Valores

```c
matriz[1][2] = 100;
```

Exemplo:

```c
#include <stdio.h>

int main() {

    int matriz[2][2] = {

        {1,2},
        {3,4}

    };

    matriz[1][0] = 99;

    printf("%d", matriz[1][0]);

    return 0;
}
```

Saída:

```txt
99
```

---

# Percorrendo Matrizes

Como existem:

```txt
linhas + colunas
```

Precisamos de:

```txt
dois for
```

---

# Estrutura Geral

```c
for(int i = 0; i < linhas; i++) {

    for(int j = 0; j < colunas; j++) {

    }

}
```

---

# Exemplo de Impressão

```c
#include <stdio.h>

int main() {

    int matriz[2][3] = {

        {1,2,3},
        {4,5,6}

    };

    for(int i = 0; i < 2; i++) {

        for(int j = 0; j < 3; j++) {

            printf("%d ", matriz[i][j]);

        }

        printf("\n");

    }

    return 0;
}
```

Saída:

```txt
1 2 3
4 5 6
```

---

# Entendendo o `for`

## Variável `i`

Representa:

```txt
linha
```

---

## Variável `j`

Representa:

```txt
coluna
```

---

# Como a Matriz é Percorrida

| i | j | Elemento |
|---|---:|---:|
| 0 | 0 | matriz[0][0] |
| 0 | 1 | matriz[0][1] |
| 0 | 2 | matriz[0][2] |
| 1 | 0 | matriz[1][0] |
| 1 | 1 | matriz[1][1] |
| 1 | 2 | matriz[1][2] |

---

# Entrada de Dados

```c
#include <stdio.h>

int main() {

    int matriz[2][2];

    for(int i = 0; i < 2; i++) {

        for(int j = 0; j < 2; j++) {

            printf("Digite [%d][%d]: ", i, j);

            scanf("%d", &matriz[i][j]);

        }

    }

    return 0;
}
```

---

# Saída de Dados

```c
for(int i = 0; i < 2; i++) {

    for(int j = 0; j < 2; j++) {

        printf("%d ", matriz[i][j]);

    }

    printf("\n");

}
```

---

# Memória na Matriz

Os elementos são armazenados de forma contínua.

Exemplo:

```c
int matriz[2][3] = {

    {1,2,3},
    {4,5,6}

};
```

Na memória (exemplo):

| Elemento | Endereço |
|---|---:|
| matriz[0][0] | 1000 |
| matriz[0][1] | 1004 |
| matriz[0][2] | 1008 |
| matriz[1][0] | 1012 |
| matriz[1][1] | 1016 |
| matriz[1][2] | 1020 |

Observe:

```txt
linha 0 inteira
↓
linha 1 inteira
```

Isto é chamado:

```txt
row-major order
```

---

# Obtendo Quantidade de Linhas

```c
sizeof(matriz) / sizeof(matriz[0])
```

---

# Obtendo Quantidade de Colunas

```c
sizeof(matriz[0]) / sizeof(matriz[0][0])
```

---

# Exemplo

```c
int matriz[3][4];

int linhas =
    sizeof(matriz)
    / sizeof(matriz[0]);

int colunas =
    sizeof(matriz[0])
    / sizeof(matriz[0][0]);
```

Resultado:

```txt
3 linhas
4 colunas
```

---

# Matrizes em Funções

Sintaxe:

```c
void mostrar(int matriz[][3], int linhas)
```

Observe:

```txt
número de colunas obrigatório
```

---

# Exemplo

```c
#include <stdio.h>

void mostrar(int matriz[][3], int linhas) {

    for(int i = 0; i < linhas; i++) {

        for(int j = 0; j < 3; j++) {

            printf("%d ", matriz[i][j]);

        }

        printf("\n");

    }

}

int main() {

    int matriz[2][3] = {

        {1,2,3},
        {4,5,6}

    };

    mostrar(matriz, 2);

    return 0;
}
```

---

# Erro Comum

Errado:

```c
void mostrar(int matriz[][])
```

Motivo:

```txt
o compilador precisa saber o número de colunas
```

---

# Matriz de Strings

Também podemos ter:

```c
char nomes[3][20];
```

Significa:

```txt
3 strings
20 caracteres cada
```

---

# Resumo Geral

| Conceito | Explicação |
|---|---|
| Matriz | vetor de vetores |
| Acesso | `matriz[i][j]` |
| Índice inicial | `0` |
| Estrutura | linhas × colunas |
| Percorrer | dois `for` |
| Memória | contínua |
| Funções | coluna obrigatória |

---

# Exercícios

## Exercício 1

Crie uma matriz `3x3` e exiba todos os elementos.

---

## Exercício 2

Leia uma matriz `2x2` e mostre os valores.

---

## Exercício 3

Faça um programa que calcule a soma dos elementos de uma matriz.

---

## Exercício 4

Encontre o maior elemento da matriz.

---

## Exercício 5

Encontre o menor elemento.

---

## Exercício 6

Conte quantos números pares existem.

---

## Exercício 7

Calcule a soma de cada linha.

---

## Exercício 8

Calcule a soma de cada coluna.

---

## Exercício 9

Mostre a diagonal principal.

Exemplo:

```txt
1 2 3
4 5 6
7 8 9
```

Diagonal principal:

```txt
1 5 9
```

---

## Exercício 10

Mostre a diagonal secundária.

---

## Exercício 11

Faça a transposta da matriz.

---

## Exercício 12

Leia notas de alunos:

```txt
3 alunos
4 notas
```

Depois calcule a média de cada aluno.