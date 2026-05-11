# Builder de Descricao da GGMAX

Este projeto e um builder local/estatico para editar, comparar e validar descricoes de anuncio da GGMAX em tempo real.

## Regra de trabalho

Antes de alterar o projeto, leia este README para entender a estrutura atual, os pontos seguros de edicao e as decisoes ja tomadas. Depois de qualquer mudanca estrutural, funcional ou de fluxo, atualize este README na mesma entrega.

## Estrutura atual

- `index.html`: arquivo unico do app. Contem o HTML da replica visual, CSS extraido da GGMAX, estilos do editor flutuante e JavaScript do builder.
- `README.md`: mapa do projeto, regras de manutencao, historico e instrucoes de hospedagem.

## Pontos importantes

- A visualizacao principal deve continuar replicando a descricao real da GGMAX.
- Nao alterar a estrutura visual da descricao renderizada, especialmente os blocos com classes `hun-section-blog-detail`, `title-announcement`, `single-post`, `description-container` e `hun-content-default`.
- As ferramentas do builder devem ficar no painel flutuante ou em camadas auxiliares que nao cubram a descricao real.
- O tema claro/escuro atual deve continuar funcionando pelo mecanismo de classe `dark` no `body`.
- O texto-base da descricao fica em `DEFAULT_TEXT` e tambem aparece inicialmente nos elementos `previewA` e `previewB`.

## Funcionalidades existentes

- Edicao em tempo real das versoes A e B.
- Comparacao lado a lado em telas grandes.
- Alternancia entre tema claro e escuro.
- Menu flutuante do builder com paineis separados para editar, visualizar mobile, revisar sugestoes, estilizar texto, inserir emojis/simbolos e salvar progresso.
- Switch compacto para alternar a versao A/B em edicao.
- Copia entre versoes A e B.
- Download do texto ativo em `.txt`.
- Salvamento automatico no `localStorage` do navegador.

## Funcionalidades adicionadas em 2026-04-27

- Visualizador mobile dentro do painel do builder, com presets de largura e zoom iniciando em 50% sobre uma proporcao de smartphone real. Ele nao substitui nem altera a visualizacao real da GGMAX.
- Diagnostico comercial/textual com checagens de seguranca, prazo, garantia, chamada para chat, precos e pre-requisitos.
- Snippets rapidos para inserir argumentos de venda e botao de correcao de termos comuns.
- Conversor de texto para estilos Unicode: negrito, italico, negrito italico, sem serifa, monoespacado e largura cheia. O editor tambem possui botoes rapidos de negrito/italico perto do textarea.
- O editor de texto acompanha o tema claro/escuro da previa e tem botao `Aa` para remover estilos Unicode da selecao.
- Ao aplicar um estilo Unicode sobre outro, o builder normaliza a selecao antes de converter, permitindo trocar monoespacado por negrito, italico etc.
- Catalogo de emojis, simbolos e separadores para inserir no cursor ou copiar.
- Catalogo de emojis ampliado com categorias: GGMAX, Genshin, Servicos, Confianca, Divisores, Teclado e Numeros.
- O menu flutuante fecha o painel aberto quando acionado novamente e tambem fecha ao clicar fora do drawer/menu.
- O visualizador mobile usa controle segmentado para escolher texto ativo/A/B e possui moldura interna para aproximar a leitura do layout inspecionado em mobile.
- No desktop, o drawer do builder usa mais altura da tela para evitar cortes no visualizador mobile.
- A aplicacao de estilos Unicode preserva a posicao vertical, horizontal e selecao do textarea.
- Os botoes de acao usam feedback azul temporario ao clicar, sem ficarem marcados como ativos permanentemente.
- A navegacao de categorias de emojis fica em uma faixa horizontal responsiva.
- A faixa de categorias de emojis aceita arrastar/deslizar lateralmente com mouse ou touch.
- O visualizador mobile aceita arrastar/deslizar dentro da tela do aparelho para rolar a descricao.
- O menu flutuante fica oculto enquanto um painel esta aberto para evitar sobreposicao com o drawer.
- O botao circular de menu tambem fica oculto enquanto o drawer esta aberto para nao cobrir a previa.
- Salvamento manual com historico por navegador, restauracao, copia e exclusao de snapshots.
- Botao para copiar texto ativo.
- A URL com `#builder` abre o painel automaticamente, util para validacao e compartilhamento interno.
- Tambem e possivel abrir direto um painel com hashes como `#builder-mobile`, `#builder-symbols`, `#builder-style`, `#builder-advisor` e `#builder-history`.

## Como as sugestoes funcionam

- O painel Sugestoes roda apenas no navegador, sem chamada a IA, servidor ou banco externo.
- Ele analisa o texto ativo usando regras locais e palavras-chave para identificar presenca de seguranca/manual, prazo, garantia, chamada para chat, precos e pre-requisitos.
- O botao de correcao aplica substituicoes comuns cadastradas em `COMMON_FIXES`, como `Mondstat` para `Mondstadt` e termos sem acento.
- As sugestoes sao um checklist de qualidade comercial/textual. Elas nao substituem revisao humana antes de publicar.

## Como o salvamento funciona

- O autosave grava o estado atual no `localStorage` sempre que o usuario edita texto ou muda controles do builder.
- O botao `Salvar progresso` cria um snapshot manual nomeado no historico local do navegador.
- Cada usuario/equipe tem seu proprio historico no navegador que esta usando. Nao existe sincronizacao entre pessoas.
- O historico permite restaurar, copiar ou excluir snapshots.

## Uso local

- Abrir direto: `index.html` funciona como arquivo estatico.
- Servidor local opcional: `python -m http.server 8765 --bind 127.0.0.1` e acessar `http://127.0.0.1:8765/`.
- Abrir direto no builder: `http://127.0.0.1:8765/#builder`.

## Persistencia

- O autosave usa a chave `ggmax-description-live-editor-v3-site-faithful`.
- O historico manual usa `ggmax-description-live-editor-v3-site-faithful-manual-history`.
- Os dados ficam no navegador de cada pessoa. Nao ha banco de dados nem sincronizacao entre usuarios.

## Hospedagem

Como o projeto e estatico, as opcoes gratuitas recomendadas sao:

- Cloudflare Pages: melhor equilibrio para equipe, Git integrado, previews e plano gratuito forte para sites estaticos. Fonte: https://pages.cloudflare.com/
- GitHub Pages: melhor se o projeto ficar em repositorio publico no GitHub e a equipe ja usa GitHub. Fonte: https://docs.github.com/pages
- Netlify: mais rapido para publicar sem configurar nada usando drag and drop, e tambem permite deploy por Git. Fonte: https://docs.netlify.com/site-deploys/create-deploys/

Recomendacao pratica: usar Cloudflare Pages conectado a um repositorio GitHub. Como este projeto nao tem build, a configuracao de deploy deve deixar o comando de build vazio e publicar a raiz do projeto.

## Historico

- 2026-04-27: README inicial criado para servir como fonte de consulta antes de evoluir o builder.
- 2026-04-27: Builder ampliado com visualizador mobile, diagnostico, estilos Unicode, catalogo de simbolos, copia ativa e historico manual por navegador.
- 2026-04-27: Builder reorganizado em menu flutuante com paineis, switch A/B compacto, editor de estilos reforcado e catalogo de emojis categorizado.
- 2026-04-27: Ajustes de usabilidade no menu, fechamento por clique externo, preservacao de scroll ao estilizar texto, melhoria de contraste, visualizador mobile mais fiel e simbolos fantasiosos.
- 2026-04-27: Refinos de responsividade nas categorias de simbolos, proporcao real de celular no mobile, feedback temporario em botoes e abertura direta do menu apos fechar painel.
- 2026-04-27: Corrigida sobreposicao do menu e adicionado drag/touch no visualizador mobile e nas categorias de emojis.
- 2026-04-27: Ajuste final do botao de menu oculto durante drawer aberto, textarea seguindo tema e normalizacao/troca de estilos Unicode.
- 2026-05-11: Botao de menu movido para o topo central da pagina; menu (launcher) agora abre suspenso para baixo. Corrigido bug critico onde clicar nas categorias de emojis nao funcionava (setPointerCapture no container desviava o evento click do botao filho, quebrando a delegacao de eventos). enableDragScroll refatorado para usar listeners no document em vez de captura de ponteiro. CSS morto (bloco ::before duplicado) removido. padding-top da pagina aumentado para 90px para evitar sobreposicao do conteudo com o botao fixo no topo.
- 2026-05-11: Dois novos grupos adicionados ao catalogo de simbolos, ambos estritamente da categoria Unicode So (Other Symbol): Setas (76 setas Unicode — hook, curva, dupla, tripla, pontilhada, branca, harpoon, etc.) e Marcas (30 marcas tipograficas e tecnicas — copyright, trademark, service mark, numero, grau, celsius, fahrenheit, diametro, telefone, estimado, etc.).
