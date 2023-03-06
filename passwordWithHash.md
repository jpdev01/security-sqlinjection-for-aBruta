O salto é um valor aleatório gerado o qual será adicionado a entrada padrão da senha com o objetivo de gerar o código hash da senha.

```
String salto = BCrypt.gensalt();
```
Uma vez que temos o salto, vamos adicioná-lo a senha passada pelo usuário na hora de realizar o registro.
```
String senhaHashed = BCrypt.hashpw(usuario.getSenha(), salto);
```

Validando o login por exemplo:
```
BCrypt.checkpw(passwordToValidate, dbUser.getPassword());
```