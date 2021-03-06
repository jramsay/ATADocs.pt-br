---
title: Monitorar eventos e a integridade do sistema de proteção avançada contra ameaças do Azure
description: Use o centro de integridade do ATP do Azure para verificar como o serviço do ATP do Azure está funcionando, ser alertado sobre possíveis problemas e exibir eventos de sistema no Visualizador de Eventos.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 1/3/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fc192856a247ca4ee47e5e73ddc366bb7592a0c0
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910387"
---
# <a name="work-with-azure-atp-health-and-events"></a>Trabalhar com eventos e integridade do ATP do Azure

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="azure-atp-health-center"></a>Centro de integridade do ATP do Azure 

O centro de integridade do ATP do Azure informa sobre o desempenho da instância do ATP do Azure e alerta quando há problemas.

## <a name="working-with-the-azure-atp-health-center"></a>Trabalhando com o centro de integridade do ATP do Azure

O centro de integridade do ATP do Azure permite que você saiba que há um problema gerando um alerta (um ponto vermelho) acima do ícone de Centro de Integridade na barra de menus.

![Barra de ferramentas do ponto vermelho do centro de integridade do ATP do Azure](media/atp-health-bar.png)

### <a name="managing-azure-atp-health"></a>Gerenciando a integridade do ATP do Azure
Para verificar a integridade geral da instância do ATP do Azure, clique no ícone do Centro de Integridade na barra de menus ![Ícone do centro de integridade do ATP do Azure](media/atp-red-dot.png)

- Todos os problemas abertos podem ser gerenciados configurando-os para **Fechar** ou **Suprimir** clicando nos três pontos no canto do alerta e fazendo sua escolha.

-   **Abrir**: todas as novas atividades suspeitas aparecem nesta lista.

-   **Fechar**: é usado para rastrear atividades suspeitas que você identificou, pesquisou e corrigiu como mitigado.

    > [!NOTE]
    > O Azure ATP poderá reabrir uma atividade fechada se a mesma atividade for detectada novamente em um curto período.
    
-   **Suprimir**: suprimir uma atividade significa que você deseja ignorá-la por enquanto e apenas ser alertado novamente se houver uma nova instância. Se houver um alerta semelhante, o Azure ATP não o reabrirá. Mas, se o alerta parar por sete dias e, depois, for observado novamente, você será alertado novamente.

-   **Reabrir**: você pode reabrir um alerta fechado ou suprimido para que ele seja exibido novamente como **Aberto** na linha do tempo.

-   **Excluir**: na linha do tempo de alerta de segurança, você também tem a opção de excluir um problema de integridade. Se você excluir um alerta, ele será excluído da instância e você NÃO poderá restaurá-lo. Após clicar em Excluir, será possível excluir todos os alertas de segurança do mesmo tipo.



![Imagem dos problemas da central de integridade do Azure ATP](media/atp-health-issue.png)






## <a name="see-also"></a>Consulte Também

- [Trabalhando com atividades suspeitas](working-with-suspicious-activities.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)
