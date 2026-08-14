---
title: "Debugando usando GDB"
date: 2026-08-11
draft: true
---

# Oque é o GDB?

O GDB **(GNU Project Debugger)** é uma ferramenta criada pelo projeto GNU, utilizada principalmente para análise e execução linha-a-linha de programas desenvolvidos nas linguagens C, C++, Objective-C, Ada e Pascal, isso permite o usuário ver o que está acontecendo "por dentro" do programa e procurar por erros que passaram despercebidos durante o processo de desenvolvimento.

Além de ser uma [ferramenta de código aberto](https://sourceware.org/gdb/current/) que está diariamente em processo de evolução, ela também é completamente gratuita, sem nenhuma espécie de [paywall](https://pt.wikipedia.org/wiki/Acesso_pago) ou plano de assinatura!

# Quais são as funcionalidades do GDB?

No geral, é possível resumir maioria dos processos do GDB pelas seguintes funções:

- Começar o seu programa com parâmetros específicos que afetem o seu comportamento
- Parar o programa em condições específicas
- Examinar o que estava acontecendo no programa enquanto ele está pausado
- Modificar informações que estão sendo utilizadas pelo programa para examinar o seu comportamento

Com essas 4 funcionalidades básicas é possível realizar maioria dos processos de depuração de programas de maneira eficiente. E é justamente isso que vamos abordar nessa postagem.

# Código de exemplo

O código abaixo possui um erro, proposital, que será utilizado para auxiliar na explicação de como utilizar o GDB:

```c
#include <stdio.h>

void calcular_soma(int notas[], int tamanho, int *soma_ponteiro) {
    for (int i = 0; i < tamanho; i++) {
        soma_ponteiro = soma_ponteiro + notas[i];
    }
}

int main() {
    // Notas de 5 alunos (média real = 7.8)
    int notas[] = {7, 8, 9, 5, 10};
    // Deve somar um total de 39
    int soma_total = 0;
    int quantidade = sizeof(notas) / sizeof(notas[0]);

    calcular_soma(notas, quantidade, &soma_total);

    int media = soma_total / quantidade;

    printf("Soma total: %d\n", soma_total);
    printf("Média calculada: %d\n", media);
    return 0;
}
```

O algoritmo acima deve implementar um sistema que calcule a soma e média de notas de N alunos. O valor da soma total de notas é calculado pela função `calcular_soma(...)` e é guardado na variável `soma_total`, enquanto a média geral é calculada pela fórmula `soma_total / quantidade`.

Porém, ao executar o código acima obtemos o seguinte resultado:

```
$ gcc -o main main.c && ./main
Soma total: 0
Média calculada: 0
```
