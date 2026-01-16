📘 Guia Linux para SRE
(Em construção — conteúdo será organizado em seções focadas na prática diária de um SRE)

🟢 Conteúdo 1 — Linux Básico (Sobrevivência)
📁 **Navegação no sistema**

* `pwd` → mostra onde você está
* `ls -l` → lista com detalhes
* `cd nome_da_pasta` → entra na pasta
* `cd ..` → volta um nível
* `cd /` → vai para raiz do sistema
* `mkdir nome` → cria pasta
* `mkdir -p caminho/{a,b,c}` → cria várias pastas ao mesmo tempo
* `mkdir teste1 && cd teste1 && echo ok` → mkdir teste1 → cria um diretório chamado teste1. & → separa comandos caso de erro ele para, executando-os em sequência. cd teste1 → entra no diretório recém-criado. echo ok → imprime a palavra ok na tela.


📄 **Update**
* `apt update` → update principal linux 
* `apt list` → lista de updates
* `apt install nano` →  instalar nano (editor de texto)
* `apt remove nano` → desistalar nano


📄 **Arquivos**

* `touch arquivo.txt` → cria arquivo vazio
* `rm arquivo.txt` → remove arquivo
* `cp origem destino` → copia **arquivo/pasta**
* `mv origem destino` → move/renomeia
* `cat / less / head / tail` → ler arquivos
* `cat Arquivo_1.txt > Arquivo_2.txt ` → Faz copia do conteudo de um arquio para outro  * `cat Arquivo_1.txt  Arquivo_2.txt > Arquivo_3.txt ` → Faz copia do conteudo dos arquivos para um novo arquivo.
* `echo hi docker > docket.txt` → Escreve dentro do arquivo "hi docker"
* `find etc/kernal` →  vai listar todas pastas e arquivos com os nomes etc/kernal
* `find -type f -name "docker.txt" ` →  vai listar todos os files com nome "docker.txt" dentro do diretorio (Variação: find -type f -name "docke*.txt" => listar todos os files com inicio docke*)
* `find -type d -name "pasta_docker" ` →  vai listar todos os diretorios com o nome


🔑 **Copiar (detalhes importantes)**

* `cp arquivo1.txt pasta/` → copia **arquivo** para pasta
* `cp -r pasta1 pasta2` → copia **pasta** e todo o conteúdo (r = recursivo)
* `cp arquivo{1,2,3}.txt destino/` → copia **vários arquivos** usando `{}`
* `cp *.log logs/` → copia todos os arquivos que terminam com **.log**

✏ **Editores**
✏ Editores (Vim e Nano)
### Vim (avançado)
```
vim arquivo.txt         # abrir arquivo

# Modos
i                       # inserir texto
ESC                     # voltar para comando

# Comandos (após ESC)
:w                      # salvar
:q                      # sair
:wq                     # salvar e sair
:q!                     # sair sem salvar
u                       # desfazer
/palavra                # buscar (n = próxima)

# Edição prática
dd                      # apaga linha
yy                      # copia linha
p                       # cola linha
```

### Nano (simples)
```
nano arquivo.txt        # abrir arquivo

# Atalhos
Ctrl + O                # salvar
Ctrl + X                # sair
Ctrl + K                # recortar linha
Ctrl + U                # colar
Ctrl + W                # procurar
```

---

🔐 **Permissões básicas**

* `chmod +x arquivo.sh` → torna executável
* `ls -l` → ver permissões

---

🟡 Conteúdo 2 — Linux Intermediário (Trabalho Real)
📊 **Processos**

* `ps` → lista processos numerando com PID
* `top` → monitor em tempo real (q para sair)
* `htop` → versão melhor (se instalado)
* `kill PID` → encerra um processo

🔧 **Serviços**

* `systemctl status nome.service`
* `systemctl start nome.service`
* `systemctl stop nome.service`
* `systemctl restart nome.service`
* `systemctl enable nome.service` (iniciar no boot)

🌐 **Rede**

* `ifconfig` ou `ip a` → ver interfaces
* `ping google.com` → testar conexão
* `curl http://localhost:8080` → testar endpoint
* `ss -lntp` → portas abertas e serviços


⚙️ **Scripts básicos**
Arquivo: `start.sh`

```
#!/bin/bash
echo "Iniciando app..."
date
```

Permissão e execução:

```
chmod +x start.sh
./start.sh
```

---

🔴 Conteúdo 3 — Linux para SRE (Rotina Real)
🔁 **Troubleshooting**

* `top` → consumo de CPU
* `free -h` → memória
* `vmstat 5` → saúde do sistema
* `ping / curl` → teste de rede
* `ss -lntp` → portas abertas
* `journalctl -xe` → erros recentes do sistema

🔐 **Permissões avançadas**

* `chown usuario:grupo arquivo`
* `chmod 640 arquivo` (r/w para dono, r para grupo)
* `groups usuario` (ver grupos)
* `usermod -aG grupo usuario` (adicionar grupo)

👤 **Usuários básicos**

* `docker exec -it -u bruno c43da21ea07a7 bash` (docker exec (executa comando dentro de um container em execução) → -it (interativo + terminal) → -u bruno (define usuário dentro do container) → c43da21ea07a7 (ID ou nome do container) → bash (abre shell Bash).)
* `useradd -m usuario` (criar usuário interativo)
* `usermod  usuario` (modificar usuario)
* `userdell  usuario` (deletar usuario)
* `passwd usuario` (definir senha)
* `id usuario ` (ver UID, GID e grupos)
* `whoami`  (mostrar usuário atual)


👥 **Criação e gerenciamento de grupos**

* `groupadd grupo` (criar grupo novo)
* `groupdel grupo` (remover grupo)
* `groupmod -n novo_nome grupo` (renomear grupo)
* `groupmod -g GID grupo` (alterar o GID do grupo)
* `groups usuario` (ver grupos do usuário)
* `usermod -aG grupo usuario` (adicionar usuário ao grupo)
* `gpasswd -d usuario grupo` (remover usuário do grupo)
* `cat /etc/group` (ver grupos exisitente)

🔐 **Permissões ligadas a grupos**
ls -la
[Tipo][Dono][Grupo][Outros] 
* `chmod u+x docker.txt` (adicionar u (usuário) + x (permissão de executar) ao arquivo)
* `chgrp grupo arquivo` (mudar grupo dono do arquivo)  
* `chmod 640 arquivo` (dono: leitura/escrita, grupo: leitura, outros: sem acesso)
* `chmod 770 arquivo` (dono e grupo: leitura/escrita/execução, outros: sem acesso)
* `ls -l` (ver dono e grupo de cada arquivo)

**📂 Exemplo prático**

* `groupadd devops` (criar grupo devops)
* `usermod -aG devops bruno` (adicionar usuário ao grupo)
* `chgrp devops /projetos` (mudar grupo dono do diretório)
* `chmod 770 /projetos` (dar acesso total ao dono e grupo)

🌍 **Variáveis de ambiente**

* `echo $PATH` → caminhos de busca
* `export VAR=valor` → variável temporária
* `~/.bashrc` → tornar permanente

📌 **Estrutura de logs e apps (simulação SRE)**

```
mkdir -p ~/APPS/webapp/{logs,config,bin}
vim ~/APPS/webapp/bin/start.sh
chmod +x ~/APPS/webapp/bin/start.sh
./start.sh
```

Ver logs e filtrar:

```
tail -f ~/APPS/webapp/logs/app.log
grep ERROR ~/APPS/webapp/logs/app.log (Procurar palavra ERROR dentro de app.log)
grep ERROR ~/APPS/webapp/logs/app1.log app2.log (Procurar palavra ERROR dentro de app1.log e app2.log)
grep ERROR app* (Procurar palavra ERROR dentro de qualquer arquivo que tenha app*> exemplo:app1 app2 app3)
grep -i -r ERROR . (Procurar em tudo a palavra erro no diretorio atual)
```

---

🧠 **Resumo para Memorizar**
NAVEGAR:  `cd /` `ls` `pwd`
ARQUIVOS: `touch` `cp` `mv` `rm`
LOGS:     `grep` `tail -f` `less` `journalctl`
REDE:     `ping` `curl` `ss -lntp`
PROCESSO: `ps` `top` `kill`
PERMISSÃO: `chmod` `chown`
