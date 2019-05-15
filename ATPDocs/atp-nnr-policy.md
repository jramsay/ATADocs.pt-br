---
title: Resolução de nomes de rede da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Este artigo fornece uma visão geral dos usos e da funcionalidade avançada de resolução de nomes de rede do ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 03/31/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ac873fc-b763-41d7-878e-7c08da421cb5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1489f1b24065a153734bdd46975576d469b57f24
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196939"
---
# <a name="what-is-network-name-resolution"></a>O que é a Resolução de nomes de rede?

A Resolução de nomes de rede ou NNR é um componente principal da funcionalidade do ATP do Azure. O ATP do Azure captura atividades com base no tráfego de rede, nos eventos do Windows e no ETW, atividades que normalmente contêm dados de IP.  

Usando a NNR, o ATP do Azure é capaz de correlacionar atividades brutas (que contêm endereços IP) e os computadores relevantes envolvidos em cada atividade. Com base nas atividades brutas, o ATP do Azure cria perfis de entidades, incluindo computadores, e gera alertas de segurança de atividades suspeitas.

Para resolver endereços IP de nomes do computador, os sensores do ATP consultam o endereço IP do nome do computador "por atrás" do IP, usando um dos seguintes métodos:

1. NTLM sobre RPC (porta TCP 135)
2. NetBIOS (porta UDP 137)
3. RDP (porta TCP 3389), apenas o primeiro pacote do **Client hello**
4. Consulta ao servidor DNS usando a pesquisa de DNS reverso do endereço IP (UDP 53)

> [!NOTE]
>Nenhuma autenticação é realizada em quaisquer das portas.

Depois de recuperar o nome do computador, o sensor do ATP do Azure verifica o Active Directory Domain Services para ver se há um objeto de computador correlacionado com o mesmo nome do computador. Se o sensor encontrar a correlação, ele associará esse IP ao objeto do computador.

Os dados da NNR são cruciais para a detecção das seguintes ameaças:

- Suspeita de roubo de identidade (Pass-the-Ticket)
- Suspeita de ataque de DCSync (replicação de serviços de diretório)
- Reconhecimento de mapeamento de rede (DNS)

Para melhorar a capacidade de determinar se um alerta é um **Verdadeiro Positivo (TP)** ou um **Falso Positivo (FP)**, a ATP do Azure inclui o grau de certeza de resolução do nome do computador na evidência de todos os alertas de segurança. 
 
Por exemplo, quando os nomes dos computadores são resolvidos com **certeza alta**, ela aumenta a confiança no resultado do alerta de segurança como um **Verdadeiro Positivo** ou **TP**. 

A evidência inclui a hora, o IP e o nome do computador para o qual o IP foi resolvido. Quando a certeza de resolução for **baixa**, use essas informações para investigar e verificar qual dispositivo era a fonte verdadeira do IP nesse momento. Depois de confirmar o dispositivo, você poderá determinar se o alerta é um **Falso Positivo** ou **FP**, semelhante aos exemplos a seguir:

- Suspeita de roubo de identidade (pass-the-ticket) – o alerta foi disparado para o mesmo computador.
- Suspeita de ataque DCSync (replicação de serviços de diretório) – o alerta foi disparado de um controlador de domínio.
- Reconhecimento de mapeamento de rede (DNS), o alerta foi disparado de um servidor DNS.

    ![Certeza da evidência](media/nnr-high-certainty.png)


### <a name="prerequisites"></a>Pré-requisitos
|Protocolo|  Transport|  Porta|   Dispositivo| Direção|
|--------|--------|------|-------|------|
|NTLM via RPC| TCP |135|   Todos os dispositivos na rede| Entrada|
|NetBIOS|   UDP|    137|    Todos os dispositivos na rede| Entrada|
|DNS|   UDP|    53| Controladores de domínio| Saída|
|

Quando a porta 3389 é aberta em dispositivos no ambiente, o sensor do ATP do Azure a usa para fins de resolução de nomes da rede.
Abrir a porta 3389 **não é um requisito**, é apenas um método adicional que pode fornecer o nome do computador se a porta já estiver aberta para outras finalidades.

Para se certificar de que o ATP do Azure está funcionando de forma ideal e que o ambiente está configurado corretamente, o ATP do Azure verifica o status de resolução de cada Sensor e emite um alerta de monitoramento por método, fornecendo uma lista de sensores do ATP do Azure com baixas taxas de sucesso de resolução de nomes ativas que usam cada método.

Cada alerta de monitoramento oferece detalhes específicos sobre o método, os sensores e a política problemática além de recomendações de configuração.

![Alerta de baixa taxa de sucesso da Resolução de Nomes de Rede (NNR)](media/atp-nnr-success-rate.png)


### <a name="configuration-recommendations"></a>Recomendações de configuração

- RPC sobre NTLM:
    - A porta 135 deve estar aberta para a comunicação de entrada de Sensores do ATP do Azure em todos os computadores no ambiente.
    - Verifique todas as configurações de rede (firewalls), pois isso pode impedir a comunicação com as portas relevantes.

- NetBIOS:
    - A porta 137 deve estar aberta para a comunicação de entrada de sensores do ATP do Azure em todos os computadores no ambiente.
    - Verifique todas as configurações de rede (firewalls), pois isso pode impedir a comunicação com as portas relevantes.
- DNS inverso:
    - O Sensor deve ser capaz de alcançar o servidor DNS e as Zonas de Pesquisa Inversa devem estar habilitadas.


## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)