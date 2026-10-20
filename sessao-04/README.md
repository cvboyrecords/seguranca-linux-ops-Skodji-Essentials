# 🛡️ Laboratório Sincrono | Sessão 4: Gestão de Utilizadores e Grupos

<p align="center">
  <b>Módulo:</b> Segurança Linux & Ops — Skodji Digital (Percurso Activation)<br>
  <b>Projeto:</b> Learn2Earn / CVTECH Lda.<br>
  <b>Plataforma:</b> WSL2 (Ubuntu) / KillerCoda Playground<br>
  <b>Autor:</b> CV BOY RECORDS PRODUCTIONS
</p>

---

## 📋 1. Resumo Executivo e Cenário

Neste laboratório atuámos como **Administradores de Sistemas** da **CVTECH Lda.** O objetivo principal foi provisionar o acesso inicial de novos colaboradores, estruturar os utilizadores por departamentos funcionais e aplicar estritamente o **Princípio do Menor Privilégio (PoLP)**, garantindo que os privilégios administrativos (`sudo`) ficassem restritos exclusivamente ao responsável de TI.

### Tabela de Atribuição de Contas

| Colaborador / Conta | Nome de Utilizador | Departamento (Grupo) | Privilégio Administrativo (`sudo`) |
| :--- | :--- | :--- | :--- |
| **Alice Fortes** | `alice` | Recursos Humanos (`rh`) | Não |
| **Bruno Lima** | `bruno` | Tecnologia de Informação (`ti`) | **Sim** |
| **Carla Santos** | `carla` | Finanças (`financas`) | Não |
| **Estagiário (Teste)** | `estagiario` | Múltiplos / Teste | Não (Conta Temporária) |

---

## 🛠️ 2. Resolução dos Desafios Passo a Passo

### Desafio 1: Criação de Grupos, Contas e Definição de Passwords

1. **Criação dos grupos departamentais:**
   ```bash
   sudo groupadd rh
   sudo groupadd ti
   sudo groupadd financas
   grep -E '^(rh|ti|financas):' /etc/group
