# Brute Force & Enumeração — Hands-On (Kali Linux / DVWA / Metasploitable)

**Resumo**  
Projeto prático realizado no curso *Cibersegurança Santander 2025 (DIO)*. Objetivo: executar técnicas de enumeração e ataques de força bruta em ambiente controlado (Kali Linux + Metasploitable2 / DVWA), documentar os passos e evidências e entregar resultados em repositório público.

---

## 🧭 Objetivos
- Reconhecimento e enumeração de portas/serviços (Nmap).
- Identificação de serviços vulneráveis (FTP, SMB, HTTP).
- Ataques de força bruta em serviços (Medusa/Hydra).
- Validação de acessos com smbclient/ftp.
- Documentar evidências e reproduzir procedimentos em ambiente controlado.

---

## 🛠️ Ambiente utilizado
- Kali Linux (VM) — atacante
- Metasploitable2 / DVWA (VM) — alvo
- Rede privada (VirtualBox Host-Only)
- IP alvo no laboratório: `192.168.56.101`

> **Aviso ético**: este material foi gerado em ambiente controlado e autorizado para fins educacionais. Não execute testes contra sistemas sem permissão escrita.

---

## ⚙️ Comandos e fluxo usado (exemplos)
**Reconhecimento (Nmap)**  
```bash
nmap -sV -p 21,22,80,139,445,3389 192.168.56.101
