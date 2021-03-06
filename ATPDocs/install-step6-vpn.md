---
title: Instalar a Integração de VPN da Proteção Avançada contra Ameaças do Azure
description: Colete informações de contabilidade para o Azure ATP integrando uma VPN.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/05/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0d9d2a1d-6c76-4909-b6f9-58523df16d4f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 589e8f647abc4654d48006dd1e9b3d6a9538660f
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912993"
---
# <a name="integrate-vpn"></a>Integrar a VPN

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

O Azure ATP (Proteção Avançada contra Ameaças) pode coletar informações de contabilidade de soluções de VPN. Quando configurada, a página de perfil do usuário inclui informações de conexões de VPN, tais como os endereços IP e os locais de origem das conexões. Isso complementa o processo de investigação, fornecendo informações adicionais sobre a atividade de usuário, bem como uma nova detecção para conexões de VPN anormais. A chamada para resolver um endereço IP externo de um local é anônima. Nenhuma identificação pessoal será enviada nesta chamada.

O Azure ATP integra-se à sua solução de VPN escutando eventos de contabilidade do RADIUS encaminhados para os sensores do Azure ATP. Este mecanismo é baseado em Contabilização RADIUS padrão ([RFC 2866](https://tools.ietf.org/html/rfc2866)) e têm suporte dos seguintes fornecedores de VPN:

- Microsoft
- F5
- Check Point
- Cisco ASA

## <a name="prerequisites"></a>Pré-requisitos

Para habilitar a integração de VPN, verifique se você definiu os seguintes parâmetros:

- Abra a porta UDP 1813 em seus sensores do Azure ATP e/ou nos sensores autônomos do Azure ATP.

> [!NOTE]
> Quando a **Contabilização RADIUS** é habilitada, o sensor do ATP do Azure ativa uma política de firewall pré-provisionada pelo Windows chamada **Sensor da Proteção Avançada contra Ameaças do Azure** para permitir a entrada da Contabilização RADIUS na porta UDP 1813.

O exemplo abaixo usa o Servidor de Roteamento e Acesso Remoto (RRAS) da Microsoft para descrever o processo de configuração de VPN.

Se estiver usando uma solução de VPN de terceiros, confira a documentação para ver instruções de como habilitar a Contabilização RADIUS.

## <a name="configure-radius-accounting-on-the-vpn-system"></a>Configurar a Contabilização de RADIUS no sistema de VPN

Execute as seguintes etapas em seu servidor RRAS.

1. Abra o console de Roteamento e Acesso Remoto.
1. Clique com o botão direito do mouse no nome do servidor e clique em **Propriedades**.
1. Na guia **Segurança**, em **Provedor de contabilização**, selecione **Contabilização RADIUS** e clique em **Configurar**.

    ![Configuração RADIUS](media/radius-setup.png)

1. Na janela **Adicionar servidor RADIUS**, digite o **Nome do servidor** do sensor mais próximo da Proteção Avançada contra Ameaças do Azure (que tenha conectividade com a rede). Para HA, é possível adicionar sensores extras da Proteção Avançada contra Ameaças do Azure como servidores RADIUS. Em **Porta**, verifique se o padrão de 1813 está configurado. Clique em **Alterar** e digite uma nova cadeia de caracteres alfanuméricos secreta compartilhada. Anote a nova cadeia de caracteres secreta compartilhada, pois você precisará preenchê-la mais tarde durante a configuração do ATP do Azure. Marque a caixa **Enviar mensagens de conta habilitada e de contabilização desabilitada do RADIUS** e, em seguida, clique em **OK** em todas as caixas de diálogo abertas.

    ![Configuração de VPN](media/vpn-set-accounting.png)

### <a name="configure-vpn-in-atp"></a>Configurar VPN no ATP

O Azure ATP coleta dados da VPN que ajudam a criar o perfil dos locais dos quais os computadores se conectam à rede e a detectar conexões VPN suspeitas.

Para configurar dados de VPN no ATP:

1. No portal do Azure ATP, clique na engrenagem de configuração e, em seguida, em **VPN**.
1. Ativar **Contabilização Radius** e digite o **Segredo Compartilhado** configurado anteriormente em seu servidor VPN do RRAS. Em seguida, clique em **Salvar**.

    ![Configurar VPN do Azure ATP](media/atp-vpn-radius.png)

Depois que isso for habilitado, todos os sensores do ATP do Azure passarão a escutar na porta 1813 os eventos de contabilização do RADIUS, e a instalação da VPN estará concluída.

 Depois que o sensor do Azure ATP receber os eventos de VPN e os enviar para o serviço de nuvem do Azure ATP para processamento, o perfil de entidade indicará locais distintos de VPN acessados e as atividades no perfil indicarão os locais.

## <a name="see-also"></a>Consulte Também

- [Ferramenta de dimensionamento do Azure ATP](https://aka.ms/aatpsizingtool)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do Azure ATP](prerequisites.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
