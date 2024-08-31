---
title: "Integração entre GitHub e Discord para Notificações de Pull Requests"
description: "Aprenda a configurar uma integração entre GitHub e Discord para enviar notificações automáticas sobre Pull Requests abertos e mesclados na branch master. Mantenha sua equipe informada em tempo real com este guia passo a passo usando GitHub Actions."
pubDate: "Sep 01 2024"
heroImage: "/articles/10-integracao-github-discord-notificacoes-pull-requests/hero.png"
---

Integrar GitHub e Discord pode ser uma maneira eficaz de manter sua equipe informada sobre eventos importantes, como a abertura ou o fechamento de Pull Requests (PRs). Neste artigo, você aprenderá como configurar uma integração que envia notificações para um canal específico do Discord sempre que um PR é aberto ou mesclado na branch `master`.

## Pré-requisitos

Antes de começar, você precisará de:

1. Acesso a um repositório no **GitHub**.
2. Um servidor Discord com permissões para **criar webhooks**.
3. Acesso ao GitHub Actions no **repositório**.

## Passo 1: Criar um Webhook no Discord

Primeiro, precisamos criar um webhook no Discord, que será usado para enviar mensagens automáticas para um canal específico.

1. No Discord, vá até o servidor onde você deseja que as notificações sejam enviadas.
2. Clique com o botão direito no canal desejado e selecione **Configurações do Canal**.
3. No menu lateral, selecione Integrações e, em seguida, clique em **Webhooks**.
4. Clique em **Novo Webhook**, dê um nome ao webhook (por exemplo, "GitHub Bot"), escolha o canal e clique em **Copiar URL do Webhook**. Essa URL será usada mais tarde.

## Passo 2: Adicionar o Webhook como Segredo no GitHub

Para manter suas credenciais seguras, vamos armazenar o ID e o Token do webhook como segredos no GitHub.

1. No repositório do GitHub, vá até as Configurações.
2. No menu lateral, clique em **Secrets and variables** > **Actions**.
3. Clique em **Novo segredo** e adicione dois segredos:
   - Nome: `DISCORD_WEBHOOK_ID`
     - **Valor**: Extraia a parte numérica do URL do webhook, por exemplo, `123456789`.
   - Nome: `DISCORD_WEBHOOK_TOKEN`
     - Valor: Extraia a parte alfanumérica após o ID no URL, por exemplo, `P85V9JQxwH1qpoxxDj4G8lvG3OI34p0SIiCnwKXTsGj`.

## Passo 3: Criar a GitHub Action

Agora que o webhook está configurado, podemos criar uma GitHub Action que enviará notificações ao Discord quando determinados eventos ocorrerem. A seguir está um exemplo de arquivo YAML para a ação:

```yml
name: notify

on:
  pull_request:
    types: [opened, closed]
    branches:
      - master
  push:
    branches:
      - master

jobs:
  notify:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Send message for pull request opened
        if: github.event_name == 'pull_request' && github.event.action == 'opened'
        uses: appleboy/discord-action@master
        with:
          webhook_id: ${{ secrets.DISCORD_WEBHOOK_ID }}
          webhook_token: ${{ secrets.DISCORD_WEBHOOK_TOKEN }}
          color: "#48f442"
          username: "The Bot"
          message: |
            🎉 Novo Pull request aberto!

            **${{ github.event.pull_request.title }}**

            ${{ github.event.pull_request.body }}

            [Repositório](${{
              github.event.repository.html_url
            }})
              
            [Pull Request](${{
              github.event.pull_request.html_url
            }})

      - name: Send message for merge to master
        if: github.event_name == 'pull_request' && github.event.action == 'closed' && github.event.pull_request.merged == true
        uses: appleboy/discord-action@master
        with:
          webhook_id: ${{ secrets.DISCORD_WEBHOOK_ID }}
          webhook_token: ${{ secrets.DISCORD_WEBHOOK_TOKEN }}
          color: "#48f442"
          username: "The Bot"
          message: |
            🚀 Pull request mesclado na master!

            **${{ github.event.pull_request.title }}**

            Autor: ${{ github.event.pull_request.user.login }}

            [Repositório](${{
              github.event.repository.html_url
            }})

            [Pull Request](${{
              github.event.pull_request.html_url
            }})
```
## Como Funciona?

1. Definição de Eventos (`on`): A ação é disparada quando um Pull Request é aberto ou fechado, e também quando há um push para a branch `master`.

2. Job de Notificação:
  - Se um PR for aberto, a ação envia uma mensagem ao Discord usando a `discord-action` com detalhes sobre o PR.
  - Se um PR for fechado e mesclado, outra mensagem é enviada, indicando que o PR foi integrado à branch `master`.
3. Parâmetros da Mensagem:
  - `webhook_id` e `webhook_token` utilizam os segredos que você configurou no GitHub.
  O `username` define o nome do bot que aparecerá no Discord.
  - A `message` contém o conteúdo da notificação, formatado com detalhes do PR.

## Passo 4: Testar a Integração

Após configurar a ação e realizar um push no repositório, você verá as notificações no canal do Discord especificado. Teste abrindo um PR e mesclando-o para verificar se as mensagens estão sendo enviadas corretamente.

## Conclusão

Essa integração entre GitHub e Discord permite que sua equipe receba atualizações em tempo real diretamente no Discord, mantendo todos informados sobre o progresso dos Pull Requests. Esse fluxo de trabalho pode ser ajustado conforme necessário, permitindo notificações para outros eventos do GitHub ou até mesmo enviando mensagens personalizadas com base nos dados do repositório.

--- 

Se tiver dúvidas ou quiser trocar ideias sobre desenvolvimento, fique à vontade para me contatar no <a href="https://www.linkedin.com/in/gabrielcaiana/" target="_blank">LinkedIn</a> ou no <a href="http://github.com/gabrielcaiana" target="_blank">GitHub</a>. Será um prazer continuar a conversa!

