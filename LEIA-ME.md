# Terapeuta do Alegrete — página de vendas

Página estática, autocontida. Não depende de servidor, banco nem build.

```
index.html            ← a página de vendas do Terapeuta do Alegrete
outros-livros.html    ← a página com todos os livros do autor
img/capa.jpg          ← capa do Terapeuta do Alegrete
img/autor.jpg         ← Nelson Carús com o personagem
img/outros-livros.jpg ← os livros na prateleira
img/livro-*.jpg       ← a capa de cada um dos quatro livros anteriores
img/combo-cinco-livros.jpg ← os cinco livros em leque (bloco do combo)
```

Cada arquivo `.html` carrega tudo dentro de si (HTML + CSS + JS). Os dois têm o
mesmo visual e cada um tem o seu próprio bloco de configuração no começo.

## Como colocar o link de checkout

Abra o `index.html` num editor de texto. Logo no começo do arquivo, procure por
**"EDITE SOMENTE ESTE BLOCO"**. É só trocar os valores entre aspas:

```js
window.CONFIG = {
  checkout:  "https://pag.ae/82brvgxeu",         // PagBank — Terapeuta do Alegrete
  whatsapp:  "5555999060004",                   // (55) 99906-0004 — já configurado
  whatsMsg:  "Olá! Vim pelo site do Terapeuta do Alegrete e quero falar sobre o livro.",
  preco:     "R$ 61,50",
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

## A página dos outros títulos — `outros-livros.html`

O bloco "Do mesmo autor", entre a oferta e as perguntas, leva para essa página.
Ela apresenta os quatro livros anteriores na ordem em que foram escritos, depois
o Terapeuta do Alegrete como livro 05, e termina no **combo**.

### As cores

A base é a paleta enviada — Prussian Blue, Twilight Indigo, Faded Copper,
Coffee Bean e Apricot Cream. Por cima dela, **cada livro pinta o seu próprio
bloco com as cores da sua capa**:

| Livro | Fundo | Cor de destaque |
|---|---|---|
| Entre a vida e a morte | creme quente | rosa-antigo da ilustração |
| Na espreita da morte | cinza-pedra | o azul do vidro |
| Um sonho além da vida | marinho profundo | o vermelho do coração |
| Crônicas, contos e histórias | azul claro | o azul do círculo |
| Terapeuta do Alegrete | marinho | o dourado da capa |

Isso está logo no começo do `<style>`, num bloco chamado **UM BLOCO POR LIVRO** —
uma linha por livro. Para mudar a cor de um livro, mexe só na linha dele.

### O bloco de configuração

```js
window.CONFIG = {
  precoLivro:    "",              // o preço, igual para os quatro
  precoObs:      "Frete incluso",
  precoCombo:    "",              // o preço do combo com os cinco
  comboObs:      "Os cinco livros, frete incluso",
  comboCheckout: "",              // link de pagamento do combo
  ...
  livros: {
    "entre-a-vida-e-a-morte": { checkout: "" },
    "na-espreita-da-morte":   { checkout: "" },
    "um-sonho-alem-da-vida":  { checkout: "" },
    "cronicas-contos":        { checkout: "" }
  }
};
```

O preço é **um só para os quatro livros** — escreve uma vez em `precoLivro` e ele
aparece nos quatro blocos. O combo tem o seu próprio preço em `precoCombo`.

A página funciona com tudo vazio e vai ficando completa conforme você preenche:

| Campo | Vazio | Preenchido |
|---|---|---|
| `precoLivro` / `precoCombo` | o preço nem aparece | aparece acima dos botões |
| `checkout` / `comboCheckout` | o botão cai no WhatsApp, com o nome do livro já na mensagem | o botão leva direto para o pagamento |

**Nenhum botão fica morto em nenhum momento.** Enquanto o link de checkout não
estiver lá, ele abre o WhatsApp; assim que você colar o link, vira compra direta.

### O cabeçalho camaleão

O cabeçalho assume a cor da seção que está imediatamente atrás dele, e o "Carús"
e o botão "Ver o combo" assumem a cor de destaque daquela seção — a mesma cor do
botão de compra do livro. Isso é automático: cada seção já declara as suas cores
no bloco **UM BLOCO POR LIVRO**, e o cabeçalho só copia. Se você mudar a cor de
um livro lá, o cabeçalho acompanha sozinho.

### As animações

Só os rótulos ("LIVRO 03") e os títulos animam ao entrar na tela: o risquinho se
desenha da esquerda para a direita e o título sobe. Fotos, textos e botões
aparecem parados, de propósito, para a página não ficar agitada. Quem tem o
aparelho configurado para reduzir animações não vê nenhuma.

### O ícone da aba (favicon)

São as letras **NC** desenhadas em código, dentro do próprio `outros-livros.html`
— não existe arquivo de imagem. Ele se inverte sozinho conforme o aparelho
estiver no modo claro ou escuro.

### O combo

O bloco final vende os cinco juntos: *na compra de quatro livros, o quinto é por
nossa conta*. A foto é a dos cinco em leque. O botão usa `comboCheckout`.

## Rastreamento (Google Tag Manager)

O container **GTM-KBP8CVPN** está instalado nas **duas** páginas, no formato que
o Google pede: o script o mais alto possível dentro do `<head>` e o `<noscript>`
logo depois da abertura do `<body>`.

Não precisa mexer em nada aqui: daqui para a frente, tags, conversões e pixels
são configurados dentro do painel do Tag Manager, não no código da página.

Um aviso: os botões de compra levam para o **PagBank**, que é um domínio de
fora. A conversão em si acontece lá, e o Tag Manager sozinho não enxerga isso —
ele só registra o clique que saiu daqui. Para contar venda de verdade é preciso
configurar a conversão do lado do PagBank ou trabalhar com o clique no botão
como evento.

## Como publicar

Qualquer hospedagem de site estático serve. Arraste a pasta inteira para:

- **Netlify Drop** — netlify.com/drop (mais rápido, leva 30 segundos)
- **Vercel**, **Cloudflare Pages**, **GitHub Pages**
- ou o FTP da hospedagem que já usar

## Antes de publicar, confira

- [x] Link de checkout do Terapeuta do Alegrete colado (PagBank)
- [x] Número de WhatsApp: (55) 99906-0004 — configurado
- [x] **Preço:** R$ 61,50 nas duas páginas, igual ao checkout
- [ ] Texto do FAQ bate com a realidade do envio, prazo e formas de pagamento
- [x] Página `outros-livros.html` criada
- [x] Resumo dos quatro livros — textos enviados pela autoria
- [x] Capas dos quatro livros e foto do combo na pasta `img/`
- [x] `precoLivro` (R$ 61,50) e `precoCombo` (R$ 238,10) preenchidos
- [ ] Falta o link de checkout de **Um sonho além da vida**
- [ ] Confirmar se o frete está incluso nos R$ 61,50
- [x] Nome grafado **Carús** nas duas páginas

## Os links de pagamento (PagBank)

| Livro | Link | Preço | Pagamento |
|---|---|---|---|
| Terapeuta do Alegrete | `pag.ae/82brvgxeu` | R$ 61,50 | Pix e boleto |
| Entre a vida e a morte | `pag.ae/82bCWXnG3` | R$ 61,50 | Pix e boleto |
| Na espreita da morte | `pag.ae/82bDp7phJ` | R$ 61,50 | Pix |
| Um sonho além da vida | **falta** | — | — |
| Crônicas, contos e histórias | `pag.ae/82bDqBsm9` | R$ 61,50 | Pix |
| Combo 4 + 1 | `pag.ae/82bDPu2HJ` | R$ 238,10 | Pix |

Enquanto o link de *Um sonho além da vida* não existir, o botão dele continua
caindo no WhatsApp — é só colar o link em `CONFIG` que ele vira compra direta.

## Textos que dependem de informação que ainda não confirmamos

Estes trechos estão escritos de forma genérica de propósito — revise antes de publicar:

- FAQ "Quanto tempo demora para chegar?" — prazo e rastreio
- FAQ "Quais formas de pagamento são aceitas?" — cartão, Pix e boleto
- FAQ "Dá para pedir uma dedicatória do autor?" — confirmar se o autor faz
- Bloco da oferta: "Envio para todo o Brasil"
- **Formas de pagamento:** o FAQ da página de vendas fala em cartão, Pix e
  boleto. Nos links do PagBank aparecem só Pix e boleto — e em três deles,
  só Pix. Vale acertar o texto do FAQ com a realidade.
- `outros-livros.html`, livro 03: a frase de abertura *"Até onde pode ir um
  sonho?"* foi escrita por mim a partir do texto enviado — os outros três livros
  abrem com a pergunta que veio no texto original.
