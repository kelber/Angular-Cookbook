# Gitflow
https://danielkummer.github.io/git-flow-cheatsheet/index.pt_BR.html


> git flow init

#### Nova funcionalidade
> git flow feature start MYFEATURE

#### Finalizar funcionalidade
> git flow feature finish MYFEATURE


#### Publicar === Push
> git flow feature publish MYFEATURE


#### Obter funcionalidade === Pull
> git flow feature pull MYFEATURE


#### Criar versões RELEASE
*da branch develop*
> git flow release start RELEASE

> git flow release publish RELEASE


#### Finalizar versão
> git flow release finish RELEASE

1 - Mescla a versão no master
2 - Etiqueta a versão
3 - Mescla a versão também na branch develop
4 - Remove a branch da versão


### Hotfix
> git flow hotfix start RELEASE  // marca versão com defeito

1 - arrumar o que precisa

> git flow hotfix finish RELEASE
1 - Mescla tanto na master quanto na develop atualizando tudo.
2 - O merge da master é etiquetado
  


