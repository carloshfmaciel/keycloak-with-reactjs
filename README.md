## Sobre

Aqui temos um exemplo rodando KeyCloak e integrando com uma aplicação reactjs que utiliza uma biblioteca chamada "keycloak-js" que orquestra o processo de login com o keycloak.

### Fonte
https://medium.hexadefence.com/securing-a-react-app-using-keycloak-ac0ee5dd4bfc

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
![](/screenshots/0001.PNG)

Criar um novo realm com um nome desejado clicando no botão abaixo. 
![](/screenshots/0002.PNG)

Informar um nome para esse novo realm e clicar em CREATE.(O realm é a unidade organizacional onde os logins estarão agrupados) Ex: "maciel"
![](/screenshots/0003.PNG)

Após o realm ser criado e estar selecionado conforme figura abaixo, vamos criar um client id novo clicando no botão Create Client
![](/screenshots/0004.PNG)

Nos campos "Client Id", vamos dar o nome do novo client. Ex: "carrefour-app" e vamos clicar em Next
![](/screenshots/0005.PNG)

Na tela seguinte, vamos deixar checado apenas a opção "Standard Flow" e clicar em Save.
![](/screenshots/0006.PNG)

Agora descemos até a parte de "Access Settings" e incluímos nos campos "Root URL", "Home URL" e "Validate Redirect Uris", "Valid post logout redirect URIs" o endereco que a nossa aplicação react estará subindo na nossa máquina. No exemplo abaixo: "http://localhost:3000/". Além disso em "Web origins", deixamos um "*". Feito isso clicamos em "Save".
![](/screenshots/0007.PNG)

Agora subimos na tela e clicamos na aba "Advanced"
![](/screenshots/0008.PNG)

Descemos até a parte de "Advanced Settings" e no campo "Proof Key for Code Exchange Code Challenge Method" selecionamos o valor S256. Descemos e clicamos no botão "Save"
![](/screenshots/0009.PNG)

Agora vamos definir para que esse realm, o nome do usuário seja o email. Para isto basta clicar na opção "Realm Settings" do lado esquerdo da tela. Clicar na aba "Login" e checar a opção "Email as username" para ON.
![](/screenshots/0011.PNG)

Vamos agora criar um usuario para testarmos o login. Clicar na opção "Users" do lado esquerdo da tela e clicamos no botão "Create New User"
![](/screenshots/0010.PNG)

Vamos informar o campo "Email", "First name" e "Last name". e clicar no botão "Create".
![](/screenshots/0012.PNG)

Agora na aba "Credentials" vamos definir uma senha para esse usuário, clicando em "Set password"
![](/screenshots/0013.PNG)

Basta informar uma senha nos campos abaixo e desabilitar a opção "Temporary" deixando ela OFF. Por último clicar em "Save" e depois em "Save Password". Pronto, já temos um usuário para logar no keycloak.
![](/screenshots/0014.PNG)

## Rodando a aplicação reactjs

Agora, na raiz do projeto, vamos instalar as dependências da aplicação.

```
npm install
```
![](/screenshots/0015.PNG)

Agora vamos abrir o projeto em um editor de código e vamos ajustar as configurações de conexão do keycloak. Abra o arquivo App.js e ajustar as propriedades "url", "realm" e "clientId" conforme as informações definidas no keycloak na criação do realm e do client.
![](/screenshots/0016.PNG)

Por último vamos startar o projeto
```
npm start
```

A aplicação irá abrir uma pagina do browser e irá redirecionar para a página de login do keycloak. Basta informar o usuário e a senha criados e clicar em "Sign in".
![](/screenshots/0017.PNG)

Ao ser logado automaticamente o keycloak irá redirecionar para a aplicação. Clicando nesses botões será possível ver alguns recursos da biblioteca keycloak-js exibindo propriedades que foram retornadas pelo keycloak como o token e JWT.
![](/screenshots/0018.PNG)
