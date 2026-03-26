# Exercícios - Comandos Linux (grep, sed, head, tail, cut)

**1. Alguém acaba de doar um laptop para sua escola e você deseja instalar Linux nele. Ele veio sem manual e você é obrigado a inicializá-lo a partir de um pen drive USB sem nenhuma interface gráfica. Aparece um terminal shell e você sabe que, para cada processador presente, haverá uma linha dedicada no arquivo `/proc/cpuinfo`:**

**(a) Usando os comandos `grep` e `wc`, exiba o número de processadores presentes.**
```bash
grep "processor" /proc/cpuinfo | wc -l
```

**(b) Faça o mesmo com `sed` em vez de `grep`.**
```bash
sed -n '/processor/p' /proc/cpuinfo | wc -l
```

**2. Explore seu arquivo local `/etc/passwd` com os comandos `grep`, `sed`, `head` e `tail` de acordo com as tarefas descritas abaixo:**

**(a) Quais usuários têm acesso a um shell Bash?**
```bash
grep "/bin/bash" /etc/passwd
# Ou com sed:
sed -n '/\/bin\/bash/p' /etc/passwd
```

**(b) Muitos dos usuários de seu sistema existem para lidar com programas específicos ou para fins administrativos. Eles não têm acesso a um shell. Quantos deles estão presentes no sistema?**
```bash
grep -E "nologin|false" /etc/passwd | wc -l
```

**(c) Quantos usuários e grupos existem em seu sistema (lembre-se: use apenas o arquivo `/etc/passwd`)?**
```bash
# Total de Usuários
sed -n '$=' /etc/passwd

# Total de Grupos
sed 's/^[^:]*:[^:]*:[^:]*:\([^:]*\):.*/\1/' /etc/passwd | grep '^1000$'
```

**(d) Liste apenas a primeira, a décima e a última linha do arquivo `/etc/passwd`.**
```bash
# Primeira linha
head -n 1 /etc/passwd 

# Décima linha
head -n 10 /etc/passwd | tail -n 1

# Última linha
tail -n 1 /etc/passwd
```

**3. Considere um arquivo de exemplo `/etc/passwd`. Copie as linhas dele para um arquivo local chamado `mypasswd` para este exercício.**

**(a) Liste todos os usuários no grupo 1000 (use `sed` para selecionar apenas o campo apropriado) do arquivo `mypasswd`.**
```bash
sed -n '/^[^:]*:[^:]*:[^:]*:1000:/s/:.*//p' mypasswd
```

**(b) Liste apenas o nome completo de todos os usuários deste grupo (use `sed` e `cut`).**
```bash
sed -n '/:1000:/p' mypasswd | cut -d: -f5
```

**4. Usando novamente o arquivo `mypasswd` dos exercícios anteriores, imagine um comando Bash que selecione um indivíduo do Main Office para ganhar uma rifa. Use o comando `sed` para imprimir apenas as linhas do Main Office e, em seguida, uma sequência de comando `cut` para recuperar o primeiro nome de cada usuário a partir dessas linhas. Depois, classifique esses nomes aleatoriamente e imprima apenas o nome principal da lista.**
```bash
sed -n '/Main Office/p' mypasswd | cut -d: -f5 | cut -d' ' -f1 | shuf | head -n 1
```
