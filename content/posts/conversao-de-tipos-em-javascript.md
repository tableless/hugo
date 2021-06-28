---
title: Conversão de tipos em JavaScript
authors: Gabriel Prates
type: post
date: 2016-09-05
url: /conversao-de-tipos-em-javascript/
titulo_personalizado:
  - 'Conversão de tipos em <strong>JavaScript</strong>'
categories:
  - Código
  - Destaques
  - Javascript

---
Um dia desses eu recebi um quebra-gelo no Telegram, com o seguinte:

<pre class="lang-javascript">Number(null);   // 0
null == 0;  // true né?
</pre>

De cara eu pensei que seria `false`, mas fiz questão de rodar no console e ver no que dava. Claro que deu `false`. Mesmo assim, quis entender o motivo de `Number(null)` retornar `` e fui procurar na [documentação][1] do ECMAScript 6, ou ECMAScript 2015.

O JavaScript, ou ECMAScript, tem um conjunto de operações abastratas que ocorrem por baixo dos panos. Dentre estas operações, temos as conversões de tipos (_Types Conversions_), que é executada sempre que necessário &#8211; que é justamente o caso do `Number(null)`.

Existem várias operações abstratas de conversão de tipos em JS, mas vou abordar apenas as mais comuns.

### ToPrimitive

Praticamente tudo em JS é tratado como um objeto, então a conversão _ToPrimitive_ transforma o _input_ para o seu devido tipo primitivo, isto é, retorna o valor sem ser um objeto. Talvez seja um pouco óbvio e muito comum, mas é interessante ver no console. Primeiro vejamos os tipos primitivos:

<pre class="lang-javascript">// Tipos primitivos
String('foo');      // 'foo'
Number(2016);       // 2016
Boolean(true);      // true
</pre>

Agora, já que temos objetos pra quase tudo em JS, veja o retorno ao rodar no console do Chromium/Chrome:

<pre class="lang-javascript">// Tratando como objetos
new String('foo');
// String {0: "f", 1: "o", 2: "o", length: 3, [[PrimitiveValue]]: "foo"}

new Number(2016);
// Number {[[PrimitiveValue]]: 2016}

new Boolean(false);
// Boolean {[[PrimitiveValue]]: false}
</pre>

Veja que os objetos sempre guardam o valor primitivo, que é retornado por baixo dos panos quando precisamos utilizar o valor para alguma outra operação, como por exemplo:

<pre class="lang-javascript">var ano = new Number(2016);
ano + 1; // 2017

var str = new String('foo');
str.concat(' bar'); // 'foo bar'
</pre>

Para converter valores do tipo `Object`, é feita uma análise de qual o valor primitivo do objeto, por exemplo:

<pre class="lang-javascript">// `Object(2010)` retorna o valor primitivo do objeto `Number`,
// nesse caso, 2010
Object(2010) + 6;   // 2016

// `Object('foo')` retorna o valor primitivo do objeto `String`,
// nesse caso, 'foo'
Object("foo").concat(' bar');   // 'foo bar'

// `Object(true)` retorna o valor primitivo do objeto `Boolean`,
// nesse caso, true
Object(true) && false;  // false
</pre>

&nbsp;

### ToNumber

A operação abstrata _ToNumber_ transforma a entrada em um tipo numérico, e é aqui que entramos naquele exemplo do `Number(null)`.

A conversão para valores numéricos funciona basicamente com as seguintes regras:

<pre class="lang-javascript">// Estas regras estão definidas no ECMAScript
Number(undefined);  // NaN
Number(null);       // +0
Number(true);       // 1
Number(false);      // +0
</pre>

Então, por regra, é por isso que Number(null) retorna 0, e isso não siginifica que `null == 0`, já que são valores primitivos diferentes.

Mas e quanto a conversão de _string_ para _number_, `Number("2016")`?

Para fazer a conversão de uma string, o _ToNumber_ tenta interpretar a string na codificação **UTF-16** e caso não consiga, retorna `NaN`, assim:

<pre class="lang-javascript">Number("2016");       // 2016
Number("20.16");      // 20.16
Number("-0");         // -0
Number("+Infinity");  // +Infinity
Number("++Infinity"); // NaN
Number("201 6");      // NaN
Number("foo");        // NaN

// Para objetos, o retorno é correspondente ao
// valor primitivo do tipo do objeto
Number(Object(2016))  // 2016
Number(Object("21"))  // 21
Number(Object("foo")) // NaN
</pre>

&nbsp;

### ToBoolean

A operação abstrata _ToBoolean_ transforma a entrada em um tipo booleano, que assim como o _ToNumber_, segue algumas regras. Vamos lá:

<pre class="lang-javascript">!!undefined;        // false
!!null;             // false
!!Number(+0);       // false
!!Number(-0);       // false
!!Number(NaN);      // false

// Qualquer outro valor numérico retorna true
!!Number(21);       // true

// String retorna `false` se estiver vazia,
// caso contrário, retorna `true`
!!String("");       // false
!!String("foo");    // true

!!Object();         // true
</pre>

&nbsp;

### ToString

A operações abstratas _ToString_ tem a função de transformar a entrada em uma _string_, e assim como as outras operações aqui descritas, também segue as suas regras de conversão, que são:

<pre class="lang-javascript">String(undefined);      // "undefined"
String(null);           // "null"
String(true);           // "true"
String(false);          // "false"

// Para objetos, o retorno é correspondente ao
// valor primitivo do tipo do objeto
String(Object(2016))  // '2016'
String(Object("21"))  // '21'
String(Object(true))  // 'true'
String(Object(true))  // 'true'
String(Object())      // '[object Object]'
</pre>

Para converter um `Number` para _string_, há uma série de considerações a se fazer, vou citar algumas. Tomando como base `String(Number(m))`:

<pre class="lang-javascript">// 1. Se m for NaN:
String(Number(NaN)); // "NaN"

// 2. Se m for +0 ou −0:
String(Number(-0)); // "0"

// 3. Se m for menor que 0 (zero):
String(Number(-2016)); // "-2016"

// 4. Se m for +Infinity:
String(Number(+Infinity)); // "Infinity"

// 5. Para números muito grandes, muito pequenos,
// ou que tem alguma forma particular para serem
// representados como Number:
    Number(2345678987654321123456);  // 2.3456789876543211e+21
 String(Number(2345678987654321123456)); // "2.3456789876543211e+21"
</pre>

&nbsp;

### ToObject

Por último, temos a _ToObject_, que transforma a entrada em um objeto, quando possível. Até aqui já tivemos a oportinudade de perceber esse tipo de conversão, já que alguns dos exemplos mostraram como _ToObject_ funciona. O que acontece basicamente é que _ToObject_ avalia o tipo primitivo da entrada e retorna um novo objeto daquele tipo, com o valor da entrada. Veja bem:

<pre class="lang-javascript">Object(2016);   // Number {[[PrimitiveValue]]: 2016}
Object('foo');  // String {0: "f", 1: "o", 2: "o", length: 3, [[PrimitiveValue]]: "foo"}
Object(true);   // Boolean {[[PrimitiveValue]]: true}
</pre>

Enfim, achei a resposta para o `Number(null)` retornar `` e deu pra aprender um bocado. Recomendo que você dê uma olhada na [documentação do ECMAScript][2], existem várias outras operações abstratas interessantes.

Como curiosidade, olha só e tente adivinhar qual o resultado do último:

<pre class="lang-javascript">Object(true);               // new Boolean(true)
Object(true) == Boolean(true);      // true
Object(true) == new Boolean(true);  // ??
</pre>

O próprio `Boolean(true)` retorna o valor primitivo `true`, que faz com que o objeto gerado em `Object(true)` sofra uma conversão para o valor primitivo e assim fazer a igualdade. Já `new Boolean(true)` retorna um novo objeto, que na comparação `==` retorna `false`. Isso porque ao comparar dois objetos em JS, a comparação é para saber se os dois objetos são iguais. Faça o teste: `<span class="p">{}</span><span class="w"> </span><span class="err">==</span><span class="w"> </span><span class="p">{}</span>`.

Bom… é isso. Espero que eu tenha sido claro, mas se você ficou com dúvidas, me mande um tweet, vamos trocar ideia (:

Até a próxima.

* * *

&nbsp;

Este post foi originalmente postado em meu blog, no dia 12 de junho de 2016, no link abaixo:
  
<a href="http://gabrielprates.com/2016/07/12/conversao-de-tipos-em-js.html" target="_blank">http://gabrielprates.com/2016/07/12/conversao-de-tipos-em-js.html</a>

 [1]: https://www.ecma-international.org/ecma-262/6.0/index.html#sec-type-conversion
 [2]: https://www.ecma-international.org/ecma-262/6.0/index.html
