---
title: "O que são micro frontends"
description: "O termo Micro Frontends surgiu pela primeira vez no ThoughtWorks Technology Radar no final de 2016. Ele estende os conceitos de microsserviços para o mundo do frontend."
pubDate: "Jul 08 2022"
heroImage: "/articles/01-microfrontends/example-microfrontends.png"
---

O termo Micro Frontends surgiu pela primeira vez no ThoughtWorks Technology Radar no final de 2016. Ele estende os conceitos de microsserviços para o mundo do frontend. A tendência atual é construir um aplicativo de navegador poderoso e rico em recursos, também conhecido como aplicativo de página única, que se baseia em uma arquitetura de microsserviço. Com o tempo, a camada de front-end, geralmente desenvolvida por uma equipe separada, cresce e fica mais difícil de manter. Isso é o que chamamos de Monólito de Frontend.

A ideia por trás do Micro Frontends é pensar em um site ou aplicativo da web como uma composição de recursos pertencentes a equipes independentes . Cada equipe tem uma área de negócio ou missão distinta com a qual se preocupa e se especializa. Uma equipe é multifuncional e desenvolve seus recursos de ponta a ponta , do banco de dados à interface do usuário.

## Exemplo de frontends monolíticos

<img src="/articles/01-microfrontends/frontend-monoliticos.png" alt="frontend monolíticos" />

## Exemplo de times com organização em verticais

<img src="/articles/01-microfrontends/teams-microfronend.png" alt="times com organização em verticais" />

## Quais são os principais benefícios de utilizar esse tipo de arquitetura

1. Independência de framework.
2. Códigos mais fáceis de serem testados.
3. Responsabilidade única.
4. Deploys independentes.
5. Maior escalabilidade.
6. Uma forma de evoluir frontends legados.
7. Possibilidades de upgrade, update e reescrita de pequenas partes.
8. Códigos menores e mais coesos.

## E quais dificuldades podemos encontrar ao utilizar os micro frontends

1. Tamanho da aplicação e do payload
2. Complexidade
3. Responsabilidade compartilhada
4. Testes E2E
5. Manter o style da aplicação

## Estratégias para aplicar os micro frontends

1. Server Side
2. Iframes
3. Run-time com frameworks javascript
4. Run-time com web components

## Boas práticas de utilização

### Autonomia tecnológica

Cada time deve ser capaz de escolher e atualizar sua stack tecnologica de forma independente.

### Código isolado

O código de cada time deve ser isolado e auto-contido, sem estados compartilhados ou variáveis globais.

### Nomeclaturas pré-estabelecidas

Onde a ideia 2 não for aplicada, deve haver uma convenção na nomeclatura de local storage, cookies, eventos e outros recursos para evitar conflitos.

### referência a recursos nativos do browser

Favoreça recursos nativos do browser ao invés de API customizadas para realizar a comunicação entre os serviços

### Resiliência

A feature desenvolvida deve ser resiliente e utilizável mesmo que haja problemas ao carregar o código javascript.(ssr)

### Resumo

Utilizar micro frontends pode ser uma ótima opção, mas isso vai depender muito com contexto e maturidade dos times, então é importante avaliar se realmente é o momento certo para isso, e se faz sentido.

Para obter mais conteúdos eu recomendo a leitura do site [MicroFrontends.org](https://micro-frontends.org/).
