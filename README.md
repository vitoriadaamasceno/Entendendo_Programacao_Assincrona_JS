# Programação Assincrona JavaScript
Antes de entendermos o que seria a programação assincrona, vamos lembrar o que seria a programação sincrona:
>Programação sincrona a cada linha de codigo é executada de forma seguida na ordem que está escrito.
Sendo assim na programação assincrona as instruções são executadas indenpendente da ordem, ou seja,  o ato de executar uma tarefa em "segundo plano", sem nosso controle direto disso. Sem explicitamente trabalhar com threads e coordená-las. 
Quando enviamos uma requisição de dados a uma API, temos uma promessa de que estes dados irão chegar, mas enquanto isso não acontece, o sistema deve continuar rodando. Se, por exemplo, o servidor estiver caído, essa promessa de dados pode não se cumprir, e temos que lidar com isso. As Promises trabalham neste contexto - elas são a ferramenta que o JavaScript utiliza para lidar com código assíncrono.
Existem alguns tipos de metodos assincronos usados em JS ,são eles:
- Async/await
- Callbacks
- Promisses

## Async/await
O async/await também trabalha com o código assíncrono baseado em Promises, porém esconde as promessas para que a leitura e a escrita seja mais fluídas.
Definindo uma função como **async**, podemos utilizar a palavra-chave **await** antes de qualquer expressão que retorne uma promessa. Dessa forma, a execução da função externa (a função async) será pausada até que a Promise seja resolvida.
Exemplo
```
    let response = await fetch(`https://api.com/api/user/${userId}`);
    let userData = await response.json();
```
E para que esse await seja possivel o codigo deverá ser assim:

```
async function getUser(userId) {
    let response = await fetch(`https://api.com/api/user/${userId}`);
    let userData = await response.json();
    return userData.name;
}
```
**Lembrando que await só funciona se estiver dentro de outra função async. Caso não esteja, você ainda pode usar .then()**


## Promisses

