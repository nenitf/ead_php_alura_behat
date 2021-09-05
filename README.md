# ead_php_alura_behat

> Projeto referente a [este](https://cursos.alura.com.br/course/php-introducao-bdd) curso.

[**NÃO CONSEGUI SEGUIR O CURSO!**](https://cursos.alura.com.br/forum/curso-php-introducao-bdd/todos/1)

## Disclaimer

Fiz a aula com o braço quebrado, portanto foi estudo mais passivo com copy/paste de código.

No vim possuo a função:

```vim
function! NN_GitAula2()
    let log = system("git log --pretty=format:\%s")
    vnew
    put=log
    normal! gg
    if search('^:zap: add aula')>0
        normal! 3W
        let s:numero_aula = expand('<cword>')+1
        echom system("git add -A && git commit -m \":zap: add aula ".s:numero_aula."\"")
    else
        echom system("git add -A && git commit -m \":zap: add aula 1\"")
    endif
    bdelete!
endfunction
```

E no terminal executava a cada zip novo de cada aula:

```sh
vim README.md -c "call NN_GitAula2()" -c qa!
```

## Anotações

- [Contextos](https://docs.behat.org/en/latest/user_guide/context.html#context-class-requirements)
- [Organização](https://docs.behat.org/en/latest/user_guide/organizing.html)
- Comandos:

```sh
php vendor/bin/behat --init

# geração de código
php vendor/bin/behat --dry-run --append-snippets
php vendor/bin/behat --dry-run --append-snippets --snippets-for=formacaoEmMemoria # contexto específico

# execução
php vendor/bin/behat
php vendor/bin/behat -s unidade # tag unidade em caso de multiplos contextos

# ver passos existentes (de libs tb)
php vendor/bin/behat -dl
php vendor/bin/behat -dl --lang=pt

```

## Ambiente necessário

Para executar este sistema é necessário ter instalado:

- Composer
- PHP (>= 7.3)
    - PDO SQLite

```sh
php -r "var_dump([
    extension_loaded('pdo'),
    extension_loaded('sqlite3'),
    extension_loaded('pdo_sqlite')
]);"
```


<!--
### Docker

A imagem oficial do PHP (php:latest) já possui o ambiente necessário para executar este sistema, caso não deseje instalar
as dependências (PHP e Composer) separadamente. Os exemplos a seguir partem do princípio que `Docker` será utilizado.
-->

## Iniciar o sistema

1. Execute composer install para instalar todas as dependências necessárias

2. Crie o banco de dados executando o comando php vendor/bin/doctrine orm:schema-tool:create

3. Execute o seguinte comando para criar um usuário com e-mail “email@example.com” e senha “123456”

```sh
php vendor/bin/doctrine dbal:run-sql "INSERT INTO usuarios (email, senha) VALUES ('email@example.com', '\$argon2i\$v=19\$m=65536,t=4,p=1\$WHpBb1FzTDVpTmQubU55bA\$jtZiWSSbmw1Ru4tYEq1SzShrMu0ap2PjblRQRubNPgo');"
```

4. Inicialize o projeto em um servidor web:

```sh
php -S 0.0.0.0:8080 -t public
```

<!--
## Iniciar o sistema

Antes de mais nada, é preciso instalar os componentes utilizados pelo sistema. Para isso, execute:

```
$ docker run --rm -itv $(pwd):/app -w /app -u $(id -u):$(id -g) composer install --ignore-platform-reqs
```

Para inicializar o sistema, o primeiro passo é criar o banco de dados. Para isso, crie um arquivo vazio chamado db.sqlite
na raiz deste projeto.

Depois, execute o seguinte comando: 
```
$ docker run --rm -itv $(pwd):/app -w /app -u $(id -u):$(id -g) php:latest php vendor/bin/doctrine orm:schema-tool:create
```

Este comando criará a estrutura do banco de dados SQLite. Agora vamos inserir um usuário com e-mail `email@example.com` e senha `123456`:

```
$ docker run --rm -itv $(pwd):/app -w /app -u $(id -u):$(id -g) php:latest php vendor/bin/doctrine dbal:run-sql "INSERT INTO usuarios (email, senha) VALUES ('email@example.com', '\$argon2i\$v=19\$m=65536,t=4,p=1\$WHpBb1FzTDVpTmQubU55bA\$jtZiWSSbmw1Ru4tYEq1SzShrMu0ap2PjblRQRubNPgo');"
```

Tendo feito isso, basta subir um servidor de testes. Isso pode ser feito com:

```
docker run -itv $(pwd):/app -w /app -u $(id -u):$(id -g) -p 8080:8080 php:latest php -S 0.0.0.0:8080 -t public
```

Pronto! Basta acessar no seu navegador o endereço http://localhost:8080/ e começar a interagir com o sistema.
-->
