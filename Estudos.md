# ch02 

 // normalize url by removing querystring, optional trailing slash, and making it lowercase

 - const path = req.url.replace(/\/?(?:\?.*)?$/, '').toLowerCase()

 - http://localhost:3000/?foo=bar SERVIRÁ HOMEPAGE 


Node é adequado para projetos pequenos , para maiores usar o nginx ou uma cDN 


## servindo conteúdo estático : 
ch02\02-helloworld.js

Deve ser carregado pelo NODE (não serve automaticamente como nginx-apache...)


# ch03 Rotas 

A ordem das rotas no express é importante 
Scaffolding= Boilerplate
scaffolding do Node é o express-generator 

res.type('text/plain') /// define o cabeçalho do contentType alternativa ao res.writeHead

app.use((req, res) => {  /// usando o .use ao inves de .get o express adiciona middleware 

MVC  

- View: 
  - Pug - a engine converte pug (abstraçao HTML )para HTML 
  - HandleBars: mais parecida com html 
  - React


app.use(express.static(__dirname + '/public')) // permite distribuir recursos estáticos como imagens css ou JS 

# Ch05 Quality Assurance  (QA)

Ferramentas de garantia de Qualidade de software 

## Lint 

- npm install --save-dev eslint

ou instale globalmente 

### Configuração: 

- ./node_modules/.bin/eslint --init

Node: CommonJS 

Caso tenha Js do lado do cliente pode-se ter uma isntalação de lint separada (dois projetos distintos)

Problemas Jest x Lint :

Adicione ch05\.eslintrc.js

```
module.exports = {
    "env": {
        "commonjs": true,
        "es6": true,
        "node": true,
        "jest": true, /// resolve os problemas de jest com variaveis globais não definidas
    },
    "extends": "eslint:recommended",
    "globals": {
        "Atomics": "readonly",
        "SharedArrayBuffer": "readonly"
    },
    "parserOptions": {
        "ecmaVersion": 2018
    },
    "rules": {
      "no-console": "off",
    },
};
```

### Execução : 

npm run lint 

### Desativando um teste para uma linha 

// Express recognizes the error handler by way of its four argumetns, so we have to disable ESLint's no-unused-vars rule

/* eslint-disable no-unused-vars */
exports.serverError = (err, req, res, next) => res.render('500')
/* eslint-enable no-unused-vars */


## Jest , Mocha, Jasmine, Ava, tape

Install as dev dependence 

  - npm install --save-dev jest 

```
  "scripts": {
    "test": "jest",
    "lint": "eslint meadowlark.js lib"
  },
```

Modo Watch (hotreload) dos tests 

  - npm test -- --watch 

Alguns exemplos 

ch05\integration-tests\basic-navigation.test.js

ch05\lib\__tests__\handlers.test.js

### Code Coverage 

  - npm test -- --coverage

## Testes de integração 

Puppeteer : Versão headless ( navegador sem UI ) do Chrome 

- npm install --save-dev puppeter 
- npm install --save-dev portfinder


Testes feitos usando o id dos objetos para interação 

Testes são assincronos (await e promisse.all)

A aplicação precisa ser requerida como módulo caso executado 
diretamente pelo node um arquivo require.main será igual ao objeto global module


```
if(require.main === module) {
  app.listen(port, () => {
    console.log( `Express started on http://localhost:${port}` +
      '; press Ctrl-C to terminate.' )
  })
} else {
  module.exports = app
}
```

beforeEach  : faz no inicio de cada teste 

beforeAll: faz no inicio dos testes uma vez só (cuidado para um teste nao afetar o outro)

## Integração Contínua

Testes executados sempre que subimos um código 

- Travis CI, github, CircleCI, 

# Ch06 - Requisição e Resposta 

Protocolo - nome host - porta - path - querystring - fragmento

http:// - www.bing.com - :3000 - /search - ?q=grunt&first=9 - #q=express

## querystring - string de pesquisa - pares nome/valor
Devem ser codificados em URL encodeURIComponent (espaço vira +)

## fragmento 
Não é passado para o servidor, é de uso do navegador usado para controlar a aplicação ex: exibir uma parte do documento marcada por uma tag de ancora 

ex: <a id="chapter06">

## Rota para mostrar os headers das requisições 

```
app.get('/headers', (req, res) => {
  res.type('text/plain')
  const headers = Object.entries(req.headers)
    .map(([key, value]) => `${key}: ${value}`)
  res.send(headers.join('\n'))
})
```

- Segurança : 

Desativar o cabeçalho X-Powered-By para não revelar o 

## Tipos de mídia 

Content-type determina o tipo de conteudo servido 

tipo - subtipo - parametros opcionais 

text/html;charset=UTF-8

## Corpo 

GET não tem corpo e POST tem 

application/x-www-for-urlencoded  ( formato semelhante a querystring)

## Objeto de requisição 

accepts determina se o cliente aceitará um tipo especcífico 

secure retorna true se https

req. params, query,body, route,cookies/req.signedCookies, headers, accepts(types) , ip, path, hostname, xhr, protocol,  secure , req.url/req.originalUrl

## Objeto de resposta 

Cookie requer middleware 

end encerra a conexão sem enviar resposta 

type define Content-Type 

format : permite enviar diferentes conteudos dependendo de accept 


req. status(code), set(name,value), cookie(name,value,[options]), clearCookie(name, [options]), redirect([status],url), send(body), json(json), jsonp(json), end, type(type), format (object), attachment([filename]), download(path,[filename],[callback ]) 
sendFile(path, [options], [callback]), links(links), locals, render(view,[locals],callback)



## Formulários : 

Middleware de processamento 
const bodyParser = require('body-parser')

app.use(bodyParser.urlenconded({extended: false}))

