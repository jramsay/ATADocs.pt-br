---
title: Política de dados pessoais da Proteção Avançada contra Ameaças do Azure
description: Fornece links para informações sobre como excluir informações particulares e dados pessoais do Azure ATP.
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 06/21/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 8cfd442e05827811c929f5d6e89ab03dad8a3367
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912403"
---
# <a name="azure-atp-data-security-and-privacy"></a>Privacidade e segurança de dados do Azure ATP

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>Pesquisar e identificar dados pessoais

Na Proteção Avançada contra Ameaças do Azure, você pode exibir dados pessoais identificáveis ​​do [portal do Azure ATP](workspace-portal.md) usando a [barra de pesquisa](workspace-portal.md#search-bar).

Pesquise um usuário ou computador específico e clique na entidade para ir à [página de perfil](entity-profiles.md) do usuário ou do computador. O perfil fornece detalhes abrangentes sobre a entidade do Active Directory, incluindo atividade de rede relacionada a essa entidade e seu histórico.

Os dados pessoais do Azure ATP são coletados do Active Directory por meio do sensor do Azure ATP e armazenados em um banco de dados de back-end.

## <a name="update-personal-data"></a>Atualizar dados pessoais

Os dados pessoais de usuário do ATP do Azure são derivados do objeto do usuário no Active Directory da organização. Portanto, as alterações feitas ao perfil de usuário no AD da organização são refletidas no Azure ATP.


## <a name="delete-personal-data"></a>Excluir dados pessoais

- Depois que um usuário é excluído do Active Directory da organização, o Azure ATP exclui automaticamente o perfil de usuário e qualquer atividade de rede relacionada dentro de um ano. Você também pode [excluir](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) quaisquer alertas de segurança que contenham dados pessoais.

- Recomendam-se permissões **somente leitura** no contêiner de **Objetos Excluídos**. Para saber mais sobre como a permissão de contêiner de **Objetos Excluídos é usada pelo serviço do ATP do Azure, confira a recomendação de contêiner de Objetos Excluídos nos [Pré-requisitos do ATP do Azure](prerequisites.md#before-you-start).

## <a name="export-personal-data"></a>Exportar dados pessoais

No Azure ATP você pode [exportar](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) as informações de alerta de segurança para o Excel. Essa função também exporta os dados pessoais.

## <a name="audit-personal-data"></a>Auditar dados pessoais

O Azure ATP implementa a auditoria de alterações de dados pessoais, incluindo a exclusão e exportação de registros de dados pessoais. O tempo de retenção da trilha de auditoria é de 90 dias. A auditoria no Azure ATP é um recurso de back-end e não está acessível aos clientes.

## <a name="additional-resources"></a>Recursos adicionais

- Para saber mais sobre a confiança e a conformidade do Azure ATP, confira o [Portal de Confiança do Serviço](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) e o [site Conformidade do Microsoft 365 Enterprise com o RGPD](/microsoft-365/compliance/gdpr?view=o365-worldwide&preserve-view=true).

## <a name="security-and-privacy-for-azure-atp-us-government-gcc-high-customers"></a>Segurança e privacidade para clientes do US Government GCC High do ATP do Azure
Para saber mais sobre os padrões de conformidade do ATP do Azure e o local dos dados dos clientes do US Government GCC High, revise a [Descrição do serviço Enterprise Mobility + Security for US Government](/enterprise-mobility-security/solutions/ems-govt-service-description).