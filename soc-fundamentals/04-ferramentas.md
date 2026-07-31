# Ferramentas de um SOC

## Habilidades base para um SOC Analyst

- **Operating Systems:** familiaridade com Windows e Linux facilita a investigação de incidentes, análise de logs e identificação de ameaças.
- **Network:** conhecimentos básicos de redes são necessários para identificar vazamentos de dados, analisar tráfego e investigar IPs, domínios e URLs maliciosos.
- **Malware Analysis:** importante para entender o comportamento e o objetivo de um malware, como ele infecta o sistema, se comunica com servidores C2 e quais impactos pode causar.

## SIEM (Security Information and Event Management)

Solução que coleta, centraliza, correlaciona e analisa logs de diferentes dispositivos e sistemas em tempo real, com o objetivo de detectar ameaças e gerar alertas.

**Principais funções para o analista:**
- Coletar logs de diversas fontes.
- Filtrar e correlacionar eventos.
- Detectar atividades suspeitas.
- Gerar alertas de possíveis incidentes.
- Auxiliar na investigação.

**Exemplos:** IBM QRadar, ArcSight ESM, FortiSIEM, Splunk, Microsoft Sentinel, Wazuh.

## Log Management

Centraliza os logs de toda a infraestrutura de TI em um único lugar (firewalls, proxies, servidores Windows/Linux, Exchange, Active Directory, EDRs, aplicações web etc.), evitando a necessidade de acessar cada dispositivo separadamente.

Facilita a investigação de incidentes, identificação de acessos suspeitos, detecção de conexões indevidas e verificação de comunicação com servidores C2. Também acelera a correlação de eventos.

## EDR (Endpoint Detection and Response)

Monitora continuamente os endpoints (computadores, notebooks, servidores) para detectar atividades maliciosas e responder rapidamente a incidentes.

Permite:
- Investigar um dispositivo remotamente (processos, conexões de rede, arquivos, usuários).
- **Isolar um endpoint comprometido** da rede, impedindo movimentação lateral.
- Buscar **Indicadores de Comprometimento (IOCs)** em todos os endpoints monitorados — ex: pesquisar o hash de um arquivo malicioso para ver se ele está presente em outras máquinas.

## SOAR (Security Orchestration, Automation and Response)

Integra diversas ferramentas de segurança (SIEM, EDR, firewalls, Threat Intelligence, Active Directory etc.), permitindo que trabalhem juntas.

> Não substitui o SIEM nem o EDR — ele os integra e automatiza processos entre eles.

Principal função: automatizar tarefas repetitivas, reduzindo o tempo do analista e acelerando investigação/resposta. Usa **playbooks** (fluxos de trabalho automatizados) para diferentes tipos de incidentes.

**Exemplos de automação:**
- Consulta automática de reputação de IP no VirusTotal.
- Pesquisa automática de hashes suspeitos.
- Criação automática de tickets de incidente.
- Isolamento de endpoint via EDR.
- Bloqueio automático de IP malicioso no firewall.
- Envio de notificações para a equipe.

## Case Management

Módulo responsável por gerenciar os incidentes investigados: casos abertos, em andamento e encerrados, histórico da investigação, evidências e ações realizadas.

Ao abrir um incidente, o SOAR normalmente associa automaticamente um playbook, orientando o analista sobre quais verificações e ações realizar.
