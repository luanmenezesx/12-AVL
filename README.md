# Árvores AVL (Adelson-Velsky e Landis)
---

## 📚 Introdução

Uma **Árvore AVL** é uma árvore binária de busca **auto-balanceada**, onde a diferença de altura entre as subárvores esquerda e direita de qualquer nó (chamada de **fator de balanceamento**) não pode ser maior que 1.

Esta propriedade garante que operações de busca, inserção e remoção sejam realizadas em tempo **O(log n)**, mesmo no pior caso.

---

## 🎯 Objetivos de Aprendizagem

Ao concluir esta atividade, você deverá compreender:

1. **Árvore Binária de Busca (ABB)**: Estrutura base onde cada nó tem no máximo dois filhos, com valores à esquerda menores e à direita maiores.

2. **Altura de um Nó**: A distância do nó até a folha mais distante em sua subárvore.
   - Nó folha: altura = 0
   - Nó NULL: altura = -1

3. **Fator de Balanceamento (FB)**: Diferença entre a altura da subárvore esquerda e direita.
   ```
   FB = altura(subárvore esquerda) - altura(subárvore direita)
   ```
   - FB > 1: árvore "pesada" à esquerda
   - FB < -1: árvore "pesada" à direita
   - -1 ≤ FB ≤ 1: árvore balanceada

4. **Rotações**: Operações para rebalancear a árvore após inserções/remoções.

---

## 🔄 Tipos de Rotações

### 1. Rotação Simples à Direita

Utilizada quando ocorre desbalanceamento **Esquerda-Esquerda** (FB > 1 no nó y e valor inserido à esquerda do filho esquerdo).

**Visualização:**
```
        y                    x
       / \                  / \
      x   T3    =>         T1  y
     / \                      / \
    T1  T2                   T2 T3
```

**Passos da implementação:**
1. Armazene o filho esquerdo de `y` em `x`
2. Transfira a subárvore direita de `x` (T2) para a esquerda de `y`
3. Faça `y` se tornar filho direito de `x`
4. Recalcule as alturas de `y` e depois de `x`
5. Retorne `x` como nova raiz da subárvore

### 2. Rotação Simples à Esquerda

Utilizada quando ocorre desbalanceamento **Direita-Direita** (FB < -1 no nó x e valor inserido à direita do filho direito).

**Visualização:**
```
      x                      y
     / \                    / \
    T1  y        =>        x   T3
       / \                / \
      T2 T3              T1 T2
```

**Passos da implementação:**
1. Armazene o filho direito de `x` em `y`
2. Transfira a subárvore esquerda de `y` (T2) para a direita de `x`
3. Faça `x` se tornar filho esquerdo de `y`
4. Recalcule as alturas de `x` e depois de `y`
5. Retorne `y` como nova raiz da subárvore

### 3. Rotação Dupla Esquerda-Direita

Usada em casos **Esquerda-Direita** (FB > 1 e valor inserido à direita do filho esquerdo).

**Solução:** 
1. Rotação esquerda no filho esquerdo
2. Rotação direita no nó desbalanceado

### 4. Rotação Dupla Direita-Esquerda

Usada em casos **Direita-Esquerda** (FB < -1 e valor inserido à esquerda do filho direito).

**Solução:**
1. Rotação direita no filho direito
2. Rotação esquerda no nó desbalanceado

---

## 💻 Estrutura do Código

### Estrutura do Nó
```cpp
struct NO {
    int valor;      // Dado armazenado
    NO* esq;        // Ponteiro para filho esquerdo
    NO* dir;        // Ponteiro para filho direito
    int altura;     // Altura do nó (para balanceamento)
};
```

### Funções Principais

- `insereArvore()`: Insere um elemento e rebalanceia se necessário
- `alturaNo()`: Retorna a altura de um nó
- `fatorBalanceamento()`: Calcula o FB de um nó
- `girarDireita()`: **[A IMPLEMENTAR]** Rotação à direita
- `girarEsquerda()`: **[A IMPLEMENTAR]** Rotação à esquerda

---

## ✅ Atividade Proposta

Faça um fork deste repositório e realize as seguintes atividades:

### Tarefa 1: Implementar `girarDireita()`

- [ ] Localize a função `NO* girarDireita(NO* y)` no arquivo `AVL.cpp`
- [ ] Siga os 5 passos comentados no código
- [ ] **Dica**: Use a visualização do diagrama como referência
- [ ] **Importante**: Não esqueça de recalcular as alturas após as rotações

**Exemplo de cálculo de altura:**
```cpp
no->altura = maior(alturaNo(no->esq), alturaNo(no->dir)) + 1;
```

### Tarefa 2: Implementar `girarEsquerda()`

- [ ] Localize a função `NO* girarEsquerda(NO* x)` no arquivo `AVL.cpp`
- [ ] Siga os 5 passos comentados no código
- [ ] **Dica**: Esta função é espelhada em relação à `girarDireita()`
- [ ] **Importante**: Mantenha a lógica simétrica

---

## 🧪 Como Testar

1. Compile o programa:
 - Utilize o Visual Studio 2022 ou superior para compilar o código


2. Execute e teste com sequências que causem desbalanceamento:
   - **Caso EE**: Inserir 30, 20, 10 (requer rotação direita)
   - **Caso DD**: Inserir 10, 20, 30 (requer rotação esquerda)
   - **Caso ED**: Inserir 30, 10, 20 (requer rotação dupla)
   - **Caso DE**: Inserir 10, 30, 20 (requer rotação dupla)

3. Use a opção "4 - Exibir árvore" para visualizar a estrutura após cada inserção.

---

## 📖 Referências e Recursos

- **Complexidade AVL**: Todas as operações em O(log n)
- **Inventores**: Georgy Adelson-Velsky e Evgenii Landis (1962)
- **Comparação**: AVL mantém balanceamento mais rígido que Red-Black Trees, resultando em buscas mais rápidas mas inserções/remoções ligeiramente mais lentas

### Material Complementar
- [Visualização interativa de AVL](https://www.cs.usfca.edu/~galles/visualization/AVLtree.html)
- Desenhe cada rotação no papel para melhor compreensão
- Teste com diferentes sequências de inserção

---

## 🤔 Perguntas para Reflexão

1. Por que a complexidade permanece O(log n) mesmo no pior caso?
2. O que aconteceria se não fizéssemos o balanceamento?
3. Como as rotações preservam a propriedade de árvore binária de busca?
4. Quando precisamos de rotações duplas ao invés de simples?

---

**Boa sorte com a implementação! 🚀**
