---
title: Reconhecer os alertas de integridade do ATP do Azure
description: Este artigo descreve todos os alertas de integridade para cada componente, listando a causa e as etapas necessárias para resolver o problema
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/17/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7dc8328b41308c87e51ac702d3c6ea77ab82c6d7
ms.sourcegitcommit: a8570301d24b09423210abfef49e5eec8b65c5ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2020
ms.locfileid: "92333529"
---
# <a name="understanding-azure-atp-sensor-health-alerts"></a>Reconhecer os alertas de integridade do sensor do ATP do Azure

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

O Centro de Integridade do ATP do Azure permite que você saiba quando há um problema em sua instância do ATP do Azure gerando um alerta de integridade. Este artigo descreve todos os alertas de integridade para cada componente, listando a causa e as etapas necessárias para resolver o problema.

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Todos os controladores de domínio ficam inacessíveis por um sensor

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP está offline no momento devido a problemas de conectividade com todos os controladores de domínio configurados.|Isso afeta a capacidade da ATP do Azure de detectar atividades suspeitas relacionadas aos controladores de domínio monitorados por esse sensor da ATP do Azure.| Certifique-se de que os controladores de domínio estejam em funcionamento e de que esse sensor do Azure ATP possa abrir conexões LDAP para eles. Além disso, em **Configurações**, certifique-se de configurar uma conta de serviço de diretório para cada floresta implantada.|Média|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Todos ou alguns dos adaptadores de rede de captura em um sensor não estão disponíveis

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Todos ou alguns dos adaptadores de rede de captura selecionados no sensor do Azure ATP estão desabilitados ou desconectados.|O tráfego de rede para alguns ou todos os controladores de domínio não é capturado pelo sensor do Azure ATP. Isso afeta a capacidade de detectar atividades suspeitas, relacionadas aos controladores de domínio.|Certifique-se de que esses adaptadores de rede de captura selecionados no sensor do Azure ATP estejam habilitados e conectados.|Média|

## <a name="directory-services-user-credentials-are-incorrect"></a>As credenciais de usuário de serviços de diretório estão incorretas

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|As credenciais da conta de usuário de serviços de diretório estão incorretas.|Isso afeta a capacidade dos sensores de detectar atividades usando consultas LDAP em controladores de domínio.|– Para contas do AD **padrão**: verifique se o nome de usuário, a senha e o domínio na página de configuração dos **Serviços de diretório** estão corretos.<br>– Para **Contas de Serviço Gerenciado de Grupo:** verifique se o nome de usuário e o domínio na página de configuração dos **Serviços de Diretório** estão corretos. Confira também todos os outros pré-requisitos da **conta gMSA** descritos na página [Conectar à sua floresta do Active Directory](install-step2.md#prerequisites).|Média|

## <a name="low-success-rate-of-active-name-resolution"></a>Taxa de êxito baixa de resolução de nomes ativa

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Os sensores do ATP do Azure listados não estão conseguindo resolver endereços IP para nomes de dispositivos mais de 90% das vezes usando os seguintes métodos:<br />– NTLM via RPC<br />– NetBios<br />– DNS inverso|Isso afeta as funcionalidades de detecção da ATP do Azure e pode aumentar a quantidade de alarmes falsos positivos.|– Para NTLM via RPC: A porta 135 deve estar aberta para a comunicação de entrada de sensores do ATP do Azure em todos os computadores no ambiente.<br />– Para DNS inverso: Os sensores devem ser capazes de alcançar o servidor DNS, e as Zonas de Pesquisa Inversa devem estar habilitadas.<br />– Para NetBIOS: A porta 137 deve estar aberta para a comunicação de entrada de sensores do ATP do Azure em todos os computadores no ambiente.<br />Além disso, garanta que a configuração de rede (como firewalls) não esteja impedindo a comunicação com as portas relevantes.|Baixo|

## <a name="no-traffic-received-from-domain-controller"></a>Nenhum tráfego recebido do controlador de domínio

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Nenhum tráfego foi recebido do controlador de domínio por meio desse sensor do Azure ATP.|Isso pode indicar que o espelhamento de porta dos controladores de domínio com o sensor do Azure ATP ainda não está configurado ou não está funcionando.|Verifique se o [espelhamento de porta está configurado corretamente em seus dispositivos de rede](configure-port-mirroring.md).<br></br>Na NIC de captura do sensor do Azure ATP, desabilite esses recursos em Configurações Avançadas:<br></br>União de Segmentos de Recebimento (IPv4)<br></br>União de Segmentos de Recebimento (IPv6)|Média|

## <a name="read-only-user-password-to-expire-shortly"></a>Senha de usuário somente leitura a expirar em breve

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|A senha de usuário somente leitura, usada para executar a resolução de entidades no Active Directory, está prestes a expirar em menos de 30 dias.|Se a senha do usuário expirar, todos os sensores do Azure ATP deixarão de ser executados e nenhum novo dado será coletado.|[Altere a senha de conectividade do domínio](modifying-config-dcpassword.md) e, em seguida, atualize a senha no portal do Azure ATP.|Média|

## <a name="read-only-user-password-expired"></a>A senha de usuário somente leitura expirou

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|A senha de usuário somente leitura, usada para obter dados de diretório, expirou.|Todos os sensores do Azure ATP deixam de ser executados (ou deixarão de ser executados em breve) e nenhum novo dado é coletado.|[Altere a senha de conectividade do domínio](modifying-config-dcpassword.md) e, em seguida, atualize a senha no portal do Azure ATP.|Alta|

## <a name="sensor-outdated"></a>Sensor desatualizado

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Um sensor do Azure ATP está desatualizado.|Um sensor do ATP do Azure está executando uma versão que não pode se comunicar com a infraestrutura de nuvem do ATP do Azure.|Atualize manualmente o sensor e verifique por que ele não está sendo atualizado automaticamente. Se isso não funcionar, baixe o pacote de instalação mais recente do sensor e desinstale e reinstale o sensor. Para obter mais informações, consulte [Instalando o sensor do Azure ATP](install-step4.md).|Média|

## <a name="sensor-reached-a-memory-resource-limit"></a>O sensor atingiu o limite de um recurso de memória

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP interrompeu seu funcionamento e reiniciará automaticamente para proteger o controlador de domínio de uma condição de memória insuficiente.|O sensor do Azure ATP impõe limitações de memória a si mesmo para impedir que o controlador de domínio tenha limitações de recursos. Isso ocorre quando o uso de memória no controlador de domínio é alto. Os dados do controlador de domínio são apenas parcialmente monitorados.|Aumente a quantidade de memória (RAM) no controlador de domínio ou adicione mais controladores de domínio a esse site para melhor distribuir o carregamento deste controlador de domínio.|Média|

## <a name="sensor-service-failed-to-start"></a>O serviço do sensor falhou ao iniciar

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP não conseguiu iniciar por pelo menos 30 minutos.|Isso pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio monitorados por este sensor do Azure ATP.|Monitore os logs do sensor do Azure ATP para entender a causa raiz da falha do serviço do sensor do Azure ATP.|Alta|

## <a name="sensor-stopped-communicating"></a>O sensor parou de se comunicar

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Não houve nenhuma comunicação do sensor do Azure ATP. O período padrão para este alerta é de cinco minutos.|O tráfego de rede não é mais capturado pelo adaptador de rede no sensor do Azure ATP. Isso afeta a capacidade do ATA de detectar atividades suspeitas, uma vez que o tráfego de rede não será capaz de alcançar o serviço de nuvem da ATP do Azure.|Verifique se a porta usada para comunicação entre o sensor do Azure ATP e o serviço de nuvem do Azure ATP não está bloqueada por firewalls ou roteadores.|Média|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Alguns controladores de domínio ficam inacessíveis por um sensor

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|Um sensor do Azure ATP tem funcionalidade limitada devido a problemas de conectividade com alguns dos controladores de domínio configurados.|A detecção de Passagem de hash pode ser menos precisa quando alguns controladores de domínio não podem ser consultados pelo sensor do Azure ATP.|Certifique-se de que os controladores de domínio estejam em funcionamento e de que esse sensor do Azure ATP possa abrir conexões LDAP para eles.|Média|

## <a name="some-windows-events-are-not-being-analyzed"></a>Alguns eventos do Windows não estão sendo analisados

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP está recebendo mais eventos do que pode processar.|Alguns eventos do Windows não estão sendo analisados, o que pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio monitorados por este sensor do Azure ATP.|Verifique se apenas os eventos necessários são encaminhados ao sensor do Azure ATP ou tente encaminhar alguns dos eventos para outro sensor do ATP.|Média|

## <a name="some-network-traffic-could-not-be-analyzed"></a>Não foi possível analisar parte do tráfego de rede

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do Azure ATP está recebendo mais tráfego de rede do que pode processar.|Não foi possível analisar parte do tráfego de rede, o que pode afetar a capacidade de detectar atividades suspeitas provenientes dos controladores de domínio monitorados por este sensor do ATP do Azure.|Considere [adicionar mais processadores e memória](capacity-planning.md) conforme necessário. Se esse for um sensor autônomo do Azure ATP, reduza o número de controladores de domínio monitorados.<br></br>Isso também pode ocorrer se você estiver usando controladores de domínio em máquinas virtuais VMware. Para evitar esses alertas, verifique se as configurações a seguir estão definidas como 0 ou Desabilitado na máquina virtual:<br></br>– TsoEnable<br></br>– LargeSendOffload(IPv4)<br></br>– Descarregamento de TSO do IPv4<br></br>Além disso, considere desabilitar o Descarregamento TSO gigante do IPv4. Para obter mais informações, consulte a documentação do VMware.|Média|

## <a name="some-etw-events-are-not-being-analyzed"></a>Alguns eventos do ETW não estão sendo analisados

|Alerta|Descrição|Resolução|Severidade|
|----|----|----|----|
|O sensor do ATP do Azure está recebendo mais eventos do ETW (Rastreamento de Eventos para Windows) do que ele pode processar.|Alguns eventos de ETW (Rastreamento de Eventos para Windows) não estão sendo analisados, o que pode afetar a capacidade de detectar atividades suspeitas originadas de controladores de domínio monitorados por este sensor do ATP do Azure.|Verifique se apenas os eventos necessários são encaminhados ao sensor do Azure ATP ou tente encaminhar alguns dos eventos para outro sensor do ATP.|Média|

<!--
## Windows events missing from domain controller audit policy

|Alert|Description|Resolution|Severity|
|----|----|----|----|
| Windows events missing from domain controller audit policy|For the correct events to be audited and included in the Windows Event Log, your domain controllers require accurate Advanced Audit Policy settings. Incorrect Advanced Audit Policy settings leave critical events out of your logs, and result in incomplete Azure ATP coverage.|Review your [Advanced Audit policy](configure-windows-event-collection.md) and modify as needed. | Medium|
-->

## <a name="see-also"></a>Consulte Também

- [Pré-requisitos do Azure ATP](prerequisites.md)
- [Planejamento de capacidade do Azure ATP](capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)