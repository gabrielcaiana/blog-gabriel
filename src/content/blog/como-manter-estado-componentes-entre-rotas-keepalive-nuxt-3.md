---
title: "Como Preservar o Estado dos Componentes entre Rotas com KeepAlive no Nuxt 3"
description: "Aprenda como utilizar o KeepAlive no Nuxt 3 para manter o estado dos componentes entre mudanças de rota, garantindo uma experiência de usuário mais fluida e eficiente em suas aplicações."
pubDate: "Aug 26 2024"
heroImage: "/articles/08-como-manter-estado-componentes-entre-rotas-keepalive-nuxt-3/hero.png"
---

Normalmente, quando ocorre uma mudança de página, os componentes são destruídos e recriados. Podemos manter um componente “rodando” usando a propriedade **keepAlive**, para que o **Nuxt** o envolva no componente `<KeepAlive>` para nós.

Vamos supor que temos esta página que conta continuamente:

```vue
// ~/pages/count.vue
<template>
  {{ count }}
</template>

<script setup>
const count = ref(0);
onMounted(() => {
  setInterval(() => count.value++, 1000);
});
</script>
```

Cada vez que navegamos para fora e voltamos para `/count`, este componente é recriado, reiniciando a contagem de volta para zero todas as vezes.

Se você definir a propriedade `<keepAlive>` no componente `NuxtPage`, ele preservará o estado de todos os componentes filhos:

```vue
// app.vue
<template>
  <NuxtPage keepalive />
</template>
```

Agora, se navegarmos para outra página, o componente não será destruído e continuará contando mesmo enquanto estivermos em outras páginas. Ele só será destruído em um recarregamento completo da página.

Isso também funciona para rotas filhas, desde que o componente pai que está renderizando o `NuxtPage` com `<keepAlive>` não seja destruído por uma mudança de página.

Também podemos definir a propriedade keepalive no definePageMeta, em vez de especificá-la no componente NuxtPage, o que manterá todas as páginas filhas vivas:

```vue
<template>
  <div>
    Mantendo vivo.
    <NuxtPage />
  </div>
</template>

<script setup>
definePageMeta({
  keepalive: true,
});
</script>
```

Por fim, todas as páginas filhas que têm keepalive definido como true em seu **definePageMeta** terão seu estado preservado ao alternar entre elas, independentemente do que está acontecendo no componente **NuxtPage** ou na página pai (se houver).

--- 

Gostou do conteúdo? Para aprofundar ainda mais seus conhecimentos, recomendo a leitura do guia oficial sobre KeepAlive no Vue.js. Confira em: <a href="https://vuejs.org/guide/built-ins/keep-alive.html#keepalive" target="_blank">Vue.js KeepAlive Guide</a>.

Se tiver dúvidas ou quiser trocar ideias sobre desenvolvimento, fique à vontade para me contatar no <a href="https://www.linkedin.com/in/gabrielcaiana/" target="_blank">LinkedIn</a> ou no <a href="http://github.com/gabrielcaiana" target="_blank">GitHub</a>. Será um prazer continuar a conversa!

