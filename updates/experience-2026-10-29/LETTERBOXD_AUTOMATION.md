## Integração Letterboxd automática — piloto 0.5.0

29/10/2026. Implementada uma fila persistente de sincronização pela sessão normal do site no WebView do Android. É um piloto técnico: os testes usam respostas simuladas; login, importação e escrita reais na conta pedrovicq ainda não foram validados no Chromecast.

### Uso

Após instalar a atualização, abrir Ajustes → Letterboxd → Conectar Letterboxd, entrar como pedrovicq, verificar a sessão e voltar ao app. A conexão pela TV ativa a automação para aquele perfil. O login do Safari não é compartilhado. A tela permite pausar e tentar novamente, além de mostrar o estado de cada filme.

Confirmar a conclusão de um filme e a nota coloca o registro na fila. Ao retornar da reprodução, o app tenta registrar a data no diário, marcar como assistido e enviar a nota de 0,5 a 5 estrelas. Escolher não avaliar preserva uma nota anterior. O estado “sincronizado” exige releitura do diário e da relação assistido/nota.

O app consulta antes de gravar, persiste a intenção antes do POST e não repete uma gravação de diário cujo resultado ficou desconhecido. Registros diferentes para o mesmo filme/data não são sobrescritos. Uma resposta perdida pode deixar o item pendente de conferência. Um recibo remoto não pode confirmar duas sessões locais distintas.

### Listas e recursos

Watchlist é importada de forma aditiva para Quero ver, sem modificar a fila manual. Favoritos ganham uma fileira própria em Filmes. Remover localmente um filme importado impede sua reinclusão enquanto continuar no watchlist remoto. O app não replica exclusões remotas nem envia alterações manuais de watchlist ao Letterboxd. A importação só é aplicada após todas as páginas e identificadores serem conferidos.

A sincronização começa com o app aberto, fora do player e da seleção de fontes; não exige servidor, serviço pago nem computador ligado. Um WebView temporário é destruído ao entrar na reprodução ou sair do primeiro plano. A importação completa é consultada a cada seis horas de uso, com metadados pequenos reaproveitados por até sete dias, limite de 2.100 filmes e importação máxima de 2.000 itens. Não há serviço permanente nem navegador embutido adicional.

### Validação e limites

110 testes Android aprovados, zero falhas/erros/ignorados, incluindo 11 casos do motor de sincronização e persistência/importação. Três scripts JavaScript aprovados: organização no celular, correção de episódios e adaptador Letterboxd com transporte simulado. Isso não comprova aceitação dos endpoints pela sessão real.

A API pública oficial continua restrita para projetos pessoais. Este piloto usa a sessão normal do site, não credenciais de API extraídas. Se o site exigir login/verificação ou recusar acesso, o app pausa e informa o motivo. Não há bypass de proteção do site. A autenticação e os cookies permanecem no WebView; não são enviados ao servidor do QR, ao GitHub ou ao chat.

Amigos no contexto do filme continuam usando o painel e a leitura já implementados; esta rodada não adiciona sincronização automática completa do feed social. Também não conclui todos os itens anteriores de produto. Publicação de fonte no PR #1 é separada da distribuição do APK. O canal público continua 0.4.1 até um novo APK ser publicado naquele canal.

