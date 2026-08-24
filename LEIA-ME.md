# Terapeuta do Alegrete — página de vendas

Página estática, autocontida. Não depende de servidor, banco nem build.

```
index.html      ← a página inteira (HTML + CSS + JS num arquivo só)
img/capa.jpg    ← capa do livro
img/autor.jpg   ← Nelson Carus com o personagem
```

## Como colocar o link de checkout

Abra o `index.html` num editor de texto. Logo no começo do arquivo, procure por
**"EDITE SOMENTE ESTE BLOCO"**. É só trocar os valores entre aspas:

```js
window.CONFIG = {
  checkout:  "#COLE-AQUI-O-LINK-DO-CHECKOUT",   // link da página de pagamento
  whatsapp:  "5555000000000",                   // só números, com 55 na frente
  whatsMsg:  "Olá! Quero saber sobre o livro Terapeuta do Alegrete.",
  preco:     "R$ 00,00",
  parcelas:  "ou em até 3x sem juros no cartão",
  envio:     "Envio para todo o Brasil"
};
```

Salvou, acabou. **Todos** os botões de compra da página (são 9, incluindo a barra
fixa do celular e o rodapé) passam a apontar para esse link, e o preço aparece nos
dois lugares onde ele é exibido. Não precisa mexer em mais nada.

## Como publicar

Qualquer hospedagem de site estático serve. Arraste a pasta inteira para:

- **Netlify Drop** — netlify.com/drop (mais rápido, leva 30 segundos)
- **Vercel**, **Cloudflare Pages**, **GitHub Pages**
- ou o FTP da hospedagem que já usar

## Antes de publicar, confira

- [ ] Link de checkout colado e testado
- [ ] Número de WhatsApp certo (teste clicando no botão)
- [ ] Preço e parcelamento conferidos
- [ ] Texto do FAQ bate com a realidade do envio, prazo e formas de pagamento

## Textos que dependem de informação que ainda não confirmamos

Estes trechos estão escritos de forma genérica de propósito — revise antes de publicar:

- FAQ "Quanto tempo demora para chegar?" — prazo e rastreio
- FAQ "Quais formas de pagamento são aceitas?" — cartão, Pix e boleto
- FAQ "Dá para pedir uma dedicatória do autor?" — confirmar se o autor faz
- Bloco da oferta: "Envio para todo o Brasil"
