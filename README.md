<h1 align="center">
  <a name="logo" href="https://www.gira-bicicletasdelisboa.pt/">
    <img src="https://www.gira-bicicletasdelisboa.pt/wp-content/themes/gira/resources/assets/images/logo_gira.svg" alt="Logótipo GIRA" width="300">
  </a>
  <br>
  GIRA API Documentation
</h1>

<h4 align="center">API privada da GIRA, usada pela aplicação.</h4>
<h6 align="center">A API aqui descrita é a utilizada pela aplicação oficial da GIRA, pelo que é necessário iniciar sessão junto do serviço de autenticação da EMEL.<br>Os tokens expiram a cada 2 minutos e devem ser atualizados com refresh.</h6>
<hr>

## Índice de Conteúdos
<details>
<summary>Clique para expandir</summary>

- [Autenticação](#auth)
  * [Auth](#auth-init)
  * [Refresh e Revoke](#auth-refrev)
- [API GIRA](#gira-api)
  * [Pedido](#gira-api-req)

</details>

<hr>
<h1 id="auth">Autenticação</h1>
<h2 id="auth-init">Auth</h2>
<h4>Autenticação através do sistema de login da EMEL</h4>
<h5>Os tokens obtidos têm um tempo de vida de 2 minutos.</h5>

<h3 id="auth-init-req">Pedido</h3>
<h4>URL: https://api-auth.emel.pt/auth</h4>

```javascript
{
    "Provider": "EmailPassword",
    "CredentialsEmailPassword": {
        "Email": "", // substituir pelos seus dados de acesso
        "Password": "" // substituir pelos seus dados de acesso
    }
}
```
<h3 id="auth-init-res">Resposta</h3>

```javascript
{
    "error": {
        "code": 0,
        "message": "Success"
    },
    "data": {
        "accessToken": "", // token JWT a usar nos pedidos para a API GIRA, expira 2 minutos após gerado
        "refreshToken": "", // guardar token para atualizar o token expirado
        "expiration": int // ignorar valor
    } 
}
```

<p>Pode descodificar o token JWT "accessToken" e saber mais sobre a norma JWT em <a href="https://jwt.io/">JWT.io</a>

<h2 id="auth-refrev">Refresh e Revoke</h2>
<h4>Pode atualizar ou revogar o seu token.</h4> 

<h3 id="auth-refrev-req">Pedido</h3>
<h4>Refresh URL: https://api-auth.emel.pt/token/refresh</h4>
<h4>Revoke URL: https://api-auth.emel.pt/token/revoke</h4>

```javascript
{
    "Token": "" //substituir pelo token a gerir
}
```  

<h1 id="gira-api">API GIRA</h1>
<h2>GraphQL</h2>
<h4>A API GIRA faz uso a linguagem de consulta <a href="https://graphql.org/">GraphQL</a>.</h4>
<h4>Obtenha o <i><a href="https://graphql.org/learn/schema/">schema</a></i> através de <a href="https://graphql.org/learn/introspection/">introspeção</a>.</h4> 

<h3 id="gira-api-req">Pedido</h3>
<h4>URL: https://apigira.emel.pt/graphql</h4>
<h4>Deverá incluir um cabeçalho de autenticação do tipo Bearer, que contenha o o valor da chave JSON obtido em <a href="#auth">Autenticação</a>:</h4>

```
Authorization: Bearer { authorizationToken }
```
