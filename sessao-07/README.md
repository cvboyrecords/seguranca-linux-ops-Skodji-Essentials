# 🛡️ Laboratório Sincrono | Sessão 7: Proteção de Dados, Backup e Automação

<p align="center">
  <b>Módulo:</b> Segurança Linux & Ops — Skodji Digital (Percurso Activation)<br>
  <b>Projeto:</b> Learn2Earn / CVTECH Lda.<br>
  <b>Plataforma:</b> WSL2 (Ubuntu) / KillerCoda Playground<br>
  <b>Autor:</b> CV BOY RECORDS PRODUCTIONS
</p>

---

## 📋 1. Resumo Executivo e Cenário

Para assegurar a resiliência operacional da **CVTECH Lda.** após os incidentes anteriores, implementámos uma pipeline automatizada de salvaguarda de dados da pasta `~/empresa`. A solução integra compressão eficiente (`tar.gz`), criptografia simétrica de nível militar (`OpenSSL AES-256-CBC` com `PBKDF2`), gestão segura de segredos em modo de menor privilégio e agendamento resiliente com o `cron`[cite: 40, 41, 43].

---

## 🛠️ 2. Resolução dos Desafios Passo a Passo

### Desafio 1: Arquivamento e Compressão (`tar` & `gzip`)
* Criação de arquivos compactados da estrutura corporativa e validação de integridade através de comparação diferencial rigorosa (`diff -r`)[cite: 42].
> 📸 **Evidência guardada:** `sessao7_desafio1_tar.png`

### Desafio 2: Cifragem de Ativos (`OpenSSL`) e Gestão de Segredos
* Aplicação de cifra simétrica AES-256 com *salt* e derivação de chave robusta[cite: 43].
* Proteção do ficheiro de credenciais corporativas (`~/.backup_pass`) com permissões restritas `600`[cite: 44].
> 📸 **Evidência guardada:** `sessao7_desafio2_openssl.png`

### Desafio 3: Automação via Script Bash e Agendamento `cron`
* Desenvolvimento do script `backup_cvtech.sh` com validações preventivas de diretórios, tratamento de códigos de saída (`exit 1`) e registo em ficheiro de *log*[cite: 45].
* Agendamento operacional em ambiente de produção para execução diária automatizada às 02:30.
> 📸 **Evidência guardada:** `sessao7_desafio3_cron.png`
> 📸 **Evidência guardada:** `sessao7_desafio3_restauro.png`[cite: 47]
> 📄 **Script publicado:** `backup_cvtech.sh` (sem incluir credenciais)[cite: 47]

---

## 💡 3. Questões de Análise Técnica

* **O que aconteceria se o script não verificasse a existência do ficheiro de password antes de cifrar?**
  * O comando `openssl` tentaria prosseguir sem a chave, falharia silenciosamente ou exigiria input interativo, bloqueando o agendamento em background e gerando um backup corrompido ou vazio.
* **Os backups estão no mesmo servidor que os dados originais. Que risco isso representa e como o resolverias?**
  * Representa um **ponto único de falha (SPOF)**: em caso de desastre físico do servidor, roubo de hardware ou ataque de *ransomware* avançado que comprometa o sistema operativo, tanto os dados como os backups locais seriam perdidos. A solução adequada (Regra 3-2-1) consiste em copiar os ficheiros `.enc` cifrados para um local *offsite* remoto e imutável (ex: AWS S3, armazenamento cloud encriptado ou servidor secundário via SCP/Rsync).

---
<p align="center">
  <b>CV BOY RECORDS PRODUCTIONS</b> • Integridade, Cifra e Automação de Elite 🚀
</p>
