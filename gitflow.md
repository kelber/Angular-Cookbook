
# Gitflow
https://www.youtube.com/watch?v=BYrt6luynCI&t=344s

```js
> git flow 
> git flow init -> deu enter em todos

// iniciou no develop
git push origin --all  --> todos

// começando uma ferramenta
git flow feature start comentarios
// trabalha normal e faz 
> git add .
> git commit -m "comentarios done"
> git push origin feature/comentarios

feature/comentarios > git flow feature finish
// vai fazer o merge para o develop 

> git push origin develop  --> normal ;)

// RELEASE
> git flow release start 1.0.1
> git add . -> depois de mudar 1.0.0 -> 1.0.1

> git flow release finish
// agora mostra msgn do merge  :w

// Tagging
1.0.1  // :w duas vezes

// Obs: diz release/1.0.1 foi mergerada para master
> git checkout master
> git push origin --all --follow-tags





```