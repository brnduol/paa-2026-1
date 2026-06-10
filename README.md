# Equivalência entre Diferentes Noções de Permutação

Projeto desenvolvido para a disciplina de **Projeto e Análise de Algoritmos (PAA) – 2026/1**, com o objetivo de formalizar, em um assistente de provas, a equivalência entre diferentes definições de permutação de listas de números naturais. O tema foi escolhido a partir das propostas apresentadas no projeto de formalização da disciplina. 

## Integrantes

* Bruno Eduardo
* Gustavo Valadares
* Pedro Maia

## Descrição do Projeto

O projeto tem como foco a demonstração formal da equivalência entre duas definições de permutação:

1. **Permutação Indutiva (`Permutation`)**

   * Definida por regras de inferência que permitem:

     * Permutação da lista vazia;
     * Preservação da cabeça da lista;
     * Troca de elementos adjacentes;
     * Composição transitiva de permutações.

2. **Equivalência por Contagem de Ocorrências (`equiv`)**

   * Duas listas são consideradas equivalentes quando possuem a mesma quantidade de ocorrências de cada elemento.

O objetivo principal consiste em provar formalmente que essas duas definições caracterizam exatamente o mesmo conceito matemático de permutação. 

## Objetivos

* Formalizar as definições de permutação propostas.
* Implementar a função de contagem de ocorrências em listas.
* Demonstrar que toda permutação preserva o número de ocorrências de cada elemento.
* Demonstrar que listas com o mesmo número de ocorrências de cada elemento são permutações entre si.
* Concluir a equivalência entre as duas definições.

## Estrutura Teórica

### Definição Indutiva de Permutação

A relação `Permutation` é definida por meio das seguintes regras:

* `perm_nil`
* `perm_skip`
* `perm_swap`
* `perm_trans`

Essas regras permitem construir provas de permutação entre listas através de operações elementares de troca e composição. 

### Contagem de Ocorrências

A função `num_oc` contabiliza quantas vezes um elemento aparece em uma lista.

```coq
Fixpoint num_oc x l :=
match l with
| nil => 0
| h :: tl =>
    if x =? h
    then S (num_oc x tl)
    else num_oc x tl
end.
```

### Equivalência de Listas

A definição alternativa de permutação é dada por:

```coq
Definition equiv l l' :=
  forall n:nat,
    num_oc n l = num_oc n l'.
```

Duas listas são equivalentes quando apresentam exatamente as mesmas ocorrências para qualquer número natural. 

## Principais Resultados

Durante o desenvolvimento serão formalizados os seguintes resultados:

```coq
Lemma perm_to_equiv :
  forall l l',
    Permutation l l' -> equiv l l'.

Lemma equiv_to_perm :
  forall l l',
    equiv l l' -> Permutation l l'.

Theorem perm_equiv :
  forall l l',
    Permutation l l' <-> equiv l l'.
```

Esses resultados estabelecem a equivalência completa entre as duas noções de permutação. 

## Ferramentas Utilizadas

* Rocq / Coq
* Git e GitHub
* VS Code (opcional)

## Estrutura do Repositório

```text
.
├── src/
│   ├── Permutation.v
│   ├── Equiv.v
│   └── Main.v
├── docs/
│   └── relatorio.pdf
├── README.md
```

## Como Executar

Clone o repositório:

```bash
git clone <url-do-repositorio>
cd <nome-do-repositorio>
```

Compile os arquivos:

```bash
coqc src/Permutation.v
coqc src/Equiv.v
coqc src/Main.v
```
## Referência

Tema 7 — **Equivalência entre diferentes noções de permutação**, proposto na disciplina Projeto e Análise de Algoritmos (PAA – 2026/1), ministrada pelo professor Flávio L. C. de Moura. 
