# Iteração de experiência — após 0.4.1

Esta pasta contém código em desenvolvimento e validação. **Não é um instalador e não altera o APK disponível no canal de atualização.**

O Início passa a priorizar continuidade pessoal. Filmes ganha Quero ver, Descobrir e Histórico; Séries ganha Acompanhando, Quero ver e Descobrir. A seleção é preservada por seção, a fila pode ser movida diretamente a uma posição e o painel móvel oferece organização equivalente dessas listas.

## Reproduzir o código

1. Obtenha `Nuvio-Pedro-codigo-0.4.1.zip` na [release v0.4.1](https://github.com/pedromello-a11y/cinema-tv/releases/tag/v0.4.1).
2. Extraia o ZIP e execute seu `preparar-codigo.py` conforme as instruções para reconstruir a árvore 0.4.1 sobre a base fixa.
3. Na raiz da árvore reconstruída, aplique `git apply /caminho/experiencia-sobre-0.4.1.patch`.
4. Leia `docs/EXPERIENCE.md`. Este incremento não contém nem altera a chave de assinatura. O versionCode permanece 5: ainda é uma iteração de fonte, a receber nova versão antes de distribuir.

O patch foi aplicado a uma cópia da base e os 18 arquivos resultantes foram comparados ao código validado. `git apply --check --reverse` também passou na árvore de desenvolvimento.

## Verificações

84 testes automatizados passaram (`com.nuvio.tv.ui.personal.*` e `UpdateBannerPolicyTest`), incluindo DataStore real e navegação Compose por teclas em Robolectric. O painel móvel passou por oito cenários DOM com Node/jsdom 26.1.0. O relatório identifica as limitações e o hash do patch.

Sem testes físicos nesta iteração: Chromecast, Safari, reprodução e atualização. Escrita automática Letterboxd e importação de listas continuam pendentes. [Experiência e sequência do sistema](EXPERIENCE.md).
