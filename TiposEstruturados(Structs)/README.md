# Aula Prática — Tipos Estruturados (Structs) em C

# Objetivos da Aula

Ao final desta aula você será capaz de:

- Entender o problema que as structs resolvem;
- Criar tipos estruturados em C;
- Declarar variáveis do tipo struct;
- Manipular campos utilizando o operador `.`;
- Criar vetores de structs;
- Utilizar `typedef`;
- Passar structs para funções;
- Utilizar ponteiros para structs;
- Desenvolver pequenos sistemas de cadastro.

---

# Motivação do Problema

Até agora aprendemos tipos simples:

```c
int idade;
float altura;
char nome[50];
```

Imagine que precisamos armazenar informações de uma pessoa.

Uma possível solução seria:

```c
char nome[50];
int idade;
float altura;
float peso;
```

Funciona.

Mas e se precisarmos armazenar os dados de 10 pessoas?

```c
char nome[10][50];
int idade[10];
float altura[10];
float peso[10];
```

Agora os dados da mesma pessoa ficam espalhados.

Observe:

```txt
nome[0]
idade[0]
altura[0]
peso[0]
```

Essas informações pertencem à mesma pessoa.

Mas estão separadas em locais diferentes.

Isso dificulta:

- organização;
- manutenção;
- passagem de parâmetros para funções;
- expansão do sistema.

Precisamos agrupar essas informações.

Para isso utilizamos:

# Struct

---

# O Que é uma Struct?

Uma struct é um tipo criado pelo programador.

Ela permite agrupar várias informações relacionadas.

Exemplo:

```c
struct Pessoa {

    char nome[50];
    int idade;
    float altura;
    float peso;

};
```

Agora temos um novo tipo:

```txt
Pessoa
```

---

# Criando uma Variável do Tipo Struct

```c
#include <stdio.h>

struct Pessoa {

    char nome[50];
    int idade;
    float altura;
    float peso;

};

int main() {

    struct Pessoa aluno;

    return 0;
}
```

---

# Acessando Campos

Utilizamos o operador ponto:

```c
variavel.campo
```

Exemplo:

```c
aluno.idade = 20;
```

```c
aluno.altura = 1.75;
```

---

# Exemplo Completo

```c
#include <stdio.h>
#include <string.h>

struct Pessoa {

    char nome[50];
    int idade;
    float altura;
    float peso;

};

int main() {

    struct Pessoa aluno;

    strcpy(aluno.nome, "Joao");

    aluno.idade = 20;
    aluno.altura = 1.75;
    aluno.peso = 70;

    printf("Nome: %s\n", aluno.nome);
    printf("Idade: %d\n", aluno.idade);
    printf("Altura: %.2f\n", aluno.altura);
    printf("Peso: %.2f\n", aluno.peso);

    return 0;
}
```

---

# Prática 1

Crie uma struct chamada Produto contendo:

```txt
nome
preco
quantidade
```

Depois:

- preencha os dados manualmente;
- mostre todas as informações.

---

# Recebendo Dados do Usuário

Agora vamos tornar o programa mais útil.

```c
#include <stdio.h>

struct Pessoa {

    char nome[50];
    int idade;
    float altura;
    float peso;

};

int main() {

    struct Pessoa aluno;

    printf("Nome: ");
    scanf("%s", aluno.nome);

    printf("Idade: ");
    scanf("%d", &aluno.idade);

    printf("Altura: ");
    scanf("%f", &aluno.altura);

    printf("Peso: ");
    scanf("%f", &aluno.peso);

    printf("\nDados cadastrados\n");

    printf("Nome: %s\n", aluno.nome);
    printf("Idade: %d\n", aluno.idade);
    printf("Altura: %.2f\n", aluno.altura);
    printf("Peso: %.2f\n", aluno.peso);

    return 0;
}
```

---

# Prática 2

Crie uma struct chamada Aluno contendo:

```txt
nome
matricula
nota
```

Receba os dados do teclado e exiba ao final.

---

# Vetores de Structs

Assim como fazemos:

```c
int numeros[10];
```

Também podemos fazer:

```c
struct Pessoa pessoas[10];
```

Agora cada posição do vetor guarda uma pessoa completa.

---

# Exemplo

```c
#include <stdio.h>

struct Pessoa {

    char nome[50];
    int idade;

};

int main() {

    struct Pessoa pessoas[3];

    for(int i = 0; i < 3; i++) {

        printf("Nome: ");
        scanf("%s", pessoas[i].nome);

        printf("Idade: ");
        scanf("%d", &pessoas[i].idade);

    }

    printf("\nCadastro\n\n");

    for(int i = 0; i < 3; i++) {

        printf("Nome: %s\n", pessoas[i].nome);
        printf("Idade: %d\n\n", pessoas[i].idade);

    }

    return 0;
}
```

---

# Prática 3

Cadastre 5 livros.

Cada livro deve possuir:

```txt
titulo
autor
ano
```

Ao final mostre todos os livros cadastrados.

---

# Struct Dentro de Struct

Até agora criamos estruturas contendo apenas:

```c
int
float
char
```

Mas uma estrutura também pode possuir outra estrutura como campo.

Isso é chamado de:

```txt
Struct Aninhada
```

ou

```txt
Struct dentro de Struct
```

---

# Motivação

Imagine um cadastro de pessoas.

Além do nome, queremos armazenar:

```txt
dia de nascimento
mês de nascimento
ano de nascimento
```

Poderíamos fazer:

```c
typedef struct {

    char nome[50];

    int dia;
    int mes;
    int ano;

} Pessoa;
```

Funciona.

Mas existe uma forma mais organizada.

---

# Criando uma Struct Data

Primeiro criamos uma estrutura responsável pela data.

```c
typedef struct {

    int dia;
    int mes;
    int ano;

} Data;
```

Agora temos um tipo chamado:

```txt
Data
```

---

# Utilizando uma Struct Dentro de Outra

Agora podemos criar:

```c
typedef struct {

    char nome[50];

    Data nascimento;

} Pessoa;
```

Observe:

```c
Data nascimento;
```

O campo nascimento agora é uma estrutura completa.

---

# Representação

Pessoa:

```txt
nome
└── nascimento
     ├── dia
     ├── mes
     └── ano
```

---

# Acessando os Campos

Utilizamos vários pontos.

Exemplo:

```c
pessoa.nascimento.dia
```

```c
pessoa.nascimento.mes
```

```c
pessoa.nascimento.ano
```

---

# Exemplo Completo

```c
#include <stdio.h>

typedef struct {

    int dia;
    int mes;
    int ano;

} Data;

typedef struct {

    char nome[50];
    Data nascimento;

} Pessoa;

int main() {

    Pessoa aluno;

    printf("Nome: ");
    scanf("%s", aluno.nome);

    printf("Dia: ");
    scanf("%d", &aluno.nascimento.dia);

    printf("Mes: ");
    scanf("%d", &aluno.nascimento.mes);

    printf("Ano: ");
    scanf("%d", &aluno.nascimento.ano);

    printf("\nDados cadastrados\n");

    printf("Nome: %s\n", aluno.nome);

    printf("Nascimento: %02d/%02d/%04d\n",
           aluno.nascimento.dia,
           aluno.nascimento.mes,
           aluno.nascimento.ano);

    return 0;
}
```

---

# Struct Dentro de Struct em Vetores

Também podemos fazer:

```c
Pessoa alunos[5];
```

Cada aluno possuirá:

```txt
nome
data de nascimento
```

automaticamente.

Exemplo:

```c
alunos[0].nascimento.dia
```

```c
alunos[3].nascimento.ano
```

---

# Prática

Crie as estruturas:

```c
Endereco
```

com:

```txt
rua
numero
bairro
```

e

```c
Pessoa
```

com:

```txt
nome
idade
endereco
```

Receba os dados de 3 pessoas e exiba todas as informações.

---

# Desafio

Crie as estruturas:

```c
Disciplina
```

com:

```txt
nome
cargaHoraria
```

e

```c
Aluno
```

com:

```txt
nome
matricula
disciplina
```

Cadastre 5 alunos e exiba todas as informações.

# Utilizando Typedef

Observe:

```c
struct Pessoa aluno;
```

Precisamos escrever:

```c
struct
```

sempre.

Podemos simplificar.

---

# Exemplo

```c
typedef struct {

    char nome[50];
    int idade;

} Pessoa;
```

Agora podemos fazer:

```c
Pessoa aluno;
```

Muito mais simples.

---

# Exemplo Completo

```c
#include <stdio.h>

typedef struct {

    char nome[50];
    int idade;

} Pessoa;

int main() {

    Pessoa aluno;

    scanf("%s", aluno.nome);
    scanf("%d", &aluno.idade);

    printf("%s\n", aluno.nome);
    printf("%d\n", aluno.idade);

    return 0;
}
```

---

# Prática 4

Transforme todas as structs dos exercícios anteriores utilizando `typedef`.

---

# Structs em Funções

Podemos passar uma struct para uma função.

Exemplo:

```c
void mostrarPessoa(Pessoa p)
```

---

# Exemplo

```c
#include <stdio.h>

typedef struct {

    char nome[50];
    int idade;

} Pessoa;

void mostrarPessoa(Pessoa p) {

    printf("Nome: %s\n", p.nome);
    printf("Idade: %d\n", p.idade);

}

int main() {

    Pessoa aluno = {"Joao", 20};

    mostrarPessoa(aluno);

    return 0;
}
```

---

# Problema

Quando fazemos:

```c
mostrarPessoa(aluno);
```

Toda a struct é copiada.

Para structs pequenas isso não é grave.

Mas para estruturas grandes:

```txt
nome
cpf
rg
telefone
email
endereco
cidade
estado
...
```

isso desperdiça memória.

---

# Ponteiros para Struct

Podemos passar apenas o endereço.

```c
Pessoa *p
```

---

# Exemplo

```c
#include <stdio.h>

typedef struct {

    char nome[50];
    int idade;

} Pessoa;

void mostrarPessoa(Pessoa *p) {

    printf("Nome: %s\n", p->nome);
    printf("Idade: %d\n", p->idade);

}

int main() {

    Pessoa aluno = {"Joao", 20};

    mostrarPessoa(&aluno);

    return 0;
}
```

---

# Operador ->

Observe:

```c
(*p).idade
```

equivale a:

```c
p->idade
```

A segunda forma é mais utilizada.

---

# Prática 5

Crie uma função:

```c
void mostrarAluno(Aluno *a)
```

que exiba:

```txt
Nome
Matricula
Nota
```

utilizando o operador:

```c
->
```

---

# Projeto Prático da Aula

Crie um sistema de cadastro de alunos.

Cada aluno deve possuir:

```txt
nome
matricula
nota1
nota2
```

O sistema deve:

1. Cadastrar 5 alunos
2. Calcular média
3. Mostrar os dados
4. Informar aprovado ou reprovado

Considere:

```txt
media >= 7 → aprovado
media < 7 → reprovado
```

---

# Desafio Final

Crie uma struct chamada Data:

```c
typedef struct {

    int dia;
    int mes;
    int ano;

} Data;
```

Depois crie:

```c
typedef struct {

    char nome[50];
    Data nascimento;

} Pessoa;
```

Receba os dados de 5 pessoas.

Ao final mostre:

```txt
Nome
Data de nascimento
Idade aproximada
```

---

# Resumo

Nesta aula aprendemos:

✓ Struct

✓ Campos

✓ Operador .

✓ Vetor de Struct

✓ Typedef

✓ Struct em Funções

✓ Ponteiros para Struct

✓ Operador ->

✓ Cadastro de Dados Reais

Próximo passo:

➡️ Structs com Alocação Dinâmica

➡️ Structs Encadeadas

➡️ Listas Ligadas