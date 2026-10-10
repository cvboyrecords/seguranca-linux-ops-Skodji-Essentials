# Relatório de Auditoria — Sessão 3 (Segurança Linux & Ops)
**Responsável:** Florivindo Semedo Monteiro  
**Módulo:** Segurança Linux & Ops · Skodji Digital  

## Sumário das Atividades Realizadas
- **Desafio 1:** Pesquisa avançada de logs e auditoria de credenciais em texto claro utilizando opções do `grep` (`-c`, `-ic`, `-in`, `-n`, `-v`, `-rn`, `-rli`).
- **Desafio 2:** Utilização de `head`, `tail`, contagens com `wc`, encadeamento de comandos com pipes (`|`), ordenação (`sort`), contagem de ocorrências (`uniq -c`) e construção de rankings de incidentes e IPs suspeitos.
- **Desafio 3:** Demonstração prática do perigo dos operadores de redirecionamento (`>` vs `>>`) e geração automática do relatório de auditoria consolidado.

---

## Conteúdo do Relatório de Auditoria (`relatorio_auditoria.txt`)

```text
===== RELATÓRIO DE AUDITORIA — CVTECH Lda. =====
Data: Sat Oct 10 12:21:54 CEST 2026
--- ESTRUTURA ---
/home/pc/empresa
├── README.md
├── financas
│   ├── backup
│   │   └── orcamento_2026.bak
│   └── orcamento_2026.txt
├── rh
│   ├── arquivo_2026
│   │   └── relatorio_jan.txt
│   ├── contrato_alice_v1.txt
│   ├── relatorio_fev.txt
│   └── relatorio_mar.txt
└── ti
    ├── acessos.log
    ├── config.log
    ├── deploy.sh
    └── erros.log

6 directories, 11 files
--- ERROS NOS LOGS DE TI ---
2026-10-12 08:05 ERRO falha de conexão à base de dados
2026-10-12 08:15 ERRO timeout na API REST após 30s
2026-10-12 08:25 ERRO autenticação falhou para o utilizador admin
2026-10-12 08:26 ERRO autenticação falhou para o utilizador admin
2026-10-12 08:27 ERRO autenticação falhou para o utilizador root
2026-10-12 08:50 ERRO serviço de email não responde
Total de erros: 6
--- CREDENCIAIS EM TEXTO CLARO ---
/home/pc/empresa/ti/config.log:6:DB_PASSWORD=CvTech2026!
/home/pc/empresa/ti/config.log:7:# Política: a password deve ter pelo menos 12 caracteres
/home/pc/empresa/ti/config.log:9:smtp_password=Email#2026
/home/pc/empresa/ti/deploy.sh:5:Password="Deploy#2026"
--- IPs COM MAIS FALHAS DE LOGIN ---
      6 ip=203.0.113.7
      2 ip=198.51.100.23
      1 ip=192.0.2.44
      1 ip=10.0.0.12
