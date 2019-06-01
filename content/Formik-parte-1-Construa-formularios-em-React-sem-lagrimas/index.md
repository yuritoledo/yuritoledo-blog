---
title: "Formik parte 1— Construa formulários em React, sem lágrimas"
description: "Recentemente, depois de apanhar — e continuar apanhando — de alguns forms em React mais complexos, decidi dedicar um tempo a esse carinha que dá titulo ao artigo, o Formik. Pra quem ainda não…"
date: "2018-09-11T19:53:45.747Z"
categories: 
  - React
  - React Native
  - React Brasil

published: true
canonicalLink: https://medium.com/reactbrasil/formik-construa-formul%C3%A1rios-em-react-sem-l%C3%A1grimas-a80c52887882
---

![](./asset-1.jpeg)

Recentemente, depois de apanhar — e continuar apanhando — de alguns forms em React mais complexos, decidi dedicar um tempo a esse carinha que dá titulo ao artigo, o [Formik](https://github.com/jaredpalmer/formik). Pra quem ainda não conhece, é uma lib que facilita o manuseio de formulários em React, desde os mais simples até os mais complexos (esses por sua vez, são os que estou estudando). Com esse artigo, darei uma introdução sobre seu uso e seus métodos. Tentarei repassar o que já aprendi. Futuramente, farei uma série com exemplos mais complexos, como handle de erros e integração com componentes de terceiros :)

Ele também funciona muito bem com React Native!

Caso você conheça o Redux Form, que é uma opção mais famosa, [da uma lida aqui](https://jaredpalmer.com/formik/docs/overview#why-not-redux-form) pra ver o motivo de não utilizá-lo :)

[Aqui você pode ver como fica, na prática:](http://Aqui%20você%20pode%20ver%20como%20fica,%20na%20prática%20%5Co)

<Embed src="https://codesandbox.io/embed/24v7nr5nwj" height={350} width={700} />

Para instalar basta usar:

```
npm install formik --save
ou
yarn add formik
```

Uma vez instalado, vamos para os exemplos e comparações.

Caso você já tenha feito algo com o React, seria um código mais ou menos assim:

Embed placeholder 0.39719542627662063

Até aqui beleza, nada fora do comum.

Mas aí, você tem dados no form que são aninhados, algo do tipo `user.address.city`. Nesse caso, começa a azedar:

Embed placeholder 0.21769965626925103

Agora começa a complicar um pouco né? Isso sem falar das tratativas de erro, validações e afins.

A diante, o mesmo exemplo usando o Formik

> Mais um detalhe: Toda a manipulação do form é feita via props, ou seja, o form é naturalmente um stateful component !

Embed placeholder 0.6232757350127167

Simples, não?! Algumas explicações:

-   Obrigatoriamente, o componente deve estar dentro do HoC `withFormik`
-   O `mapPropsToValues` funciona como os valores iniciais
-   Ao encapsular o formulário usando a tag `Form` do Formik, ele automagicamente já sabe que terá que rodar o handleSubmit
-   Para fazer os binds corretamente, deve-se usar o componente `Field` , e a única prop obrigatória é a `name`, que será vinculada com o valor homônimo do `mapPropsToValues`
-   Você pode usar o caminho de um `object` direto no `name` ex: `address.city.name` que o bind será feito, sem nenhum erro \\o
-   Caso você use um componente de terceiros, como o Semantic-UI, É possível usá-lo assim:

Embed placeholder 0.887666322476526

> [Mais detalhes aqui](https://jaredpalmer.com/formik/docs/api/field)

Esse foi um exemplo bem simples (posso fazer outros mais complexos :D) da utilização dessa ferramenta. Existe mais inúmeras facilidades que ela nos fornece, como error handlers, validar se campos foram “tocados” (\`onBlur\`) e não preenchidos, se o formulário como um todo ainda está intacto ou algum campo já foi alterado, habilitar a validação dos campos nos eventos de `onChange e/ou onBlur`, reiniciar os campos do form com a chamada do método `resetForm()` , validações de schema com o [Yup](https://github.com/jquense/yup) , entre outras opções!

[Dê uma olhada na documentação](https://jaredpalmer.com/formik/docs/overview), é bem simples e fácil de ler :)

Qualquer dúvida estou a disposição!

[Veja aqui, a parte 2 :)](https://medium.com/reactbrasil/formik-parte-2-melhorando-formul%C3%A1rios-em-react-com-libs-de-componentes-d2a29d3045d)

\[EDIT\]

[Veja a parte 3 também!](https://medium.com/reactbrasil/formik-parte-3-valida%C3%A7%C3%B5es-de-formul%C3%A1rio-simples-descritivas-e-poderosas-em-react-713c8b7985a4)

[E o primeiro exemplo Formik + hooks!](https://medium.com/reactbrasil/formik-com-hooks-simplicidade-e-pot%E1%BB%81ncia-useformik-parte-1-d518fec52dae)