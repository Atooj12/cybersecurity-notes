# Threat Intelligence Feed

Fluxo contínuo de dados de inteligência sobre ameaças, fornecido por empresas especializadas em segurança. É atualizado constantemente e pode conter:

- Endereços IP maliciosos
- Domínios de Command and Control (C2)
- URLs maliciosas
- E-mails usados em campanhas de phishing
- Hashes de arquivos maliciosos
- Indicadores de Comprometimento (IOCs)
- Informações sobre grupos de ameaças e campanhas de ataque

Durante uma investigação, o SOC Analyst pode consultar esses feeds para verificar se um IP, domínio ou hash já foi identificado como malicioso.

## Pontos de atenção

- A **ausência** de um indicador no feed não significa que ele seja seguro — o item ainda deve ser analisado com outras técnicas (sandbox, análise de comportamento, investigação manual).
- Endereços IP podem **mudar de proprietário** ao longo do tempo. Um IP malicioso no passado pode hoje pertencer a uma organização legítima. Por isso a reputação de um IP sempre deve ser analisada junto com outros indicadores e o contexto da investigação.
