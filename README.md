# Builder de Descrição da GGMAX

Este projeto e um builder local/estático para editar, comparar e validar descrições de anúncio da GGMAX em tempo real.

## Regra de trabalho
Antes de alterar o projeto, leia este README para entender a estrutura atual, os pontos seguros de edição e as decisões já tomadas. Depois de qualquer mudança estrutural, funcional ou de fluxo, atualize este README na mesma entrega.

## Estrutura atual
- `index.html`: arquivo único do app. Contém o HTML da réplica visual, CSS extraído da GGMAX, estilos do editor flutuante e JavaScript do builder.
- `README.md`: mapa do projeto, regras de manutenção, histórico e instruções de hospedagem.
- `favicon.ico`: ícone do site.

## Pontos importantes
- A visualização principal deve continuar replicando a descrição real da GGMAX.
- Não alterar a estrutura visual da descrição renderizada, especialmente os blocos com classes `hun-section-blog-detail`, `title-announcement`, `single-post`, `description-container` e `hun-content-default`.
- As ferramentas do builder devem ficar no painel flutuante ou em camadas auxiliares que não cubram a descrição real.
- O tema claro/escuro atual deve continuar funcionando pelo mecanismo de classe `dark` no `body`.
- O texto-base da descrição fica em `DEFAULT_TEXT` e também aparece inicialmente nos elementos `previewA` e `previewB`.

## Funcionalidades existentes
- Edição em tempo real das versões A e B.
- Comparação lado a lado em telas grandes.
- Alternância entre tema claro e escuro.
- Menu flutuante do builder com painéis separados para editar, visualizar mobile, revisar sugestões, estilizar texto, inserir emojis/símbolos e salvar progresso.
- Switch compacto para alternar a versão A/B em edição.
- Copia entre versões A e B.
- Download do texto ativo em `.txt`.
- Salvamento automático no `localStorage` do navegador.

## Funcionalidades adicionadas em 2026-04-27
- Visualizador mobile dentro do painel do builder, com presets de largura e zoom iniciando em 50% sobre uma proporção de smartphone real. Ele não substitui nem altera a visualização real da GGMAX.
- Diagnostico comercial/textual com checagens de segurança, prazo, garantia, chamada para chat, preços e pré-requisitos.
- Snippets rápidos para inserir argumentos de venda e botão de correção de termos comuns.
- Conversor de texto para estilos Unicode: negrito, itálico, negrito itálico, sem serifa, monoespacado e largura cheia. O editor também possui botões rápidos de negrito/itálico perto do textarea.
- O editor de texto acompanha o tema claro/escuro da previa e tem botão `Aa` para remover estilos Unicode da seleção.
- Ao aplicar um estilo Unicode sobre outro, o builder normaliza a seleção antes de converter, permitindo trocar monoespacado por negrito, itálico etc.
- Catálogo de emojis, símbolos e separadores para inserir no cursor ou copiar.
- Catálogo de emojis ampliado com categorias: GGMAX, Genshin, Serviços, Confiança, Divisores, Teclado e Números.
- O menu flutuante fecha o painel aberto quando acionado novamente e também fecha ao clicar fora do drawer/menu.
- O visualizador mobile usa controle segmentado para escolher texto ativo/A/B e possui moldura interna para aproximar a leitura do layout inspecionado em mobile.
- No desktop, o drawer do builder usa mais altura da tela para evitar cortes no visualizador mobile.
- A aplicação de estilos Unicode preserva a posição vertical, horizontal e seleção do textarea.
- Os botões de ação usam feedback azul temporário ao clicar, sem ficarem marcados como ativos permanentemente.
- A navegação de categorias de emojis fica em uma faixa horizontal responsiva.
- A faixa de categorias de emojis aceita arrastar/deslizar lateralmente com mouse ou touch.
- O visualizador mobile aceita arrastar/deslizar dentro da tela do aparelho para rolar a descrição.
- O menu flutuante fica oculto enquanto um painel está aberto para evitar sobreposição com o drawer.
- O botão circular de menu também fica oculto enquanto o drawer está aberto para não cobrir a previa.
- Salvamento manual com histórico por navegador, restauração, cópia e exclusão de snapshots.
- Botão para copiar texto ativo.
- A URL com `#builder` abre o painel automaticamente, útil para validação e compartilhamento interno.
- Também e possível abrir direto um painel com hashes como `#builder-mobile`, `#builder-symbols`, `#builder-style`, `#builder-advisor` e `#builder-history`.

## Como as sugestões funcionam
- O painel Sugestões roda apenas no navegador, sem chamada a IA, servidor ou banco externo.
- Ele analisa o texto ativo usando regras locais e palavras-chave para identificar presença de segurança/manual, prazo, garantia, chamada para chat, preços e pré-requisitos.
- O botão de correção aplica substituições comuns cadastradas em `COMMON_FIXES`, como `Mondstat` para `Mondstadt` e termos sem acento.
- As sugestões são um checklist de qualidade comercial/textual. Elas não substituem revisão humana antes de publicar.

## Como o salvamento funciona
- O autosave grava o estado atual no `localStorage` sempre que o usuario edita texto ou muda controles do builder.
- O botão `Salvar progresso` cria um snapshot manual nomeado no histórico local do navegador.
- Cada usuario/equipe tem seu próprio histórico no navegador que está usando. Não existe sincronização entre pessoas.
- O histórico permite restaurar, copiar ou excluir snapshots.

## Uso local
- Abrir direto: `index.html` funciona como arquivo estático.
- Servidor local opcional: `python -m http.server 8765 --bind 127.0.0.1` e acessar `http://127.0.0.1:8765/`.
- Abrir direto no builder: `http://127.0.0.1:8765/#builder`.

## Persistência
- O autosave usa a chave `ggmax-description-live-editor-v3-site-faithful`.
- O histórico manual usa `ggmax-description-live-editor-v3-site-faithful-manual-history`.
- Os dados ficam no navegador de cada pessoa. Não há banco de dados nem sincronização entre usuários.

## Hospedagem
Como o projeto e estático, as opções gratuitas recomendadas são:
- Cloudflare Pages: melhor equilíbrio para equipe, Git integrado, previews e plano gratuito forte para sites estáticos. Fonte: https://pages.cloudflare.com/
- GitHub Pages: melhor se o projeto ficar em repositório público no GitHub e a equipe já usa GitHub. Fonte: https://docs.github.com/pages
- Netlify: mais rápido para publicar sem configurar nada usando drag and drop, e também permite deploy por Git. Fonte: https://docs.netlify.com/site-deploys/create-deploys/
Recomendação prática: usar Cloudflare Pages conectado a um repositório GitHub. Como este projeto não tem build, a configuração de deploy deve deixar o comando de build vazio e publicar a raiz do projeto.

## Historico
- 2026-04-27: README inicial criado para servir como fonte de consulta antes de evoluir o builder.
- 2026-04-27: Builder ampliado com visualizador mobile, diagnostico, estilos Unicode, catálogo de símbolos, cópia ativa e histórico manual por navegador.
- 2026-04-27: Builder reorganizado em menu flutuante com painéis, switch A/B compacto, editor de estilos reforçado e catálogo de emojis categorizado.
- 2026-04-27: Ajustes de usabilidade no menu, fechamento por clique externo, preservação de scroll ao estilizar texto, melhoria de contraste, visualizador mobile mais fiel e símbolos fantasiosos.
- 2026-04-27: Refinos de responsividade nas categorias de símbolos, proporção real de celular no mobile, feedback temporário em botões e abertura direta do menu após fechar painel.
- 2026-04-27: Corrigida sobreposição do menu e adicionado drag/touch no visualizador mobile e nas categorias de emojis.
- 2026-04-27: Ajuste final do botão de menu oculto durante drawer aberto, textarea seguindo tema e normalização/troca de estilos Unicode.
