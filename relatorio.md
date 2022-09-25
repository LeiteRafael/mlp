# Workshop JavaScript

> Conhecendo a linguagem

#### Juan Arcari e Rafael Leite

##### Modelos de linguagem de programação - UFRGS - INF01121

##### Professor Leandro Krug Wives

---
## Tópicos
- Surgimento
- Primeiros anos
- Paradigmas
  - Funcional
  - POO
- Evolução da linguagem
- Features ES6
- Assicronismo
  - async/await
- Nodejs
- Aplicabilidade
- TypeScript
- Popularidade
- Mercado Atual

---
## Surgimento

Javascript foi criada em 1995 por Brendan Eich para o Netscape Navigator, com o nome de LiveScript.

A ideia inicial era proporcionar mais dinamicidade na web, pois no momento os browsers ainda eram estáticos.

A proposta era implementar a linguagem Scheme no Navigator, porém pela sintaxe e características de linguagens funcionais, optou-se por uma linguagem com a sintaxe baseada em Java, que era predominante na época.

A Microsoft, paralelamente, criou o JScript, uma dor de cabeça aos desenvolvedores web pois rodava somente no Internet Explorer.

Ao perceber este problema, a empresa ECMA padronizou a linguagem de modo que funcionasse em todos os navegadores, sendo adotado o nome ECMAScript e depois Javascript, por motivos de marketing.

---

## Primeiros anos (1997 - 2010)

Novos desenvolvimentos na internet estavam impulsionando a demanda por expansões mais avançadas.

Um desses avanços foi o surgimento do AJAX, uma técnica de desenvolvimento que permite a criação de páginas web mais interativas, como por exemplo, alterar o conteúdo de forma dinâmica sem precisar recarregar a página inteira.

Devido à expansão da linguagem no desenvolvimento de diversas funcionalidades em páginas web, o JS foi ganhando popularidade ao longo dos anos 2000.


---

## Paradigmas
### Funcional

Javascript é uma linguagem que aceita construções através de programação funcional.

#### Função de alta ordem e função anônima

```javascript
//função que recebe função como parâmetro
const calcular = (fn, x, y) => fn(x, y);

// (x, y) => x + y função anônima de soma
calcular((x, y) => x + y, 2, 3) // retorna 5
```

#### map(), filter() e reduce() em JavaScript
São funções nativas da linguagem que atuam sobre arrays
- map() - mapeia todos elementos conforme a função passada como argumento
- filter() - filtra os elementos do array conforme a função passada com argumento
- reduce() - reduz array a unico elemento aplicando a função passada com argumento e retornando no acumulador.
```javascript
//Exemplos das 3 funções sobre um array

const array = [1,2,3,4,5];

const arrayMultiplicadoPor2 = array.map(x => x * 2);
const retornaMaioresQue3 = array.filter(x => x > 3);
const somaElementosArray = array.reduce((x, y) => x + y, 0);


```
### POO(Programação Orienta a Objetos)

Assim como em outras linguagens, Orientação a Objetos em Javascript também adota o mesmo conceito de classe e objeto.

No JS, utilizamos uma função para criar uma classe.
#### Como definir uma classe
```javascript
function MinhaClasse() { // declaração da classe
    var nome; // atributo privado
    this.idade; // atributo público
}
oMinhaClasse = new MinhaClasse(); /* criação de uma nova instância da classe */
oMyClasse.idade = '10';

```
#### Herança em javascript
```javascript
function Pessoa(nome, idade) { //classe pai
    this.nome = nome
    this.idade = idade
}
function Aluno(matricula, nome, idade) { //classe filha
    this.matricula = matricula
    Pessoa.call(this, nome, idade, matricula); // chamada da classe pai
}
const aluno = new Aluno(1001, 'Rafael', 26);
console.log(aluno.nome); //Rafael
```
#### Polimorfismo
```javascript
function Animal() { }
function Gato() { }

Animal.prototype.fazerBarulho = function () {
  console.log("Barulho base");
};
Gato.prototype = new Animal();
Gato.prototype.fazerBarulho = function () {
  console.log("Miau");
};

var barulhoAnimal = new Animal().fazerBarulho; // Barulho base
var barulhoGato = new Gato().fazerBarulho(); // Miau

```
---
### Evolução do Javascript

Ao longo dos anos, JavaScript foi recebendo features e melhorias, no entanto em 2015 a linguagem recebe novas funcionalidades através do ES6.

### Features do ES6

#### Destructuring
```javascript
const objetoTeste = {
    a: 10,
    b: 20,
    c: 30
}
const { a, b, c } = objetoTeste;
// equivalente:
// const teste = objetoTeste.a;
```

#### Palavras ‘const’ e ‘let’
Definição de constantes através do uso da palavra reservada 'const' e para criação variáveis e um determinado escopo utilizamos 'let'

```javascript
const a = 10;
let b = 20;
function foo(){
    let b = 30;
    console.log(a,b) // 10,30
}
foo();
console.log(a,b) // 10,20
```
#### Adição de arrow function
```javascript
const mult = (a, b) => {
    return a * b
}
mult(a,b)
```
#### Default parameters
```javascript
function foo(a=’10’){
    console.log(a)
}
foo();   // 10
foo(20); // 20
```
#### Spread Operator
```javascript
const carro = {
  marca: 'Ford',
  modelo: 'Mustang',
  cor: 'vermelho'
}
const carroAtualizado = {
  ...carro,
  cor: 'azul',
}
console.log(carroAtualizado)
 // {marca: "Ford", model: "Mustang", cor: "azul"}
```
#### String Template
Evitar usarmos operador '+' para concatenarmos strings e variáveis
```javascript
const carro = {
  marca: 'Ford',
  modelo: 'Mustang',
  cor: 'vermelho'
}

const a = `Meu carro é ${carro.modelo} dar cor: ${carro.cor}`
```
#### Class
Como as features trazidas pela implementação do ES6, agora temos um açucar sintático para a criação de classes através do uso da palavra 'class'

```javascript
class carro{
    constructor(name) {
        this.name = name;
    }
    getName() {
        return this.name;
    }
}
const carro = new Carro();
```
### Versões mais novas do js
as versões mais novas do javascript trouxeram algumas funcionalidade bem interessantes, por exemplo:
- ES8 async/await.
- ES10 flat() diminui os nives de uma matriz.
- ES11 Private Class Variables - #atributo para definição de atributos privados dentro de uma classe.

## JavaScript e assicronismo

Um conceito muito importante dentro do javascript é o que chamamos de async/await.

#### Simulando funções assíncronas
Exemplo de função que não são executadas em ordem de chamada.

```javascript 
function funcao1(){
    console.log('mostra função 1 instantaneamente'); 
}
function funcao2(){
    setTimeout(()=> {
    console.log('mostra função 2 depois de 7 segundos'); 
    }, 7000);
}
function funcao3(){
    setTimeout(()=> {
    console.log('mostra função 3 depois de 5 segundos'); 
    }, 5000);

}
funcao1();
funcao2();
funcao3();
```
#### Utilizando async/await
Para utilização de await precisamos criar um bloco de chamadas assíncronas utilizando async. Deste modo garantimos a ordem de execução conforme a chamada da função.
```javascript
function funcao1(){
    console.log(‘mostra função 1 instantaneamente’); 
}
function funcao2(){
    setTimeout(()=> {
    console.log(‘mostra função 2 depois de 7 segundos’); 
    }, 7000);
}
function funcao3(){
    setTimeout(()=> {
    console.log(‘mostra função 3 depois de 5 segundos’); 
    }, 5000);

}
async function blocoDeExecucao(){
await funcao1();
await funcao2();
await funcao3();
}
```
### NodeJs 
Criado por Ryan Dahl em 2008, é um software capaz de interpretar e executar código javascript.Baseado no interpretador V8 do Google Chrome também utiliza bibliotecas escritas em c/c++.

### Aplicabilidade do Javascript
- Backend (APIs com Nodejs, por exemplo)
- Frontend (Frameworks: React,Angular e Vue.)
- Html + css + js (Modelo mais antigo de desenvolvimento web.)
- Softwares Desktop (Utilizando Electron, exemplo o VS Code.)

### TypeScript
Criado pela Microsoft em 2012, é um superset da linguagem javascript. Adiciona tipagem a linguagem e melhorias na importação de bibliotecas. No final de tudo "transpilamos" o código pra javascript.

### Contexto atual e mercado
Conforme o site Stack Overflow em 2021. Javascript sem matem em uma das principais linguagens atualmente. <p>
<img src="https://github.com/LeiteRafael/mlp/blob/main/ranking.PNG" height=300> <p> 
Por último, podemos notar através de uma pesquisa no LinkedIn uma grande quantidade de vagas. <p>
<img src="https://github.com/LeiteRafael/mlp/blob/main/mercado.PNG" height=200> <

### Conclusão
A aplicabilidade do Javascript cada vez está se expandindo mais por ser uma linguagem multipardigma e sua curva de aprendizado é relativamente pequena.

Ao longo dos anos, novas features do JS atenderam às demandas para melhor desempenho na web que antes tinha apenas páginas estáticas, o que resultava em mais lentidão no tempo de resposta ao usuário no carregamento das páginas. Graças ao JavaScript, sites e aplicações se tornaram mais dinâmicos. Além disso, o número de frameworks vem crescendo ao longo do tempo e aceitação da linguagem crescendo.

                                                                                   
### Referências
- https://www.freecodecamp.org/portuguese/news/os-quatro-pilares-da-programacao-orientada-a-objetos-com-javascript/
- https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Array/map
- https://medium.com/@adsonrocha/heran%C3%A7a-de-classes-com-javascript-es6-cd577e567922
- https://medium.com/@nicolasbontempo/programando-javascript-orientado-a-objetos-87b1e98af6e4
- http://es6-features.org
- https://www.w3schools.com/js/js_es6.asp
- https://blog.rocketseat.com.br/as-melhores-features-do-es6-es7-e-es8/
