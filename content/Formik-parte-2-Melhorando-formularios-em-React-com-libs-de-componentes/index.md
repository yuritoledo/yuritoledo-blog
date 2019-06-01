---
title: "Formik parte 2 — Melhorando formulários em React com libs de componentes"
description: "Dando continuidade à sequência de artigos sobre o Formik, faremos alguns testes com componentes de terceiros. Eles são uma mão na roda por serem práticos e ótimos para um rápido desenvolvimento…"
date: "2018-10-17T14:28:06.210Z"
categories: 
  - React
  - Reactjs
  - Semantic Ui

published: true
canonicalLink: https://medium.com/reactbrasil/formik-parte-2-melhorando-formul%C3%A1rios-em-react-com-libs-de-componentes-d2a29d3045d
---

![“person holding brown handheld tool” by [Malte Wingen](https://unsplash.com/@maltewingen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](./asset-1)

[**Se ainda não viu, veja a parte 1!**](https://medium.com/reactbrasil/formik-construa-formul%C3%A1rios-em-react-sem-l%C3%A1grimas-a80c52887882)

[**E agora, fresquinha, veja a parte 3!**](https://medium.com/reactbrasil/formik-parte-3-valida%C3%A7%C3%B5es-de-formul%C3%A1rio-simples-descritivas-e-poderosas-em-react-713c8b7985a4)

[**Veja a nova API do Formik com hooks!**](https://medium.com/reactbrasil/formik-com-hooks-simplicidade-e-pot%E1%BB%81ncia-useformik-parte-1-d518fec52dae)

---

Dando continuidade à sequência de artigos sobre o [Formik](https://jaredpalmer.com/formik/docs/api/formik), faremos alguns testes com componentes de terceiros. Eles são uma mão na roda por serem práticos e ótimos para um rápido desenvolvimento. Também são excelentes para quem não gosta/não tem paciência/não tem muita familiaridade com `css` para usar `[styled components ](https://www.styled-components.com/)`— No meu caso, as duas primeiras opções :D

Para o exemplo desse artigo, usarei o [Semantic UI](http://react.semantic-ui.com/), pois ele tem uma boa documentação, um ótimo playground embutido na documentação para rápidos testes / protótipos, é bonito e bem cheio de features! Uso ele no trabalho e em projetos pessoais.

Contudo, esse artigo também serve para as demais libs ([ReactBootstrap](https://react-bootstrap.github.io/), [Antd](https://ant.design/docs/react/getting-started), [Element](https://elemefe.github.io/element-react/#/en-US/quick-start)), basta seguir a documentação e fazer as adaptações.

Mão à obra!

---

Segundo a documentação do Formik, para que possamos utilizar 3rd party components_,_ existem três abordagens:

`<Field component={...} />`

`<Field render={...} />`

`<Field children />`

Eis os exemplos, respectivamente:

Embed placeholder 0.885819661207562

Todos geram o mesmo resultado no final, então simplesmente você escolhe a que melhor lhe convir. Entretanto, vamos aos poréns:

-   Porém 1: Se for usar a abordagem de `component`, você perde o intellisense (do VSCode por exemplo), porém a implementação do `Field` fica muito menor, o que o torna mais legível. Contudo, não da pra importar o `Input` do Semantic direto, é preciso criar um `stateless component`, para utilizá-lo, assim:

Embed placeholder 0.32247118161682375

-   Porém 2: Se for de `render`**,** você terá um `Field` mais verboso e terá que aplicar as `props` **direto** no  `Input`**:**

Embed placeholder 0.7039555010858778

-   Porém 3: O mesmo que o porém 2:

Embed placeholder 0.796863929810214

Ai vai do gosto do freguês. Eu particularmente fico com o **component.**

---

Como nem tudo são flores, nem `inputs`, você logo vai perceber um pequeno problema com os Dropdowns do Semantic

[**Formik Article 2 - CodeSandbox**  
_The online code editor tailored for web applications_codesandbox.io](https://codesandbox.io/s/zn82124o9l "https://codesandbox.io/s/zn82124o9l")[](https://codesandbox.io/s/zn82124o9l)

> [_Aproveita e da uma fuçada, têm tudo que já fizemos aqui!_](https://codesandbox.io/s/zn82124o9l "https://codesandbox.io/s/zn82124o9l")

Você vai notar que esse carinha abaixo, não funciona como os outros:

Embed placeholder 0.9402326574155198

Isso ocorre por que o evento de `change` do dropdown, não segue o mesmo padrão do React.

[Dá uma olhada, clicando em “Try it”](http://react.semantic-ui.com/modules/dropdown/#usage-controlled)

Esse comportamento fora do padrão não é coisa do Semantic, isso é meio “normal” em algumas libs (como o Antd também). Nesse caso, teremos que fazer assim:

Embed placeholder 0.8856269430672625

Vamos as explicações:

-   Na linha 1, além de pegar o `field` e o `props`, você também tem acesso ao `form`, que contêm a maioria dos métodos do Formik, incluindo o `[setFieldValue](https://jaredpalmer.com/formik/docs/api/formik#setfieldvalue-field-string-value-any-shouldvalidate-boolean-void)`e o `[setFieldTouched](https://jaredpalmer.com/formik/docs/api/formik#setfieldtouched-field-string-istouched-boolean-shouldvalidate-boolean-void).`
-   Na linha 7, temos a chamada do `setFieldValue`que por sua vez, recebe um parâmetro `name` — que será o mesmo `name` usado no `Field` — e o `value` que lhe será atribuído. (Como pode observar, o `value`, vem do segundo parâmetro do evento e não do primeiro, como acontece no React).  
    Caso esse seu Dropdown seja dinâmico, você pode trocar o `onChange` do exemplo, por esse: `onChange={(e, {name, value}) => setFieldValue([name], value)}`
-   Na linha 8, temos o `setFieldTouched`, que indica se o usuário já passou por aquele campo. Ele recebe os parâmetros `name`, `isTouched` e `shouldValidate .  
    `O `name` segue a mesma regra citada da linha 7`, o isTouched` é um `boolean` pra indicar se o componente foi ou não "tocado” e o `shouldValidate` é auto-explicativo :)

---

Bom, acho que por ora é apenas isso.  
O próximo artigo será sobre validações do formulário!

Falou!