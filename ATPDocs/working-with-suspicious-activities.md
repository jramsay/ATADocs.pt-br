---
title: "Trabalhar com atividades suspeitas na Proteção Avançada contra Ameaças do Azure | Microsoft Docs"
description: Descreve como examinar atividades suspeitas identificadas pelo Azure ATP
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a5e7598e94e1d6d4b09c827770e062be9fefd1c4
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2018
---
*Aplica-se a: Proteção Avançada contra Ameaças do Azure*



# <a name="working-with-suspicious-activities"></a>Trabalhando com atividades suspeitas
Este artigo explica noções básicas de como trabalhar com a Proteção Avançada contra Ameaças do Azure.

## <a name="review-suspicious-activities-on-the-attack-time-line"></a>Examinar atividades suspeitas na linha do tempo de ataque
Após fazer logon no portal do espaço de trabalho do Azure ATP, você será levado automaticamente para a **linha do tempo de atividades suspeitas** aberta. As atividades suspeitas são listadas em ordem cronológica com as atividades suspeitas mais recentes na parte superior da linha do tempo.
Cada atividade suspeita tem as seguintes informações:

-   Entidades envolvidas, incluindo usuários, computadores, servidores, controladores de domínio e recursos.

-   Os tempos e o intervalo de tempo das atividades suspeitas.

-   A severidade da atividade suspeita: alta, média ou baixa.

-   Status: aberto, fechado ou suprimido.

-   Capacidade de

    -   Compartilhar a atividade suspeita com outras pessoas na organização por email.

    -   Exportar a atividade suspeita para o Excel.

> [!NOTE]
> -   Quando você passa o mouse sobre um usuário ou computador, é exibido um perfil simplificado da entidade que fornece informações adicionais sobre a entidade e inclui o número de atividades suspeitas vinculado à entidade.
> -   Se você clicar em uma entidade, ela levará você ao perfil de entidade de usuário ou computador.

![Imagem da linha do tempo de atividades suspeitas do Azure ATP](media/atp-sa-timeline.png)

## <a name="filter-suspicious-activities-list"></a>Filtrar lista de atividades suspeitas
Para filtrar a lista de atividades suspeitas:

1.  No painel **Filtrar por** no lado esquerdo da tela, selecione uma das seguintes opções: **Tudo**, **Aberto**, **Fechado** ou **Suprimido**.

2.  Para filtrar a lista ainda mais, selecione **Alta**, **Média** ou **Baixa**.

**Gravidade da atividade suspeita**

-   **Baixa**

    Indica atividades suspeitas que podem levar a ataques projetados para usuários ou softwares mal-intencionados para obter acesso aos dados organizacionais.

-   **Média**

    Indica atividades suspeitas que podem colocar identidades específicas em risco de ataques mais graves que podem resultar em roubo de identidade ou escalonamento privilegiado

-   **Alta**

    Indica as atividades suspeitas que podem levar a roubo de identidade, elevação de privilégios ou outros ataques de alto impacto




## <a name="managing-suspicious-activities"></a>Gerenciando atividades suspeitas
Você pode alterar o status de uma atividade suspeita clicando no status atual da atividade suspeita e selecionando uma das seguintes opções **Aberto**, **Suprimido**, **Fechado** ou **Excluído**.
Para fazer isso, clique nos três pontos no canto superior direito de uma atividade suspeita específica para exibir a lista de ações disponíveis.

![Ações do Azure ATP para atividades suspeitas](./media/atp-sa-actions.png)

**Status de atividade suspeita**

-   **Abrir**: todas as novas atividades suspeitas aparecem nesta lista.

-   **Fechar**: é usado para rastrear atividades suspeitas que você identificou, pesquisou e corrigiu como mitigado.

    > [!NOTE]
    > Se a mesma atividade for detectada novamente em um curto período, o Azure ATP poderá reabrir uma atividade fechada.

-   **Suprimir**: suprimir uma atividade significa que você deseja ignorá-la por enquanto e apenas ser alertado novamente se houver uma nova instância. Isso significa que, se houver um alerta semelhante, o Azure ATP não o reabrirá. Mas, se o alerta parar por sete dias e for observado novamente, você será alertado novamente.

- **Excluir**: se você excluir um alerta, ele será excluído do sistema, do banco de dados e você NÃO poderá restaurá-lo. Depois de clicar em Excluir, você poderá excluir todas as atividades suspeitas do mesmo tipo.

- **Excluir**: a capacidade de excluir uma entidade de gerar mais de um determinado tipo de alertas. Por exemplo, você pode configurar o Azure ATP para impedir que uma entidade (usuário ou computador) específica emita novamente um alerta para um determinado tipo de atividade suspeita, como um administrador específico que executa código remoto ou um verificador de segurança que faz o reconhecimento de DNS. Além de ser capaz de adicionar exclusões diretamente na atividade suspeita conforme ela é detectada na linha do tempo, você também pode acessar a página Configuração até **Exclusões** e para cada atividade suspeita, você pode adicionar e remover manualmente entidades ou sub-redes excluídas (por exemplo, para Passagem de Tíquete). 

> [!NOTE]
> As páginas de configuração podem ser modificadas apenas por administradores do Azure ATP.


## <a name="see-also"></a>Consulte Também

- [Como trabalhar com o portal de espaço de trabalho do Azure ATP](workspace-portal.md)
- [Confira o fórum do ATP!](https://aka.ms/azureatpcommunity)