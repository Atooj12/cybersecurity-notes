# Reconnaissance (Reconhecimento)

**Pergunta que identifica a fase:** *O que o atacante consegue descobrir sobre a vítima?*

## Introdução

Reconnaissance é a primeira fase do Cyber Kill Chain e ocorre antes de qualquer tentativa efetiva de comprometimento. Nela, o atacante concentra-se em coletar o máximo de informações possível sobre a organização-alvo. Quanto maior o volume de dados obtidos, maior a superfície de ataque conhecida e mais precisas se tornam as fases seguintes — especialmente Weaponization e Delivery, que dependem diretamente do que foi descoberto aqui.

É também a fase mais difícil de eliminar por completo, já que boa parte dela pode ocorrer sem qualquer interação direta com a infraestrutura da vítima.

## Reconhecimento passivo x ativo

O Reconnaissance se divide em duas categorias com características bem distintas do ponto de vista de detecção:

| Tipo | Como funciona | Exemplos | Gera log na vítima? |
|------|----------------|----------|----------------------|
| **Passive Reconnaissance** | Coleta de dados sem qualquer interação direta com o ambiente da vítima | Google Dorking, LinkedIn, redes sociais, WHOIS, registros DNS públicos, vazamentos de dados, documentos públicos | Normalmente **não** |
| **Active Reconnaissance** | Interação direta com sistemas da vítima para obter informações | Scan de portas, banner grabbing, enumeração de serviços, descoberta de subdomínios, identificação de versões de software | **Sim**, costuma deixar rastros |

Essa distinção é o que torna essa fase estrategicamente importante: o reconhecimento passivo é praticamente invisível para a organização-alvo, enquanto o ativo já representa a primeira oportunidade real de detecção pelo SOC.

## O que o atacante busca

Durante essa fase, o atacante procura reunir informações que aumentem as chances de sucesso das próximas etapas do ataque:

- Versões de servidores e softwares usados pela organização, para cruzar com vulnerabilidades conhecidas.
- Informações públicas (OSINT) — domínios, tecnologias utilizadas, documentos e notícias sobre a empresa.
- Endereços de e-mail de funcionários, úteis para campanhas de phishing.
- Dados pessoais e profissionais de colaboradores em redes sociais, para engenharia social.
- Dispositivos expostos à internet, como servidores web, VPNs e roteadores.
- Faixas de endereços IP pertencentes à organização.
- Empresas parceiras e fornecedores, que podem servir como vetor de entrada em um ataque à cadeia de suprimentos (*supply chain attack*).

**Exemplo prático:** um atacante realiza uma busca em fóruns de vazamento de dados e encontra credenciais corporativas expostas em um *breach* antigo. Em paralelo, consulta o LinkedIn da empresa e identifica o nome do gerente de TI, que será usado posteriormente em uma campanha de phishing direcionado (*spear phishing*). Nenhuma dessas ações toca a infraestrutura da vítima — por isso, nenhuma delas gera alerta.

## O que o defensor faz

O objetivo do defensor nesta fase é reduzir a superfície de informações disponíveis publicamente e detectar tentativas de reconhecimento ativo:

- Realizar testes de invasão externos (*external pentests*) para identificar o que já está exposto.
- Monitorar vazamentos de dados através de fontes de Threat Intelligence.
- Evitar publicar documentos com metadados ou informações sensíveis.
- Monitorar tráfego externo com firewall, IDS e IPS.
- Corrigir rapidamente vulnerabilidades conhecidas por meio de patches.

## O que um Analista SOC monitora

Como o reconhecimento passivo raramente é visível, o foco prático do SOC está em identificar sinais de reconhecimento **ativo**:

| Evento monitorado | Fonte típica |
|---------------------|----------------|
| Grande volume de conexões vindas do mesmo IP | Firewall / IDS |
| Port scanning | IDS / IPS |
| Enumeração de serviços | SIEM / IDS |
| Requisições para URLs inexistentes (directory bruteforce) | WAF |
| Consultas DNS incomuns | Servidores DNS |
| Picos repentinos de tentativas de conexão em portas diferentes | Firewall |
| Tentativas repetidas de autenticação ou enumeração de usuários | SIEM / VPN |
| Acessos de países incomuns para o perfil da organização | VPN / IDS |

## Curiosidade técnica

Ferramentas amplamente usadas por profissionais de segurança (tanto ofensiva quanto defensivamente) para reconhecimento incluem o **Shodan** — um mecanismo de busca voltado a dispositivos conectados à internet — e o **theHarvester**, usado para coletar e-mails, subdomínios e nomes de funcionários a partir de fontes públicas. Conhecer essas ferramentas do lado ofensivo ajuda o analista SOC a entender exatamente qual tipo de rastro elas podem (ou não) deixar na infraestrutura monitorada.

## Resumo

Reconnaissance é a fase em que o atacante mapeia a organização-alvo, combinando coleta passiva (sem contato direto, praticamente invisível) e coleta ativa (com interação direta, capaz de gerar logs). Para o SOC, o objetivo nessa etapa é identificar sinais de reconhecimento ativo — como varreduras de porta e enumeração de serviços — antes que essas informações sejam usadas para preparar e lançar o ataque propriamente dito.
