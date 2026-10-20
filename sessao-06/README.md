# 🛡️ Laboratório Sincrono | Sessão 6: Processos e Monitorização de Sistemas

<p align="center">
  <b>Módulo:</b> Segurança Linux & Ops — Skodji Digital (Percurso Activation)<br>
  <b>Projeto:</b> Learn2Earn / CVTECH Lda.<br>
  <b>Plataforma:</b> WSL2 (Ubuntu) / KillerCoda Playground<br>
  <b>Autor:</b> CV BOY RECORDS PRODUCTIONS
</p>

---

## 📋 1. Resumo Executivo e Cenário

Nesta sessão atuámos sob pressão como **Administradores de Sistemas** da **CVTECH Lda.** para diagnosticar e mitigar um incidente de esgotamento de recursos (`CPU a 100%`) provocado por um script de sincronização com defeito (`cvtech-sync.sh`) e um processo resistente a sinais de terminação (`cvtech-relatorio.sh`)[cite: 28, 29, 36]. Utilizámos ferramentas avançadas de inspeção de processos (`ps`, `top`, `htop`), gestão de sinais (`SIGTERM` vs `SIGKILL`) e auditoria de logs operacionais[cite: 29, 30, 31].

---

## 🛠️ 2. Resolução dos Desafios Passo a Passo

### Desafio 1: Observar e Controlar Processos
* Validação de ferramentas de monitorização e extração de fotografias de processos (`ps aux`, `top`, `htop`)[cite: 30].
* Gestão prática de tarefas em segundo plano (`&`, `jobs`, `fg`, `bg`, `kill %1`)[cite: 30].
> 📸 **Evidência guardada:** `sessao6_desafio1_jobs.png`

### Desafio 2: Diagnóstico Sob Pressão e Gestão de Sinais
* Execução do cenário de incidente simulado via script autónomo[cite: 31, 36].
* Identificação do processo culpado através da ordenação por consumo de CPU (`ps aux --sort=-%cpu`)[cite: 32].
* Aplicação bem-sucedida de `SIGTERM` (sinal 15) no script de sync e demonstração técnica de resistência no script de relatório (protegido por `trap "" TERM`), exigindo o recurso estrito a `SIGKILL` (sinal 9) coordenado pelo kernel[cite: 31, 32].
> 📸 **Evidência guardada:** `sessao6_desafio2_diagnostico.png`
> 📸 **Evidência guardada:** `sessao6_desafio2_log.png`

### Desafio 3: Logs do Sistema e Relatório do Incidente
* Inspeção de registos de autenticação e histórico de comandos administrativos `sudo`[cite: 33].
* Registo cronológico do incidente extraído de `servidor.log` e consolidação no relatório técnico final.
> 📸 **Evidência guardada:** `sessao6_desafio3_logs.png`
> 📄 **Relatório gerado:** `relatorio_incidente.txt`

---

## 💡 3. Questões de Análise e Reflexão Técnica

* **Porque é que se deve tentar sempre `kill` (`SIGTERM`) antes de `kill -9` (`SIGKILL`)?**[cite: 32, 33]
  * O `SIGTERM` (15) envia um pedido educado para que o processo termine de forma graciosa, permitindo-lhe libertar recursos, fechar bases de dados abertas, gravar dados em cache e terminar sessões sem corrupção. O `SIGKILL` (9) é executado diretamente pelo kernel sem aviso prévio, impedindo qualquer salvaguarda de estado. Deve ser sempre o último recurso.
* **Que vantagens tem o `journalctl` em relação a ler ficheiros de texto com `tail` e `grep`?**
  * O `journal` armazena os logs de forma binária e estruturada, permitindo filtros avançados instantâneos por ID de processo, UID, unidade de sistema (`_COMM`), prioridade ou intervalos de tempo precisos, além de garantir maior integridade contra adulteração de texto.
* **Porque é que um relatório de incidente deve incluir a hora em que o problema começou e a hora em que foi resolvido?**
  * Permite calcular o **MTTR (Mean Time To Recovery / Tempo Médio de Recuperação)**, auditar o impacto operacional na empresa, cruzar dados com picos de tráfego de clientes e validar a eficácia da resposta da equipa de operações.

---
<p align="center">
  <b>CV BOY RECORDS PRODUCTIONS</b> • Resiliência Operacional e Resposta a Incidentes 🚀
</p>
