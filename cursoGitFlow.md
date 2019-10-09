
# Curso de Github com Willian Vasconcellos
22/10/2018


#### Inicializando o Projeto
    Studio Code e cria o primeiro commit, passou de U ( Untracked ) para A ( Added )

#### Fazendo Mudanças e vendo diff 
    1 - Voce modifica o arquivo vai para M ( Modified )
    2 - Viu a modificacao e gostou ai é só commitar.

#### Criando branchs
    - Clicar no inferior esquerdo do VSCode e criar.

#### Plugins
    1 - git add remote -> pra subir direto pelo visual studio code
        Obs: Ctrl + Shift + P -> Abre aba procura:  ai digita remote

    2 - Git history -> historico de commits x git Lens
        > git log

#### Adicionando Remoto no Github e subindo codigo
    obs: Precisa do plugin 
    1 - Vai no github e copia a linha do repositorio criado na mao.
    2 - VStudio e ctrl + shift + p    e  digita  remote
    3 - normal é *origin*  e cola só a URL do repositorio remoto
    4 - Clica no simbolo git e ... (tres pontos ) direito da um *push to*  -> vai github F5

# Faça -> git remote add origin "http.ulr.git"
> git push -u origin master

#### Puxando do remoto uma modificacao pra o local
    Ex: alguem alterou o readme.md
    OBS: Catraca no visualStudio code e atualizar...
    OBS2: Perceba que depois que vc alterou local ele mostra. 0 pra entrar e 1 pra subir - Só Refresh

#### Historico de commits
    > Plugin Git history

#### Git MERGE e REBASE  
    Os commits estao numa ordem... 1,2,3,4,5 mas nem sempre e assim...

    Ex: Eu mudo navbar items localmente e tiro comentarios no remoto por exemplo.
        agora vou e mudo tb os anchors do navbar item e faco novo commit.
        OBS: Temos 1 alteracao do navbar items, depois no remoto e depois no local os anchors

        2 Maneiras
        1-> Mais "suja"
        **pull from**  , do origin, do master  , agora git log
        Resultado: Criou merge na sequencia cronologica mas tb criou uma RAMIFICACAO linha a mais e um commit automatico a mais.
        Bom pra qdo vc terminou sua feature e vai atualizar a MASTER -> use *MERGE*

        2-> Só atualizar  *REBASE*   pull (rebase)
            Obs: Ele vai parar na primeira alteracao diferente master, adiciona os remotos e os outros adiciona depois

            obs: erro de upstream é só copiar a linha e executar terminal
            git branch --set-upstream-to=origin/*master* nomeBranch  -> *master* atualizar sempre da master

            **pull rebase** 


#### Stash - antes do commit
    Ex: Você esta criando e teve que parar no meio pra fazer outro branch; aqueles arquivos não estao prontos para commit porem voce quer "salva-lo" para depois voltar neles...

    1- ...  git stash 
    2- ... pra voltar é só *Pop stash*




# USE
#### Revertendo commit do MASTER com comando REVERT
    Subi coisa errada ... rsss :)
    > git revert  hashErrada
    :wq
    > git push origin master

    Obs: O Git salva histórico ( o que é bom ) pois se alguem pegou aquele errado. da pra resolver

#### Revertendo commit com RESET de outras branchs 
    > git log  -> vc pega o ultimo commit certo antes do errado.

    > git reset --hard  HASH_CERTO_lembre-CERTO -> Volta pra esse commit certo e ignore TUDO posterior a esse.
    > git reset --soft  HASH_CERTO_lembre-CERTO  Volte mas o restante volta pra staged pra eu checar as mudanças

- Use git RESET -> bom pra branchs separados e sem commits sujos

OBS: Se der > git push origin master vai dar erro pois commits estão errados. ai pode dar force
    > git push origin master --force


#### Editando commit com AMMEND  ou amentando coisas na modificacao  > git commit --ammend
OBS: Antes de enviar pro MASTER ou REMOTO
    Vc criou o commit e errou no texto. rss
    > git commit -m "ISCRIVI erradum"
    > git commit --amend
    :wq


#### Como pegar algo especifico de um branch e colocar no meu ?
> git checkout redesign-navbar
> git log e pega um interessante...  ex: alteração feita só no navbar-items

> git checkout master
> *git cherry-pick* HASG_INTERESSANTE  ex: pegou navbar-items 
// se quiser pegar outro commit 
> *git cherry-pick* HASG_INTERESSANTE2  ex: pegou navbar-items anchor modificacoes 



#### Commitando trechos especificos do mesmo arquivo.  ( Ex. 2 seções )
    > git add -p
    // Mostra velho e o novo
    P: Stage this hunk ? ( Adicione este pedaço )
    Resp: y,n,q (quit ), e outros.... V16 2:00
    Resp: y  
    segundo: N
    // Obs: > git status
    tem 2 pedações um modificado outro nao. ( igual que eu queria )
    > git commit -m "So update intro"
    > git show hasg ( so mudou o intro )
    > git add index.html  ( agora adiciona o 2 trecho )
    > git commit -m "Agora so o 2 pedaço"



# USE
#### Juntando commits com SQUASH -> Ex: uma feature só
    Ex: conta > git log conta 2 commits

    > git rebase -i (interativo)  HEAD~2   -> 2 ultimos commits , 3 ultimos digite HEAD~3 
    R: opções LEIA
    :wq
    // agora commit final
    Update intro and what i do in one line 
    :wq
    > git log 2 em um só

    // angularFirebase fez...
    > git merge featureNova --squash  -> juntou 3 commits antes do master



#### Juntando commits com fixup e autosquash
    // Ex. mude uma linha
    > git add .
    > git commit -m "change linha A"
    // muda mais outra coisinha...
    > git add .
    > git commit --fixup hashBobo
    // muda outra besteira
    > git add .
    > git commit --fixup hashMaisNovo
    // mudar os 3 em um só
    // copia o hash antes as 3 besteirinhas....
#### > git rebase -i --autosquash hashAntesDos3
    R: pick
    fixup
    fixup
    :wq sem mudar
    > git log uniu os 3
    Obs: correções muitas com poucas coisas limpa 

    

#### Resolvendo divergencias repositórios com --rebase
    // após umas mudanças nao conseguiu fazer > git push origin master

    > git pull origin master --rebase
    > git push origin master

#### Resolvendo conflitos com arquivos locais e remotos - Linha de comando
    ( Mais de uma pessoa modificando no mesmo arquivo alterou local e no repositorio tb mudou mesma linha)
    Ex: posterior gitflow da Mary
    > git pull origin master
    > git status   R: both modified
    > vai no arquivo e limpa o conflito

    Resolveu os conflitos.
    > **git merge --continue**
    > **git rebase --continue**   caso esteja fazendo em outros branchs
    // abriu o vim e OK
    :wq
    > git push origin master

    // Resumo
    >>>>> HEAD
        // mudanças locais

    ====================
        // mudanças que estao vindo...

    >>>>>>>>>>  hash


#### Resolvendo conflitos com arquivos locais e remotos - VsCode
    // coloridinho  :)


#### AutoCorrect
> git config --global help.autocorrect 1



#### Zip de repositorio
> git archive master --format=zip --output=master.zip


#### Git Log
> git log --prety --oneline --graph --all
> git log --since='Jan 6 2018'
> git log --until=
> git log --author=''
> git log --shortlog
> git log -3
> git shortlog -sn


## Git reFLOG
    É um log que trabalha em cima das referencias.
    Mostra tudo e dá pra recuperar até mesmo  git reset --hard



V27 - Overview das funções Github
#### Issues 
    Fantastica ferramenta pra distribuir serviço e documentar
    veja: *awesome-github-issues-templates*

    1 - Criar pasta 
    .github/issue_template.md

    ## Pre create issues
    - [] Read the guidelines 
    - [] Test in all browers 
    - [] ... 


    ## Description
        Adicione a descrição
    
    ## Screenshots

    > git push origin master
    obs: na parte de issue esse "modelo" estará la para ser seguido.  :)


#### Referenciando a issue e com commits e fechando as automaticamente
no campo Write é só colocar
    #1 e salvar ( vira link )

EX: Colocou foto vai fazer commit 
"adicionado foto no background  - Closes #1  "
Closes #1 -> artigo "closing issues with keywords"  Closes é pra fechar a issue automaticamente
Existe: close, closes, closed, fix, fixes, resolve, resolves etc...


#### Pull Requests 
Branch separado ou commit separado querendo anexar no principal.

Criando template para pull Requests.  -> 
.github/pull_request_template.md

OBS: veja modelo naquele link acima
EX:

    ### Description
        Adicione aqui descr do pull requrest
    ### Review
        - [] Check the copy
        - [] Check the ...
        - []  ...
    ### Pre-merge checklist
        - []  ...
        - []  ...

    ### Screenshots
        | Before | After |
        | ------ | ----- |
        | image  | image |

    > git add .
    obs: ele percebeu que estava no branch errado ....
        > git stash 
        > git checkout master
        > git stash apply  -> traz mudancas
    > git commit -m "add pull request template"
    > git push origin master

    
V34 - Protegendo o MASTER - Subindo so com pull requests
    1 - Settings
    2 - Protected branchs -> proteger

V35 - Como funciona o code Review
Passo 1 - > O adm vai comments nas linhas o que quer. ex: tire comments 
Passo 2 - > Review changes. ele deixa um comment, approved, request changes 

#### Resumo
1 - Cria um branch separado
2 - Faz mudanças e manda via pull request
3 - Recebe comentarios, trabalha e corrige e recebendo aprovações
4 - Faz o merge pro master

V36 - Squash e Mergeando

    Ideia: o commit da correção não é muuito importante. então nao é legal deixar ela.
    Botaão merge commit tem opção
        - Create and commit
        - Squash and merge -> juntas 2 commits em um só  --> Ideal é esse 
        - Rebase and merge -> juntar 2 colocar no topo e adicionar o branch
        Obs: *Deletar o branch que nao vai usar mais*.


#### WorkFlows do GIT
    Fluxo de trabalho - Sequencia de passos para automatizar processos

    1 - Salva arquivo
    2-  Criar commit
    3 - Envia pro github
    4- Pede um pull request
    5 - Faz code review
    6 - Faz merge no master

    Exemplos de WorkFlow
        ### Centralized Workflow
        ### Feature Branch Workflow
        ### Gitflow Workflow

### Centralized Workflow
    Só um branch ( master )
    Bom pra equipes pequenas - até 4
    Ex: John faz git push origin master
    Maria tem que fazer um 
    > git pull origin master --rebase
    resolver algo e depois colocar as suas no topo
    > git push origin master
    obs: tudo no master e sempre se atualizando


### Feature Branch Workflow
    *Mais usado*
    1 - Um branch pra cada feature
    2 - Evita conflitos e permite trabalhos em paralelo.
    3 - Equipes maiores

    Ex: Mary nova feature num branch novo e sobe pull request
    Bill recebe o pull request, bill pede mudanças e ela faz.
    Resolvido, Bill aprova e Mary faz merge.


    // fez trabalho: obs branch update-my-work-gallery
    > git add .
    > git commit -m "done"
    > git push origin update-my-work-gallery

    -> clicar no pull request e editar arquivo e CREATE


### Gitflow Workflow ( Extensões pro Git )
    veja cheatsheet do git-flow - site
    1 - Instalar: http://danielkummer.github.io/git-flow-cheatsheet/index.pt_BR.html
   
    // Criando um feature ( repositorios novos ou já existentes )
    > git flow init
        P: qual branch -> master
        P: qual dev -> develop
        Enter todos
    
    obs: develop>
    > git flow feature start update-contact
    // faz trabalho
    > git commit -m "Update contact session"
    > git flow feature publish update-contact

    Obs: Se vc for no github pra dar pull request não tem o branch "develop" só tem o master.
    > git checkout develop
    > git push origin develop
    // agora tem.

    pull request do feature/update-contact para develop

    // code review - OK vamos fazer pelo terminal
    > git flow feature finish update-contact
    Obs: merge dentro develop e removeu branch e voltou develop
    > git push origin develop
    R: Merged e lembre-se "remove  branch no botao"


#### Criando uma release para producao ( master )
    > git flow release start 1.0.0
    > git flow release finish '1.0.0'
    :wq
    // mensagem de tag   1.0.0
    :wq

    > git push origin master --tags  -> vai jogar release e tags
    > git checkout develop
    > git push origin develop

#### Criando Hotfix com GitFlow
    Ex: em producao nao esta funcionando o navbar
    > git low hotfix start fix-anchor
    // id="estavam em ingles" x css #one agora #o-que-faco

    > git add .
    > git commit -m "Fix all"
    > git flow hotfix finish fix-anchor
    :wq
    Fix anchors pra tag
    :wq
    > git checkout master
    > git push origin master --tags
    obs: Subiu mudanças e tags

####  Vamos criar gh-pages
    > git push origin gh-pages
    > 






    





