# Horário de Atendimento do Professor

* Terças e quintas das 8h às 16h podem contar comigo!
* Demais dias da semana, estou no Slack, com tempo de respostas no mesmo dia.

# Horário de Atendimento do Monitor

* Segunda: 8h30 às 10h
* Quarta: 8h30 às 10h
* Sexta: 8h30 às 9h30

# Back-end I - Node.js, models e controllers

Agora que temos o banco de dados pronto, bora contruir **aplicação servidor**, ou seja, o back-end. 

Nesta instrução, praticaremos a construção de aplicações utilizando o Node.js, relacionando com o banco de dados, produzindo os primeiros pontos de contato com o mundo lá fora - os endpoints de uma WebAPI. Tudo isso sob a arquitetura MVC!

## Etapa 1 - Criando um novo projeto Sails

1.1 Abra o terminal e navegue até o diretório onde deseja criar o projeto.
   
1.2 Execute o comando **sails new nome-projeto**.
   - Este comando criará um novo projeto Sails com o nome especificado.
     
1.3 Quando solicitado a escolher um modelo, selecione a opção **2 - Empty**.
   - Isso criará um projeto vazio sem qualquer configuração pré-definida.

1.4 Ainda no terminal, entre na pasta recém criada do projeto e digite **code .** para carregar o projeto inteiro no Visual Code.

## Quais as pastas importantes?

* api
   * controllers

* api
   * models

* views
   * pastas 

## Etapa 2 - Adicionando uma página .ejs com código HTML:

2.1 Crie um novo arquivo .ejs dentro do diretório `views`.
   - Você pode nomear o arquivo de acordo com a página que deseja criar, por exemplo, `teste.ejs`.

2.2 Escreva o código HTML dentro do arquivo .ejs para definir o conteúdo da página.

**Para configurar uma rota para esta página:**

6. Abra o arquivo `config/routes.js`.
7. Adicione uma nova rota para a página criada.
   - Se você está apenas exibindo uma view, use o formato `'GET /teste': { view: 'teste' }`.
   - Se você pretende usar um controller, você pode definir a rota para chamar uma ação específica do controller.

**Para conectar com banco de dados:**

8. Configure a conexão com o banco de dados:
   - Abra o arquivo `config/datastores.js`.
   - Adicione as informações de conexão, como adapter, URL e, se necessário, SSL.
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
