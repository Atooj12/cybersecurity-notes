# Erros comuns de um SOC Analyst

## 1. Dependência excessiva do VirusTotal

O VirusTotal é ótimo para checar reputação de arquivos, URLs, domínios e IPs, mas não deve ser a única base para decisão. Um malware pode usar técnicas de **AV Bypass** ou ser uma ameaça recente ainda não catalogada.

Além da reputação no VirusTotal, o analista deve avaliar:
- comportamento do arquivo
- contexto do incidente
- logs
- conexões de rede
- outros IOCs

## 2. Análise apressada de malware em sandbox

Uma análise de apenas 3-4 minutos pode não revelar o comportamento real do malware. Alguns ficam inativos por 10-15 minutos antes de agir, e outros detectam que estão em uma sandbox e simplesmente não executam nada suspeito.

Sempre que possível, a análise deve durar mais tempo, em um ambiente que simule um computador real (usuários configurados, documentos, softwares instalados, acesso controlado à internet, configurações parecidas com as da empresa).

## 3. Análise inadequada dos logs

Não basta analisar só o alerta inicial. Exemplo: se a máquina `JOAO-PC` se comunicou com o domínio `joao.com`, a investigação não deve parar aí — é preciso checar, via SIEM/Log Management, se outras máquinas também se comunicaram com esse domínio, já que isso pode indicar comprometimento de vários dispositivos.

Também devem ser analisados: outros usuários, outros IPs, outros domínios e eventos do mesmo período. Objetivo: entender toda a extensão do incidente.

## 4. Ignorar as datas das análises no VirusTotal

Sempre checar a data da última análise (*Last Analysis*/*Last Updated*). Uma análise antiga pode não refletir o estado atual do indicador — uma URL segura há meses pode estar comprometida hoje, assim como um IP malicioso no passado pode hoje pertencer a uma empresa legítima.

Quando possível, solicitar **Reanalyze** ou buscar informações mais recentes antes de decidir.
