![GitHub](https://img.shields.io/github/license/sir0liveira/copiar-restaurar_permissoes_acl?style=flat-square) ![GitHub repo size](https://img.shields.io/github/repo-size/sir0liveira/samba4-ad?style=flat-square) 


# Copiar permissões ACL de um Servidor de Arquivos para outro.  

#### Recentimento precisei migrar um Servidor de Arquivos para um servidor Controlador de Domínio, sei que não é o ideal, porém precisei!!! :satisfied:
#### Ambos usando Linux e Samba4 (Versões Diferentes), porém mesmo criando usuário e grupo igual ao servidor antigo, no novo servidor os IDs de usuário e grupo não eram iguais e consequentimento, diretórios sincronizados para o novo servidor com erro nas permissões ACL.  

#### Sabemos que setar todas permissões novamente não seria uma tarefa nada fácil, levando em consideração a quantidade de diretórios e arquivos.
#### Mas para minha alegria consegui migrar as permissões de uma forma bem fácil e tudo funcionou perfeitamente.

### Segue como foi feito:


#### Copiar as permissões ACL do servidor de origem, acesse o diretório onde as permissões serão copiadas. Ex.:

/mnt/Arquivos

#### Execute o comando no terminal:

find * -print > /tmp/lista && xargs -d '\n' getfacl < /tmp/lista > /tmp/lista_acl 2> /dev/null && rm -f /tmp/lista


#### Copiar o arquivo "/tmp/lista_acl" para o servidor de destino

scp /tmp/lista_acl "usuario"@"ip_servidor":/tmp

#### Restaurar as permissões ACL no servidor de destino, acesse o diretório. Ex.:

/mnt/Arquivos

#### Execute o comando no terminal:

setfacl --restore=/tmp/lista_acl

#### E pronto, você terá as permissões nos diretório e arquivos como no servidor de origem e o melhor sem precisar fazer mais nada.
