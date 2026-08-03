# Introdução ao Cyber Kill Chain

## O que é

O **Cyber Kill Chain** é um modelo desenvolvido pela Lockheed Martin em 2011 para descrever, de forma sequencial, as etapas que um atacante percorre durante uma intrusão — do planejamento inicial até a execução do objetivo final. O nome é uma referência ao conceito militar de "kill chain", usado para estruturar a cadeia de eventos de um ataque físico, e foi adaptado pela empresa para o contexto de segurança da informação.

A Lockheed Martin é uma companhia norte-americana dos setores aeroespacial, de defesa e tecnologia, formada em 1995 a partir da fusão entre Lockheed Corporation e Martin Marietta. Além de aeronaves e sistemas militares, a empresa mantém uma divisão de pesquisa voltada para cibersegurança, onde o framework foi originalmente concebido.

O modelo divide um ataque em **sete fases**, cada uma respondendo a uma pergunta específica sobre o que o invasor está tentando alcançar naquele momento:

| # | Fase | Pergunta-chave |
|---|------|-----------------|
| 1 | Reconnaissance | Como posso atacar essa organização? |
| 2 | Weaponization | Qual arma vou preparar? |
| 3 | Delivery | Como vou entregar essa arma? |
| 4 | Exploitation | Consegui executar meu código e obter acesso inicial? |
| 5 | Installation | Agora que entrei, como vou permanecer no sistema? |
| 6 | Command & Control | Como vou controlar essa máquina remotamente? |
| 7 | Actions on Objectives | Agora que tenho o controle, qual é o meu objetivo final? |

## Por que esse framework importa para um SOC Analyst

Para quem trabalha em um Security Operations Center, o valor do Cyber Kill Chain não está em decorar as sete fases, mas em usá-las como referência mental durante uma investigação. Ao analisar um alerta, a pergunta prática é: *em qual fase esse comportamento se encaixa?* Isso ajuda a responder três perguntas operacionais:

- **Qual a gravidade real do alerta?** Um scan de portas (Reconnaissance) exige atenção, mas um beaconing para um IP malicioso (Command & Control) indica que o atacante já está dentro do ambiente.
- **O que provavelmente vem a seguir?** Se um analista identifica um processo suspeito criando uma tarefa agendada (Installation), é razoável já monitorar tráfego de saída incomum, pois a fase seguinte costuma ser C2.
- **Onde as defesas falharam?** Se um ataque só foi detectado na fase de Actions on Objectives, isso significa que seis camadas de controle anteriores não geraram uma detecção eficaz — um sinal claro de que o programa de segurança precisa de ajustes.

Esse último ponto é o que dá ao Kill Chain seu principal uso para o Blue Team: ele funciona como um **mapa de cobertura defensiva**. Cada fase pode e deve ter controles de prevenção e detecção associados; quando um ataque avança sem ser identificado, isso expõe exatamente qual etapa está desprotegida.

## Estrutura de análise usada em cada fase

Ao longo desta documentação, cada uma das sete fases é analisada sob três perspectivas:

- **O que o atacante faz** — as técnicas e objetivos típicos daquela etapa.
- **O que o defensor faz** — os controles preventivos que reduzem a chance de sucesso do ataque.
- **O que o SOC monitora** — os eventos, logs e fontes de dados que permitem detectar a atividade naquela fase específica.

## Observação importante: as limitações do modelo

O Cyber Kill Chain é amplamente usado por ser simples e didático, mas vale registrar duas críticas comuns ao modelo, especialmente relevantes para quem está entrando na área:

- **É um modelo linear**, enquanto ataques reais raramente seguem uma sequência perfeita. Um atacante pode voltar à fase de Reconnaissance depois de obter acesso inicial, ou executar Actions on Objectives e C2 quase simultaneamente.
- **Foi pensado para malware tradicional**, com menos aderência a cenários como abuso de credenciais válidas, ataques a identidades em nuvem ou ameaças internas, onde não existe necessariamente "entrega de uma arma".

Por esse motivo, muitas equipes de segurança usam o Cyber Kill Chain em conjunto com o **MITRE ATT&CK**, um framework mais granular que mapeia táticas e técnicas específicas dentro de cada uma dessas fases. Entender os dois modelos — um como visão macro do ataque, outro como catálogo detalhado de técnicas — é um diferencial importante para quem atua ou pretende atuar em um SOC.

## Resumo

O Cyber Kill Chain organiza um ciberataque em sete fases sequenciais, da coleta de informações até a execução do objetivo final do invasor. Para um analista SOC, o framework serve como referência para classificar alertas, antecipar os próximos passos de um atacante e identificar lacunas nos controles de segurança. Apesar de suas limitações — principalmente por ser um modelo linear — ele continua sendo uma base sólida para estruturar o raciocínio de detecção e resposta, e costuma ser complementado por frameworks mais detalhados, como o MITRE ATT&CK.
