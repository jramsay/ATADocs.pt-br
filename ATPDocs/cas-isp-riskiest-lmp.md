---
title: Avaliações dos caminhos de movimento lateral mais arriscados da Proteção Avançada contra Ameaças do Azure
description: Este artigo apresenta uma visão geral das entidades confidenciais do ATP do Azure com o relatório de avaliação da postura de segurança de identidade dos caminhos de movimento lateral mais arriscados.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 04b1cefbb1c03d3dfe38c743b2a910a97664d01e
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913155"
---
# <a name="security-assessment-riskiest-lateral-movement-paths-lmp"></a>Avaliação de segurança: LMP (caminhos de movimento lateral) mais arriscados

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-risky-lateral-movement-paths"></a>O que são caminhos de movimento lateral arriscados?

O ATP do Azure monitora continuamente o ambiente para identificar contas **confidenciais** com os caminhos de movimento lateral mais arriscados que expõem um risco de segurança e para identificar relatórios sobre essas contas a fim de ajudar você a gerenciar o ambiente. Os caminhos serão considerados arriscados se tiverem três ou mais contas não confidenciais capazes de expor a conta **confidencial** a roubo de credenciais por atores mal-intencionados.

Saiba mais sobre LMP:

- [LMPs (caminhos de movimento lateral) do ATP do Azure](use-case-lateral-movement-path.md)
- [Movimento lateral do MITRE ATT&CK](https://attack.mitre.org/tactics/TA0008/)

## <a name="what-risk-do-risky-lateral-movement-paths-pose"></a>Que risco representam os caminhos de movimento lateral arriscados?

As organizações que não conseguem proteger as contas **confidenciais** deixam a porta aberta para atores mal-intencionados.

Agentes mal-intencionados, como ladrões, geralmente procuram a maneira mais fácil e discreta de entrar em um ambiente. Contas confidenciais com caminhos de movimento lateral arriscados são janelas de oportunidade para invasores e podem representar riscos.

Por exemplo, os caminhos mais arriscados ficam mais visíveis ao invasor e, se comprometidos, podem fornecer ao invasor acesso às entidades mais confidenciais da organização.

## <a name="how-do-i-use-this-security-assessment"></a>Como usar a avaliação de segurança?

1. Use a tabela de relatório para descobrir quais das suas contas **confidenciais** têm LMPs arriscados.
    ![Examinar as principais entidades afetadas e criar um plano de ação](media/atp-cas-isp-riskiest-lmp-1.png)
1. Tome medidas apropriadas:
    - Remova a entidade do grupo, conforme especificado na recomendação.
    - Remova as permissões de administrador local para a entidade do dispositivo especificado na recomendação.

    > [!NOTE]
    > Aguarde 24 horas e verifique se a recomendação deixou de aparecer na lista.

> [!NOTE]
> Essa avaliação é atualizada a cada 24 horas.

## <a name="see-also"></a>Consulte Também

- [Filtrar atividades da ATP do Azure no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
