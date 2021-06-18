---
title: Dicas de produtividade utilizando VSCode.
authors: Igor Giamoniano
type: post
image: https://i.ibb.co/ZLPQ69W/1.png
date: 2021-06-18
excerpt: Nesse artigo colocarei algumas dicas de como melhorar sua produtividade usando o Visual Studio Code.
categories:
  - Ferramentas
  - Freebies
---

# Dicas de produtividade utilizando VSCode.

### Introdução

Atualmente fiz o curso [Visual Studio Code Productivity Tips](https://www.linkedin.com/learning/visual-studio-code-productivity-tips/make-visual-studio-code-more-productive-for-your-projects) e pude me apaixonar *(ainda MAIS*) por esse belo, leve e ao mesmo tempo **poderoso Editor de Texto.** Ao longo desse artigo colocarei algumas dicas que achei mais interessante, espero que você faça bom uso delas e acima de tudo, divirta-se!

P.S. Todos os atalhos usados nesse artigo são para **Linux**, existem pequenas variações no Windows.


---


### 1 - Command Run > Git Clone

A primeira dica pode ser simples mas ela é bem útil para quem esta começando agora a versionar seus códigos. Vai anotando os atalhos!

**CTRL + ALT + G** - Para abrir o *Source Control* depois **F1** para abrir o *Command Panel*.

Digite: **GIT Clone** e pressione **Enter**
Cole o URL do repositório e escolha a pasta para guardar o clone. Fácil né?

---

### 2 - Peek Definition

Essa com certeza foi uma das que mais gostei, no exemplo utilizaremos **JavaScript**, faça o seguinte:

**CTRL + SHIFT + F10** - Click sobre, por exemplo uma variável ou uma biblioteca e você vera as referencias em um Pop-Up sem atrapalhar sua produção.

<img src="https://i.ibb.co/ZLPQ69W/1.png" alt="Peek Definition" border="0">

---

### 3 - Rename Symbol

Clickando sobre alguma palavra e pressionando **F2** é possível alterar todas as palavras iguais no mesmo código sem a necessidade de selecionar uma por uma. O **CTRL + F2** faz algo semelhante porem de forma mais visual.

<img src="https://i.ibb.co/3v8Fm6r/2.png" alt="Rename Symbol" border="0">

---

### 4 - Extensão: Bracket Pair Colorizer

Você com certeza em algum momento da sua vida já ficou em duvida sobre **onde começava e onde terminava algum parenteses ou chave**, com essa extensão fica mais fácil não se perder.

<img src="https://i.ibb.co/FzD6fg2/3.png" alt="Bracket Pair Colorizer" border="0">

<img src="https://i.ibb.co/4m1vfhr/4.png" alt="Bracket Pair Colorizer 2" border="0">

---

### 5 - Format On Type

Esta é configuração interessante! Em **Settings > Search Settings** digite: **Format** lá você terá as auto explicativas funções **Format On Paste**, **Format On Save** e **Format On Type**. Para mim a **Format On Type**, caiu como uma luva, pois ela faz a indentação a cada **Enter**!

<img src="https://i.ibb.co/ynxDBQk/5.png" alt="Format On Type" border="0">

---

### 6 - Extensão: Sort Lines

A extensão **Sort Lines** é uma mão na roda pra quem usa o padrão de boas práticas do **ESLint** além disso você será capaz de organizar suas linhas de varias formas como (ordem alfabética, case sensitive, padrões aleatórios, etc...). 

Basta selecionar as linhas, pressionar **F1** e digitar **Sort Line**, para ver as opções.

<img src="https://i.ibb.co/MB2sYLX/6.png" alt="Sort Lines" border="0">

---

### 7 - Mover varias linhas ao mesmo tempo

Essa pode até parecer simples mas muita gente não conhece (eu por exemplo, não conhecia). Basta selecionar a linha (ou linhas) segurar **ALT** e usar seta pra cima ▲ ou seta pra baixo ▼ do teclado para mover as linhas.

---

### 8 - Abreviação Emmet

Este tema merece uma atenção especial pois a **abreviação Emmet** é essencial quando falamos em produtividade, com ela podemos **criar tag's**, **inserir classes** e até **classes ordenadas** tudo de forma automatizada, segue alguns exemplos em **HTML**:

Ao digitar **div>ol>li**

Teremos: 
```html
<div>
  <ol>
    <li></li>
  </ol>
</div>
```

----------------------


Ao digitar: **div>ol>li*6**

Teremos:

```html
<div>
    <ol>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ol>
</div>
```
### 9 - Abreviação Emmet com Lorem

Ao digitar: **Lorem**
Teremos:
```html
Lorem ipsum dolor sit amet consectetur adipisicing elit. Quod rerum nam impedit optio harum tempora aspernatur iusto eius, voluptas maxime nihil ut sunt dolorum officia fugiat hic cum distinctio rem!
```

Ao digitar: **div>ol>li*6>Lorem**

Teremos:
```html      
<div>
        <ol>
            <li>Lorem ipsum dolor, sit amet consectetur adipisicing elit. Impedit facere blanditiis repellat, provident tempora vel cumque voluptatem repudiandae? Enim ducimus atque impedit obcaecati id quas similique aut tempora quaerat ex.</li>
            <li>Optio, laudantium cupiditate, atque doloremque, veniam recusandae itaque repellendus ab nulla reiciendis nobis fuga iusto? Ipsa dolores autem doloremque vel omnis ab, magni fugiat neque blanditiis libero aut, veniam optio?</li>
            <li>Fugiat sit, dolor voluptatem ipsa minima asperiores error ducimus sunt quasi, placeat commodi repellendus, fuga unde aliquid ratione ex doloribus? Labore, possimus sint sequi sapiente vel iste suscipit dolore voluptatibus!</li>
            <li>Hic ullam odio magni labore dicta dolor est delectus quae eius sunt? Aperiam nesciunt praesentium fuga laudantium, placeat ut exercitationem inventore blanditiis perferendis quia similique iure perspiciatis id fugiat eaque.</li>
            <li>Laboriosam nulla nesciunt temporibus fugiat, beatae, quam molestias aliquam a laborum rerum nobis ducimus dicta obcaecati doloribus, sequi voluptas repudiandae voluptate dolore aspernatur itaque alias reprehenderit earum sed impedit. Possimus?</li>
            <li>A rerum voluptatibus quis eaque pariatur doloribus itaque illum facilis tempora quidem beatae aliquid reprehenderit error nesciunt vitae dolor dignissimos exercitationem, quo natus. Repellendus, explicabo fugiat voluptates velit reiciendis nisi!</li>
       </ol>
<div>
```

### 10 - Classes sequencias com Emmet

Ao digitar: **div.exemplo$*4**

Teremos:
```html
<div class="exemplo1"></div>
<div class="exemplo2"></div>
<div class="exemplo3"></div>
<div class="exemplo4"></div>
```

### 11 - Extensão: Git Lens

Por último mas não menos importante a extensão **Git Lens**, não a toa, já esta em quase **5 milhões de downloads**. Entre varias coisas, com ela você consegue **ver seus commits** e da sua equipe e **como o código é afetado**.

<img src="https://i.ibb.co/YNmJx2V/7.png" alt="Git Lens" border="0">
