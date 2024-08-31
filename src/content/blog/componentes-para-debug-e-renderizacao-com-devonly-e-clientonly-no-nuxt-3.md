---
title: "Componentes para Debug e Renderização com DevOnly e ClientOnly no Nuxt 3"
description: "Aprenda a utilizar componentes condicionais no Nuxt para otimizar seu ambiente de desenvolvimento e melhorar a performance da sua aplicação, exibindo informações de debug e renderizando conteúdo apenas no cliente. Descubra como garantir uma build mais eficiente e segura para seus usuários."
pubDate: "Aug 31 2024"
heroImage: "/articles/09-componentes-para-debug-e-renderizacao-com-devonly-e-clientonly-no-nuxt-3/hero.png"
---

## Componentes DevOnly

Às vezes, é necessário exibir informações adicionais de depuração ou metadados durante o desenvolvimento, mas sem incluí-los na versão final de produção. Um exemplo disso é a utilização do componente DevOnly para alternar entre contas de teste, atualizar rapidamente valores no banco de dados ou modificar outras configurações diretamente no ambiente de desenvolvimento, sem permitir que os usuários finais tenham acesso a essas funcionalidades.

O componente `DevOnly` funciona conforme o esperado: tudo o que você envolve dentro dele estará disponível apenas na build de desenvolvimento. Veja um exemplo de uso no layout:

```vue
// layouts/default.vue
<template>
  <div>
    <DevOnly>
      <DevAccountSwitcher />
    </DevOnly>
    <slot />
  </div>
</template>
```

Também é possível utilizar o slot #fallback, que renderiza conteúdo apenas em builds de produção, caso essa funcionalidade seja necessária:

```vue
// layouts/default.vue
<template>
  <div>
    <DevOnly>
      <DevAccountSwitcher />
      <template #fallback>
        <div>This is rendered only in the production build.</div>
      </template>
    </DevOnly>
    <slot />
  </div>
</template>
```

## Componentes ClientOnly

Você pode definir que uma seção de seu componente seja renderizada apenas no lado do cliente usando o componente `<ClientOnly>`. Isso é útil quando uma parte do conteúdo não deve ser renderizada no servidor, melhorando a performance ao não incluir essa parte na build do servidor.

Veja como utilizá-lo:

```vue
<template>
  <div>
    <p>A regular component rendered on the server and client.</p>
    <ClientOnly>
      <p>But this part shouldn't be rendered on the server</p>
      <WillBreakOnTheServer />
    </ClientOnly>
  </div>
</template>
```

O conteúdo dentro do slot padrão do `ClientOnly` é removido da build do servidor, ajudando na performance. Também podemos especificar um slot #fallback que será renderizado no servidor, o que é útil para incluir um estado de carregamento a ser exibido durante a hidratação:

```vue
<template>
  <div>
    <p>A regular component rendered on the server and client.</p>
    <ClientOnly>
      <p>But this part shouldn't be rendered on the server</p>
      <WillBreakOnTheServer />
      <template #fallback>
        <Spinner>Just give me a moment while I load some things.</Spinner>
      </template>
    </ClientOnly>
  </div>
</template>
```

### Cuidados com Componentes Client

Os componentes Client são úteis quando utilizados em conjunto com componentes de servidor ou de forma isolada, utilizando o sufixo **.client.vue**. No entanto, é importante lembrar que, como o Nuxt envolve esses componentes com o `<ClientOnly>`, eles devem ser importados automaticamente ou manualmente através de **#components**. Caso contrário, serão importados como componentes Vue regulares.

Outro ponto a considerar é que, como esses componentes não são renderizados no servidor, não há HTML disponível até que eles sejam montados e renderizados. Isso significa que precisamos esperar um ciclo de renderização antes de acessar o template:

```vue
// ~/components/CoolComponent.client.vue
<template>
  <div ref="container">
    <!-- Do some cool stuff here -->
  </div>
</template>
<script setup>
const container = ref(null);
onMounted(async () => {
  // Nada foi renderizado ainda
  console.log(container.value); // -> null

  // Espera um ciclo de renderização
  await nextTick();

  // Agora podemos acessar!
  console.log(container.value); // -> <div ...>
});
</script>
```
--- 

Gostou do conteúdo? Para aprofundar ainda mais seus conhecimentos, recomendo a leitura do guia oficial sobre `<DevOnly />` e `<ClientOnly />`.. Confira em: <a href="https://nuxt.com/docs/api/components/dev-only" target="_blank">Nuxt DevOnly Guide</a> e <a href="https://nuxt.com/docs/api/components/client-only" target="_blank">Nuxt ClientOnly Guide</a>.

Se tiver dúvidas ou quiser trocar ideias sobre desenvolvimento, fique à vontade para me contatar no <a href="https://www.linkedin.com/in/gabrielcaiana/" target="_blank">LinkedIn</a> ou no <a href="http://github.com/gabrielcaiana" target="_blank">GitHub</a>. Será um prazer continuar a conversa!

