# Cinema TV — experiência e automação Letterboxd 0.5.0

Este diretório contém três incrementos sobre a base 0.4.1. O terceiro implementa o motor de sincronização Letterboxd e incrementa para versionCode 6 / 0.5.0-pilot. A versão é um piloto: os testes foram automatizados com dados simulados; acesso autenticado e escrita reais na conta ainda dependem de validação no Chromecast.

## Reconstruir a fonte correspondente

1. Obtenha Nuvio-Pedro-codigo-0.4.1.zip na release v0.4.1 e execute preparar-codigo.py para reconstruir a árvore 0.4.1 sobre a base fixa 9f17e8bf4abc799dc8c832d2894a8b3b166e4353.
2. Aplique experiencia-sobre-0.4.1.patch.
3. Aplique progresso-de-series.patch.
4. Aplique letterboxd-automatico.patch.
5. Consulte docs/EXPERIENCE.md e docs/LETTERBOXD_AUTOMATION.md.

A chave de assinatura não é incluída. Os patches foram aplicados a suas bases e comparados aos arquivos resultantes. A distribuição continua sob GPL-3.0 e preserva as licenças dos componentes.

## Resultado

Organização pessoal, histórico, fila manual e correção de episódios na TV e no celular; automação de assistidos/diário/notas após login normal na TV; importação aditiva de watchlist e favoritos. A fila de envios é persistente e uma tentativa de diário com resultado desconhecido não é repetida cegamente. A importação não envia edições manuais de watchlist e a nova rodada não automatiza o feed social completo.

110 testes Android passaram sem falhas, erros ou ignorados; três verificações JavaScript passaram. APK ARM32 0.5.0: 71.849.171 bytes; SHA-256 6f8dec774c044206285ffae73e18da83ba957ba4fc15101bad63754e2549c818. Identidade, integridade, arquitetura e mesma assinatura da 0.4.1 conferidas. Sem validação física de atualização, reprodução, login ou escrita Letterboxd.

O APK piloto é entregue separadamente. Esta publicação de fonte não altera latest.json nem cria uma release: o canal público continua apontando para 0.4.1.
