---
title: Relatório de avaliação de situação de segurança de identidade de criptografia fraca da Proteção Avançada contra Ameaças do Azure
description: Neste artigo, você tem uma visão geral do relatório de avaliação de situação de segurança de identidade de criptografia fraca da ATP do Azure.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: cc82212b-7d25-4ec7-828d-2475ff40d685
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 728103079da513129a55875d28f360c5cd176b47
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911934"
---
# <a name="security-assessment-weak-cipher-usage"></a>Avaliação de segurança: Uso de criptografia fraca

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-weak-ciphers"></a>O que é criptografia fraca?

A criptografia depende da codificação para criptografar dados. Por exemplo, o RC4 (Rivest Cipher 4, também conhecido como ARC4 ou ARCFOUR, que significa Alleged RC4) é um deles. Embora o RC4 seja notável por sua simplicidade e velocidade, várias vulnerabilidades foram descobertas desde sua versão original, tornando-o inseguro. O RC4 é especialmente vulnerável quando o início do fluxo de chave de saída não é descartado ou quando chaves relacionadas ou não aleatórias são usadas.

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>Como usar esta avaliação de segurança para aprimorar minha situação de segurança organizacional?

1. Analise a avaliação de segurança do uso de criptografia fraca.
    ![Analisar a avaliação do uso da criptografia fraca](media/atp-cas-isp-weak-cipher-2.png)
1. Pesquise o motivo para os clientes e os servidores identificados usarem criptografias fracas.
1. Corrija os problemas e desabilite o uso do RC4 e/ou outras criptografias fracas (como DES/3DES).
1. Para saber mais sobre como desabilitar o RC4, confira o [Microsoft Security Advisory](https://support.microsoft.com/help/2868725/microsoft-security-advisory-update-for-disabling-rc4).

> [!NOTE]
> Essa avaliação é atualizada quase em tempo real.

## <a name="remediation"></a>Remediação

Desabilite os clientes e os servidores que você não quer que usem os pacotes de criptografia do RC4 configurando as seguintes chaves do Registro. Após desabilitar, qualquer servidor ou cliente que se comunique com outro cliente ou servidor que exija o uso do RC4 poderá impedir que a conexão ocorra. Os clientes com essa configuração implantada não conseguirão se conectar a sites que exigem o RC4. Os servidores que implantam essa configuração não conseguirão atender clientes que exigem o uso do RC4.

> [!NOTE]
> Não se esqueça de testar as seguintes configurações em um ambiente controlado antes de habilitá-las na produção.
>
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]   "Enabled"=dword:00000000

Para saber mais sobre como baixar e atualizar as edições do Registro, confira o [Microsoft Security Advisory](/security-updates/SecurityAdvisories/2013/2868725).

## <a name="next-steps"></a>Próximas etapas

- [Filtrar atividades da ATP do Azure no Cloud App Security](activities-filtering-mcas.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)