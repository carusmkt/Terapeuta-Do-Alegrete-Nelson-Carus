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
  whatsapp:  "5555999060004",                   // (55) 99906-0004 — já configurado
  whatsMsg:  "Olá! Vim pelo site do Terapeuta do Alegrete e quero falar sobre o livro.",
  preco:     "R$ 51,47",
  precoObs:  "Frete já incluso no preço",     // linha pequena embaixo do preço
  envio:     "Envio para todo o Brasil, com frete incluso",
  outrosLivros: "outros-livros.html"          // página com os demais títulos do autor
};
```

Salvou, acabou. **Todos** os botões de compra da página (são 9, incluindo a barra
fixa do celular e o rodapé) passam a apontar para esse link, e o preço aparece nos
dois lugares onde ele é exibido. Não precisa mexer em mais nada.

## As mensagens do WhatsApp

Cada botão de WhatsApp abre a conversa com um texto já escrito, e esse texto diz
de onde a pessoa veio. Assim, ao receber a mensagem, dá para saber na hora que o
contato nasceu do site — e em que ponto da página ela clicou:

| Botão | Mensagem que chega para vocês |
|---|---|
| Herói — "Falar com o autor" | *Vim pelo site do Terapeuta do Alegrete e queria falar com o autor.* |
| "Tirar uma dúvida" | *…e fiquei com uma dúvida sobre o livro.* |
| Oferta — "Comprar pelo WhatsApp" | *…e quero comprar um exemplar pelo WhatsApp.* |
| FAQ — "Ainda tenho dúvida" | *…li as perguntas frequentes e ainda fiquei com uma dúvida.* |
| Rodapé — "Falar no WhatsApp" | *Vim pelo site do Terapeuta do Alegrete.* |

Para mudar o texto de um botão específico, procure no `index.html` por
`data-whatsapp="..."` e edite o que está entre aspas. Um botão sem texto próprio
usa o `whatsMsg` do bloco de configuração.

## A página dos outros títulos

O bloco "Do mesmo autor", entre a oferta e as perguntas, tem um botão apontando
para `outros-livros.html`. **Essa página ainda não existe** — enquanto não for
criada, o botão leva a um erro 404. Para apontar para outro endereço, troque o
valor de `outrosLivros` no bloco de configuração.

## Como publicar

Qualquer hospedagem de site estático serve. Arraste a pasta inteira para:

- **Netlify Drop** — netlify.com/drop (mais rápido, leva 30 segundos)
- **Vercel**, **Cloudflare Pages**, **GitHub Pages**
- ou o FTP da hospedagem que já usar

## Antes de publicar, confira

- [ ] Link de checkout colado e testado
- [x] Número de WhatsApp: (55) 99906-0004 — configurado
- [x] Preço: R$ 51,47 com frete incluso — configurado
- [ ] Texto do FAQ bate com a realidade do envio, prazo e formas de pagamento
- [ ] Página `outros-livros.html` criada (senão o botão "Ver todos os títulos" dá 404)

## Textos que dependem de informação que ainda não confirmamos

Estes trechos estão escritos de forma genérica de propósito — revise antes de publicar:

- FAQ "Quanto tempo demora para chegar?" — prazo e rastreio
- FAQ "Quais formas de pagamento são aceitas?" — cartão, Pix e boleto
- FAQ "Dá para pedir uma dedicatória do autor?" — confirmar se o autor faz
- Bloco da oferta: "Envio para todo o Brasil"
