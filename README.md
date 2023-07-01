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
**Lembrando que await só funciona se estiver dentro de outra função async. Caso não esteja, você ainda pode usar .then().**


## Promisses
Promises têm um método chamado .then(), que recebe uma função callback e retorna um "objeto-promessa". Não é um retorno dos dados, é a promessa do retorno destes dados.Uma promise é um objeto retornado por uma função assíncrona, que representa o estado atual da operação. No momento em que a promise é retornada para quem à chamou, a operação muitas vezes ainda não foi finalizada, mas o objeto da promise oferece métodos para tratar o possível sucesso ou falha da operação.

Assim, podemos escrever o código do que irá acontecer em seguida, com os dados recebidos pela Promise, e o JavaScript vai aguardar a resolução da Promise sem pausar o fluxo do programa.

O resultado pode ou não estar pronto ainda, e não há forma de pegar o valor de uma Promise de modo síncrono; Só é possível requisitar à Promise que execute uma função quando o resultado estiver disponível - seja ele o que foi solicitado (os dados da API, por exemplo), ou uma mensagem de erro caso algo tenha dado errado com a requisição (o servidor pode estar fora do ar, por exemplo).

Exemplo
```
    function getUser(userId) {
     const userData = fetch(`https://api.com/api/user/${userId}`)
       .then(response => response.json())
       .then(data => console.log(data.name))
    }
    
    getUser(1); // "Nome Sobrenome"
```

Nesse caso a função getUser() recebe um id de usuário como parâmetro, para que seja passado para o endpoint REST fictício. A função fetch() recebe como parâmetro o endpoint e retorna uma Promise.

Além disso, as Promises contam também com diversos métodos, sendo o foco aqui o método then() e o método catch­(). O método then() possui dois argumentos, que também são funções callback resolve e reject. Enquanto o then() lida com ambos casos (tanto se a Promise for resolvida quanto rejeitada), o catch() lida apenas com casos de rejeição.

## Callbacks

Em JavaScript, funções são objetos. Podemos passar objetos para funções como parâmetros? Sim.

Então, nós podemos também passar funções como parâmetros para outras funções e chamá-las dentro das funções externas. Parece complicado? Vamos ver isso no exemplo abaixo:
```
    function print(callback) {  
        callback();
    }
```

A função print( ) recebe outra função como parâmetro e a chama dentro de si. Isso é válido no JavaScript e nós chamamos de "callback". Então, a função que é passada para outra função como um parâmetro é uma função de callback. 

Callbacks garantem que uma função não seja executada antes que uma tarefa seja concluída, mas logo depois dessa tarefa ser concluída. Elas nos ajudam a desenvolver código JavaScript assíncrono e evitam que tenhamos problemas e erros.

Em JavaScript, o jeito de criar uma função de callback é passá-la como um parâmetro para outra função, chamando-a novamente em seguida, logo depois que algo aconteça ou que alguma tarefa seja concluída.

Exemplo:
```
    function enviarEmail(corpo, para, callback){
        setTimeout(() =>{
            console.log(`
                Para: ${para}
                ----------------------
                ${corpo}
                ----------------------
                De: Victor Lima  
    
            `) 
            callback("ok",5,"8s")
    
        },8000)
    }
    console.log("inicio do email")
    enviarEmail("Olá Maria , bem vinda ao curso","maria.damasceno@gmail.com",(status,amount,time) => {
        console.log(`
        Status: ${status}
    
        Contatos: ${amount}
    
        Tempo de envio: ${time}
    
        `)
        console.log("Tudo ok")
    })
    console.log("Será enviado em breve!")

```
A saida desse exemplo será:

inicio do email

Será enviado em breve!

            Para: maria.damasceno@gmail.com
            ----------------------
            Olá Maria , bem vinda ao curso
            ----------------------
            De: Victor Lima  

        

    Status: ok

    Contatos: 5

    Tempo de envio: 8s

    
Tudo ok

Links para mais informações:

[Async/await](https://developer.mozilla.org/pt-BR/docs/conflicting/Learn/JavaScript/Asynchronous/Promises)

[Promisses](https://developer.mozilla.org/pt-BR/docs/Learn/JavaScript/Asynchronous/Promises)

[Callbacks](https://www.freecodecamp.org/portuguese/news/funcoes-de-callback-em-javascript-o-que-sao-e-como-usa-las/)
