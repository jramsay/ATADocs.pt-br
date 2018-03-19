---
title: "Validar o espelhamento de porta na Proteção Avançada contra Ameaças do Azure | Microsoft Docs"
description: "Descreve como validar que o espelhamento de porta está configurado corretamente na ATP do Azure"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/3/2018
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 0a56cf27-9eaa-4ad0-ae6c-9d0484c69094
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7628fa491ddbe477cab7eb414409028c0f94f44d
ms.sourcegitcommit: 84556e94a3efdf20ca1ebf89a481550d7f8f0f69
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="validate-port-mirroring"></a>Validação do espelhamento de porta
> [!NOTE] 
> Este artigo é relevante apenas se você implantar o sensor autônomo da ATP em vez do sensor da ATP do Azure. Para determinar se você precisa usar o sensor da ATP do Azure, confira [Escolhendo o sensor certo para a implantação](atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment).
 
As etapas a seguir guiarão você pelo processo de validação da configuração correta do espelhamento de porta. Para que a ATP do Azure funcione corretamente, o respectivo sensor autônomo deve ter capacidade de reconhecer o tráfego de entrada e saída do controlador de domínio. A fonte de dados principal usada pelo Azure ATP é uma inspeção profunda de pacotes do tráfego de rede para e dos controladores de domínio. Para que a ATP do Azure reconheça o tráfego de rede, é necessário configurar o espelhamento de porta. O espelhamento de porta copia o tráfego de uma porta (de origem) para outra porta (de destino).

## <a name="validate-port-mirroring-using-net-mon"></a>Validar o espelhamento de porta usando Net Mon
1.  Instale o [Monitor de Rede da Microsoft 3.4](http://www.microsoft.com/download/details.aspx?id=4865) no sensor autônomo da ATP que você deseja validar.

    > [!IMPORTANT]
    > Se optar por instalar o Wireshark a fim de validar o espelhamento de porta, reinicie o serviço do sensor autônomo da ATP do Azure após a validação.

2.  Abra o Monitor de Rede e crie uma nova guia de captura.

    1.  Selecione apenas o adaptador de rede de **captura** ou o adaptador de rede que estiver conectado à porta do comutador configurado como o destino do espelhamento de porta.

    2.  Verifique se o Modo-P está habilitado.

    3.  Clique em **Nova captura**.

        ![Criar nova imagem da guia de captura](media/atp-port-mirroring-capture.png)

3.  Na janela Filtro de exibição, digite o seguinte filtro: **KerberosV5 OU LDAP** e, em seguida, **Aplicar**.

    ![Aplicar imagem de filtro KerberosV5 ou LDAP](media/atp-port-mirroring-filter-settings.png)

4.  Clique em **Iniciar** para iniciar a sessão de captura. Se você não vir o tráfego para e do controlador de domínio, examine a configuração do espelhamento de porta.

    ![Iniciar a captura de imagem de sessão](media/atp-port-mirroring-capture-traffic.png)

    > [!NOTE]
    > É importante ter certeza de que você vê o tráfego para e dos controladores de domínio.
    

5.  Se você vir o tráfego apenas em uma direção, você deve trabalhar com as equipes de rede ou de virtualização para ajudar a solucionar os problemas com a configuração do espelhamento de porta.

## <a name="see-also"></a>Consulte Também

- [Configurar o encaminhamento de eventos](configure-event-forwarding.md)
- [Configurar o espelhamento de porta](configure-port-mirroring.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)