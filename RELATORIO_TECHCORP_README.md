# 🛡️ Relatório Técnico de Teste de Intrusão — TECHCORP
**Ambiente Simulado — Novembro/2025**  
**Consultor:** Fabio Sales (Pentester)

[![Status](https://img.shields.io/badge/status-critical-red)](#) [![Scope](https://img.shields.io/badge/scope-web%20%2B%20ssh%20%2B%20db-blue)](#) [![Risk](https://img.shields.io/badge/risk--level-crítico-orange)](#)

---

## Índice
- [Sobre este Relatório](#sobre-este-relatório)  
- [Metodologia](#metodologia)  
- [Sumário Executivo](#sumário-executivo)  
- [Escopo Técnico](#escopo-técnico)  
- [Principais Descobertas](#principais-descobertas)  
- [CVE / CWEs Relacionadas](#cve--cwes-relacionadas)  
- [Recomendações](#recomendações)  
- [Plano 80/20](#plano-8020)  
- [Conclusão](#conclusão)  
- [Evidências & Annexos](#evidências--annexos)  
- [Contato](#contato)

---

## Sobre este Relatório
Resumo do pentest realizado no host `98.95.207.28` (ambiente simulado). Objetivo: avaliar superfície de ataque web, serviços expostos, credenciais e impacto pós-exploração.

---

## Metodologia
- PTES, OWASP WSTG, OWASP ASVS, NIST 800-115  
- Etapas: Reconhecimento → Enumeração → Descoberta de vulnerabilidades → Exploração → Pós-exploração → Relatório

---

## Sumário Executivo
O ambiente apresentou múltiplas falhas críticas (diretórios expostos, credenciais em arquivos públicos, phpMyAdmin acessível, tokens GitHub vazados, SSH com credenciais fracas). Resultado: acesso ao DB, SSH e extração de flags. Risco geral: **CRÍTICO**.

---

## Escopo Técnico
**Host alvo:** `98.95.207.28`  
**Serviços principais identificados:**
- 80 — HTTP / Apache (diretórios expostos)  
- 2222 — SSH (login com credenciais vazadas)  
- 8080 — phpMyAdmin (acessível publicamente)  
- 3306 — MySQL (acessível via painel)

---

## Principais Descobertas
1. **Diretórios expostos** em `robots.txt` (`/admin/`, `/backup/`, `/config/`, `/.git/`) — `FLAG{r0b0ts_txt_l34k4g3}`  
2. **Credenciais de banco** em `/config/database.php.txt` — `FLAG{d4t4b4s3_cr3d3nt14ls_3xp0s3d}`  
3. **Backup público** `/backup/database_backup_2024.sql`  
4. **phpMyAdmin exposto** (porta 8080) — `FLAG{v13w_d1sc0v3ry_4dv4nc3d}`  
5. **Token GitHub** em `/.git-credentials` — `FLAG{g1t_cr3d3nt14ls_l34k}`  
6. **SSH**: `techcorp / TechCorp2024!` com `.bash_history` revelando `FLAG{b4sh_h1st0ry_l34k}`  
7. **FTP anônimo** habilitado — `FLAG{ftp_4n0nym0us_4cc3ss}`

---

## CVE / CWEs Relacionadas
- Exposição de diretórios Git — *CVE-2023-23903*  
- phpMyAdmin exposto — *CVE-2020-26935*  
- Credenciais em arquivos públicos — *CWE-522*  
- Exposição via arquivos/backups — *CWE-538*  
- Autenticação fraca — *CWE-521*

---

## Recomendações (Resumo)
**Imediatas (Críticas):**
- Remover/fechar acesso público a `/config/`, `/backup/`, `/.git/`, `/admin/`  
- Remover phpMyAdmin da internet (usar VPN / IP whitelisting)  
- Rotacionar todas as credenciais expostas (DB, SSH, GitHub tokens)  
- Invalidar token GitHub e auditar repositórios  
- Apagar/criptografar backups expostos  
- Limpar/proteger `.bash_history` e evitar comandos com credenciais em linha de comando

**Médio prazo:**
- Implementar MFA, políticas de senha forte, hardening de Apache/SSH, segregação de ambientes, auditoria contínua

---

## Plano 80/20 (Prioridades)
1. Remover diretórios expostos  
2. Rotacionar senhas e tokens  
3. Remover phpMyAdmin da internet  
4. Bloquear acesso a `.git` e backups  
5. Hardening SSH e limpar históricos

---

## Conclusão
Ambiente com vulnerabilidades de alto impacto que permitem comprometimento fácil. Aplicação urgente das correções listadas é mandatória para reduzir risco.

---

## Evidências & Annexos
Prints, comandos (curl, nmap, ffuf, ssh), arquivos e listas de flags estão anexados no relatório completo (ver `RELATORIO_FINAL_M3_CYBER_SEC.pdf`).

---

## Contato
**Fabio Sales** — Pentester  
(Use as informações de contato internas para comunicação segura)

---

> _Gerado automaticamente a partir do relatório técnico._
