# Passagem de desenvolvimento para Claude — Cinema TV de Pedro

Data: 29/10/2026. Este documento é o ponto de partida para continuar o projeto, sem reescrevê-lo.

## Estado e fonte correta

- Repositório de distribuição: https://github.com/pedromello-a11y/cinema-tv
- PR de desenvolvimento: https://github.com/pedromello-a11y/cinema-tv/pull/1
- Branch: experience/personal-sections
- Checkpoint funcional anterior a este guia: fc99ebee9bbe78875aa02acff4fd35058dbf338f.
- APK entregue: 0.5.0-pilot, versionCode 6, applicationId com.pedrovicq.cinema, armeabi-v7a (Chromecast HD).
- Arquivo Nuvio-Pedro-0.5.0-Chromecast-HD.apk: 71.849.171 bytes.
- SHA-256: 6f8dec774c044206285ffae73e18da83ba957ba4fc15101bad63754e2549c818.
- Certificado SHA-256: 8b42b203779975e6a985b13f32f6b4ce165090cfdec4e0940f5673122a386f1e.
- O canal público latest.json e a release pública continuam em 0.4.1. Entregar o APK pelo chat não publicou uma release 0.5.0 no GitHub.
- O repositório NÃO contém diretamente a árvore Android completa: contém distribuição, documentação e patches. Clonar somente main não recupera a versão entregue.

### Reconstrução A: usando apenas GitHub

1. Baixar Nuvio-Pedro-codigo-0.4.1.zip na release https://github.com/pedromello-a11y/cinema-tv/releases/tag/v0.4.1.
2. Extrair e executar preparar-codigo.py, com Git/Python e acesso à rede, escolhendo uma pasta nova. Ele recupera NuvioMedia/NuvioTV tag 1.0.0 e exige o commit 9f17e8bf4abc799dc8c832d2894a8b3b166e4353.
3. Na árvore reconstruída, aplicar, nesta ordem, os arquivos deste branch em updates/experience-2026-10-29/:
   - experiencia-sobre-0.4.1.patch
   - progresso-de-series.patch
   - letterboxd-automatico.patch
4. Conferir app/build.gradle.kts: 0.5.0-pilot, versionCode 6, PERSONAL_EDITION=true.
5. Criar um checkout Git normal dessa árvore para o desenvolvimento seguinte. Preservar licença e atribuições. Não sobrescrever main do repositório de distribuição sem organizar a migração.

### Reconstrução B: ZIP cumulativo entregue a Pedro

Nuvio-Pedro-codigo-0.5.0.zip já contém o patch cumulativo, preparar-codigo.py, GPL-3.0, guia e validação. Extrair e executar o preparador em uma pasta nova. NÃO reaplicar os três patches da opção A, pois já estão incorporados.

## Plataforma e compilação

Aplicativo Android TV nativo em Kotlin/Jetpack Compose, Hilt, coroutines/Flow, DataStore e componentes de reprodução herdados do NuvioTV. Não é um site empacotado em APK.

Usar JDK 17, Gradle Wrapper 8.13, SDK Android 36. O projeto declara NDK 29.0.14206865; instalar componentes adicionais apenas conforme as tarefas habilitadas exigirem. Algumas integrações herdadas têm configuração local opcional, ausente do código público.

Comandos a partir da árvore Android:
- ./gradlew :app:testFullDebugUnitTest --tests 'com.nuvio.tv.ui.personal.*' --tests 'com.nuvio.tv.updater.UpdateBannerPolicyTest' --tests 'com.nuvio.tv.data.repository.WatchProgressRepositoryProfileIsolationTest'
- node tools/check-letterboxd-sync.cjs
- node tools/check-personal-phone.cjs
- node tools/check-personal-episodes.cjs
- ./gradlew :app:assembleFullRelease

Os dois scripts do painel precisam de jsdom 26.1.0 disponível em NODE_PATH. Essa dependência é somente de teste. Em Windows, usar gradlew.bat ou ambiente compatível.

No ambiente anterior, 110 testes Android passaram, sem falhas, erros ou ignorados; os três scripts JavaScript passaram. O transporte Letterboxd foi simulado. Testes Robolectric nativos precisam de ambiente compatível; a configuração MockK/Byte Buddy deve ser conferida no novo ambiente.

Houve problemas ambientais de cache/classes Java antigas e processos de build concorrentes. Não copiar pastas build, .gradle, SDK ou caches do ambiente anterior. Em máquina com RAM limitada, reduzir workers e ajustar heap. A primeira tentativa release foi encerrada durante otimização; a segunda produziu APKs assinados, mas o comando permaneceu na etapa de empacotamento e foi interrompido depois de o APK ARM32 ser copiado e validado. NÃO registrar isso como uma execução assembleFullRelease concluída com sucesso. No novo ambiente, executar o build até terminar normalmente.

A cópia entregue foi verificada com aapt/apksigner: pacote, versão, arquitetura, não depurável, integridade ZIP e mesma assinatura da 0.4.1. O adaptador JavaScript dentro do APK foi comparado à fonte.

## Assinatura e atualização: preservar

A chave privada de assinatura e suas senhas NÃO estão no GitHub nem no ZIP de código. Precisam ser transferidas/configuradas em ambiente privado antes de produzir uma atualização para o aplicativo instalado. NÃO substituir a chave por outra para contornar essa pendência.

Variáveis aceitas: NUVIO_RELEASE_STORE_FILE, NUVIO_RELEASE_KEY_ALIAS, NUVIO_RELEASE_KEY_PASSWORD, NUVIO_RELEASE_STORE_PASSWORD. Não registrar valores em código, prompts ou logs. As credenciais do Letterboxd ficam na sessão normal da TV, não no repositório.

Preservar applicationId e certificado; a próxima versão destinada à atualização precisa de versionCode superior a 6. Usar a variante full e o APK armeabi-v7a. O instalador não é o ZIP de código.

O atualizador pessoal está em ui/personal/PersonalUpdater.kt. O flag FEATURE_IN_APP_UPDATES_ENABLED da implementação herdada não descreve sozinho o atualizador pessoal. O feed é https://raw.githubusercontent.com/pedromello-a11y/cinema-tv/main/latest.json. Só alterar o feed depois de publicar e verificar o APK correspondente. Android pede confirmação de instalação; não prometer atualização silenciosa.

## Decisões de produto de Pedro

- Chromecast com Google TV HD e controle D-pad; aproximadamente 300 MB livres relatados. Otimizar início, memória, disco e cache. Não exigir servidor pago ou computador sempre ligado.
- Prioridade atual: experiência, sistema, opções e fluxos primeiro; acabamento visual depois.
- Um histórico e listas pessoais; sem separar Pedro/Rapha.
- Início: Continuar de onde parei mistura filmes e séries.
- Filmes: Quero ver, Próximos da fila escolhidos e ordenados manualmente, Descobrir e Histórico. Ao concluir, remover de Quero ver/fila e preservar histórico.
- Séries: distinguir salvar para depois e acompanhar. Mostrar pendências; séries em dia saem das pendências, mas continuam acompanhadas e retornam a cada episódio novo. Permitir corrigir episódios com prévia e desfazer.
- Agenda: calendário mensal das séries acompanhadas.
- Bombando: tendências gerais dentro de Filmes/Séries, sem fingir personalização ou chamar qualquer ranking por nota de Top 250 IMDb oficial.
- Áudio original, legendas pt-BR, preferência por 1080p/720p; chips de filtro, ordenação por seeds e identificação de CAM/TS quando houver evidência. Não confundir lançamento de episódio com existência de fonte reproduzível.
- Escolher fonte na primeira reprodução e reaproveitar preferências nos próximos episódios, com fallback visível. Próximo episódio após contagem cancelável.
- Trailer original; priorizar legendas pt-BR quando disponíveis, sem afirmar legenda não verificada.
- Operações de organização na TV e no celular; paridade completa continua pendente.
- Minimalismo moderno, personalidade cinematográfica, capas oficiais verticais em fileiras horizontais; imagem grande do selecionado. Cor predominantemente das artes, acento verde com borda contínua de foco, sem tracejado nos cantos.
- Menu esquerdo totalmente oculto até acionado; sobrepõe conteúdo. Rolagem horizontal não pode fazer as fileiras pularem verticalmente.
- Referência visual escolhida: terceira geração da segunda rodada de imagens, com Interestelar. A imagem original deve ser anexada por Pedro; este guia não a substitui. Fotos do app na TV são evidência da implementação, não necessariamente do visual final aprovado.
- Não reintroduzir marca/logotipo Nuvio Pedro na experiência principal.
- Metadados do selecionado: IMDb quando houver fonte correta, ano/gênero, sinopse curta, duração e término estimado.

## Letterboxd: separar implementação de comprovação

Conta: pedrovicq. Pedro relatou seis amigos. Deseja favoritos/watchlist, assistidos, notas em meias estrelas e amigos no contexto do filme.

0.5.0 implementa fila persistente pela sessão normal do site em WebView; conferência de identidade antes das operações; resolução exata de filme; diário/assistido/nota com releitura; importação aditiva de watchlist e favoritos; pausa fora do primeiro plano e durante reprodução/fontes. Tentativa de diário com resultado desconhecido não é repetida cegamente. Sessões locais distintas não podem reutilizar o mesmo recibo remoto.

A conclusão do filme considera posição de aproximadamente 90% e cobertura real mínima de 80%, com confirmação ao sair. A confirmação de nota cria a intenção persistente de envio. Meio a cinco estrelas; sem nota não deve apagar nota anterior.

Login real, aceitação dos endpoints pela sessão do site, importação e escrita ao vivo NÃO foram comprovados no Chromecast. 110 testes passando não provam isso. A API oficial era restrita na pesquisa anterior; revisar o acesso legítimo disponível antes de mudar a integração. Não contornar desafios de acesso, extrair credenciais de outros clientes ou declarar sucesso com resposta simulada.

A importação não replica exclusões remotas nem envia edições manuais do watchlist. O feed social completo não foi automatizado. Amigos por filme têm painel e rotas de leitura já implementados, ainda dependentes de validação ao vivo. Falha não pode virar lista vazia nem apagar cache válido.

## Arquivos para começar a ler

Na árvore reconstruída:
- docs/EXPERIENCE.md e docs/LETTERBOXD_AUTOMATION.md.
- app/src/main/java/com/nuvio/tv/ui/personal/: telas, foco, listas, agenda, conclusão, atualizador, painel móvel e integração.
- LetterboxdSyncEngine.kt, LetterboxdSyncStore.kt, LetterboxdWebSession.kt e LetterboxdSyncHost.kt.
- app/src/main/assets/personal/letterboxd-sync.js e phone.html.
- data/local/LibraryPreferences.kt, domain/model/PersonalLibraryState.kt, ui/screens/player/PlayerViewModel.kt.
- app/src/test/java/com/nuvio/tv/ui/personal/ e tools/check-*.cjs.

Leia os documentos cronológicos pela revisão mais recente. Trechos antigos dizem que funções ainda não foram implementadas; o estado 0.5.0 deste guia prevalece para esta passagem.

## Próximas ações

1. Reconstruir e conferir a fonte 0.5.0; registrar o estado em CLAUDE.md no checkout Android.
2. Validar build reproduzível e assinatura privada antes de prometer atualização.
3. Validar login/sincronização no Chromecast com ações reais escolhidas por Pedro. Não criar avaliações fictícias na conta apenas para testar.
4. Medir abertura, navegação por controle, memória, disco, reprodução e retomada. Verificar que a atualização preserva listas e progresso.
5. Completar paridade do painel móvel, histórico, backup/restauração, estados e recuperação de falhas.
6. Retomar recomendações, coleções/Top 250 com fonte identificada, aviso antecipado de CAM e feed social completo conforme viabilidade.
7. Refinar visual e telas herdadas usando a imagem aprovada e evidência física.

Não recomeçar do zero nem trocar a arquitetura sem demonstrar necessidade. Relatar separadamente: implementado, testado automaticamente, validado no aparelho e pendente.
