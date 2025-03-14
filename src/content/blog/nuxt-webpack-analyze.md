---
title: "Como adicionar a análise de pacotes do webpack em seu projeto nuxt"
description: "Visualize o tamanho dos arquivos de saída do webpack com um mapa de árvore interativo dentro do seu projeto com nuxtjs."
pubDate: "Jan 21 2024"
heroImage: "/articles/05-nuxt-webpack-analyze/webpack-analyzer.png"
image:
  src: '/articles/05-nuxt-webpack-analyze/webpack-analyzer.png'
  alt: 'Visualize o tamanho dos arquivos de saīda do webpack com um mapa de árvore interativo com zoom.'
  width: 400
  height: 300
head:
  meta:
    - name: 'keywords'
      content: 'nuxt, webpack, performance, frontend'
    - name: 'robots'
      content: 'index, follow'
    - name: 'author'
      content: 'Gabriel Caiana'
    - name: 'copyright'
      content: '© 2022 Gabriel Caiana'
---

Sabemos como é importante colocar em produção aplicações que tenham o melhor desempenho possível, porém conforme começamos a desenvolver um projeto adicionamos diversos pacotes para determinadas tarefas e no final isso terá um impacto no desempenho da aplicação, como podemos análisar isso utilizando o nuxtjs?

Recentemente descobri uma forma muito fácil e interativa para mapear e análisar os pacotes que estão sendo utilizados no projeto, podemos criar um comando simples no `package.json` da seguinte forma:

```javascript
"scripts": {
  "dev": "nuxt",
  "build": "nuxt build",
  "analyze": "nuxt build --analyze"
}
```

ou podemos executar direto no terminal com yarn

```zsh
yarn build --analyze
```

ou até mesmo utilizando o comando npx

```zsh
npx nuxt build --analyze
```

com isso o webpack analyzer deve ser inicializado em seu navegador e com isso podemos visualizar toda a árvore de pacotes que o projeto está utilizando

![Exemplo de uso do webpack analyzer ](https://cloud.githubusercontent.com/assets/302213/20628702/93f72404-b338-11e6-92d4-9a365550a701.gif)

Temos também uma barra a esquerda que permite que você escolha quais pedaços mostrar com os seus devidos tamanhos. podemos ver um exemplo disso na imagem abaixo:

![imagem dos chunks do projeto](/articles/05-nuxt-webpack-analyze/chunks.png)

Você também pode clicar duas vezes nas caixas, passar o mouse sobre elas para obter mais detalhes e clicar com o botão direito em um pedaço para ocultá-lo facilmente ou para ocultar todos os outros pedaços.

Espero que esse artigo possa ajudar você a analisar seu projeto e melhora-lo, vejo você no próximo post.

**Link:** https://www.npmjs.com/package/webpack-bundle-analyzer



