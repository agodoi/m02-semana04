# Horário de Atendimento do Professor

* Terças e quintas das 8h às 16h podem contar comigo!
* Demais dias da semana, estou no Slack, com tempo de respostas no mesmo dia.

# Horário de Atendimento do Monitor

* Segunda: 8h30 às 10h
* Quarta: 8h30 às 10h
* Sexta: 8h30 às 9h30

# Resumo de Conceitos dos Autoestudos

# Back-end I - Node.js, models e controllers

Agora que temos o banco de dados pronto, bora contruir **aplicação servidor**, ou seja, o back-end. 

Nesta instrução, praticaremos a construção de aplicações utilizando o Node.js, relacionando com o banco de dados, produzindo os primeiros pontos de contato com o mundo lá fora - os endpoints de uma WebAPI. Tudo isso sob a arquitetura MVC!


## Conceitos de Node.js

* Node.js é um ambiente de executar comandos **JavaScript** para fora do navegador;
* É um ambiente assíncrono e baseado em eventos;
	*  Execuções de forma não sequencial e não bloqueante, permitindo que o programa continue sua execução enquanto aguarda a conclusão de operações assíncronas, como operações de entrada/saída (I/O), chamadas de rede, ou outras operações que podem levar tempo para serem concluídas.
 	* É single-threaded, que significa que não precisa de mult-threaded para lidar com escalonamentos. Uma thread é uma programação concorrente e paralela, processamento de tarefas em segundo plano.
* O Node.js possui um conceito chamado **Event Loop** que:
	* Faz execuções de assíncronas;
 	* Operações de entradas e saídas de dados são assíncronos;
  	* Gerencia fila de eventos de forma eficiente, executando-os ordenadamente;
  	* É bão na tolerância de falhas, mantendo sua aplicação em execução.

## Módulos e pacotes do Node.js

* npm --> gerenciador de pacotes que dá acesso ao repositório do Node.js com milhares de arquivos
* requeire ( ) --> usado para importar módulos no Node.js
* package.js --> usado para gerenciar as dependências da sua aplicação

### Arquitetura Node.js vs Arquitetura Tradicional

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana04/blob/main/imgs/arquiteturaNodeJS.png">
   <img alt="DataStores" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana04/blob/main/imgs/arquiteturaNodeJS.png)">
</picture>


## No seu projeto

O Node.js será o **interpretador** (e não compilador) do seu JS fora do navegador e suportará o funcionamento da rede (Internet) para você chegar até o seu banco de dados. Como o Node.js é assíncrono, você pode fazer vários INSERT ou SELECT de "forma paralela" mas sem ser paralela.

E o Sails? É um framework web MVC (Model-View-Controller) para Node.js, projetado para facilitar o desenvolvimento de aplicativos web modernos e escaláveis.

Conclusão:

* Em 1º preciso do Node.js
	* Em 2º vem o Sails
 		* **api/controller** --> local onde você colocar as regras de negócio: buscar, criar, atualizar ou excluir dados.
   		* **api/models** --> local das suas tabelas
   		* **views** --> local do HTML + CSS + JS



## Kahoot


## Etapa 1 - Criando um novo projeto Sails

a) Abra o terminal e navegue até o diretório onde deseja criar o projeto.
   
b) Execute o comando **sails new nome-projeto**.
   - Este comando criará um novo projeto Sails com o nome especificado.
     
c) Quando solicitado a escolher um modelo, selecione a opção **2 - Empty**.
   - Isso criará um projeto vazio sem qualquer configuração pré-definida.

d) Ainda no terminal, entre na pasta recém criada do projeto e digite **code .** para carregar o projeto inteiro no Visual Code.

## Quais as pastas importantes?

* api
   * controllers

* api
   * models

* config
   * datastore.js

* config
   * models.js 

* config
   * routes.js

* views
   * pastas que você irá criar (nesse caso será **mypages**)

* package.json (penúltimo arquivo)

## Etapa 2 - Configurando o datastores.js

a) Vá na seguinte pasta do seu projeto Sails:
* **Config**
	* **datastores.js** (são as suas conexões de qualquer banco, tipo MySQL, PostgreSQL, etc)
 		* **linha 51** onde tem ```// adapter: 'sails-mysql',```, **apague** e substitua por ```adapter: 'sails-postgresql',``` sem as // barras
   		* **linha 52** adicione a sua URL do seu Render como assim ```url: 'postgres://bdgodoi_user:ZmTVzKJXGWyB65nRGeW7S2AkMUEI3gZ1@dpg-cojpieu3e1ms73bflb6g-a.oregon-postgres.render.com/bdgodoi',```
       		* **linha 53** adicione ```ssl: true```

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_datastores.png">
   <img alt="DataStores" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_datastores.png)">
</picture>

## Etapa 3 - Configure o package.json

a) Busque pelo arquivo **package.json** (penúltimo arquivo do menu vertical da esquerda). Aí dentro tem todas as dependências. Como estamos trabalhando com o **PostgreSQL**, não há pacotes default para ele. Então temos que instalar manualmente. 

b) Para instalar a biblioteca do **PostgreSQL** no seu projeto, digite esse comando **dentro da pasta do seu projeto** usando o terminal ```npm install sails-postgresql```. Quando terminar, vá no arquivo **package.json** que você vai encontrar o que a seta vermelha está apontando.

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_com_postgresql.png">
   <img alt="Desespero" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana03b/blob/main/imgs/sails_com_postgresql.png)">
</picture>

Caso queira acessar a documentação [https://www.npmjs.com/package/sails-postgresql](https://www.npmjs.com/package/sails-postgresql).

## Etapa 4 - Testando a conexão

No terminal, dê um ```sails lift``` na mesma pasta do seu projeto.

Caso apareça as velas, isto é, sails, sucesso na conexão!!! Se você for no seu DBeaver e conferir o que está no seu banco de dados, vai notar que não mudou nada em suas tabelas porque até o momento não criamos nenhum **model** novo nesse projeto.

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana04/blob/main/imgs/velaOk.png">
   <img alt="Velas" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana04/blob/main/imgs/velaOk.png)">
</picture>
 

## Etapa 5 - Criando um model (tabela)

a) No seu terminal, dê um **Ctrl+C** e dentro da pasta do projeto, digite ```sails generate model Heroe``` (enter). Ele vai criar um arquivo chamado **Heroe** no modelo Sails na pasta **\api\models**. Você poderia criar um arquivo manualmente **Heroe.js** sem problemas com o botão direito do mouse.

b) Confira em **api/models** se seu arquivo **Heroe.js** foi criado e pode deletar o arquivo **.gitkeep**. Não vamos utilizá-lo. Esse arquivo aparece para manter a pasta não-vazia.

c) Copie e cole esse código dentro do **api/models/Heroe.js**
```
/**
 * MyTable.js
 *
 * @description :: A model definition represents a database table/collection.
 * @docs        :: https://sailsjs.com/docs/concepts/models-and-orm/models
 */

module.exports = {
tableName: "heroe",
  attributes: {
    cpf: {
      type: "string", //pode ter string, bool, float e number
      required: true, //signica que é not null
    },
    name: {
      type: "string",
      required: true, //signica que é not null
    },
    last_name: {
      type: "string",
      required: true,
    },
    age: {
      type: "string",
      required: true,
    },
    status: {
      type: "string",
      required: true,
    },
    type: {
      type: "string",
      defaultsTo: "others", //se passar NULL, automaticamente preencha com "others"
    },
  },
};
```
d) Os desenhos Sails que estão em forma de comentários, você pode apagar.

e) Depois, digite ```sails lift``` no terminal e dentro da pasta do seu projeto;

f) O prompt vai te perguntar se você quer trabalhar como:

**1) FOR DEV**	--> 	faz *alter* (adiciona dados), cria tabelas, mas não deleta colunas

**2) TESTS**	--> 	faz *drop*, zera tudo em cascata (devido à primary key e foreing key) e recomeça a tabela.

**3) STAGING** 	--> 	é para quando você está em **produção**, pois ele não altera o banco. Trabalhar em **produção** é quando usuários reais utilizam seu projeto.


Escolha a opção **1) FOR DEV**. 

g) Aguarde o aparecimento da Vela do Sails no seu terminal e vá no seu DBeaver e confira se subiu a nova tabela.

Se tudo correu bem, você terá em seu Dbeaver algo assim como na figura:

<picture>
   <source media="(prefers-color-scheme: light)" srcset="https://github.com/agodoi/m02-semana04/blob/main/imgs/dbeaver_ok.png">
   <img alt="DBeaver OK!" src="[YOUR-DEFAULT-IMAGE](https://github.com/agodoi/m02-semana04/blob/main/imgs/dbeaver_ok.png)">
</picture>


# Etapa 6 - Ajustando o pai dos Models

a) Vá no arquivo config/models.js e cole essa atualização. Ela serve para deixar todos os seus models já com os atributos **createdAt: { type: 'number', autoCreatedAt: true, }, updatedAt: { type: 'number', autoUpdatedAt: true, } e id: { type: 'number', autoIncrement: true, },**

```
/**
 * Default model settings
 * (sails.config.models)
 *
 * Your default, project-wide model settings. Can also be overridden on a
 * per-model basis by setting a top-level properties in the model definition.
 *
 * For details about all available model settings, see:
 * https://sailsjs.com/config/models
 *
 * For more general background on Sails model settings, and how to configure
 * them on a project-wide or per-model basis, see:
 * https://sailsjs.com/docs/concepts/models-and-orm/model-settings
 */

module.exports.models = {


  /***************************************************************************
  *                                                                          *
  * Whether model methods like `.create()` and `.update()` should ignore     *
  * (and refuse to persist) unrecognized data-- i.e. properties other than   *
  * those explicitly defined by attributes in the model definition.          *
  *                                                                          *
  * To ease future maintenance of your code base, it is usually a good idea  *
  * to set this to `true`.                                                   *
  *                                                                          *
  * > Note that `schema: false` is not supported by every database.          *
  * > For example, if you are using a SQL database, then relevant models     *
  * > are always effectively `schema: true`.  And if no `schema` setting is  *
  * > provided whatsoever, the behavior is left up to the database adapter.  *
  * >                                                                        *
  * > For more info, see:                                                    *
  * > https://sailsjs.com/docs/concepts/orm/model-settings#?schema           *
  *                                                                          *
  ***************************************************************************/

  schema: true,


  /***************************************************************************
  *                                                                          *
  * How and whether Sails will attempt to automatically rebuild the          *
  * tables/collections/etc. in your schema.                                  *
  *                                                                          *
  * > Note that, when running in a production environment, this will be      *
  * > automatically set to `migrate: 'safe'`, no matter what you configure   *
  * > here.  This is a failsafe to prevent Sails from accidentally running   *
  * > auto-migrations on your production database.                           *
  * >                                                                        *
  * > For more info, see:                                                    *
  * > https://sailsjs.com/docs/concepts/orm/model-settings#?migrate          *
  *                                                                          *
  ***************************************************************************/

  migrate: 'drop',


  /***************************************************************************
  *                                                                          *
  * Base attributes that are included in all of your models by default.      *
  * By convention, this is your primary key attribute (`id`), as well as two *
  * other timestamp attributes for tracking when records were last created   *
  * or updated.                                                              *
  *                                                                          *
  * > For more info, see:                                                    *
  * > https://sailsjs.com/docs/concepts/orm/model-settings#?attributes       *
  *                                                                          *
  ***************************************************************************/

  attributes: {
    createdAt: { type: 'number', autoCreatedAt: true, },
    updatedAt: { type: 'number', autoUpdatedAt: true, },
    id: { type: 'number', autoIncrement: true, },
  },

  dataEncryptionKeys: {
    default: 'Ts8sNZeopBy8tvyP4C3Ntmz9T3Y3NK7g5sitCe7M9nk='
  },

  cascadeOnDestroy: true

};

```

## Etapa 7 - Criando um controller

a) Vá no seu terminal, dentro da pasta do projeto, e se você não estiver vendo o path do seu projeto, dê um **Ctrl+C**;

b) Digite ```sails generate controller HeroesController``` (nome do controller sempre no plural como boas práticas);

Deve aparecer essa mensagem: **info: Created a new controller ("HeroesController") at api/controllers/HeroesControllerController.js!**

E se você for em **api/controller** verá um novo arquivo **HeroesController.js**.

c) Note que cada arquivo gerado no Sails possui um help [https://sailsjs.com/docs/concepts/actions](https://sailsjs.com/docs/concepts/actions) onde você poderá explorar todas as opções do Sails. Nesse help você fica sabendo as ações possíveis dentro do Controller.

d) Copie esse código e cole no seu **api/controller/HeroesController.js**. Mas antes, apague tudo o que está no api/controller/HeroesController.js.

```
/**
 * HeroesController
 *
 * @description :: Server-side actions for handling incoming requests.
 * @help        :: See https://sailsjs.com/docs/concepts/actions
 */

module.exports = {
  create: async function(req, res){
     Heroe.create(req.body)
        .fetch()
        .exec(function(err){
            if(err) return (err);
            return res.json({ sucess: "Parabéns! Seu herói foi criada." });
    });
  },

  getALL: async function(req, res){
    Heroe.find().exec(function(err,tasks){
        if(err) return res.severError(err);
        return res.json(tasks);
    });
  },

  getById: async function(req, res){
    Heroe.findOne({ id: req.params.id }).exec(function(errs, task){
        if(err) return res.serverError(err);
        if(!task) return res.notFound();
        return res.json(task);  
    });
  },

  update: async function (req,res){
    Heroe.update({ id: req.params.id }, req.body).exec(function(err) {
        if(err) return res.serverError(err);
        return res.json({message: "Herói atualizado com sucesso."});
    });
  },

  delete: async function (req,res){
    Heroe.destroy({ id: req.params.id }, req.body).exec(function(err) {
        if(err) return res.serverError(err);
        return res.json({message: "Herói apagado com sucesso."});
    });
  },
};
```


## Etapa 8 - Configurando routes.js

Esse arquivo serve para configurar as rotas. 

Por exemplo, se você digitar no seu navegador **http://localhost:1337/** ele vai mandar carregar alguma homepage com a simples **/**.

```
'/': { view: 'pages/homepage' },
```

Outro exemplo: se digitar  **http://localhost:1337/heroe**, o routes ficaria assim:

```
'/minhaPagina': { view: 'pages/mypage' },
```

Portanto, copie e cole esse código para o seu routes.js

```
/**
 * Route Mappings
 * (sails.config.routes)
 *
 * Your routes tell Sails what to do each time it receives a request.
 *
 * For more information on configuring custom routes, check out:
 * https://sailsjs.com/anatomy/config/routes-js
 */

module.exports.routes = {

  '/': { view: 'pages/homepage' },
  '/mypage': { view: 'pages/mypage' },
  "POST /heroes": "HeroesController.create",
  "GET /heroes": "HeroesController.getAll",
  "GET /heroes/:id": "HeroesController.getById",
  "PUT /heroes/:id": "HeroesController.update",
  "DELETE /heroes/:id": "HeroesController.delete",
};
```

O que está acontecendo no routes?

* **'/':** está sendo direcionado para **/pages/homepage** que é uma página que já existe no exemplo vazio do Sails
* **/mypage:** está sendo direcionado para um arquivo que vamos criar chamado pages/minhaPagina
* A tarefa POST (que é o mesmo que CREATE) será direcionado para TasksController.create
* A tarefa GET geral (que é o mesmo que SELECT *) será direcionado para TasksController.getAll
* A tarefa GET via ID ( que é o mesmo que SELECT WHERE) será direcionado para TasksController.getById

#### Boas práticas:

* Se o Visual Code mudar **POST** para **post**, não deixa ficar assim. Sempre deixe padronizado para POST, GET, PUT, DELETE

## Etapa 9 - Adicionando uma página .ejs com código HTML

Essa etapa serve para você criar todas as suas homepages e todas elas devem ficar dentro da pasta **view** para ficar tudo ornganizadinho e bonitinho.

a) Crie um arquivo dentro da pasta **views/pages** chamado **mypage.ejs**. Para criar um novo arquivo, clique com o botão direito do mouse sobre a pasta **views/pages** e escolha **New File**. Essa será a sua primeira página HTML daqui alguns instantes.

b) Escreva o código HTML dentro do arquivo .ejs que você acabou de criar.

```
  <section>
    <form name="task-form" action="/heroe" method="post">
      <label for="cpf">CPF:</label>
      <input type="text" id="cpf" name="cpf" required><br>
  
      <label for="name">Primeiro Nome:</label>
      <input type="text" id="name" name="name" required><br>
  
      <label for="last_name">Último Nome:</label>
      <input type="text" id="last_name" name="last_name" required><br>
  
      <label for="age">Idade:</label>
      <input type="text" id="age" name="age" required><br>
  
      <label for="status">Status:</label>
      <input type="text" id="status" name="status" required><br>
  
      <label for="type">Tipo:</label>
      <input type="text" id="type" name="type" value="others"><br>
  
      <input type="submit" value="Salvar">
  
    </form>
  </section>
```
c) Lembre-se de sempre que alterar alguma coisa essas pastas/arquivos, digite ```sails lift``` no terminal e dentro da pasta do seu projeto e depois, opte por **1) FOR DEV**.

* api / controllers
* api / models
* config / datastore.js
* config / routes.js 
* views / pastas que você irá criar
* package.json (penúltimo arquivo)

## Etapa 10 - Testando finalmente sua integração

a) Abra o seu navegador e digite na URL: http://localhost:1337 que vai entrar a página da home

<picture>
   <source media="(prefers-color-scheme: light)" srcset="">
   <img alt="DBeaver OK!" src="[YOUR-DEFAULT-IMAGE]()">
</picture>

b) Agora, acrescente http://localhost:1337/mypage que vai carregar o formulário de entrada de dados.

<picture>
   <source media="(prefers-color-scheme: light)" srcset="">
   <img alt="DBeaver OK!" src="[YOUR-DEFAULT-IMAGE]()">
</picture>


c) Vá no seu DBeaver e confira se sua tabela está com os dados que o front-end postou.
