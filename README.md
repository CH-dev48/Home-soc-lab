# 🛡️ Home-Soc-Lab: Implementação e Monitoramento com Wazuh SIEM

## 📖 Sobre o Projeto
Este projeto consiste na construção de um laboratório de *Security Operations Center* (SOC) para simular um ambiente corporativo. O objetivo principal é aplicar técnicas de Tratamento e Resposta a Incidentes (IH&R), utilizando o Wazuh (SIEM open-source) para coletar, normalizar e correlacionar logs de endpoints.

A centralização dos logs no SIEM otimiza o trabalho da equipe, permitindo a análise de incidentes sem a necessidade de acessar individualmente cada ativo da rede.

## 🏗️ Topologia e Arquitetura
* **Manager/SIEM:** Ubuntu Server (VM) executando o Wazuh Manager.
* **Endpoint Monitorado:** Windows 10 (VM) com o Wazuh Agent instalado.
* **Configurações Customizadas:** Foram aplicadas regras personalizadas no arquivo `local_rules.xml` para refinar a detecção de ameaças.

## ⚔️ Simulação de Ameaças (Threat Hunting) e Mapeamento MITRE ATT&CK
Foram realizados testes práticos de intrusão e evasão, mapeados diretamente no framework MITRE ATT&CK para garantir uma inteligência orientada ao contexto das ameaças modernas.

### 1. Ataque de Força Bruta (Brute Force)
* **Tática:** Credential Access
* **Técnica:** T1110
* **Descrição:** Execução de script PowerShell simulando múltiplas falhas de autenticação (`Event ID 4625`).
* **Evidência:** ![Força Bruta](Cenario1_ForcaBruta_Dashboard.jfif)

### 2. Escalonamento de Privilégios (Criação de Administrador Oculto)
* **Tática:** Privilege Escalation / Persistence
* **Técnica:** T1136.001 (Local Account)
* **Descrição:** Criação não autorizada do usuário `attacker_admin` via linha de comando.
* **Evidência:** ![Escalonamento](Cenario1_ForcaBruta_Detalhe.png)

### 3. Evasão de Defesa e Execução Suspeita (DLL Hijacking)
* **Tática:** Defense Evasion / Privilege Escalation
* **Técnica:** T1574.001 (DLL Search Order Hijacking)
* **Descrição:** Detecção avançada de criação de arquivos `.ps1` e carregamento suspeito de DLLs em pastas críticas do Windows.
* **Evidência:** ![DLL Hijacking](Cenario3_evasao_DLL.png)
### 4. Execução de Script Suspeito (Evasão via PowerShell)
* **Tática:** Execution / Defense Evasion
* **Técnica:** T1059.001 (Command and Scripting Interpreter: PowerShell)
* **Descrição:** Monitoramento do Sysmon (Event ID 11) detectou a criação de arquivos temporários `.ps1` durante a execução de comandos ofuscados ou scripts maliciosos.
* **Evidência:** ![Execução de Script](Cenario3_Evasao_ScriptPowerShell.png)

*(Nota: Outra técnica de Evasão de Defesa mapeada no laboratório foi a T1070 - Limpeza de Logs de Eventos do Windows).*

---
*Projeto desenvolvido para fins educacionais e aprimoramento em Cibersegurança.*
