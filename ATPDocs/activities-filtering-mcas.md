---
title: Filtragem de atividades de Proteção Avançada contra Ameaças do Azure e políticas no Microsoft Cloud App Security
description: Visão geral de filtragem de atividade e políticas do ATP do Azure com o Microsoft Cloud App Security.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/01/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 397e5a77-2bc7-454c-9fe5-649ebaab16b3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cd30fac510bd291c78eb668d9540cd6733efc704
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912118"
---
# <a name="use-activity-filters-and-create-action-policies-with-azure-atp-in-microsoft-cloud-app-security"></a>Usar filtros de atividade e criar políticas de ação com o ATP do Azure no Microsoft Cloud App Security

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Este artigo foi criado para ajudá-lo a entender como filtrar e criar políticas de ação para atividades do ATP do Azure usando o Microsoft Cloud App Security.

Para saber mais sobre como concluir sua integração, confira [Integração do Cloud App Security do ATP do Azure](/cloud-app-security/aatp-integration).

Usar o ATP do Azure com o Microsoft Cloud App Security oferece análise de atividades e alertas com base na UEBA (análise de comportamento de entidade e usuário), identificando os comportamentos mais arriscados na sua empresa, fornecendo uma pontuação de prioridade de investigação abrangente além de filtragem de atividade e políticas personalizáveis de atividades.

## <a name="prerequisites"></a>Pré-requisitos

Para fazer uma investigação completa sobre os recursos no ambiente híbrido, é necessário:

- Uma licença válida do Microsoft Cloud App Security
- Uma licença válida do ATP do Azure vinculada à instância do Azure Active Directory

>[!NOTE]
>Se você não tiver uma assinatura do Cloud App Security, use o portal do Cloud App Security para investigar os alertas do ATP do Azure e faça uma análise aprofundada sobre os usuários e suas atividades gerenciadas locais. No entanto, as informações relacionadas a seus aplicativos na nuvem permanecerão indisponíveis.

## <a name="filter-azure-atp-activities-in-cloud-app-security"></a>Filtrar atividades do ATP do Azure no Cloud App Security

As atividades do ATP do Azure podem ser acessadas no menu principal **Investigar** do Cloud App Security selecionando o submenu **Log de atividades** ou no menu **Alertas** por status, categoria, severidade, aplicativo, nome de usuário ou política.

Para acessar as atividades do ATP do Azure por usuário:

1. Filtre a fila **Alertas** usando o campo NOME DE USUÁRIO.
    ![Filtrar alertas por nome de usuário](media/atp-mcas-alerts-queue.png)
1. Clique no nome de usuário em qualquer um dos alertas na lista resultante para abrir a **Página de usuário** do usuário que você deseja investigar.

1. Filtre as atividades do usuário usando os campos disponíveis ou adicione uma nova regra de filtro usando o botão +.
    ![Filtrar atividades do usuário](media/atp-mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>Criar políticas de atividade no Cloud App Security

Após filtrar as atividades e identificar as políticas de atividade que você gostaria de implementar ou a não conformidade em sua organização, use a opção **Criar política de atividade** do menu de filtro para criar imediatamente uma nova política personalizada por usuário, dispositivo ou locatário.

Para criar uma nova política de atividade:

1. Em qualquer página do **Log de atividades**, aplique um filtro (como Aplicativo, Nome de Usuário, Tipo de atividade) etc.
    - Para filtrar as atividades do ATP do Azure, selecione a opção **Active Directory** no filtro Aplicativo.
    ![Criar nova política de atividade](media/atp-mcas-create-new-policy.png)
1. Clique no botão **Nova política da pesquisa**.
1. Adicione um **Nome da política**.
    ![Criar nova política de atividade -etapa 2](media/atp-mcas-create-policy.png)
1. Adicione uma **Descrição** da política.
1. Atribua a **severidade** da política.
1. Selecione uma **categoria** para a política.
1. Escolha ou modifique os filtros para criar e atribuir da política.
1. Refine ou adicione mais filtros.
1. Salve e aplique a nova política.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre os recursos adicionais e de pontuação de prioridade de investigação da funcionalidade do [Microsoft Cloud App Security](/cloud-app-security/).

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!