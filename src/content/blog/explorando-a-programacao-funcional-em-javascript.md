---
title: "Explorando a Programação Funcional em JavaScript"
description: "A Programação Funcional (FP) é um paradigma de programação que trata a computação como uma avaliação de funções matemáticas e evita a mudança de estado e dados mutáveis. Em JavaScript, um linguagem multiparadigma, a programação funcional está se tornando cada vez mais popular devido à sua capacidade de criar código mais limpo, conciso e fácil de entender."
pubDate: "Mar 30 2024"
heroImage: "/articles/07-explorando-a-programacao-funcional-em-javascript/hero.png"
---

A Programação Funcional é um paradigma de programação que trata a computação como uma avaliação de funções matemáticas e evita a mudança de estado e dados mutáveis. Em JavaScript, que é uma linguagem multiparadigma, a programação funcional está se tornando cada vez mais popular porque oferece uma maneira de criar código mais limpo, conciso e fácil de entender. Os conceitos da programação funcional serão explorados e aplicados com exemplos JavaScript de uso.

## Funções como Cidadãos de Primeira Classe

Uma característica central da programação funcional é o tratamento de funções como cidadãos integrais. Em JavaScript, isso significa que as funções podem ser atribuídas a variáveis, passadas como argumentos para outras funções e retornadas como valores de outras funções. Isso possibilita a composição de funções de uma maneira poderosa e flexível.

```javascript
// Função sendo atribuida a uma variável
const sum = function(a, b) {
  return a + b
}

// Função sendo passada como argumento
const execute = function(a ,b, operation) {
  return operation(a,b)
}


console.log(execute(5,5,sum)) // Saída: 10
```

## Imutabilidade e Estruturas de Dados Imutáveis

Os dados em programação funcional são tratados como imutáveis. Ou seja, uma vez que os dados são criados, eles não podem ser alterá-los. No JavaScript, isso pode ser feito com estruturas de dados imutáveis ou clonagem profunda. Bibliotecas como [Immutable.js](https://immutable-js.com/) ou [Lodash](https://lodash.com/) podem ser úteis se você precisar manipular dados imutáveis.

```javascript
// Usando Object.freeze para tornar um objeto imutável
const pet = Object.freeze({
  name: 'Dog',
  breed: 'Labrador'
});

// Tentativa de modificação de um objeto imutável
pet.breed = 'Shih Tzu';

console.log(pet.breed); // Saída: Labrador (não foi modificada)
```

## Funções de Ordem Superior

Funções de ordem superior são funções que podem aceitar outras funções como argumentos ou retornar funções. Elas são uma parte fundamental da programação funcional e permitem abstrações poderosas.

```javascript
function multiplier(x) {
  return function(y) {
    return x * y
  }
}

const execute = multiplier(3)
console.log(execute(6)) // Saída: 18
```

## Pureza e Evitando Efeitos Colaterais

Funções puras são aquelas que produzem o mesmo resultado dado o mesmo conjunto de entradas e não têm efeitos colaterais observáveis. Isso torna o código mais previsível e fácil de testar.

```javascript
// Função impura
let counter = 0;

function increment() {
  counter++;
  return counter;
}

console.log(increment()); // Saída: 1
console.log(increment()); // Saída: 2

// Função pura equivalente
function incrementPure(counter) {
  return counter + 1;
}

let newCounter = 0;

newCounter = incrementPure(newCounter);
console.log(newCounter); // Saída: 1

newCounter = incrementPure(newCounter);
console.log(newCounter); // Saída: 2
```

## Composição de Funções

A composição de funções é uma técnica onde várias funções são combinadas para formar uma nova função. Isso permite criar código modular e reutilizável.

```javascript
// Função de composição
function compose(...functions) {
  return function(intialVal) {
    return functions.reduceRight((acc, func) => func(acc), intialVal);
  };
}

// Exemplo de uso da função de composição
const sumAndMultiplier = compose(
  x => x * 2,
  x => x + 5
);

console.log(sumAndMultiplier(3)); // Saída: 16 (5 + 3 = 8 * 2 = 16)
```

## Conclusão

A programação funcional propaga uma poderosa e abordagem distinta para o desenvolvimento de software. A propósito, o JavaScript, com seu suporte nativo à programação funcional, proliferou, implementando cada vez mais seus benefícios por criar código limpo e modular, fácil de entender e testar. Ao usar os conceitos e técnicas de programação funcional, os desenvolvedores podem produzir rotinas complexas e códigos mais sofisticados e, portanto, estão prontos para os desafios enfrentados pelo desenvolvimento moderno de software.

Caso queria explorar mais a fundo o tema, recomendo que leia também o Artigo [Entendendo Programação Funcional em JavaScript de uma vez](https://medium.com/tableless/entendendo-programa%C3%A7%C3%A3o-funcional-em-javascript-de-uma-vez-c676489be08b) escrito pelo [Matheus Lima](https://twitter.com/matheusml)