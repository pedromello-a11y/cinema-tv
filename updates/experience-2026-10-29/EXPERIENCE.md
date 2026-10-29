# Cinema TV — organização e continuidade

29/10/2026. Iteração de experiência sobre o código da versão 0.4.1. Ainda não é uma nova versão distribuída em APK. A prioridade atual é fechar sistema, opções e fluxos; o refinamento visual vem depois.

## O que muda

Antes, o Início misturava listas pessoais com catálogos gerais, Filmes e Séries tinham pouca distinção entre organização e descoberta, e a fila precisava ser movida um passo por vez. Agora:

| Área | Organização e comportamento |
| --- | --- |
| Início | Continuar assistindo mistura filmes e episódios. Abaixo ficam pendências de séries e escolhas pessoais. Catálogos gerais passam para Descobrir. |
| Filmes → Quero ver | Continuação, Próximos da fila em ordem manual e demais filmes salvos. Um filme não se repete entre essas fileiras. A fila persistida conserva sua ordem mesmo quando um item aparece em Continuar. |
| Filmes → Descobrir | Catálogos de filmes dos add-ons, preservando sua identidade. O app não transforma um catálogo popular em ranking personalizado. |
| Filmes → Histórico | Filmes concluídos, mais recentes primeiro, sem episódios nem duplicação por revisualização. Ações para assistir novamente e organizar uma nova intenção de rever. |
| Séries → Acompanhando | Em andamento, episódios pendentes, em dia, estreias acompanhadas, episódios a confirmar, pausadas e concluídas. Fileiras sem títulos não aparecem. |
| Séries → Quero ver | Séries guardadas para depois, separadas do acompanhamento ativo. Salvar e acompanhar são intenções distintas. |
| Séries → Descobrir | Catálogos de séries. |
| Agenda | Calendário mensal já existente das séries acompanhadas. Data de lançamento não garante fonte reproduzível. |
| Busca e Ajustes | Acessos próprios no menu principal, sem uma Biblioteca genérica duplicando Filmes e Séries. |

Cada seção preserva a capa e a fileira selecionadas. O menu principal continua oculto e sobreposto ao abrir; navegar lateralmente não desloca a fileira na vertical. As mensagens de lista vazia oferecem a ação apropriada, diferenciando uma lista pessoal vazia de ausência de catálogo.

## Controle remoto

- Cima na primeira fileira: ações do título. Cima novamente: seletores da seção.
- Esquerda/direita nos seletores: escolher; OK: entrar. Baixo: ações do título.
- Esquerda na primeira capa ou em Assistir, ou Voltar: abrir menu principal. Direita: retornar ao conteúdo.
- Organizar: salvar, remover, entrar/sair da fila ou alterar acompanhamento.
- Mover na fila: escolher posição com esquerda/direita ou ir ao início/fim; Salvar confirma, Cancelar e Voltar descartam a prévia. A sequência de foco é explícita.
- Ao focar Organizar, Detalhes ou Amigos, aparece uma descrição curta da ação. Duração não se repete no bloco de informações.

## Pelo celular

O painel local passa a ter Filmes, Séries, Histórico e Ajustes. Permite selecionar qualquer posição da fila de uma vez, acompanhar uma série já salva e guardar um filme assistido para rever. As ações usam as mesmas preferências persistidas na TV.

Consultas periódicas sem mudança não remontam as listas nem destroem o foco. O painel não atualiza a lista enquanto o seletor de posição está aberto. O estado enviado contém resumos de acompanhamento, sem transferir o catálogo completo de episódios a cada consulta.

Esta conexão ainda exige a mesma rede e a central aberta na TV. A paridade completa de todas as preferências e correções de progresso permanece pendente.

## Validação

84 testes automatizados passaram, além de 8 cenários de contrato DOM do painel móvel. O relatório detalhado acompanha o patch. Testes cobrem separação pessoal/descoberta, histórico, agrupamento de séries, não duplicação de títulos, persistência da ordem após reiniciar o DataStore e navegação por teclas. Capturas são da interface nativa renderizada em Robolectric com dados de teste, não do Chromecast de Pedro.

O script `tools/check-personal-phone.cjs` verifica o contrato DOM do painel: seções, listas distintas, cancelamento, movimento, acompanhamento, rever, foco após atualização e erro sem perda do estado. Executar com Node e `jsdom@26.1.0` disponível em `NODE_PATH`. Essa dependência é apenas de teste e não entra no APK. Não equivale a validação física no Safari.

## Sequência de evolução antes do acabamento visual

1. Completar correções de progresso de séries e histórico, com desfazer, incluindo ações equivalentes no celular.
2. Completar preferências de reprodução/fontes nas duas interfaces e recuperação da biblioteca.
3. Implementar escolhas por tempo disponível e coleções com fontes reais; uma lista ordenada por nota não será chamada de Top 250 IMDb oficial.
4. Resolver escrita e importação Letterboxd. O piloto publicado tem conexão/leitura; login real, leitura ao vivo e envio automático ainda não estão validados. O envio automático de avaliações e importação de watchlist/favoritos não estão implementados.
5. Consolidar um APK para teste de ponta a ponta no Chromecast HD: atualização preservando dados, reprodução/retomada, foco, espaço e abertura. Depois, finalizar tipografia, iconografia e consistência visual das telas herdadas.

Nenhum novo canal, assinatura, dependência nativa ou serviço em segundo plano foi acrescentado por esta iteração. O feed público continua apontando para o APK 0.4.1 publicado.
