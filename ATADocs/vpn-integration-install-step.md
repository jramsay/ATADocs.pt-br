---
title: Instalar o Advanced Threat Analytics-etapa 7
description: Nesta etapa da instalação do ATA, você integra sua VPN.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 11/07/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e0aed853-ba52-46e1-9c55-b336271a68e7
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ab9203edf49031e749a1d814fda08c52845345a5
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90908667"
---
# <a name="install-ata---step-7"></a>Instalação do ATA – Etapa 7

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!div class="step-by-step"]
> [«Etapa 5](install-ata-step5.md) 
>  [Etapa 8»](install-ata-step7.md)

## <a name="step-7-integrate-vpn"></a>Etapa 7. Integrar a VPN

O Microsoft Advanced Threat Analytics (ATA) versão 1,8 e superior pode coletar informações de contabilidade de soluções de VPN. Quando configurada, a página de perfil do usuário inclui informações de conexões de VPN, tais como os endereços IP e os locais de origem das conexões. Isso complementa o processo de investigação, fornecendo informações adicionais sobre a atividade de usuário. A chamada para resolver um endereço IP externo de um local é anônima. Nenhuma identificação pessoal será enviada nesta chamada.

O ATA integra-se à solução de VPN escutando eventos contábeis do RADIUS encaminhados para os Gateways do ATA. Este mecanismo é baseado em Contabilização RADIUS padrão ([RFC 2866](https://tools.ietf.org/html/rfc2866)) e têm suporte dos seguintes fornecedores de VPN:

- Microsoft
- F5
- Cisco ASA

> [!IMPORTANT]
> A partir de setembro de 2019, o serviço de localização geográfica de VPN do Advanced Threat Analytics responsável por detectar locais de VPN agora dá suporte exclusivamente a TLS 1,2. Verifique se o centro do ATA está configurado para dar suporte a TLS 1,2, já que as versões 1,1 e 1,0 não têm mais suporte.

## <a name="prerequisites"></a>Pré-requisitos

Para habilitar a integração de VPN, verifique se você definiu os seguintes parâmetros:

- Abra a porta UDP 1813 nos Gateways do ATA e Gateways Lightweight do ATA.

- O Centro do ATA deve ser capaz de acessar o *ti.ata.azure.com* usando HTTPS (porta 443) para que ele possa consultar a localização dos endereços IP de entrada.

O exemplo abaixo usa o Servidor de Roteamento e Acesso Remoto (RRAS) da Microsoft para descrever o processo de configuração de VPN.

Se estiver usando uma solução de VPN de terceiros, confira a documentação para ver instruções de como habilitar a Contabilização RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurar a Contabilização de RADIUS no sistema de VPN

Execute as seguintes etapas em seu servidor RRAS.

1. Abra o console de Roteamento e Acesso Remoto.
1. Clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.
1. Na guia **Segurança**, em **Provedor de contabilização**, selecione **Contabilização RADIUS** e clique em **Configurar**.

    ![Configuração RADIUS](media/radius-setup.png)

1. Na janela **Adicionar Servidor RADIUS**, digite o **Nome do servidor** do Gateway do ATA ou Gateway Lightweight do ATA mais próximo. Em **Porta**, verifique se o padrão de 1813 está configurado. Clique em **Alteração** e digite uma nova cadeia de caracteres alfanuméricos secreta compartilhada da qual você possa se lembrar. Você precisa preenchê-la mais tarde em sua Configuração do ATA. Marque a caixa **Enviar mensagens de Contabilização RADIUS Ligada e Desligada** caixa e, em seguida, clique em **OK** em todas as caixas de diálogo abertas.

    ![Captura de tela mostrando a configuração de VPN](media/vpn-set-accounting.png)

### <a name="configure-vpn-in-ata"></a>Configurar VPN no ATA

O ATA coleta dados de VPN e identifica quando e onde as credenciais estão sendo usadas por meio da VPN e integra os dados em sua investigação. Isso fornece informações adicionais para ajudá-lo a investigar os alertas relatados pelo ATA.

Para configurar dados de VPN no ATA:

1. No console do ATA, abra a página Configuração do ATA e vá para **VPN**.

    ![Menu de configuração do ATA](media/config-menu.png)

1. Ativar **Contabilização Radius** e digite o **Segredo Compartilhado** configurado anteriormente em seu servidor VPN do RRAS. Em seguida, clique em **Salvar**.

    ![Configurar a VPN do ATA](media/vpn.png)

Depois que ela estiver habilitada, todos os Gateways do ATA e Gateways Lightweight escutarão na porta 1813 para eventos de contabilização RADIUS.

A instalação está concluída e você pode ver atividade de VPN na página de perfil do usuário:

![Configuração de VPN](media/vpn-user.png)

Depois que o Gateway do ATA recebe os eventos de VPN e os envia ao centro do ATA para processamento, o centro do ATA precisa acessar *ti.ata.azure.com* usando HTTPS (porta 443) para ser capaz de resolver os endereços IP externos nos eventos de VPN para seu local geográfico.

> [!div class="step-by-step"]
> [«Etapa 6](install-ata-step5.md) 
>  [Etapa 8»](install-ata-step7.md)

## <a name="related-videos"></a>Vídeos Relacionados

- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>Consulte Também

- [Guia de implantação da POC (prova de conceito) do ATA](https://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](https://aka.ms/aatpsizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
