---
title: "Debugando usando GDB"
date: 2026-08-11
draft: false
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

void imprimir_elemento(int *arr, int tamanho, int indice)
{
    printf("Elemento %d: %d\n", indice, arr[indice]);
}

int main(void)
{
    int numeros[5] = {10, 20, 30, 40, 50};
    int idx;
    
    printf("Digite um índice (0-4): ");
    scanf("%d", &idx);
    
    imprimir_elemento(numeros, 5, idx);
    
    return 0;
}
```
