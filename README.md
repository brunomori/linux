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

📄 **Arquivos**

* `touch arquivo.txt` → cria arquivo vazio
* `rm arquivo.txt` → remove arquivo
* `cp origem destino` → copia **arquivo/pasta**
* `mv origem destino` → move/renomeia
* `cat / less / head / tail` → ler arquivos

🔑 **Copiar (detalhes importantes)**

* `cp arquivo1.txt pasta/` → copia **arquivo** para pasta
* `cp -r pasta1 pasta2` → copia **pasta** e todo o conteúdo (r = recursivo)
* `cp arquivo{1,2,3}.txt destino/` → copia **vários arquivos** usando `{}`
* `cp *.log logs/` → copia todos os arquivos que terminam com **.log**

✏ **Editores**

* `vim arquivo`

  * ESC → sair do modo de edição
  * `:w` → salvar
  * `:q` → sair
  * `:wq` → salvar e sair
* `nano arquivo` → editor simples

🔐 **Permissões básicas**

* `chmod +x arquivo.sh` → torna executável
* `ls -l` → ver permissões

---

🟡 Conteúdo 2 — Linux Intermediário (Trabalho Real)
📊 **Processos**

* `ps aux` → lista processos
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

📝 **Logs**

* `less /var/log/syslog`
* `journalctl -u nome.service` → logs do serviço
* `grep ERRO app.log` → filtrar erros
* `tail -f app.log` → acompanhar ao vivo

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
grep ERROR ~/APPS/webapp/logs/app.log
```

---

🧠 **Resumo para Memorizar**
NAVEGAR:  `cd /` `ls` `pwd`
ARQUIVOS: `touch` `cp` `mv` `rm`
LOGS:     `grep` `tail -f` `less` `journalctl`
REDE:     `ping` `curl` `ss -lntp`
PROCESSO: `ps` `top` `kill`
PERMISSÃO: `chmod` `chown`
