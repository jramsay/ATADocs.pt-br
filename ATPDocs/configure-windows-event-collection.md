---
title: Configurar a coleção de Eventos do Windows na Proteção Avançada contra Ameaças do Azure
description: Nesta etapa da instalação da ATP, você configura a coleção de Eventos do Windows.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/04/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 88692d1a-45a3-4d54-a549-4b5bba6c037b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8a7c22c2ea752b0443fac2b4e74b2ff4813bfee8
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910474"
---
# <a name="configure-windows-event-collection"></a>Configurar a coleção de Eventos do Windows

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

A detecção da ATP do Azure (Proteção Avançada contra Ameaças do Azure) depende de entradas específicas do log de eventos do Windows para aprimorar algumas detecções e fornecer informações adicionais sobre quem realizou ações específicas, como logons NTLM, modificações no grupo de segurança e eventos semelhantes. Para que os eventos corretos sejam auditados e incluídos no Log de Eventos do Windows, seus controladores de domínio exigem configurações precisas de política de auditoria avançada. Configurações de política de auditoria avançada incorretas podem ocasionar que eventos necessários não sejam registrados no log de eventos e resultar em uma cobertura incompleta da ATP do Azure.

Para aprimorar os recursos de detecção de ameaças, a ATP do Azure precisa que os seguintes eventos do Windows sejam [configurados](#configure-audit-policies) e [coletados](#configure-event-collection) pela ATP do Azure:

- 4726 – conta de usuário excluída
- 4728 – membro adicionado ao grupo de segurança global
- 4729 – membro removido do grupo de segurança global
- 4730 – grupo de segurança global excluído
- 4732 – membro adicionado ao grupo de segurança local
- 4733 – membro removido do grupo de segurança global
- 4743 – conta de computador excluída
- 4753 – grupo de distribuição global excluído
- 4756 – membro adicionado ao grupo de segurança universal
- 4757 – membro removido do grupo de segurança universal
- 4758 – grupo de segurança universal excluído
- 4763 – grupo de distribuição universal excluído
- 4776 – controlador de domínio tentou validar credenciais para uma conta (NTLM)
- 7045 – novo serviço instalado
- 8004 – autenticação NTLM

## <a name="configure-audit-policies"></a>Configurar políticas de auditoria

Modifique as políticas de auditoria avançadas do seu controlador de domínio usando as instruções a seguir:

1. Faça logon no servidor como **administrador do domínio**.
1. Carregue o Editor de Gerenciamento de Política de Grupo de **Gerenciador do Servidor** > **Ferramentas** > **Gerenciamento de Política de Grupo**.
1. Expanda as **Unidades organizacionais de controladores de domínio**, clique com o botão direito do mouse em **Política de controladores de domínio padrão** e, em seguida, selecione **Editar**.

    > [!NOTE]
    > Você pode usar a Política de controladores de domínio padrão ou um GPO dedicado para definir essas políticas.

    ![Editar política de controlador de domínio](media/atp-advanced-audit-policy-check-step-1.png)

1. Na janela que é aberta, acesse **Configuração do Computador** > **Políticas** > **Configurações do Windows** > **Configurações de Segurança** e, dependendo da política que você deseja habilitar, faça o seguinte:

    **Para configuração da política de auditoria avançada**

    1. Acesse **Configuração da Política de Auditoria Avançada** > **Políticas de Auditoria**.
        ![Configuração avançada da política de auditoria](media/atp-advanced-audit-policy-check-step-2.png)
    1. Em **Políticas de Auditoria**, edite cada uma das políticas a seguir e selecione **Configurar os eventos de auditoria a seguir** para eventos de **Êxito** e de **Falha**.

        | Política de auditoria | Subcategoria | IDs dos eventos de gatilho |
        | --- |---|---|
        | Logon da conta | Auditoria da validação de credenciais | 4776 |
        | Gerenciamento de Contas | Auditoria do gerenciamento da conta de computador | 4743 |
        | Gerenciamento de Contas | Auditoria do gerenciamento do grupo de distribuição | 4753, 4763 |
        | Gerenciamento de Contas | Auditoria de gerenciamento do grupo de distribuição | 4728, 4729, 4730, 4732, 4733, 4756, 4757, 4758 |
        | Gerenciamento de Contas | Auditoria de gerenciamento de conta de usuário | 4726 |
        | Sistema | Auditoria da extensão do sistema de segurança | 7045 |

        Por exemplo, para configurar **Gerenciamento de Grupo de Segurança de Auditoria**, em **Gerenciamento de Conta**, clique duas vezes em **Gerenciamento de Grupo de Segurança de Auditoria** e, em seguida, selecione **Configurar os eventos de auditoria a seguir** para eventos de **Êxito** e de **Falha**.

        ![Auditoria de gerenciamento do grupo de distribuição](media/atp-advanced-audit-policy-check-step-4.png)

    <a name="ntlm-authentication-using-windows-event-8004"></a> **Para políticas locais (ID do evento: 8004)**

    > [!NOTE]
    >
    > - As políticas de grupo de domínio para coletar o Evento 8004 do Windows devem ser aplicadas **somente** aos controladores de domínio.
    > - Quando o evento 8004 do Windows é analisado pelo sensor da ATP do Azure, as atividades de autenticação NTLM da ATP do Azure são aprimoradas com os dados acessados pelo servidor.

    1. Acesse **Políticas Locais** > **Opções de Segurança**.
    1. Em **Opções de Segurança**, configure as políticas de segurança especificadas, da seguinte maneira

        | Configuração de política de segurança | Valor |
        |---|---|
        | Segurança de rede: Restringir NTLM: Tráfego NTLM de saída para servidores remotos | Auditar tudo |
        | Segurança de rede: Restringir NTLM: Autenticação NTLM neste domínio | Habilitar tudo |
        | Segurança de rede: restringir NTLM: Auditar tráfego NTLM de entrada | Habilitar auditoria para todas as contas |

        Por exemplo, para configurar **Tráfego NTLM de saída para servidores remotos**, em **Opções de Segurança**, clique duas vezes em **Segurança de rede: restringir NTLM: Tráfego NTLM de saída para servidores remotos** e, em seguida, selecione **Auditar todos**.

        ![Auditar tráfego NTLM de saída para servidores remotos](media/atp-advanced-audit-policy-check-step-3.png)

    > [!NOTE]
    > Se você optar por usar uma política de segurança local em vez de usar uma política de grupo, adicione os logs de auditoria de **Logon da Conta**, **Gerenciamento da Conta** e **Opções de Segurança** em sua política local. Se você estiver configurando a política de auditoria avançada, force a [subcategoria de política de auditoria](/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override).

1. Após a aplicação por meio do GPO, os novos eventos ficam visíveis nos **Logs de Eventos do Windows**.

<!--
## Azure ATP Advanced Audit Policy check

To make it easier to verify the current status of each of your domain controller's Advanced Audit Policies, Azure ATP automatically checks your existing Advanced Audit Policies and issues health alerts for policy settings that require modification. Each health alert provides specific details of the domain controller, the problematic policy as well as remediation suggestions.

![Advanced Audit Policy Health Alert](media/atp-health-alert-audit.png)

Advanced Security Audit Policy is enabled via **Default Domain Controllers Policy** GPO. These audit events are recorded on the domain controller's Windows Events.
-->

## <a name="configure-event-collection"></a>Configurar coleta de eventos

Esses eventos podem ser coletados automaticamente pelo sensor da ATP do Azure ou, se o sensor da ATP do Azure não for implantado, eles poderão ser encaminhados para o sensor autônomo da ATP do Azure de uma das seguintes maneiras:

- [Configurar o sensor autônomo da ATP do Azure](configure-event-forwarding.md) para escutar eventos de SIEM
- [Configurar o encaminhamento de eventos do Windows](configure-event-forwarding.md)

> [!NOTE]
>
> - Os sensores autônomos do ATP do Azure não dão suporte à coleção de entradas de log do ETW (Rastreamento de Eventos para Windows) que fornecem os dados para várias detecções. Para cobertura completa do seu ambiente, é recomendável implantar o sensor do ATP do Azure.
> - É importante revisar e verificar suas [políticas de auditoria]() antes de configurar a coleta de eventos para garantir que os controladores de domínio estejam configurados corretamente para registrar os eventos necessários.

## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/aatpsizingtool)
- [Pré-requisitos do Azure ATP](prerequisites.md)
- [Referência de logs de SIEM do Azure ATP](cef-format-sa.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)