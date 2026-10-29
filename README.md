# Cinema TV — edição pessoal

Aplicativo para Android TV baseado no [NuvioTV 1.0.0](https://github.com/NuvioMedia/NuvioTV), com interface pessoal para controle remoto, biblioteca local e distribuição própria.

## Instalar

Baixe **Nuvio-Pedro-0.4.1-Chromecast-HD.apk** na [release v0.4.1](https://github.com/pedromello-a11y/cinema-tv/releases/tag/v0.4.1). A variante é **armeabi-v7a**, preparada para Chromecast com Google TV HD. O ZIP é código-fonte, não instalador. Atualize a instalação existente, preservando os dados.

É um piloto de conexão e leitura Letterboxd. Login, leitura ao vivo e atualização no aparelho físico ainda precisam ser verificados. A edição não fornece filmes nem fontes de vídeo; os provedores são configurados pelo usuário.

## Atualizar pelo aplicativo

Na 0.4.1 o canal já vem configurado, preservando um endereço salvo antes. Use **Ajustes → Buscar atualização**. O Android solicita confirmação para instalar. O APK é conferido por tamanho, SHA-256, identidade, versão e assinatura. Instalação silenciosa não está disponível.

Na 0.4.0 sem canal conectado, abra **Ajustes → Organizar pelo celular**, leia o QR na mesma rede e mantenha a central aberta. Em **Canal de atualizações**, conecte:

```text
https://raw.githubusercontent.com/pedromello-a11y/cinema-tv/main/latest.json
```

Volte à central na TV e use **Buscar atualização**.

## Novidades da 0.4.1

- Amigos e notas no contexto do filme, no Início e nos detalhes.
- Ajustes → Letterboxd · conexão e avaliações: sessão no site dentro do app, com verificação de pedrovicq.
- Lista das avaliações locais pendentes, preservando as meias estrelas.
- Consulta alternativa pela página do Letterboxd e cache de até 24 filmes.
- Componente web carregado apenas ao entrar na tela de conexão.

O **envio automático de notas, registro no diário e importação de favoritos/watchlist ainda não estão ativos**. Fazer login não marca avaliações como enviadas. A leitura ao vivo dos amigos e a persistência da sessão precisam ser testadas no Chromecast. Top 250 IMDb, recomendações pessoais completas e paridade integral do celular continuam pendentes.

## Recursos já presentes

Menu oculto, foco verde contínuo, títulos Space Grotesk e interface Manrope; biblioteca pessoal, fila manual, séries acompanhadas e agenda; caches menores e catálogo inicial persistido; painel móvel, limpeza de arquivos do app; filtros de fontes, preferências de áudio/legendas, conclusão e notas locais.

## Código e licença

**Nuvio-Pedro-codigo-0.4.1.zip**, na mesma release, inclui o patch cumulativo, licenças, instruções e um script que recupera a base fixa `9f17e8bf4abc799dc8c832d2894a8b3b166e4353` antes de aplicar as alterações. A árvore reconstruída contém o código correspondente ao APK. Código sob GPL-3.0; fontes sob licenças OFL próprias. A chave de assinatura não é distribuída.

## Validação

APK: 71,807,067 bytes; SHA-256:
```text
158367a0aab05bdb8736a94b414c71f15f60d90eb5d8808bfb470871a49403df
```

75 testes automatizados passaram. Veja `validacao-0.4.1.json` na release. Sem validação física de login, reprodução, desempenho ou atualização no Chromecast.
