🔐 Projeto Prático: Simulação de Ataques de Força Bruta com Kali Linux e Medusa
📌 Objetivo do Projeto

Implementar, documentar e compartilhar um projeto prático utilizando o Kali Linux e a ferramenta Medusa, em conjunto com ambientes vulneráveis como Metasploitable 2 e DVWA (Damn Vulnerable Web Application), com o objetivo de simular cenários reais de ataque de força bruta e aplicar medidas de prevenção.

Este projeto tem fins exclusivamente educacionais e visa desenvolver competências em:

🔎 Enumeração de serviços

⚔️ Ataques de força bruta

🔐 Password Spraying

🌐 Análise de vulnerabilidades web

🛡️ Implementação de medidas defensivas

🖥️ Ambiente de Laboratório

O laboratório foi configurado em ambiente virtual isolado para garantir segurança durante os testes.

Hypervisor: VirtualBox

Máquina Atacante: Kali Linux

Máquina Alvo: Metasploitable 2

Aplicação Web Vulnerável: DVWA

Tipo de Rede: Host-Only (ambiente isolado)

🔎 1️⃣ Enumeração Inicial com Nmap

A fase de reconhecimento é fundamental para identificar portas abertas e serviços ativos.

Comando utilizado:
sudo nmap -sV 192.168.56.102
Principais Serviços Identificados:
Porta	Serviço	Versão	Risco
21	FTP	vsftpd 2.3.4	Crítico
23	Telnet	Linux telnetd	Crítico
80	HTTP	Apache 2.2.8	Médio
445	SMB	Samba 3.x	Alto
3306	MySQL	5.0.51a	Médio
⚔️ 2️⃣ Ataque de Força Bruta – FTP

Foi utilizado o Medusa para realizar um ataque de dicionário contra o serviço FTP.

Comando:
medusa -h 192.168.56.102 -U users.txt -P passwords.txt -M ftp
Resultado:

Usuário: msfadmin

Senha: msfadmin

Status: SUCCESS

Análise:

O ataque foi bem-sucedido devido à ausência de bloqueio de conta e uso de credenciais padrão. Isso demonstra a importância do hardening básico em servidores.

💻 3️⃣ Password Spraying – SMB

Técnica utilizada para testar uma única senha contra múltiplos usuários, reduzindo risco de bloqueio.

Comando:
medusa -h 192.168.56.102 -U users.txt -p msfadmin -M smbnt

Foi identificado reaproveitamento de credenciais em múltiplos serviços, facilitando possível movimentação lateral.

🌐 4️⃣ Teste em Aplicação Web – DVWA

A aplicação DVWA foi utilizada para simular ataques automatizados em formulários de login.

URL: http://192.168.56.102/dvwa

Cenário: Teste de vulnerabilidade em autenticação sem limitação de tentativas.

🛡️ Medidas de Prevenção Recomendadas

Com base nos testes realizados, recomenda-se:

✅ Implementação de políticas de senha forte

✅ Bloqueio de conta após múltiplas tentativas

✅ Uso de MFA (Autenticação Multifator)

✅ Implementação de Fail2Ban

✅ Substituição de FTP e Telnet por SFTP e SSH

✅ Monitoramento contínuo de logs

📊 Lições Aprendidas

A enumeração direciona ataques de forma estratégica.

Credenciais padrão representam alto risco.

Controles básicos poderiam mitigar a maioria dos ataques simulados.

A reutilização de senhas aumenta o impacto de invasões.

📚 Conclusão

Este projeto permitiu compreender, na prática, como ataques de força bruta são executados e como podem ser prevenidos. A experiência reforça a importância da segurança proativa e do monitoramento constante em ambientes corporativos.

⚠️ Aviso: Todos os testes foram realizados em ambiente controlado e isolado, exclusivamente para fins educacionais.
