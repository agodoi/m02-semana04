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
   * routes.js 

* views
   * pastas que você irá criar

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

a) No seu terminal e dentro da pasta do projeto, digite ```sails generate model myTable``` (enter). Ele vai criar um arquivo chamado **myTable** no modelo Sails na pasta \api\models. Você poderia criar um arquivo manualmente **myTable.js** sem problemas. 

b) Confira em api/models se seu arquivo **myTable** foi criado e pode deletar o arquivo **.gitkeep**. Não vamos utilizá-lo.

c) Na linha 9, dentro do **module.exports**, você vai criar os atributos da sua tabela colando esse código:

```
module.exports = {
tableName: "tasks",
  attributes: {
    id: {
      type: "number",
      autoIncrement: true,
    },
    title: {
      type: "string",
      required: true, //signica que é not null
    },
    description: {
      type: "string",
      required: true,
    },
    dueDate: {
      type: "string",
      required: true,
    },
    status: {
      type: "string",
      required: true,
    },
    createdData:{
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

**1) FOR DEV**	--> faz alter

**2) TESTS**	--> faz drop

**3) STAGING** 	--> quando você está em produção, pois ele não altera o banco. Trabalhar em produção é quando usuários reais utilizam seu projeto.



e após aparecer a Vela do Sails, vá no seu DBeaver e confira se subiu a nova tabela.



## Etapa 2 - Adicionando uma página .ejs com código HTML

a) Crie um novo arquivo .ejs dentro do diretório **views**.
   - Você pode nomear o arquivo de acordo com a página que deseja criar, por exemplo, **teste.ejs**.

b) Escreva o código HTML dentro do arquivo .ejs para definir o conteúdo da página.

```
<form action="/salvarDado" method="post">
  <label for="nome">Nome:</label>
  <input type="text" id="nome" name="nome" required>
  <button type="submit">Salvar</button>
</form>

```

## Etapa 3 - Configure uma rota para esta página

a) Abra o arquivo **config/routes.js**.
b) Adicione uma nova rota para a página criada.
   - Se você está apenas exibindo uma view, use o formato **'GET /teste': { view: 'teste' }**.
   - Se você pretende usar um controller, você pode definir a rota para chamar uma ação específica do controller.



9. Configure as opções do modelo:
   - Abra o arquivo `config/models.js`.
   - Configure `migrate: 'alter'` para que as alterações no modelo sejam automaticamente refletidas no banco de dados.
10. Crie um novo modelo:
    - Execute o comando `sails generate model nome-model`.
    - Isso criará um novo modelo com o nome especificado.
11. Edite o arquivo do modelo criado para adicionar os atributos necessários.

**Para criar o respectivo controller:**

12. Crie o controller associado ao modelo:
    - Execute o comando `sails generate controller NomeModel`.
    - Isso criará um novo controller com métodos CRUD básicos para o modelo especificado.
13. Edite o controller gerado conforme necessário para adicionar lógica personalizada para cada ação CRUD.

Seguindo esses passos, você será capaz de criar um projeto Sails, adicionar páginas, configurar rotas e conectar-se a um banco de dados, tudo de forma clara e didática. Certifique-se de ajustar os nomes e detalhes conforme necessário para atender às necessidades específicas do seu projeto.
