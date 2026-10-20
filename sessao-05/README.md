# 🛡️ Laboratório Sincrono | Sessão 5: Permissões, Controlo de Acessos e Autenticação

<p align="center">
  <b>Módulo:</b> Segurança Linux & Ops — Skodji Digital (Percurso Activation)<br>
  <b>Projeto:</b> Learn2Earn / CVTECH Lda.<br>
  <b>Plataforma:</b> WSL2 (Ubuntu) / KillerCoda Playground<br>
  <b>Autor:</b> CV BOY RECORDS PRODUCTIONS
</p>

---

## 📋 1. Resumo Executivo e Cenário

Nesta sessão configurámos o servidor de ficheiros departamental da **CVTECH Lda.**, aplicando o modelo de permissões tradicional do Linux (`chmod`, `chown`, `chgrp`) para isolar pastas por departamento. Implementámos também políticas de segurança de contas, expiração de passwords com o comando `chage` e mecanismos de bloqueio/auditoria[cite: 18].

### Tabela de Permissões das Pastas Departamentais

| Caminho da Pasta | Dono : Grupo | Permissões Octal | Política de Acesso |
| :--- | :--- | :--- | :--- |
| `/srv/cvtech/rh` | `root:rh` | `770` (`rwxrwx---`) | Apenas membros do departamento de RH (`alice`)[cite: 18] |
| `/srv/cvtech/ti` | `bruno:ti` | `770` (`rwxrwx---`) | Apenas membros do departamento de TI (`bruno`)[cite: 18] |
| `/srv/cvtech/financas` | `root:financas` | `770` (`rwxrwx---`) | Apenas membros do departamento de Finanças (`carla`)[cite: 18] |
| `/srv/cvtech/publico` | `root:root` | `755` (`rwxr-xr-x`) | Leitura pública; escrita restrita ao administrador (`root`)[cite: 18] |

---

## 🛠️ 2. Resolução dos Desafios Passo a Passo

### Desafio 1: Leitura de Permissões e Estrutura Inicial
* Análise comparativa das permissões de leitura entre `/etc/passwd` (`644`) e `/etc/shadow` (`640`)[cite: 19].
* Criação da árvore de diretórios do servidor sob `/srv/cvtech/`[cite: 19].
> 📸 **Evidência guardada:** `sessao5_desafio1_leitura.png`

### Desafio 2: Aplicação de Permissões e Testes de Acessos Cruzados
* Atribuição correta de grupos e donos utilizando `chgrp` e `chown`[cite: 20].
* Aplicação de restrições estritas com `chmod 770` e `chmod 640` no ficheiro confidencial de RH (`confidencial.txt`)[cite: 20].
* Validação prática de isolamento utilizando `sudo -u` (garantindo que a Carla recebe `Permission denied` ao tentar ler dados do RH ou entrar na pasta de TI)[cite: 21].
> 📸 **Evidência guardada:** `sessao5_desafio2_acessos.png`

### Desafio 3: Autenticação, Hardening e Política de Passwords
* Inspeção dos parâmetros globais em `/etc/login.defs` e auditoria de hashes em `/etc/shadow`[cite: 22].
* Aplicação de política de expiração estrita na conta da Carla (`chage -M 90 -W 7 -I 30`)[cite: 22].
* Demonstração de procedimentos de bloqueio (`passwd -l`) e desbloqueio (`passwd -u`) de contas em cenários de incidentes.
* Verificação de atividade do utilizador com o utilitário `lastlog2`[cite: 23].
> 📸 **Evidência guardada:** `sessao5_desafio3_politica.png`
> 📄 **Relatório gerado:** `auditoria_acessos.txt`[cite: 23]

---

## 💡 3. Questões de Reflexão Técnica

* **Qual é a vantagem de bloquear uma conta com `passwd -l` em vez de a remover com `userdel`?**
  * O bloqueio preserva o histórico, os ficheiros pessoais, as configurações e os registos associados à conta para efeitos de auditoria ou investigação forense, permitindo reativá-la instantaneamente após a resolução do incidente.
* **Porque é que a Carla consegue listar a pasta pública mas não criar lá ficheiros?**[cite: 21, 24]
  * A pasta pública possui permissões `755` (`rwxr-xr-x`), onde o grupo e os outros possuem permissão de leitura (`r`) e execução (`x`, necessária para entrar na pasta e listar conteúdos), mas não possuem a permissão de escrita (`w`).
* **Numa pasta, qual é a diferença entre `r` e `x`?**[cite: 19]
  * A permissão `r` (*read*) permite listar os nomes dos ficheiros contidos na pasta. A permissão `x` (*execute*) é indispensável para atravessar o diretório, aceder aos metadados e abrir os ficheiros lá dentro. Sem `x`, o acesso é vedado mesmo que haja permissão `r`.

---
<p align="center">
  <b>CV BOY RECORDS PRODUCTIONS</b> • Operação Digital Resiliente e Segura 🚀
</p>
