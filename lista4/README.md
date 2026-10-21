# Respostas – Flexbox

## 1. Revisão da parte 1

### 1. Qual é a diferença entre contêiner e item?

O contêiner é o elemento pai que organiza os itens. Os itens são os elementos que ficam dentro dele. A propriedade `display: flex;` é escrita no contêiner.

### 2. Qual é o eixo principal padrão?

O eixo principal é horizontal, da esquerda para a direita, pois o valor padrão de `flex-direction` é `row`.

## 2. Crescer: flex-grow

### 3. O que é a sobra de espaço?

É o espaço que resta depois de considerar os tamanhos iniciais dos itens. Quando todos têm `flex-grow: 0`, a sobra não é distribuída entre eles.

### 4. Qual é o valor padrão de flex-grow?

O valor padrão é `0`, o que significa que o item não cresce para ocupar a sobra do espaço.

### 5. Analogia da pizza

- **Mesa:** espaço disponível no contêiner.
- **Prato:** espaço inicial de cada item.
- **Sobra:** espaço ainda disponível.
- **Peso do flex-grow:** proporção da sobra recebida por cada item.

### 6. Como fazer a marca ocupar a sobra?

A declaração é `flex-grow: 1;`, colocada no elemento da marca.

### 7. Três itens com base 0, faixa de 600px e pesos 2, 3 e 1.

**Passo 1 – Somar os pesos:**

2 + 3 + 1 = 6

**Passo 2 – Calcular uma parte:**

600 / 6 = 100px

**Passo 3 – Calcular a largura de cada item:**

- Item 1: 2 * 100 = 200px
- Item 2: 3 * 100 = 300px
- Item 3: 1 * 100 = 100px

**Resposta:** 200px, 300px e 100px.

### 8. Três itens com base de 100px, faixa de 600px e pesos 0, 1 e 2.

**Passo 1 – Somar os tamanhos iniciais:**

100 + 100 + 100 = 300px

**Passo 2 – Calcular a sobra:**

600 - 300 = 300px

**Passo 3 – Somar os pesos:**

0 + 1 + 2 = 3

**Passo 4 – Calcular uma parte:**

300 / 3 = 100px

**Passo 5 – Calcular as larguras finais:**

- Item 1: 100 + (0 * 100) = 100px
- Item 2: 100 + (1 * 100) = 200px
- Item 3: 100 + (2 * 100) = 300px

**Resposta:** sobra de 300px e larguras finais de 100px, 200px e 300px.

## 3. Encolher: flex-shrink

### 9. Quando flex-shrink entra em ação?

Entra em ação quando falta espaço. Seu valor padrão é `1`.

### 10. Dois itens de 400px em uma faixa de 600px.

**Passo 1 – Somar os tamanhos:**

400 + 400 = 800px

**Passo 2 – Calcular quanto falta:**

800 - 600 = 200px

**Passo 3 – Dividir a redução:**

200 / 2 = 100px

**Passo 4 – Calcular a largura final:**

400 - 100 = 300px

**Resposta:** cada item fica com 300px.

### 11. Primeiro item com flex-shrink: 0.

O primeiro item permanece com 400px.

600 - 400 = 200px

**Resposta:** o primeiro fica com 400px e o segundo com 200px. O conjunto cabe exatamente na faixa.

### 12. Exemplo de flex-shrink: 0.

Um ícone pode usar `flex-shrink: 0;` para não ficar achatado ou deformado quando faltar espaço.

## 4. Tamanho de partida e atalho flex

### 13. O que é flex-basis?

Define o tamanho inicial do item. Se houver `width: 200px` e `flex-basis: 10rem`, o `flex-basis` define o tamanho de partida.

### 14. Por que usar flex-basis: 0?

Porque os itens começam com tamanho-base zero, permitindo que o `flex-grow` distribua o espaço disponível proporcionalmente aos pesos.

### 15. Tabela dos atalhos flex

| Atalho | Grow | Shrink | Basis |
|---|---:|---:|---|
| `flex: initial` | 0 | 1 | auto |
| `flex: 1` | 1 | 1 | 0% |
| `flex: auto` | 1 | 1 | auto |
| `flex: none` | 0 | 0 | auto |

### 16. Itens de 100px e 300px em uma faixa de 600px.

**Com `flex: 1`:**

Os itens começam com base zero e dividem igualmente o espaço disponível.

600 / 2 = 300px

**Resultado:** 300px para cada item.

**Com `flex: auto`:**

**Passo 1 – Somar os tamanhos iniciais:**

100 + 300 = 400px

**Passo 2 – Calcular a sobra:**

600 - 400 = 200px

**Passo 3 – Dividir a sobra:**

200 / 2 = 100px

**Passo 4 – Calcular as larguras finais:**

- Primeiro item: 100 + 100 = 200px
- Segundo item: 300 + 100 = 400px

**Resultado:** 200px e 400px.

Os resultados diferem porque `flex: 1` usa base zero e `flex: auto` considera os tamanhos iniciais do conteúdo.

### 17. flex: 1 e flex: auto sempre dão o mesmo resultado?

**Falso.** `flex: 1` usa base zero, enquanto `flex: auto` utiliza a base automática. Os resultados podem ser diferentes dependendo dos tamanhos iniciais dos itens.

## 5. O mínimo que trava o encolhimento

### 18. Qual propriedade segura o item?

A propriedade padrão `min-width: auto` pode impedir que o item encolha abaixo do tamanho mínimo do conteúdo. O ajuste é `min-width: 0;`.

### 19. Quando esse problema acontece?

Pode acontecer em uma página com menu lateral e texto principal quando uma palavra muito longa ultrapassa a largura disponível.

## 6. order e align-self

### 20. Observe o código.

HTML:

    <div class="barra">
      <span>A</span>
      <span>B</span>
      <span class="primeiro">C</span>
    </div>

CSS:

    .barra {
      display: flex;
    }

    .primeiro {
      order: -1;
    }

**a) Qual é a ordem visual?**

C, A, B.

**b) Qual é a ordem de foco ao apertar Tab?**

A, B, C, seguindo a ordem do HTML.

**c) Por que isso importa para quem usa leitor de tela?**

Porque a ordem visual pode ser diferente da ordem de navegação, dificultando a compreensão da página.

### 21. Qual é o valor padrão de order?

O valor padrão é `0`. O item com `order: -1` aparece antes do item com `order: 2`.

### 22. O pai tem align-items: stretch.

- `align-self: flex-end;`: o filho fica alinhado ao final do eixo transversal.
- `align-self: auto;`: o filho segue o alinhamento definido pelo pai e, nesse caso, fica esticado.

### 23. Quando usar align-self e align-items?

`align-items` alinha todos os itens do contêiner. `align-self` permite definir um alinhamento diferente para um item específico.

## 7. A página com miolo

### 24. Quais são os itens de cada contêiner?

HTML:

    <div class="pagina">
      <header>topo</header>
      <div class="miolo">
        <aside>menu</aside>
        <main>texto</main>
      </div>
      <footer>rodape</footer>
    </div>

- **Itens de `.pagina`:** `header`, `.miolo` e `footer`.
- **Itens de `.miolo`:** `aside` e `main`.

### 25. Por que .miolo precisa de display: flex?

Porque `display: flex;` transforma `.miolo` em um contêiner flexível, permitindo organizar o menu e o texto lado a lado.

### 26. Explique cada declaração.

CSS:

    .pagina {
      display: flex;
      flex-direction: column;
      min-height: 100vh;
    }

    .miolo {
      display: flex;
      flex: 1;
    }

    aside {
      flex: 0 0 10rem;
    }

    main {
      flex: 1;
      min-width: 0;
    }

- `display: flex;`: transforma a página em um contêiner flexível.
- `flex-direction: column;`: organiza os elementos verticalmente.
- `min-height: 100vh;`: define a altura mínima igual à altura da janela.
- `.miolo { display: flex; }`: coloca o menu e o texto lado a lado.
- `flex: 1;` em `.miolo`: permite ocupar o espaço disponível.
- `flex: 0 0 10rem;` em `aside`: define uma base de 10rem, sem crescer ou encolher.
- `flex: 1;` em `main`: permite ocupar o espaço restante.
- `min-width: 0;`: permite que o conteúdo encolha abaixo do tamanho mínimo automático.

## 8. Erros comuns e síntese

### 27. Por que flex-grow: 1 não funciona no contêiner?

Porque `flex-grow` controla o crescimento dos itens, não do próprio contêiner. A correção é colocar a propriedade no item que deve ocupar a sobra.

### 28. Duas formas de resolver um item que ultrapassa a faixa.

- `min-width: 0;`: permite que o item encolha, sendo útil principalmente para textos longos.
- `flex-shrink: 0;`: impede que o item encolha, sendo útil para ícones e botões que precisam manter o tamanho. É necessário garantir espaço suficiente para evitar transbordamento.

### 29. Resumo das propriedades.

- **flex-basis:** define o tamanho inicial do item.
- **flex-grow:** determina quanto o item cresce para ocupar o espaço sobrando.
- **flex-shrink:** determina quanto o item encolhe quando falta espaço.
- **order:** define a ordem visual dos itens.
- **align-self:** permite alinhar individualmente um item no eixo transversal.