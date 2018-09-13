---
title: Verificação de política de auditoria avançada da Proteção Avançada contra Ameaças do Azure | Microsoft Docs
description: Este artigo fornece uma visão geral da verificação de política de auditoria avançada da ATP do Azure.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/30/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d37a55bdb1c437f7775f530cfc143146eb38ba96
ms.sourcegitcommit: 93a133430ac85d6db7afad5f6f2583b3a39c423a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2018
ms.locfileid: "43469690"
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*


# <a name="azure-atp-advanced-audit-policy-check"></a>Verificação de política de auditoria avançada da ATP do Azure

A detecção da ATP do Azure depende de Logs de Eventos do Windows para obter visibilidade em determinados cenários, tais como logons de NTLM, modificações de grupos de segurança e eventos semelhantes. Para que os eventos corretos sejam auditados e incluídos no Log de Eventos do Windows, seus controladores de domínio exigem configurações precisas de política de auditoria avançada. Configurações de política de auditoria avançada incorretas fazem com que eventos críticos fiquem de fora de seus logs e resultam em uma cobertura incompleta da ATP do Azure.

Para facilitar a verificação do status atual de cada uma das políticas de auditoria avançada do controlador de domínio, a ATP do Azure verifica automaticamente as políticas de auditoria avançadas existentes e emite alertas de integridade para as configurações de política que exigem modificação. Cada alerta de integridade fornece detalhes específicos sobre o controlador de domínio e a política que apresenta problemas, bem como sugestões de correção.

![Alerta de Integridade da política de auditoria avançada](media/atp-health-alert-audit-policy.png)


A política de auditoria de segurança avançada está habilitada via GPO. Esses eventos de auditoria são registrados nos Eventos do Windows do controlador de domínio. Isso deve ser habilitado na **Política de controladores de domínio padrão** no Active Directory.

<br>Modifique as políticas de auditoria avançadas do seu controlador de domínio usando as instruções a seguir:

1. Faça logon no servidor como **administrador do domínio**.
2. Carregue o Editor de Gerenciamento de Política de Grupo de **Gerenciador do Servidor** > **Ferramentas** > **Gerenciamento de Política de Grupo**. 
3. Expanda as **Unidades organizacionais de controladores de domínio**, clique com o botão direito do mouse em **Política de controladores de domínio padrão** e selecione **Editar**. 

    ![Editar política de controlador de domínio](media/atp-advanced-audit-policy-check-step-1.png)

4. Na janela que é aberta, vá para **Configuração do computador** > **Políticas** > **Configurações do Windows** > **Configurações de segurança** > **Configuração de política de auditoria avançada**.

    ![Configuração Avançada de Política de Auditoria](media/atp-advanced-audit-policy-check-step-2.png)

5. Vá para Logon na conta, clique duas vezes em **Validação de credenciais de auditoria** e selecione **Configurar estes eventos de auditoria**, tanto para eventos de êxito quanto para os de falha. 

    ![Validação de credenciais](media/atp-advanced-audit-policy-check-step-3.png)

6. Vá para Logon na conta, clique duas vezes em **Gerenciamento do grupo de segurança de auditoria** e selecione **Configurar estes eventos de auditoria**, tanto para eventos de êxito quanto para os de falha.

    ![Auditoria de gerenciamento do grupo de distribuição](media/atp-advanced-audit-policy-check-step-4.png)

7. Após a aplicação por meio do GPO, os novos eventos ficam visíveis nos **Logs de Eventos do Windows**.

## <a name="see-also"></a>Consulte Também
- [Pré-requisitos do Azure ATP](atp-prerequisites.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)