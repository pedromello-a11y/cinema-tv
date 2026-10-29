# Código de experiência — após 0.4.1

Este pacote contém código em desenvolvimento e validação. **Não é um APK e não altera o instalador disponível no canal de atualização.**

O Início prioriza continuidade pessoal. Filmes ganha Quero ver, Descobrir e Histórico; Séries ganha Acompanhando, Quero ver e Descobrir. A seleção é preservada por seção e a fila pode ser movida diretamente a uma posição.

A segunda rodada acrescenta correção de episódios das séries acompanhadas na TV e no painel móvel: visto/não visto, Já vi até aqui, temporada, prévia e desfazer. O desfazer restaura datas e posição parcial exatas e recusa alterações quando existe progresso posterior nos episódios atingidos.

## Reproduzir o código

1. Obtenha `Nuvio-Pedro-codigo-0.4.1.zip` na [release v0.4.1](https://github.com/pedromello-a11y/cinema-tv/releases/tag/v0.4.1).
2. Extraia e execute seu `preparar-codigo.py` conforme as instruções para reconstruir a árvore 0.4.1 sobre a base fixa.
3. Na raiz reconstruída, aplique `git apply /caminho/experiencia-sobre-0.4.1.patch`.
4. Aplique `git apply /caminho/progresso-de-series.patch`.
5. Leia `docs/EXPERIENCE.md`. Nenhum incremento contém ou altera a chave de assinatura. O versionCode permanece 5; será necessário incrementar a versão antes de distribuir um APK.

O primeiro patch foi aplicado e seus 18 arquivos comparados à árvore da primeira rodada. O segundo foi aplicado sobre a cópia dessa base e seus 13 arquivos foram comparados ao código validado. Ambos passaram também pela verificação reversa correspondente.

## Validação atual

98 testes automatizados passaram, sem falhas ou ignorados: `com.nuvio.tv.ui.personal.*`, `UpdateBannerPolicyTest` e `WatchProgressRepositoryProfileIsolationTest`. Incluem DataStore real, restauração do histórico e navegação Compose por teclas em Robolectric.

Dois scripts DOM passaram com Node/jsdom 26.1.0: organização do painel e correção de episódios. Essa dependência não entra no APK. Relatórios JSON incluem os hashes dos patches e resultados dos testes.

Sem testes físicos nesta rodada: Chromecast, Safari, reprodução e atualização. Escrita automática Letterboxd e importação de listas continuam pendentes.

## Estado de distribuição

O APK público continua 0.4.1-pilot (versionCode 5). As duas rodadas estão publicadas no [PR #1](https://github.com/pedromello-a11y/cinema-tv/pull/1), no branch `experience/personal-sections`. Este pacote preserva o código completo dos dois incrementos. A publicação do código foi autorizada por Pedro; ainda não houve lançamento de um novo APK.
