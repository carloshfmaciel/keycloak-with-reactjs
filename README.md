## Sobre

Aqui temos um exemplo rodando KeyCloak e integrando com uma aplicação reactjs que utiliza uma biblioteca chamada "keycloak-js" que orquestra o processo de login com o keycloak.

## Dependências
- Docker e Docker compose
- NodeJs

## Como rodar o Keycloak

Rodar docker-compose no diretorio "docker"
```
docker-compose up
```

## Configurando o KeyCloak

Acessar o administrativo do keycloak. Informar usuario "admin" e senha "admin"

```
http://localhost:8080/auth/admin/master/console/
```

Criar um novo realm com um nome desejado clicando no botão abaixo. 
0002

Informar um nome para esse novo realm e clicar em CREATE.(O realm é a unidade organizacional onde os logins estarão agrupados) Ex: "maciel"
0003

Após o realm ser criado e estar selecionado conforme figura abaixo, vamos criar um client id novo clicando no botão Create Client
0004

Nos campos "Client Id", vamos dar o nome do novo client. Ex: "carrefour-app" e vamos clicar em Next
0005

Na tela seguinte, vamos deixar checado apenas a opção "Standard Flow" e clicar em Save.
0006

Agora descemos até a parte de "Access Settings" e incluímos nos campos "Root URL", "Home URL" e "Validate Redirect Uris", "Valid post logout redirect URIs" o endereco que a nossa aplicação react estará subindo na nossa máquina. No exemplo abaixo: "http://localhost:3000/". Além disso em "Web origins", deixamos um "*". Feito isso clicamos em "Save".
0007

Agora subimos na tela e clicamos na aba "Advanced"
0008

Descemos até a parte de "Advanced Settings" e no campo "Proof Key for Code Exchange Code Challenge Method" selecionamos o valor S256. Descemos e clicamos no botão "Save"
0009

Agora vamos definir para que esse realm, o nome do usuário seja o email. Para isto basta clicar na opção "Realm Settings" do lado esquerdo da tela. Clicar na aba "Login" e checar a opção "Email as username" para ON.
0011


Vamos agora criar um usuario para testarmos o login. Clicar na opção "Users" do lado esquerdo da tela e clicamos no botão "Create New User"
0010

Vamos informar o campo "Email", "First name" e "Last name". e clicar no botão "Create".
0012

Agora na aba "Credentials" vamos definir uma senha para esse usuário, clicando em "Set password"
0013

Basta informar uma senha nos campos abaixo e desabilitar a opção "Temporary" deixando ela OFF. Por último clicar em "Save" e depois em "Save Password". Pronto, já temos um usuário para logar no keycloak.
0014

## Rodando a aplicação reactjs

Agora, na raiz do projeto, vamos instalar as dependências da aplicação.

```
npm install
```
0015

Agora vamos abrir o projeto em um editor de código e vamos ajustar as configurações de conexão do keycloak. Abra o arquivo App.js e ajustar as propriedades "url", "realm" e "clientId" conforme as informações definidas no keycloak na criação do realm e do client.
0016

Por último vamos startar o projeto
```
npm start
```

A aplicação irá abrir uma pagina do browser e irá redirecionar para a página de login do keycloak. Basta informar o usuário e a senha criados e clicar em "Sign in".
0017

Ao ser logado automaticamente o keycloak irá redirecionar para a aplicação. Clicando nesses botões será possível ver alguns recursos da biblioteca keycloak-js exibindo propriedades que foram retornadas pelo keycloak como o token e JWT.
0017