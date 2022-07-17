GIT & GITHUB
====
Estudo git-github, focado em  controle de versão com git, ferramenta essa essencial para desenvolvedores, aqui também fica a práica de subir/baixar os arquivos do projeto juntamente com o versionamento para github. 
Este estudo ficará aqui disponível para consulta em formato de manual prático e rápido. <br><br>

![](img.jpg) <br>
***
#### Existem 4 estágios em que um arquivo pode estar quando faz parte de um projeto:


 | Untracked | Tracked | Modified | Staged |

- Untracked: (não rastreado), o arquivo ainda não estão sendo monitorados pelo git ou quando o projeto tem alguns arquivos, mas o git ainda não controla esses arquivos, arquivo novo criado agora ou copiado agora
- Tracked: a partir desse momento os arquivos estão controlando esses arquivos também são conhecidos como "new file"
- Modified: quando modificamos um arquivo que está sendo rastreado pelo git e ele detectou que o arquivo foi modificado, nessa etapa podem ocorrer erros/conflitos, se 2 pessoas alteraram o mesmo arquivo, deve-se fazer "merge"
- Staged (preparado): quando o arquivo já foi rastreado, modificado, finalizado e está pronto pra ser enviado para o repositório através de commits


#### Em outras palavras ou explicando de outra forma:

- Um arquivo no git podem estar em 1 dos 4 estágios:
- untracked : não versionado no commit anterior;
- not staged : sofreu mudanças desde o ultimo commit e ainda não foi selecionado para o próximo commit;
- staged : sofreu mudanças e foi selecionado para o próximo commit;
- commited : não foram modificados desde o ultimo commit;


# --------------------------------------------------------------------|

 
#### Criando repositório no gitHub (bare remoto) e sincronizando com local
```shell
# Criar repositório no github
# Criar uma pasta local para sincronizar com o bare remoto
# inicializar o git nesta pasta
	$ git init

# identificar o user (caso não tenha ainda --global)
	$ git config user.name ....... user.email

# registrar o repositório do github (bare) localmente
	$ git add origin https://github/.../....git

# Adicionar arquivos para o primeiro commit
        $ git add .

# realizar o primeiro commit
        $ git commit -a -m "primeiro commit"

# enviar do local para github
	$ git push origingithub master

# -------------------------------------------------------------------- |




#### Ciclo
- Ao iniciar "git init" entra no "Untracked".
- Ao realizar "git add" entra no "tracked" e o git está monitorando ESSE arquivo
- Ao modificar o arquivo ele entrar no "modified", precisa fazer "add".
- Para o arquivo ser transferido para o "Staged" é obrigatório que o arquivo esteja no "tracked".- 
- Se o arquivo estiver no estágio "tracked" ele pode ser commitado "git commit -m" para entrar no "staged"
- Estando no estágio "Staged" ele pode ser transmitido para o repositório remoto	
- Git é descentralizado, a própria máquina local é um repositório

#### Para ignorar arquivos recursivamente:
- Colocar no arquivo .gitignore da seguinte forma: 
	 *****file/***  <sub>(vai ignorar a pasta "file" tanto na pasta atual quanto recursivamente)</sub>
	
#### Para definir a pessoa gerenciadora da pasta
``` shell
	$ git config user.name "nome da pessoa"
	$ git config user.email "email@gmail.com"
```

#### Para definir configurações do user para tudo (global)
``` shell
	$ git config user.name "nome da pessoa"
	$ git config user.email "email@gmail.com"
```

#### Para visualizar as configurações do "git config"
``` shell
	$ git config --lis
```

#### Fazendo commit:
``` shell
	$ git add
	$ git commit -m "mensagem do commit"
```

#### Comando "git add ." *(com ponto)*
- se executar o comando  "git add" e alterar algum arquivo do repositório local, na sequencia gerar commit e vai subir no commit


#### Localizando commits
``` shell
	$ git log vai mostrar uma lista enorme dos commits
# vai mostra abaixo no final da página o sinal ":" 
# nesse momento pressionar / + 'nome de busca' Ex.: /code.html
# o git vai buscar o commit onde existe o arquivo "code.html"
```

#### Alterar comportamento ao mostrar a lista no "git log"
``` shell
	$ git config core.pager cat
# conferir arquivo ".git/config"
# a partir de agora não vai mostar mais o ":" e vai listar completamente**
```

#### Desfazer comportamento para mostrar a lista logs com ":" e busca
``` shell
	- $ git config core.pager less
```

#### Fazendo mais com comando "git log"
``` shell
# mostrar os três últimos logs
	$ git log -3

# mostra cada log em uma linha também mostra o resumo do hash
	$ git log --oneline
		
# mostra os três últimos cada commit em uma linha
	$ git log -3 --oneline 
		
```

#### Pesquisando commits no "git log"
``` shell
# mostra logs anterior a 30-03-2021
	$ git log --before=2021-03-30

# mostra logs após 30-03-2021
	$ git log --after=2021-03-30

# mostra os logs de 7 dias atras
	$ git log --since="7 days ago"

# mostra logs de 1 mês atras
	$ git log --before="1 month ago"
```

#### Voltando no tempo, visualizar tempo passado
``` shell
# volta no commit '4ff58d9'
	$ git checkout 4ff58d9
		
# para voltar ao 'HEAD' mais alto
	$ git checkout master		
```

#### Renomear arquivo
``` shell
# renomar arquivo de file1.txt para file10.txt
	$ git mv file1.txt file10.txt
		
```

#### Renomear arquivo diretamente pela pasta
- ele vai deletar o original e criar uma cópia com nome novo
#### Removendo arquivos
``` shell
	$ git rm arquivo.txt
```

#### Dica
_"Faça pequenos commits!"_


#### Checando a diferença entre arquivos no "staged"
``` shell
	$ git diff --staged # somente após incluí-los no staged
```

#### Checando a diferença entre o HEAD e algum outro commit antigo
``` shell
# mostra  a diferença entre o HEAD até o commit 3d9d4cb (antigo)
	$ git diff 3d9d4cb

```

#### Checar a diferença entre o commit atual e um outro antigo
``` shell
# checar a diferença entre o commit 'cb'(mais antigo) até 'ad' (mais novo)
	$ git diff 3d9d4cb..5a886ad

```

#### Corrigindo mensagem de commit
```shell
	$ git commit --amend -m "Nova mensagem corrigida"
```

#### Feito commit mas faltou criar ou adicionar um arquivo novo
``` shell
# crie o arquivo novo
	$ git add .
	$ git commit --amend -m "Comentario sobre o commit"

	$ git push --force originthub master
```

#### Tirando arquivos de staged (git add)
```	 shell
	$ git restore --staged fileName.txt
	$ git restore --staged (desse modo vai retonar com todos os arquivos do staged)
# vai voltar o arquivo para 'untracked'
```

#### Feita uma alteração indevida em um arquivo pronto
``` shell
# acessa o arquivo no último commit
	$ git checkout arquivo.html
	$ git status 	# (nota-se que os arquivos estão como antes)

# ou

	$ git restore fileName.txt 
# ou use ( . ) para todos os arquivos
# usar checkout arquivo por arquivo
```

#### Remover um commit que foi feito
``` shell
	$ git reset HEAD --hard
# head é o último estágio do commit
# então vai resetar todas as alterações e retornar ao estágio anterior
```

#### Fiz um commit que não deveria ter sido feito - Descartar último commit
``` shell
	$ git reset HEAD^ --hard 

# faz voltar para o último commit e descarta o primeiro, descartando também o código (atenção!)
```


#### Remover um commit mas não desfazer alterações
``` shell
	$ git reset --soft 7573031
# Vai apagar o commit 7573031, mas os arquivos alterados vão manter
# os arquivos vão ficar no staged
```

#### Criando uma branch
*** <mark>Um branch nada mais é do que uma ramificação do projeto</mark>***
``` shell
	$ git branch nomeDaBranch
# Quando cria uma branch, ela traz todos os commits anteriores
```

#### Mudar para outra branch
``` shell
	$ git checkout nomeDaBranch
```

#### Removendo uma branch:
``` shell
	$ git branch -d nomeDaBranch
	$ git branch -D nomeDaBranch 
```

#### Merge <sub>*(unir uma ou mais branch(s))*</sub>
``` shell
# ir para branch principal:
	$ git checkout nomeDaBranchPrincipal

# Juntar as branchs (merge)
	$ git merge nomeDaBranchSecundaria

```

#### Rebase
``` shell
# rebase é: refazer a base, base é o local onde é criado uma branch
# reorganização da base

# Criar uma branch de outra forma (rebase)
	$ git checkout -b nomeDaBranch (cria a branch e já muda para ela)

# depois de fazer as alterações dos arquivos e no projeto
# agora seria a hora de fazer 'merge' mas:
	$ git checkout master # (ir para a branch principal)
# fazer o 'rebase':
	$ git rebase nomeDaBranch
```


#### Clone e Push
###### clonar um repositório para outro local:
- acessar a pasta na qual irá receber a cópia
``` shell
	$ git clone /home/pasta/pasta .
#ou seja
	$ git clone "pasta origem" + (.)	#-> o ponto é para que seja clonado somente os arquivos
```

- Ao fazer push gerou um erro, porque esse não é o repositório "bare", veja a resolução em [Bare e Repository.](estudo-git/README#^idbare) 


#### Fetch e pull
- o fetch baixa as atualizações de um repositório remoto, porém não faz o merge (baixa e não merge)
- nesse caso ele fará um "base" no branch ao invés de fazer "merge"
- CASO: em outra pasta é feito clone "git clone ~/pasta/pasta", e é feito alguns commits
ao fazer "push" ocorreu erro, então nessa pasta clone, fiz "git fetch"
``` shell
	$ git fetch
```

- nota-se que ele baixou alguma coisa, mas os arquivos novos do repositorio principal, não aparecem no "ls", isso é o que o "fetch" faz
- então para que o repositório "clone" seja realmente atualizado com os arquivos precisa-se fazer "git rebase"
``` shell
	$ git Rebase 	#(reorganização da base)
```

#### Pull
- é uma junção dos comandos "fetch" e "rebase"
~~~ shell
	$ git pull
~~~

#### Bare e Repository ^idbare
- BARE: o git é descentralizado, cada repositório no git é um novo nó na rede, pode-se definir um repositório como sendo o central, onde cada um dos desenvolvedores, cada um com seu repositório local, submete os dados para o central
- Criando o Bare: no local onde será o repositório central:
```	shell
	$ git init --bare
```
#### Exemplificando
```shell 
# criado um projeto
# dentro do projeto criado 3 diretórios "desenv-julius", "desenv-maria" e "rep-bare"
# dentro do diretório "rep-bare" foi inicializado o bare:
	
	$ git init --bare
	
# acessado o diretório do "desenv-julius"
# criado um diretório "secao04" e acessado esse diretório
# feito clone do repositório central (bare)
	$ git clone ~/../../rep-bare/ .

# feita a configuração do usuário
	$ git config user.name ..... e email

# adicionado os arquivos do projeto
# feito os commits normais (add, commit)
# enviado os arquivos para o repositório central (bare)
	$ git push

# acessado o diretório da "desenv-maria"
# realizado clone do repositório central (bare)
	$ git clone ~/../../rep-bare/ .

# feita a configuração da desenv Maria (git config user.name ... ...)
# criado os arquivos do projeto da parte da Maria
# realizados todos os commits
# enviar para o repositório central (bare)
	$ git push
```

	
#### Sequencia correta para centralização:

1. **localhost:** Criar diretório "rep-bare" _ou_ **remoto:** Criar repositótio "github" e/ou "bitbucket"
2. no diretório do desenvolvedor onde será realizado o projeto:
	1. localhost:	`$ git clone ~/.../.../repo-bare/ .`
	2. remoto: 		`$ git clone https:https://github.com/username/projeto.git .` <sub>Obs: não esquecer do (.) no final </sub>
	3. Se não tiver ainda definido global, então setar configuração do user....
	4. criar os arquivos do projeto
	5. gerar os commits normalmente
	6. Empurrar o desenvolvimento para o rep
		1. localhost:	`$ git push`
		2. remoto:		`$ git push origin nomeDaBranch`
	7. ao voltar a trabalhar no projeto, sempre antes realizar pull _(baixar)_ para trazer novas alterações que tenham sido enviadas para o rep central por outro desenvolvedor

#### Trabalhando com Tags
- Partes entregáveis do projeto, ou seja, o projeto será entregue em partes, para no final todas trabalhar unificadamente
- enquanto isso, entrega-se uma tag para o cliente testar, enquanto trabalha-se em uma nova parte (tag)
- Tag seria uma versão pronta para uso, mesmo que seja uma versão incompleta
- com a tag define-se um estado de um repositório
- gera-se "release" para o projeto
- cada versão do projeto, define-se uma tag

#### Para criar uma tag:
``` shell
	$ git tag v1.0	#cria a tag identificada por "v1.0"

	$ git tag (mostra as tags criadas)

#agora precisa-se enviar a tag para o repośitório central:
	$ git push origin "nomeDaTag"

#"origin" é o repositório remoto

# Consultar algo no ponto da tag:
	$ git checkout "nomeDaTag"

# estando na tag e quiser criar uma branch a partir deste ponto
	$ git switch -c "new-Branch-Name"
```

#### Dando continuidade na exemplificação de tags
```shell
# Julius e Maria definiram que o que fizeram até agora pode ser considerada a versão 1.0 do projeto
# Julius critou uma tag versão 1.0
	$ git tag v1.0
	
# Maria atualizou seu repositório:
	-$ git pull origin -f (para ver se existem branchs diferentes no rep)
	
# Maria quer ver como está a versão 1.0
	$ git checkout v1.0
	
# neste ponto não se pode realizar commits!!
# após olhar, maria volta para a branch master
	$ git checkout master
	
# Maria encontrou alguns erros na v1.0
# então vai fazer checkout na v1.0 e criar uma nova branch de correção a partir deste ponto
	$ git checkout v1.0
	
# maria já visualiza as dicas do git, cria uma branch a partir do ponto onde ela está
	$ git switch -c correcoes-v1.0
	
# agora basta trabalhar nas correções
# feito as correções maria empurra para o repositório
	$ git push origin correcoes-v1.0

# Julius consulta se existem atualizações
	$ git pull -force

# Julius visualiza as novas branchs
	$ git pull origin correcoes-v1.0

# Julius ajuda nas correções após empurra para o repositório
	$ git push origin correcoes

# Maria vai consultar se existe algo novo no repositório antes de voltar a trabalhar
	$ git pull -force

# após puxa os arquivos:
	$ git pull origin correcoes-v1.0

# Maria trabalha no arquivo
# Maria vai unir o que foi feito
# para isso deve estar na branch "master"
	$ git checkout master

# após isso faz a união dos arquivos do projeto
# após empurra os arquivos para o repositório
	$ git push origin master

# Maria cria uma nova branch com as correções
	$ git tag v1.1

# Maria envia a tag para o repositório
	$ git push origin v1.1 (nome-da-tag)

# acessa quem quer e tem acesso
```

# atualizar a página web do github, nota-se que os arquivos do local agora estão lá

# verificar se existe algum repositório remoto registrado ou
# ver a lista dos repositórios remotos registrados no local
	$ git remote -v
```


==Observações:==
- para o git salvar as credenciais de acesso ao bare remoto e não ser solicitado no próximo push, execute seguinte comando:
	$ git config credential.helper store


#### Usando git clone e git pull
``` shell
# clonando um repositório existente no github, baixando no repositório local
	$ git clone https://github.com/jfpadilha/geek-git1.git .	(.) para não trazer a pasta toda

# "pull" é o comjunto do (fetch + merge)
	$ git pull origin branchName
```


#### Adicionando colaboradores ao seu projeto
- Um desenvolvedor fez clone do meu projeto
- ele consegue ver os commits, criar branchs, adicionar e alterar os arquivos do projeto
- Esse desenv não consegue fazer push, pois não tem permissão no repositório github para enviar arquivos.

#### Permitindo usuários no gitHub
- Acesso sua conta no gitHub
- abra o projeto
- acesse "Settings"
- acesse "Manage access"
- clique em "Invite a collaborator"
- insira  e-mail do colaborador
- agora o colaborador precisa acessar seu email e abrir o link que lhe foi enviado
- o colaborador abriu o link que recebeu do github, deve clicar em "View invitation" e clicar em "Acept invitation"
- Após isso o novo colaborador possui permissão para fazer push no projeto
- Para adicionar mais colaboradores, basta reiniciar todo esse processo
- No github, pode-se adicionar uma quantidade ilimitada para projetos públicos e máximo 3 pessoas em repositórios privados _(conta gratuita)_

#### Consultando o histórico de commits
``` shell
# No repositório local para consultar a lista dos commits

	$ git reflog			# (mostra todo o histórico dos commits, incluindo as correções)
	$ git log 				# (mostra a lista dos commits em formato normal)
	$ git log --oneline 	# (mostra os commits de forma resumida)
	$ git log -para 		# (mostra o que foi alterado no arquivo e adicionado no commit)
	$ git log -p -2		 	# (mostra o que foi alterado nos últimos 2 commits)
	$ git log -p file.txt 	# (mostra as alterações do arquivo chamdo file.txt)
	$ git log --merges 		# (mostra apenas os commits de merge)
```
#### Visualizando detalhes dos commits (Git show)
``` shell
	$ git show				# (mostra detalhes do último commit)
	$ git show 1.4			# (mostra o commit da tag nomeada 1.4)
	$ git show master		# (mostra o último commit da branch master)
	$ git show-branch		# (mostra o último commit da branch master)
```
- No github:
	- acesse o projeto
	- abrir aba "Code"
	- abrir a lista de commits

#### Desfazendo com checkout _(voltando estado inicial)_
- Feita uma edição no projeto
- antes do de enviar para o estágio "tracked" (git add .)
- percebe-se que foi feito algo errado, é decidido então revogar o cógido para o original antes da edição
- caso o arquivo já estaja em staged faz-se necessário:
``` shell
	$ git restore --staged fileName.txt
#e então
	$ git checkout -- .		#(menos menos epaço e ponto)
```

#### Desfazendo apenas um arquivo entre vários modificados:
```shell
	$ git checkout -- fileName.txt 	
```


#### Voltando um arquivo que já está no tracked (git add .) antes do staged _(commit)_
```shell
	$ git checkout HEAD -- .			# (com ponto no final é vale para todos os arquivos)
# OU
	$ git checkout HEAD -- fileName.txt # (apenas o arquivo fileName.txt)
```

#### Desfazendo com Revert e Reset
#### Revert - como e quando usar
- adicionada uma linha de código em um arquivo
- realizado um commit
```shell
	$ git revert <commit-Id-Old>
```
- o git cria um novo commit com novo id E
- remove a linha adicionada no commit de cima

_<sub>é o mesmo processo que editar o mesmo arquivo, remover o código adicionado anteriormente, e efetuar outro commit, mas, desse modo, usando "revert" teremos todo o histórico do processo, navegando entre os commitos</sub>_

###### ---> Na prática:
- após commitar vamos reverter
```shell
	$ git revert fd14d80
```
- o git irá abrir um editor de texto (vim), então salva-se esse arquivo após isso sair
- se for no vim usar o comando ":wq"
- revert realizado!
- pode-se fazer o push

#### Reset - como e quando usar
- feito seus ajustes no projeto e realizado o commit
- se faz necessário desfazer o código, bem como o commit, já que não pretende deixar esse processo nos logs do git
- então nesse caso pode-se utilizar o "reset"
```shell
	$ git reset --soft HEAD~1	# (o último número, é referente a quantidade de commits que se deseja 
	voltar)
```

- após isso, a quantidade de commits foi desfeito e os arquivos volta para o estagio "modified"
- agora pode-se fazer as alterações manuais, ou voltar o código ao original ($ git checkout -- .)
- Ao realizar push, poderá mostrar o seguinte erro:
	**"error: failed to push some refs to 'https://github.com/youraccount/yourproject.git'""
- significa que no github/bitbucket está diferente do repositório local, faz-se necessário rodar um "pull" para somente após realizar o "push"

#### Conflitos com Merge
- primeiramente, conflito não é comum, se ocorrrer existem erros na divisão das tarefas
- quando 2 ou mais desenvs alteram o mesmo arquivo, ficam "conflitos em anerto"
- Basta configurar da melhor forma, após pode-se 
---> resolvendo:
```shell
# ao editar o código de algum arquivo e após executar a sequencia normal:
	$ git add . -> 
	$ git commit -m "coments"
	$ git push origin master

# na sequencia ao fazer push com o comando:
	$ git push -u origin master

# vai apresemtar o erro:
#"Failed to push, some ref to tth...."

# então realizar primeiramente:
	$ git pull origin master
	
# vai fazer pull mas ao mesmo tempo vai mostrar que possui erros

# o git irá marcar o arquivo com os conflitos encontrados

# remover os sinais que ficaram no commit
```

---> nova tentativa
```shell
	$ git status 		# (e veja as alterações)
	$ git push origin master
```


#### Trabalhando com Issues
###### Parte 1
- No github abra o projeto
- Clicar em "issues"
- ali pode-se abrir um protocolo para ajuste de algum item do projeto, como um ticket
- Na hora de abrir, basta informar um título para o ticket, e informar o descritivo do chamado.

###### Parte 2
- pelo terminal acessar o projeto
- alterar o(s) arquivo(s) conforme ajuste solicitado na issue
```shell
	$ git add .
	$ git commit -m "Mensagem do commit. Closes #1"		
# assim encerra-se a issue com "Closes" + "#1" que é o número da issue
```

#### Dica sobre issu
- Crie seu projeto
- Abra a tela "issues"
- Crie ali dentro todas as tarefas
- Assim que vá resolvendo vai commitando o projeto

#### Fork
- Basicamente: o Fork é obter uma "cópia" de um outro projeto para seu repositório, para que se modifique ou se dê continuidade no projeto

#### Sobre Pull Request
- Requisição de pull:
	_É fazer uma solicitação para o dono do projeto original, para que o mesmo avalie seu código e insira o mesmo no projeto original._
***
***

#### Dica de inicialização de 2 formas:
###### Forma 1
```shell 
# Create a new repository on the command line

# echo "# Nome-do-Projeto" >> README.md
$ git init
$ git add README.md
$ git commit -m "first commit"
$ git branch -M master
$ git remote add origin https://github.com/username/nomeDoProjeto.git
$ git push -u origin master
```

###### Forma 2
```shell
# push an existing repository from the command line

$ git remote add origin https://github.com/username/nomeDoProjeto.git
$ git branch -M master
$ git push -u origin master
```
###### Forma 3
```shell
$ git pull -f origin master # irá forçar a baixar a branch master, para isso primeiro criar o repositorio no github
```

#### Salvar token github para não precisar inserir token/senha toda hora:
```shell
# ao fazer push, informar login e token, após executar o comando abaixo:
	$ git config --global credential.helper cache
```
<br>

<sub>_Vem mais conteúdo por aí..._</sub>
