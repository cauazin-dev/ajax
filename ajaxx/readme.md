# Pesquisa Comparativa: XMLHttpRequest, Fetch, Promises e Async/Await

## Introdução

As APIs são conjuntos de regras e padrões que permitem que diferentes sistemas, aplicações ou partes de um programa se comuniquem entre si. Existe quatro formas de realizar requisições e manipular operações assíncronas em JavaScript, que são: **XMLHttpRequest**, **Fetch API**, **Promises** e **Async/Await**.  


---

## 1: XMLHttpRequest (XHR)

### O que é
O **XMLHttpRequest** (XHR) é uma API tradicional usada para enviar e receber dados de um servidor sem recarregar a página.  
Foi o método original utilizado no **AJAX** (Asynchronous JavaScript and XML).

### Vantagens:

Compatível com praticamente todos os navegadores, inclusive os mais antigos.

Permite controle detalhado da requisição (progresso, cabeçalhos, etc.).

### Desvantagens: 

Código mais complexo e difícil de ler.

Não utiliza Promises, dificultando o fluxo assíncrono.

Tratamento de erros é mais manual e verboso.
### Exemplo
```javascript
const xhr = new XMLHttpRequest();
xhr.open("GET", "dados.json", true);
xhr.onload = function() {
  if (xhr.status === 200) {
    console.log(xhr.responseText);
  }
};
xhr.send();

```
---
### 2: Fetch API
 
 ---
 ### O que é

A Fetch API é uma alternativa moderna ao XHR.
Ela utiliza Promises e fornece uma interface mais simples e intuitiva para realizar requisições HTTP.

 Exemplo
```Javascript 
fetch("dados.json")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error("Erro:", error));
```
 ### Vantagens

Sintaxe mais simples e moderna.

Baseada em Promises, o que facilita a leitura e o encadeamento.

Fácil integração com Async/Await.

### Desvantagens

Não lança erro automaticamente para status HTTP como 404.

Precisa de polyfill em navegadores antigos.

---

### 3: Promises
--- 
 ### O que é

As Promises representam uma operação assíncrona que pode estar em três estados: pendente (pending), resolvida (fulfilled) ou  rejeitada (rejected).

Foram introduzidas no ES6 (ECMAScript 2015) e servem como base para o Fetch e o Async/Await.

### Exemplo
``` Javascript
function buscarDados() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Dados recebidos!");
    }, 1000);
  });
}

buscarDados()
  .then(resultado => console.log(resultado))
  .catch(erro => console.error("Erro:", erro));
```
### Vantagens

Evitam o “callback hell”.

Tornam o código assíncrono mais legível.

Permitem melhor controle do fluxo com .then() e .catch().

### Desvantagens

Encadeamento excessivo pode deixar o código confuso.

Requer bom entendimento do funcionamento interno de Promises.

---
### 4: Async/Await
---
### O que é

O Async/Await é uma evolução das Promises, introduzido no ES8 (2017).
Permite escrever código assíncrono com aparência síncrona, tornando-o mais legível e fácil de manter.

### Exemplo
```Javascript
async function carregarDados() {
  try {
    const resposta = await fetch("dados.json");
    const dados = await resposta.json();
    console.log(dados);
  } catch (erro) {
    console.error("Erro na requisição:", erro);
  }
}

carregarDados();
```
### Vantagens

Sintaxe simples e limpa.

Tratamento de erros eficiente com try...catch.

Ideal para códigos modernos e de fácil manutenção.

### Desvantagens

Requer navegadores modernos.

Pode travar a thread principal se usado incorretamente com tarefas pesadas.