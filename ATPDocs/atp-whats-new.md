---
title: Novidades do Azure ATP | Microsoft Docs
description: Descreve as versões mais recentes do Azure ATP e fornece informações sobre as novidades de cada versão.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0693bd3a25d6438874d422bedf8da05931a15d54
ms.sourcegitcommit: 158bf048d549342f2d4689f98ab11f397d9525a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="whats-new-in-azure-atp"></a>Novidades do Azure ATP 

## <a name="azure-atp-release-226"></a>Azure ATP versão 2.26

Lançado em 25 de março de 2018

- Quando o Azure ATP alerta sobre uma atividade suspeita que você identifica como um positivo benigno (uma ação legítima que não é uma atividade suspeita), você tem a opção de excluir computadores e endereços IP de mais detecções, como: downgrade de criptografia, força bruta de LDAP, PAC forjado, força bruta e Pass-the-hash.
-   O desempenho do sensor do Azure ATP foi aprimorado.
-   Uma nova região foi adicionada para a implantação do Espaço de trabalho. Agora é possível implantar um espaço de trabalho na Ásia. 


## <a name="azure-atp-release-225"></a>Azure ATP versão 2.25

Lançada em 18 de março de 2018

- Agora há compatibilidade com a MFA (Autenticação Multifator) no Azure ATP. Os locatários usando MFA agora podem entrar no portal do Azure ATP.
- O Azure ATP agora tem uma página [**Status do sistema**](https://health.atp.azure.com/) para fornecer informações sobre se o Portal de Gerenciamento do espaço de trabalho está funcionando e ativo, se há problemas com as detecções e se o sensor pode enviar tráfego para a nuvem. Você pode acessar o **Status do sistema** na barra de menus do Azure ATP.


## <a name="azure-atp-release-224"></a>Versão 2.24 do Azure ATP

Lançada em 11 de março de 2018

**Detecções novas e atualizadas**
  - Criação de serviços suspeitos – invasores tentam executar serviços suspeitos na sua rede. Agora, o Azure ATP gera um alerta ao identificar que um novo serviço que parece suspeito está sendo executado por uma pessoa em um computador específico. Essa detecção se baseia em eventos (e não no tráfego de rede) e ocorre em qualquer controlador de domínio da rede que esteja encaminhando o evento 7045 para o Azure ATP. Para saber mais, consulte o [Guia de atividades suspeitas](suspicious-activity-guide.md).

**Investigação aprimorada**
  - O Azure ATP tem um [perfil de entidade](entity-profiles.md) aperfeiçoado. O perfil de entidade oferece uma plataforma projetada para investigações aprofundadas das atividades do usuário – como os recursos acessados, computadores em que fizeram logon, e muito mais. O perfil de entidade também fornece os dados de diretório e permite identificar possíveis caminhos de movimentação lateral de/para a entidade. Assim, é possível saber mais sobre violações em potencial na sua organização.

  - Com o ATP, é possível marcar manualmente as entidades como *confidenciais*, a fim de aperfeiçoar as detecções e o monitoramento. Essa marcação afeta diversas detecções do Azure ATP, como a detecção de modificação de grupos confidenciais e o [caminho de movimentação lateral](use-case-lateral-movement-path.md), que dependem de entidades consideradas confidenciais.

**Novos relatórios para ajudá-lo a investigar**
  - O [relatório de senhas expostas em texto não criptografado](reports.md) permite detectar quando os serviços enviam credenciais de conta em texto sem formatação. Assim, é possível investigar os serviços e aprimorar o nível de segurança da rede. Esse relatório substitui os alertas de atividade suspeita em texto não criptografado.
  - O [relatório de caminhos de movimento lateral para contas confidenciais](reports.md) lista as contas confidenciais que estão expostas por meio de caminhos de movimentação lateral. Dessa forma, é possível reduzir esses caminhos e fortalecer sua rede a fim de minimizar o risco de superfície de ataque. Assim, você pode impedir a movimentação lateral, para que os invasores não se movimentem entre usuários e computadores ao longo da rede até encontrarem o prêmio máximo da segurança virtual: suas credenciais de conta do administrador.

- Agora, é possível acessar facilmente a documentação em um link fornecido com um alerta de atividade suspeita, a fim de exibir as [etapas de investigação a serem seguidas](suspicious-activity-guide.md). 

**Melhorias de desempenho**
 -  A infraestrutura do sensor do Azure ATP teve seu desempenho aprimorado: a exibição agregada do tráfego permite otimizar a CPU e o pipeline de pacotes. Além disso, reutiliza soquetes para os controladores de domínio minimizarem as sessões de SSL para o DC.

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Planejamento de capacidade do Azure ATP](atp-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)