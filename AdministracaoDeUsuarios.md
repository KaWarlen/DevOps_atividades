# Exercícios - Administração de Usuários e Permissões no Linux

**1. Cadastre os usuários alice, bob, carlos, daniel e erica.**

```bash
sudo useradd alice
sudo useradd bob
sudo useradd carlos
sudo useradd daniel
sudo useradd erica
```

**2. Crie no seu diretório home os diretórios `produção`, `rh`, `financeiro` e `ti`.**

```bash
cd ~
mkdir produção rh financeiro ti
```

**3. Cadastre os grupos `funcionarios`, `gerentes` e `informatica`.**

```bash
sudo groupadd funcionarios
sudo groupadd gerentes
sudo groupadd informatica
```

**4. Colocar os usuários dentro do grupo conforme abaixo:**
- **funcionarios:** alice, daniel, erica.
- **gerentes:** bob, carlos.
- **informatica:** carlos, alice.

```bash
sudo usermod -aG funcionarios alice
sudo usermod -aG funcionarios daniel
sudo usermod -aG funcionarios erica

sudo usermod -aG gerentes bob
sudo usermod -aG gerentes carlos

sudo usermod -aG informatica carlos
sudo usermod -aG informatica alice
```

**5. Alterar o usuário dono dos diretórios conforme abaixo:**
- **produção:** usuário dono bob e grupo funcionarios.
- **rh:** usuário dono erica e grupo gerentes.
- **financeiro:** usuário dono bob grupo gerentes.
- **ti:** usuário dono carlos grupo informatica.

```bash
sudo chown bob:funcionarios ~/produção
sudo chown erica:gerentes ~/rh
sudo chown bob:gerentes ~/financeiro
sudo chown carlos:informatica ~/ti
```

**6. Altere as permissões dos diretórios conforme abaixo:**
- **produção:** Usuário e outros somente leitura. Grupo leitura, escrita e execução. 
- **rh:** Usuário e outros sem permissão. Grupo leitura, escrita e execução.
- **financeiro:** Usuário somente leitura, grupo escrita e execução e outros nenhuma.
- **ti:** Usuário leitura, escrita e execução, grupo leitura e outros nenhuma.
   
> **Observação:** Em cada item faça a alteração das permissões no modo octal e no modo literal.

```bash
# produção (Octal: 474 | Literal: u=r,g=rwx,o=r)
chmod 474 ~/produção
chmod u=r,g=rwx,o=r ~/produção

# rh (Octal: 070 | Literal: u=,g=rwx,o=)
chmod 070 ~/rh
chmod u=,g=rwx,o= ~/rh

# financeiro (Octal: 430 | Literal: u=r,g=wx,o=)
chmod 430 ~/financeiro
chmod u=r,g=wx,o= ~/financeiro

# ti (Octal: 740 | Literal: u=rwx,g=r,o=)
chmod 740 ~/ti
chmod u=rwx,g=r,o= ~/ti
```

**7. Supondo os detalhes dos arquivos pertencentes a um determinado diretório, analise a figura 1 e responda o que se pede:**

*(Figure 1: Resultado Obtido do comando ls -l)*

**a) Quais os nomes dos diretórios contidos nessa relação? Qual o nome dos arquivos contidos nesta relação?**
- **Diretórios:** pgms, teste1, teste2 e Faturamento.
- **Arquivos:** Controle, mbox, exemplo e Linux.

**b) Existe algum usuário do mesmo grupo de Rui? Caso positivo, qual?**
- Sim, Pedro e Tiago.

**c) Qual o tamanho do arquivo Controle?**
- 1565 bytes.

**d) Quais as permissões de acesso que os usuários do mesmo grupo de João possuem para acessar o arquivo Controle?**
- Leitura, Escrita e Execução (`rwx`).

**e) Eu sou do grupo do usuário Pedro, que permissões tenho com relação ao arquivo exemplo?**
- Leitura e execução (`r-x`).

**f) Diga o comando completo para permitir que os usuários do mesmo grupo de Rui possam ler e gravar, mas não possam executar o arquivo Linux.**
- `sudo chmod 764 Linux`
   
**g) Qual o código octal para a permissão de acesso do arquivo exemplo?**
- `755`

**h) Qual o código literal para a permissão de acesso do arquivo exemplo?**
- `u=rwx,g=rx,o=rx`

**i) Altere o dono do arquivo Linux para Rui.**
- `sudo chown Rui Linux`

**j) Altere o grupo do arquivo Linux para Staff.**
- `sudo chown :staff Linux`
