# ead_php_alura_behat

> Projeto referente a [este](https://cursos.alura.com.br/course/php-introducao-bdd) curso.

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

## Setup inicial

```sh
composer i
```
