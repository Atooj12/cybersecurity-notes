# Weaponization e Delivery (Armamentização e Entrega)

## Introdução

Com as informações coletadas na fase de Reconnaissance, o atacante avança para duas etapas que, juntas, transformam conhecimento sobre a vítima em uma tentativa concreta de comprometimento: primeiro ele **prepara** a ferramenta de ataque (Weaponization), depois **entrega** essa ferramenta até o alvo (Delivery). Até o fim da fase de Delivery, é importante destacar, o sistema da vítima ainda pode não estar comprometido — a invasão de fato só se confirma na fase seguinte, Exploitation.

---

## Weaponization (Armamentização)

**Pergunta que identifica a fase:** *Como o atacante prepara o ataque?*

Nesta etapa, o atacante escolhe a técnica que será usada e monta as ferramentas necessárias para executá-la. Diferente das fases seguintes, a Weaponization acontece inteiramente fora da infraestrutura da vítima — o que a torna, na prática, invisível para o SOC da organização-alvo.

### O que o atacante faz

- Desenvolve ou adapta malware para a vulnerabilidade identificada.
- Desenvolve ou reaproveita um *exploit* específico para uma falha conhecida.
- Produz documentos maliciosos (macros em Word/Excel, PDFs manipulados).
- Cria páginas falsas de phishing e templates de e-mail.
- Escolhe as ferramentas que serão usadas no restante do ataque.
- Configura a infraestrutura de suporte, como servidores de Command & Control (C2) ou domínios falsos.

### O que o defensor faz

Como essa fase ocorre fora do perímetro da organização, o defensor não consegue impedir diretamente a preparação do ataque. Ainda assim, algumas ações reduzem as chances de sucesso das fases seguintes:

- Varreduras periódicas de vulnerabilidades no próprio ambiente.
- Aplicação rápida de patches de segurança.
- Acompanhamento de novas técnicas usadas por grupos de ameaça (Threat Intelligence).
- Uso de soluções como EDR, antivírus e filtros de e-mail, que atuam como barreira quando a ferramenta preparada finalmente chegar ao ambiente.

### O que um Analista SOC monitora

Por ocorrer fora da rede da organização, o SOC não observa a Weaponization diretamente. O que é possível fazer é monitorar **indicadores externos** que ajudam a antecipar ataques:

| Fonte de dado | O que é observado |
|-----------------|----------------------|
| Threat Intelligence Feeds | Novos IOCs e campanhas de phishing em circulação |
| Feeds de CVE | Vulnerabilidades recém-divulgadas para softwares usados pela empresa |
| Fornecedores de segurança | Novas famílias de malware |
| Plataformas de Vulnerability Management | Exploits publicados para sistemas do ambiente |
| SIEM / EDR | Atualização de regras de detecção (Sigma, YARA) |

---

## Delivery (Entrega)

**Pergunta que identifica a fase:** *Como o atacante faz o conteúdo malicioso chegar até a vítima?*

Delivery marca o primeiro contato real entre atacante e vítima. É aqui que a "arma" preparada na etapa anterior é enviada ao alvo — por e-mail, por um site comprometido, ou por qualquer outro canal. Vale reforçar: **entrega não significa infecção**. O arquivo malicioso pode chegar até o usuário sem que nada seja executado; a exploração de fato só acontece na fase seguinte.

### O que o atacante faz

| Vetor de entrega | Descrição |
|---------------------|-------------|
| E-mail de phishing | Envio de URLs ou anexos maliciosos (Word, PDF, Excel, ZIP) |
| Site comprometido ou falso | Hospedagem do malware, incluindo *drive-by download* |
| Redes sociais / mensageria | Divulgação de links maliciosos |
| Mídia removível | Uso de dispositivos USB infectados |
| Upload direto | Caso o atacante já possua algum acesso prévio ao ambiente |

**Exemplo prático:** um atacante envia um e-mail se passando pelo setor financeiro, com um anexo em Excel contendo uma macro maliciosa. O e-mail passa pelos filtros de spam por usar um domínio recém-registrado, mas ainda não classificado como malicioso pelas listas de reputação. Nesse momento, o ataque está na fase de Delivery — o arquivo chegou à caixa de entrada, mas nada foi executado ainda.

### O que o defensor faz

- Uso de *Secure Email Gateway* para filtrar e-mails maliciosos.
- Análise de anexos e URLs em sandbox antes da entrega ao usuário.
- Antivírus e EDR para detectar arquivos maliciosos no endpoint.
- Filtros anti-spam e anti-phishing.
- Bloqueio de domínios maliciosos via firewall, proxy e DNS seguro.
- Treinamento de colaboradores para reconhecimento de phishing e engenharia social.

### O que um Analista SOC monitora

- Grande volume de e-mails de phishing.
- Downloads de arquivos suspeitos.
- Acessos a domínios recém-criados ou com baixa reputação.
- Cliques em URLs maliciosas.
- Detecções de antivírus/EDR relacionadas a anexos.
- Alertas de sandbox indicando comportamento malicioso.

Esses eventos costumam aparecer em **SIEM**, **Secure Email Gateway**, **Firewall** e **EDR**.

## Curiosidade técnica

Frameworks ofensivos como o **Metasploit** e o **Cobalt Strike** são amplamente usados tanto por testadores de invasão legítimos quanto por grupos de ameaça reais para as fases de Weaponization e Delivery — o que reforça por que conhecer ferramentas ofensivas, mesmo atuando no Blue Team, ajuda o analista a reconhecer padrões de tráfego e comportamento associados a elas (como *beacons* característicos do Cobalt Strike, já visíveis a partir da fase de Command & Control).

## Resumo

Weaponization é a etapa de preparação do ataque — invisível para o SOC, já que ocorre fora do ambiente da vítima — enquanto Delivery é o primeiro contato direto, quando o conteúdo malicioso efetivamente chega ao alvo através de e-mail, sites comprometidos ou outros vetores. Nenhuma das duas fases implica comprometimento por si só: o objetivo do defensor é impedir que o conteúdo entregue seja executado, o que só se confirma (ou não) na fase de Exploitation.
