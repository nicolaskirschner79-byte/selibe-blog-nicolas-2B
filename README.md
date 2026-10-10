# Universo Thalita

Blog editorial independente sobre **Thalita Rebouças**. A autora ocupa o centro da identidade visual: nome em grande escala, universo de papel, temas das obras, monograma, percurso por capítulos e conexões entre literatura e adaptações. O projeto não representa a autora ou suas editoras.

## O que está implementado

- 29 páginas pré-geradas, com 13 obras, seis artigos completos, seis eventos e quatro adaptações.
- Cinco ilustrações originais criadas com IA, inspecionadas e entregues em PNG mestre, AVIF e WebP responsivos; entrada em ameixa com páginas, música e cinema.
- Mapa literário em perspectiva CSS 3D: cinco temas documentados, conexões SVG, seleção por clique ou teclado, apresentação com fonte e marcador pessoal.
- Livro procedural em Three.js: girar por botões ou arraste, abrir e fechar capa/páginas, materiais de papel, lombada, marca-página e luz. A entrada explora Fala sério, mãe! com uma representação editorial própria.
- Símbolos originais nas capas conforme os temas das fichas; navegação por capítulos, seção da autora e obras adaptadas para as telas.
- Busca em título, resumo e corpo dos artigos; filtros por coleção/categoria e tema/tag; paginação e ordenação.
- Lista pessoal de livros e artigos no navegador; tratamento de armazenamento bloqueado.
- Sugestões de leitura por temas, com regra determinística e motivo visível.
- Revelações suaves durante a rolagem em títulos, textos, imagens, fichas e rodapé; cartões em cascata, ilustrações com recorte animado e capas com entrada em perspectiva.
- Controles de movimento, preferência reduzida, navegação móvel, leitura estimada, sumário, compartilhamento e progresso de leitura.
- RSS, sitemap, metadados, JSON-LD, 404, referências e política editorial.

A biblioteca é uma seleção pesquisada. As capas são representações editoriais originais; os catálogos oficiais estão nas fichas. Não foram inventados retratos, cenas históricas, entrevistas, vendas ou testemunhos.

## Executar

Requer Node.js 22 ou superior e npm. O lockfile acompanha o projeto.

1. Instale as dependências com **npm ci**.
2. Gere as páginas com **npm run build**.
3. Execute as verificações com **npm run check**.
4. Em seu computador, abra a prévia com **npm run preview** e acesse http://localhost:8080.

A prévia usa um servidor HTTP simples, sem coleta de dados ou painel. Depois de editar conteúdo ou código, rode o build e atualize o navegador. No ambiente gerenciado de Sites, utilize o supervisor oficial quando o controle de navegador estiver disponível; não inicie servidores paralelos.

## Organização

| Pasta | Conteúdo |
| --- | --- |
| src/ | Interface, estilos, lógica pura, validação e modelo 3D |
| scripts/ | Geração estática, verificações, otimização de imagens e servidor local |
| data/content.json | Fontes, perfil, obras, eventos, adaptações e artigos |
| data/evidence.json | Registro de 30 afirmações verificadas |
| data/assets.json | Origem, prompts, créditos e uso de cada arte |
| data/publication.json | Instante real de criação editorial e audiência inicial |
| assets/masters/ | Cinco PNGs originais de 1672 px de largura |
| assets/images/ | Variantes AVIF/WebP de 800 e 1600 px |
| assets/fonts.css | Duas famílias, auto-hospedadas e com fallback |
| licenses/ | OFL das fontes, MIT do Three.js e referência da licença GSAP |
| docs/ | Design, edição, publicação e limites de verificação |
| qa/ | Rotas e relatório automatizado |
| dist/ | Saída de produção, gerada pelo build |

## Arquitetura

HTML pré-gerado, CSS e módulos JavaScript, com Three.js e GSAP/ScrollTrigger. A orientação de Sites para interações locais favorece HTML/JS estático; por isso o projeto usa um gerador pequeno em vez da combinação Astro/TypeScript/Pagefind sugerida no briefing. O conteúdo chega inteiro em HTML. O índice de busca é um JSON local, sem serviços ou credenciais.

src/motion.mjs coordena as entradas com um único IntersectionObserver, Web Animations nativas e GSAP como alternativa. Os elementos aparecem uma vez ao entrar na área visível; imagens, títulos e texto têm ritmos próprios. Pausa e foco revelam o conteúdo imediatamente. Não há rolagem forçada ou alteração da ordem de leitura. A suíte inclui 30 grupos de verificação, com entrega de interseções e ciclo das animações simulados em Happy DOM.

src/atlas.mjs usa os temas publicados para conectar as 13 obras; mostra até cinco livros por vez, com links HTML para todas as obras do tema. Animações e resposta ao ponteiro suspendem fora da tela e respeitam a pausa. CSS Scroll Timeline e View Transitions acrescentam profundidade na arte, progresso por capítulos e continuidade entre capas quando o navegador oferece suporte; os demais mantêm navegação e leitura normais.

Three.js carrega apenas após ação do leitor, com um contexto WebGL por vez. A ilustração de entrada aparece antes da interação. O modelo substitui a arte quando solicitado; a chamada para a biblioteca segue sendo um link HTML. As fichas têm o mesmo modelo em um modal e mantêm título, apresentação e link fora do canvas.

## Verificação

O relatório em qa/report.json discrimina testes e medidas. Happy DOM verifica eventos e estados da interface em Node, sem renderização gráfica. **Não equivale a teste em Chrome/Safari/Firefox.** A revisão visual de layouts, a renderização WebGL em GPU e Core Web Vitals não foram medidas neste ambiente. Consulte docs/verificacao.md.

## Atualização e publicação

Siga docs/edicao.md e docs/publicacao.md. A versão inicial é privada em Sites; os metadados excluem a indexação pública. SITE_URL altera o domínio canônico; SITE_PUBLIC=1 libera metadados de indexação somente quando a audiência tiver sido alterada expressamente.

O projeto inclui configuração de build estático para Vercel. Isso não implica uma implantação na Vercel ou a criação de um repositório no GitHub.

