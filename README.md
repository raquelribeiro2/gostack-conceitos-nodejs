# 🚀 Bootcamp GoStack 2020 - Projeto NodeJS

## Executar projeto do repositório

- Abra a pasta no editor de código de sua preferência e execute o comando ``` yarn ``` ou ``` npm install ``` para instalar as dependências. 
- Há um arquivo Insomnia anexado ao projeto, importe-o e utilize-o para fazer os testes necessários. 

# Conteúdo aprendido neste módulo

## Conceitos NodeJS

### O que é NodeJS?

- Utiliza a linguagem Javascript no back-end;
    - Não lidamos com eventos do usuário final;
    - Rotas e integrações;
- O Node é uma plataforma, não uma linguagem;
- Construída em cima do motor V8 do Chrome;

## Criando projeto Node

- Crie uma pasta com o nome que desejar, abra-a e execute o seguinte comando:

```jsx
$ yarn init -y
```
- Este comando criará o arquivo *package.json*

### Instalação do Express

- O Express é um micro framework, um conjunto de ferramentas pro Node.
- Ele dá disponibilidade de incluir e gerenciar as rotas na aplicação, além de gerenciar também os middlewares.
- Para instalá-lo, basta executar:

```jsx
$ yarn add express
```

### Request

- Guarda as informações da requisição que o usuário fez, por exemplo, qual a rota que o usuário está utilizando, os parâmetros passados através dessa rota.

### Response

- Tem as informações disponíveis para retornar respostas pro usuário.

### Arquivo index.js

```jsx
const express = require('express');

const app = express();

// Inserção da rota através do método GET com retorno de uma mensagem como resposta
app.get('/', (req, res) => {
  return res.json({ message: 'Olá!' });
});

// Porta em que o back-end está sendo executado, com mensagem de sucesso para o dev
app.listen(3333, () => {
  console.log('Back-end started!')
});
```

## Nodemon

### Instalação do Nodemon

- Ferramenta que faz a reinicialização automática do servidor, toda vez que o Node detecta uma atualização no código.
- Para instalá-lo basta executar:

```jsx
$ yarn add nodemon -D
```

### Configuração Nodemon

- Vá até o arquivo package.json:

```json
{
  "name": "backend",
  "version": "1.0.0",
Coloque o caminho da pasta da inicialização em main (principal)
  "main": "src/index.js",
  "license": "MIT",
Adicione os scripts e o comando dev, que usará para iniciar o servidor.
O Nodemon buscará automaticamente o comando main para iniciar o servidor.
  "scripts": {
    "dev": "nodemon"
  },
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.4"
  }
}
```

## Métodos HTTP

### GET

- Buscar uma ou mais informações no back-end.

### POST

- Criar uma informação no back-end.

### PUT/PATCH

- **PUT**
    - Altera várias informações no back-end.

- **PATCH**
    - Altera uma informação específica no back-end, como por exemplo, somente o avatar.

### DELETE

- Deletar uma informação no bask-end.

## Criação das rotas

```jsx
const express = require('express');

const app = express();

// Inserção da rota através do método GET com retorno de uma mensagem como resposta;
// O nome que vem logo após a '/' é chamado de recurso, pois se refere a qual recurso
// o usuário quer acessar. Por exemplo, o recurso Projects ('/projects').
app.get('/projects', (req, res) => {
  return res.json([
	'Projeto 1',
	'Projeto 2',
	]);
});

app.post('/projects', (req, res) => {
  return res.json([
	'Projeyo 1',
	'Projeto 2',
	'Projeto 3',
	]);
});

app.put('/projects/:id', (req, res) => {
  return res.json([
    'Projeto 4',
    'Projeto 2',
    'Projeto 3',
  ]);
})

app.delete('/projects/:id', (req, res) => {
  return res.json([
    'Projeto 2',
    'Projeto 3',
  ]);
})

// Porta em que o back-end está sendo executado, com mensagem de sucesso para o dev.
app.listen(3333, () => {
  console.log('Back-end started!')
});
```

## Tipos de Parâmetros

- São formas do front-end que está requisitando as rotas da aplicação, enviar algum tipo de informação.

### Query Params

- Será utilizado para filtros e paginação.
- Utilizados normalmente em parâmetros GET.
- Para utilizar uma Query Params basta adicionar um "?" após o recurso na rota e passar o parâmetro, como o exemplo abaixo.
- Também pode ser adicionado mais de um parâmetro e para isso, é só adicionar o "&".

```jsx
/projects?title=React&owner=Raquel
```

- No Insomnia, há uma aba para colocar Query Params.
- E o próprio Insomnia te mostra a preview de como ficará a URL, como mostrado abaixo:

![image](https://user-images.githubusercontent.com/57918707/93836632-bf4ced00-fc59-11ea-8694-d569e13d3efa.png)

- No VSCode já podemos passar esses parâmetros:

```jsx
app.get('/projects', (req, res) => {
// O que está dentro de req.query (request.query) é o que foi adicionado no Insomnia
  const { title, owner } = req.query;

  console.log(title);
  console.log(owner);

  return res.json([
    'Projeto 1',
    'Projeto 2',
  ]);
});
```

- Quando enviar a requisição no Insomnia, aparecerá a resposta no console, das informações separadas, pois os parâmetros estão desestruturados.

![image](https://user-images.githubusercontent.com/57918707/93836660-dbe92500-fc59-11ea-9c5d-aa5d8ad015ba.png)

### Route Params

- Será utilizado para identificar recursos quando quiser Atualizar e Deletar.
- Para utilizar uma Route Params basta adicionar ":" **+** o nome do parâmetro após a "/":

```jsx
/projects/:id
```

- No Insomnia, esse parâmetro é passado diretamente pela URL, tanto no método PUT quanto no método DELETE:

![image](https://user-images.githubusercontent.com/57918707/93836705-fd4a1100-fc59-11ea-8ab7-d4fc855738ef.png)

![image](https://user-images.githubusercontent.com/57918707/93836720-06d37900-fc5a-11ea-8dd4-36166ce41880.png)

- No VSCode ficará:

```jsx
app.put('/projects/:id', (req, res) => {
  const { id } = req.params;

  console.log(id);

  return res.json([
    'Projeto 4',
    'Projeto 2',
    'Projeto 3',
  ]);
})

app.delete('/projects/:id', (req, res) => {
  const { id } = req.params;

  console.log(id);
  
  return res.json([
    'Projeto 2',
    'Projeto 3',
  ]);
})
```

- Quando enviar a requisição no Insomnia, aparecerá a resposta no console, das informações separadas, pois o parâmetro está desestruturado.
- Update e Delete, respectivamente:

![image](https://user-images.githubusercontent.com/57918707/93836771-28ccfb80-fc5a-11ea-8a81-41ba2f53d301.png)

### Request Body

- Este é o conteúdo para criar ou editar um recurso.
- Essas informações são passadas através de JSON.
- No Insomnia, será selecionado em Body o tipo JSON e será passada a seguinte informação:

![image](https://user-images.githubusercontent.com/57918707/93836805-3e422580-fc5a-11ea-9063-cf76ac322f8e.png)

- No VSCode ficará da seguinte forma:

```jsx
app.post('/projects', (req, res) => {

  const body = req.body;

  console.log(body);
  
  return res.json([
    'Projeto 1',
    'Projeto 2',
    'Projeto 3',
  ]);
})
```

- Porém, a resposta no console será undefined:

![image](https://user-images.githubusercontent.com/57918707/93836824-5023c880-fc5a-11ea-9fcf-d3413cf1d7be.png)

- Isso ocorre porque, por padrão, o Express não interpreta o que é enviado através de JSON.
- Para que ele entenda, basta adicionar no começo do código a seguinte linha:

  

```jsx
const express = require('express');

const app = express();

app.use(express.json()); // adicione esta linha
```

- O *use* é usado quando queremos adicionar algum tipo de função, onde todas as rotas terão que passar por ela, no caso, a função *express.json()*.
- Feito isso, obteremos a seguinte resposta no console:

![image](https://user-images.githubusercontent.com/57918707/93836843-6598f280-fc5a-11ea-8be8-488364ca5625.png)

- Se desestruturar os parâmetros, a resposta ficará da seguinte forma:

![image](https://user-images.githubusercontent.com/57918707/93836880-7e090d00-fc5a-11ea-8381-159790aa23dd.png)

## Aplicação Funcional

- Para começar, vamos instalar e importar a seguinte biblioteca.

### Biblioteca uuidv4

```jsx
$ yarn add uuidv4
```

### Importar função

```jsx
const { uuid } = require('uuidv4');
```

- Essa função irá criar um Universal Unique ID.

### Rotas GET e POST

```jsx
const express = require('express');
const { uuid } = require('uuidv4');

const app = express();

app.use(express.json());

// Foi criada a variável projects que recebe um array vazio;
// Este array está na memória volátil, então caso o programa seja fechado ou
// reiniciado, por exemplo, as informações serão perdidas.
const projects = []; 

app.get('/projects', (req, res) => {
  // const { title, owner } = req.query;

  // console.log(title);
  // console.log(owner);

	// Retornará todos os projetos contidos no array.
  return res.json(projects);
});

app.post('/projects', (req, res) => {
  const { title, owner } = req.body;

  const project = { id: uuid(), title, owner };

	// O push faz a inserção dos dados de project no array products
  projects.push(project);
  
	// Sempre retornar o último valor inserido, nunca a lista toda
  return res.json(project);
})
```

- Depois de salvo, quando rodar a requisição de criação no Insomnia, obterá o seguinte resultado:

![image](https://user-images.githubusercontent.com/57918707/93836919-a7c23400-fc5a-11ea-89c3-ebdac6053a0a.png)

- A requisição List deverá listar essa informação que acabamos de criar:

![image](https://user-images.githubusercontent.com/57918707/93836938-bc9ec780-fc5a-11ea-9f68-49bdf669e19d.png)

### Rota PUT

```jsx
app.put('/projects/:id', (req, res) => {
  const { id } = req.params;
	const { title, owner } = req.body;

// A variável projectIndex faz sentido com a função findIndex, pois eu irei 
// armazenar na variável, o índice (index) ou a posição do projeto encontrado 
// dentro do array
// Eu irei percorrer todo o meu array de projects, onde para cada project
// farei a comparação de index (id) igual a id.
  const projectIndex = projects.findIndex(project => project.id === id);

// Se esse meu índex for menor que 0, ou seja, não encontrar nenhum registro,
// retornará o erro abaixo
  if (projectIndex < 0) {
    return res.status(400).json({ error: 'Project not found' });
  }

	const project = {
    id,
    title,
    owner,
  }
	
// Vou no meu array de projects, procurar na posição projectIndex e substituir o 
// valor que está dentro dessa posição pelo valor que acabei de criar, project.
projects[projectIndex] = project;

  return res.json(project);
})
```

- Caso não encontre, o Insomnia retornará a seguinte mensagem, pois o ID 1 não existe:

![image](https://user-images.githubusercontent.com/57918707/93836967-d3451e80-fc5a-11ea-879e-12e655dcce04.png)

- Criei o seguinte projeto:

![image](https://user-images.githubusercontent.com/57918707/93836991-e8ba4880-fc5a-11ea-988c-28118857a114.png)

- Adicionei o ID na rota, troquei a informação desejada, e a requisição foi enviada com sucesso:

![image](https://user-images.githubusercontent.com/57918707/93837001-f1ab1a00-fc5a-11ea-9db8-f508620bc12a.png)

### Rota DELETE

```jsx
app.delete('/projects/:id', (req, res) => {
  const { id } = req.params;

  const projectIndex = projects.findIndex(project => project.id === id);

  if (projectIndex < 0) {
    return res.status(400).json({ error: 'Project not found' });
  }

// Vou percorrer meu array de projects, e usar a função splice, que serve para
// retirar informações contidas num array
// Aí passo qual é o índice que eu quero remover (projectIndex)
// e quantas posições eu quero remover à partir desse índice, no caso, 1, 
// que é apenas a informação contida neste índice (projectIndex)
  projects.splice(projectIndex, 1);

  return res.status(204).send();
})
```

- Como resposta no Insomnia, após colocar o ID existente na URL, aparecerá o status 204 - No Content, ou seja, sem conteúdo:

![image](https://user-images.githubusercontent.com/57918707/93837026-0f787f00-fc5b-11ea-83d0-177731944e9b.png)

- Para confirmar que foi deletado com sucesso, vá até a lista e envie a requisição, seu array estará vazio novamente:

![image](https://user-images.githubusercontent.com/57918707/93837034-18695080-fc5b-11ea-9e2d-f16f987ddeac.png)

### Adicionando filtro à rota de GET

```jsx
app.get('/projects', (req, res) => {
  const { title } = req.query;

// Crio a variável results, e irei verificar se o title foi preenchido pelo usuário
  const results = title

// Se o title foi preenchido pelo usuário, a variável results será preenchida com
// projects.filter, ou seja, vou pegar meus projetos e filtrar
// Para cada um dos projetos, eu vou verificar se no título (title) do projeto
// inclui (includes, que retorna true ou false) a palavra que está dentro do title
// O includes verifica se o texto title está contido no texto project.title
    ? projects.filter(project => project.title.includes(title))

// Se for vazio, retorna todos os projetos, pois não foi adicionado nenhum filtro
    : projects;

// Se encontrar, retorna os resultados encontrados
  return res.json(results);
});
```

- Resposta com o filtro habilitado:

![image](https://user-images.githubusercontent.com/57918707/93837063-31720180-fc5b-11ea-95ac-1f231b41e3cb.png)

- Resposta com o filtro desabilitado:

![image](https://user-images.githubusercontent.com/57918707/93837093-48b0ef00-fc5b-11ea-823c-492eaa9b4106.png)

## Middlewares

- Interceptador de requisições, que pode interromper totalmente a requisição ou alterar dados da requisição.
- Ele vai agir enquanto as requisições estão chegando e ele pode mudar dados dessa requisição antes da resposta ser retornada pro usuário.
- Todas as rotas podem ser consideradas middlewares,

```jsx
app.get('/projects', (req, res) => {
// pois elas interceptam a requisição:
  const { title } = req.query;

// pegam os dados da requisição
  const results = title
    ? projects.filter(project => project.title.includes(title))
    : projects;

// e podem interromper, retornar uma resposta para o usuário
  return res.json(results);
});
```

- O formato de um middleware é uma função:

```jsx
// Essa função sempre irá receber como primeiro parâmetro a requisição (request)
// como segundo parâmetro, a resposta (response)
// e como terceiro parâmetro, o next
function logRequests(req, res, next) {
// Buscar dentro do request, o método que está sendo chamado (get, post, put, delete)
// e qual é a rota (url) que está sendo chamada de dentro da aplicação
	const { method, url } = request;

// converter o método para Upper Case, ou seja, caixa alta
	const logLabel = `[${method.toUpperCase()}] ${url}`;
	
	console.log(logLabel);
}
```

- Utilizamos os middlewares quando queremos que algum trecho de código seja disparado de forma automática em uma ou mais rotas da nossa aplicação.
- No caso acima, o middleware será disparado de forma automática em todas as requisições para mostrar no console qual é a rota que está sendo chamada pelo Insominia.
- Após enviar a requisição no Insomnia, tivemos a seguinte resposta:

![image](https://user-images.githubusercontent.com/57918707/93837126-641bfa00-fc5b-11ea-8c3e-4f7f81fcfe25.png)

- A minha rota de projetos não retornou nada no Insomnia, ficou rodando eternamente.
- Neste caso, a requisição foi interrompida totalmente, pois não chamamos o parâmetro *next*.
- Se este parâmetro não for chamado, o próximo middleware, que no caso é a rota GET, não será disparado, pois o fluxo do Node é linear.

```jsx
// Início da aplicação

const express = require('express');
const { uuid } = require('uuidv4');

const app = express();

// Usuário fez uma requisição 
// Após requisição passou por este middleware, express.json
// O express.json converteu o corpo da requisição de JSON para um objeto que a 
// gente consegue entender na aplicação
app.use(express.json());

const projects = [];

function logRequests(req, res, next) {
  const { method, url } = req;

  const logLabel = `[${method.toUpperCase()}] ${url}`;
  
  console.log(logLabel);

// Adicione, para a leitura continuar sendo feita
  return next(); 
}

// Depois, a primeira coisa lida foi o app.use(logRequests) que chamou a função acima
// Se não houver o next(), a leitura não continua para o próximo middleware
app.use(logRequests);

// Próximo middleware
app.get('/projects', (req, res) => {
  const { title } = req.query;

  const results = title
    ? projects.filter(project => project.title.includes(title))
    : projects;

  return res.json(results);
});

app.post('/projects', (req, res) => {
  const { title, owner } = req.body;

  const project = { id: uuid(), title, owner };

  projects.push(project);

  return res.json(project);
})

app.put('/projects/:id', (req, res) => {
  const { id } = req.params;
  const { title, owner } = req.body;

  const projectIndex = projects.findIndex(project => project.id === id);

  if (projectIndex < 0) {
    return res.status(400).json({ error: 'Project not found' });
  }

  const project = {
    id,
    title,
    owner,
  }

  return res.json(project);
})

app.delete('/projects/:id', (req, res) => {
  const { id } = req.params;

  const projectIndex = projects.findIndex(project => project.id === id);

  if (projectIndex < 0) {
    return res.status(400).json({ error: 'Project not found' });
  }

  projects.splice(projectIndex, 1);

  return res.status(204).send();
})

app.listen(3333, () => {
  console.log('Back-end started!')
});
```

- Com o *next()* adicionado, obteremos as respostas no console:

![image](https://user-images.githubusercontent.com/57918707/93837157-7f870500-fc5b-11ea-9293-1913e1b74aa6.png)

## Aplicando middleware apenas na rota de listagem

```jsx
const express = require('express');
const { uuid } = require('uuidv4');

const app = express();

app.use(express.json());

const projects = [];

function logRequests(req, res, next) {
  const { method, url } = req;

  const logLabel = `[${method.toUpperCase()}] ${url}`;
  
  console.log(logLabel);

  return next();
}

// app.use(logRequests);

// Podem ser adicionados quantos middlewares quiser, separados por vígulas
// Eles serão executados em ordem
app.get('/projects', logRequests, (req, res) => {
  const { title } = req.query;

  const results = title
    ? projects.filter(project => project.title.includes(title))
    : projects;

  return res.json(results);
});

app.post('/projects', (req, res) => {
  const { title, owner } = req.body;

  const project = { id: uuid(), title, owner };

  projects.push(project);

  return res.json(project);
})
```

- Isso fará com que a função seja chamada somente no método GET, enviando a resposta no console somente para este método.

![image](https://user-images.githubusercontent.com/57918707/93837192-94639880-fc5b-11ea-8cce-09221c3e6048.png)

## Middleware após o next()

```jsx
const express = require('express');
const { uuid } = require('uuidv4');

const app = express();

app.use(express.json());

const projects = [];

function logRequests(req, res, next) {
  const { method, url } = req;

  const logLabel = `[${method.toUpperCase()}] ${url}`;
  
  console.log('1');
// mede o tempo da requisição no início
  console.time(logLabel);

  next();

  console.log('2');

// ao fim
  console.timeEnd(logLabel);
}

app.use(logRequests);

app.get('/projects', (req, res) => {
  console.log('3');
  
  const { title } = req.query;

  const results = title
    ? projects.filter(project => project.title.includes(title))
    : projects;

  return res.json(results);
});
```

- Colocando os *console.log()*, percebemos a ordem das requisições e o tempo:

![image](https://user-images.githubusercontent.com/57918707/93837213-a80eff00-fc5b-11ea-862e-9073afdfa47a.png)

- Percebemos que após o *next()*, ele executa o middleware da rota GET e somente depois volta ao *console.log('2')*.
- Os middlewares são muito utilizados para validação, quando quero verificar se o dado que o usuário tá me enviando está no formato correto.

```jsx
const express = require('express');
// Na função isUuid é passada uma string e ela retorna se é um ID válido ou não 
const { uuid, isUuid } = require('uuidv4');

const app = express();

app.use(express.json());

const projects = [];
// Será utilizada para validar se o id que está sendo enviado para o projeto
// tanto na rota put quanto na delete, é um id válido
function validateProjectId(req, res, next) {
// pega o ID (route params) que vem através da nossa rota put ou delete
  const { id } = req.params;

// Se não for um ID válido, retorna o erro
	if (!isUuid(id)) {
    return res.status(400).json({ error: 'Invalid project ID.' });
  }

// Se for válido, vai para o próximo middleware
  return next();
}

// A chamada do middleware se dá com uma parte da rota, como primeiro parâmetro
// E como segundo parâmetro, a função.
app.use('/projects/:id', validateProjectId);
```
