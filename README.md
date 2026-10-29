# Cinema TV — edição pessoal

Aplicativo para Android TV baseado no [NuvioTV 1.0.0](https://github.com/NuvioMedia/NuvioTV), com interface pessoal para controle remoto, biblioteca local e distribuição própria.

## Instalar

Baixe **Nuvio-Pedro-0.4.0-Chromecast-HD.apk** na [release v0.4.0](https://github.com/pedromello-a11y/cinema-tv/releases/tag/v0.4.0). A variante é **armeabi-v7a**, preparada para Chromecast com Google TV HD. O ZIP é código-fonte, não instalador.

É um piloto. A reprodução e a atualização no aparelho físico ainda precisam ser verificadas. A edição não fornece filmes nem fontes de vídeo; os provedores são configurados pelo usuário.

## Atualizar pelo aplicativo

Na versão 0.4.0, abra **Ajustes → Organizar pelo celular**, leia o QR e mantenha a central aberta. No campo **Canal de atualizações**, salve:

```text
https://raw.githubusercontent.com/pedromello-a11y/cinema-tv/main/latest.json
```

Depois use a central de atualizações na TV. O Android solicita confirmação para instalar; o fluxo não é uma instalação silenciosa. O APK é conferido por tamanho, SHA-256, identidade, versão e assinatura. A versão atual aparecerá como atualizada quando o aplicativo já estiver na 0.4.0.

## Esta versão

- Menu oculto, foco verde contínuo, títulos Space Grotesk e interface Manrope.
- Biblioteca pessoal, fila manual, séries acompanhadas e agenda.
- Caches menores, imagens limitadas e catálogo inicial persistido.
- Painel móvel, limpeza de arquivos do app e mecanismo de atualização.
- Filtros de fontes, preferência de áudio e legendas, conclusão e notas locais.

A autenticação e a escrita automática no Letterboxd **não estão implementadas**. O painel social público ainda não foi validado com dados ao vivo. Top 250 IMDb, recomendações pessoais completas e paridade integral do celular continuam pendentes.

## Código e licença

Baixe **Nuvio-Pedro-codigo-0.4.0.zip** na mesma release. Inclui o patch cumulativo, licenças, instruções e um script que recupera a base fixa `9f17e8bf4abc799dc8c832d2894a8b3b166e4353` antes de aplicar as alterações. A árvore reconstruída contém o código correspondente ao APK. O código permanece sob GPL-3.0; as fontes possuem licenças OFL próprias. A chave de assinatura não é distribuída.

## Validação

APK: 71.787.355 bytes; SHA-256:
```text
bc9c8eb4768272bf43218354c8c0defc67ebfa5457ce1596b3daf450ee0cb59f
```

57 testes automatizados passaram. Veja `validacao-0.4.0.json` na release para os limites da validação.
