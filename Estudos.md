# ch02 

 // normalize url by removing querystring, optional trailing slash, and making it lowercase

 - const path = req.url.replace(/\/?(?:\?.*)?$/, '').toLowerCase()

 - http://localhost:3000/?foo=bar SERVIRÁ HOMEPAGE 


Node é adequado para projetos pequenos , para maiores usar o nginx ou uma cDN 


## servindo conteúdo estático : 
ch02\02-helloworld.js

Deve ser carregado pelo NODE (não serve automaticamente como nginx-apache...)


# ch03
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

# Ch05


## Quality Assurance  (QA)

Ferramentas de garantia de Qualidade de software 

## Lint 

- npm install --save-dev eslint

### Configuração: 

- ./node_modules/.bin/eslint --init

## Jest , Mocha, Jasmine, Ava, tape

- Install as dev dependence 
  - npm install --save-dev jest 

```
  "scripts": {
    "test": "jest",
    "lint": "eslint meadowlark.js lib"
  },
```

- Modo Watch (hotreload) dos tests 
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


