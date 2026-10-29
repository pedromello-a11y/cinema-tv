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

Esta conexão ainda exige a mesma rede e a central aberta na TV. A paridade completa de todas as preferências permanece pendente.

## Correção de episódios

Na TV: Séries → selecione uma série acompanhada → Organizar (+) → Corrigir episódios. No painel do celular: Séries → Corrigir episódios. O acompanhamento precisa ter carregado o catálogo da série; a tela informa quando os episódios ainda não estão disponíveis.

- Escolher temporada e episódio, marcar visto ou não visto, usar Já vi até aqui ou Marcar temporada.
- Conferir a quantidade e os episódios atingidos antes de confirmar; Cancelar e Voltar descartam a prévia.
- Já vi até aqui inclui o episódio escolhido e temporadas anteriores. As marcações excluem episódios futuros, sem data confirmada, especiais e os que já estão vistos.
- Desfazer restaura as datas do histórico e a posição parcial anteriores, preservando episódios fora da correção. Se houver reprodução ou alteração posterior nos mesmos episódios, o app recusa o desfazer antigo.
- A última correção pode ser desfeita durante a sessão, inclusive ao alternar TV e celular. Outra correção substitui essa possibilidade; reiniciar o app a encerra, preservando as alterações já salvas.
- Uma prévia desatualizada é recusada antes da gravação. O painel recarrega o progresso para nova conferência.

A gravação e a restauração usam o repositório do player e o perfil original. O acompanhamento e as pendências leem esse mesmo histórico; as datas da Agenda continuam vindo do catálogo. O catálogo de episódios só é enviado ao painel quando o editor está aberto. Corrigir episódios não muda a intenção de acompanhar nem a fila de filmes.

Não foi acrescentado serviço em segundo plano nem outro cache de catálogo. O desfazer guarda uma única correção em memória. A restauração em provedores externos não foi testada; esta etapa não implementa escrita Letterboxd.

## Validação

98 testes automatizados passaram na rodada atual, sem falhas ou testes ignorados, além dos dois scripts de contrato DOM do painel móvel. Testes cobrem separação pessoal/descoberta, histórico, agrupamento de séries, não duplicação de títulos, persistência da ordem após reiniciar o DataStore e navegação por teclas. Para episódios: seleção em lote, conflitos, confirmação única, restauração exata de datas e posição parcial, isolamento de perfil, prévia/cancelamento e foco em episódios futuros. Capturas são da interface nativa renderizada em Robolectric com dados de teste, não do Chromecast de Pedro.

O script `tools/check-personal-phone.cjs` verifica o contrato DOM do painel: seções, listas distintas, cancelamento, movimento, acompanhamento, rever, foco após atualização e erro sem perda do estado. Executar com Node e `jsdom@26.1.0` disponível em `NODE_PATH`. Essa dependência é apenas de teste e não entra no APK. Não equivale a validação física no Safari.

O script `tools/check-personal-episodes.cjs` acrescenta abertura/fechamento do editor, seleção, episódio futuro bloqueado, prévia/cancelamento, confirmação sem duplicação, desfazer e atualização após conflito. O relatório `validacao-progresso-series.json` acompanha o segundo patch, aplicado depois de `experiencia-sobre-0.4.1.patch`.

## Sequência de evolução antes do acabamento visual

1. Ampliar os acessos à correção de episódios nas telas herdadas e completar correções de histórico de filmes. A edição de séries acompanhadas com prévia e desfazer está implementada na TV e no painel.
2. Completar preferências de reprodução/fontes nas duas interfaces e recuperação da biblioteca.
3. Implementar escolhas por tempo disponível e coleções com fontes reais; uma lista ordenada por nota não será chamada de Top 250 IMDb oficial.
4. Resolver escrita e importação Letterboxd. O piloto publicado tem conexão/leitura; login real, leitura ao vivo e envio automático ainda não estão validados. O envio automático de avaliações e importação de watchlist/favoritos não estão implementados.
5. Consolidar um APK para teste de ponta a ponta no Chromecast HD: atualização preservando dados, reprodução/retomada, foco, espaço e abertura. Depois, finalizar tipografia, iconografia e consistência visual das telas herdadas.

Nenhum novo canal, assinatura, dependência nativa ou serviço em segundo plano foi acrescentado por esta iteração. O feed público continua apontando para o APK 0.4.1 publicado.
