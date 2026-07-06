---
title: Como Atualizar seu Blog (Git Add, Commit e Push) Direto pelo Celular usando Termux e Tmux
date: 2026-07-06T12:38:00-03:00
tags:
  - "#Tutorial"
  - Git
  - Atualizando
LocalPublicado: Blog
draft: false
---
Se você escreve no seu blog pelo celular (seja usando o Obsidian Mobile ou outro editor) e quer uma forma rápida, leve e independente de enviar suas alterações para o GitHub, o terminal é o seu melhor amigo.
Usando o **Termux** (emulador de terminal para Android) e o **tmux** (gerenciador de sessões), você consegue fazer todo o ciclo do Git (`add`, `commit` e `push`) em segundos.

## 🛠️ O que você vai precisar (Preparação Inicial)
Caso ainda não tenha o `tmux` instalado no seu Termux, abra o aplicativo no celular e instale com o comando:

`bash
pkg install tmux
`

## 🚀 Passo a Passo para Publicar seu Post

### 1. Criar ou Acessar uma Sessão Persistente no Tmux
O `tmux` garante que, se a sua internet oscilar ou você fechar o aplicativo sem querer, o comando não seja interrompido.
Abra o Termux e crie uma sessão chamada "blog":

`bash
tmux new -s blog
`

_(Se você já criou essa sessão antes, basta se reconectar a ela usando: `tmux a -t blog`)_

### 2. Navegar até a Raiz do seu Blog
Entre na pasta onde o repositório Git do seu blog está configurado:

`bash
cd /DATA/AppData/observatorio
`

### 3. Verificar as Alterações (Opcional)
Para garantir que apenas os seus novos posts da pasta `content/posts/` vão subir (e validar que nossa limpeza do `.gitignore` deu certo!), rode

`bash
git status
`
Você verá seus novos arquivos listados em vermelho.

### 4. Adicionar os Novos Arquivos
Para preparar todos os novos posts e imagens para o envio:

`bash
git add .
`

### 5. Criar o Commit (A Mensagem de Publicação)
Gere o ponto de salvamento local com uma mensagem de sua preferência:

`bash
git commit -m "Post: novo texto publicado via Termux"
`

### 6. Enviar para o GitHub (O Push Final)
Agora, envie tudo para o seu repositório remoto para disparar o deploy (seja no Cloudflare Pages ou GitHub Pages):

`bash
git push
`

## 💡 Dica de Ouro: Criando um Atalho Automático (Alias)

Ficar digitando todos esses comandos no teclado do celular pode ser chato. Você pode criar um **único comando personalizado** que faz tudo de uma vez só.

1. Abra o arquivo de configuração do seu terminal
	   micro ~/.bashrc
2. Adicione a seguinte linha no final do arquivo:
	   alias publicar_blog="cd /DATA/AppData/observatorio && git add . && git commit -m 'Update via Termux' && git push"
3. Salve e feche. Recarregue o terminal com `source ~/.bashrc`.

Pronto! Da próxima vez que você quiser publicar um post da sua estrutura, basta abrir o Termux e digitar apenas:

`bash
publicar_blog
`

O terminal vai entrar na pasta, dar o add, fazer o commit e realizar o push de forma 100% automática!
