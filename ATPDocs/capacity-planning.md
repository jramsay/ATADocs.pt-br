---
title: Guia de início rápido para planejamento de implantação da Proteção Avançada contra Ameaças do Azure
description: Ajuda você a planejar a implantação e a decidir quantos servidores do Azure ATP serão necessários para dar suporte à sua rede
author: shsagir
ms.author: shsagir
ms.date: 05/20/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 6955ea798cc138142f0b3f4443df777ed2d07cac
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913256"
---
# <a name="quickstart-plan-capacity-for-azure-atp"></a>Início Rápido: Planejar capacidade para o ATP do Azure

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Neste guia de início rápido, você determinará quantos sensores do ATP do Azure serão necessários.

## <a name="prerequisites"></a>Pré-requisitos

- Baixe a [ferramenta de dimensionamento do ATP do Azure](https://aka.ms/aatpsizingtool).
- Confira o artigo sobre a [arquitetura do ATP do Azure](architecture.md).
- Confira o artigo sobre os [pré-requisitos do ATP do Azure](prerequisites.md).

## <a name="use-the-sizing-tool"></a>Usar a ferramenta de dimensionamento

A maneira recomendada e mais simples de determinar a capacidade da implantação do ATP do Azure é usar a ferramenta de dimensionamento. Caso isso não seja possível, colete informações sobre o tráfego manualmente. Para saber mais sobre o método manual, confira a seção [Estimador de tráfego do controlador de domínio](#manual-sizing), no final deste artigo.

1. Execute a ferramenta de dimensionamento do ATP do Azure, **TriSizingTool.exe**, do arquivo zip que você baixou.
1. Quando concluir a execução da ferramenta, abra os resultados de arquivo do Excel.
1. No arquivo do Excel, localize e clique na planilha **Resumo do ATP do Azure**. A outra planilha não é necessária, pois ela se destina ao planejamento do ATA.
    ![Ferramenta de planejamento de capacidade de amostra](media/capacity-tool.png)

1. Localize o campo **Pacotes ocupados/s**, na tabela do sensor do ATP do Azure, no arquivo de resultados do Excel, e anote isso.
1. Compare o campo **Pacotes ocupados/s** com o campo **PACOTES POR SEGUNDO**, na seção [Tabela do sensor do ATP do Azure](#sizing) deste artigo. Use os campos para determinar a capacidade de memória e CPU que será usada pelo sensor.

## <a name="azure-atp-sensor-sizing"></a><a name="sizing"></a> Dimensionamento do sensor do ATP do Azure

Um sensor do ATP do Azure pode ter suporte para monitoramento de um controlador de domínio com base na quantidade de tráfego de rede gerado pelo controlador de domínio. A tabela a seguir representa uma estimativa. O valor final que o sensor analisa depende da quantidade de tráfego e da distribuição desse tráfego.

A capacidade da CPU e da memória RAM a seguir se refere ao **consumo do próprio sensor**, e não à capacidade do controlador de domínio.

|Pacotes por segundo|CPU (núcleos)\*|Memória\*\* (GB)|
|----|----|-----|
|0 - 1k|0.25|2.50|
|1k - 5k|0.75|6.00|
|5k - 10k|1.00|6.50|
|10k - 20k|2.00|9.00|
|20k - 50k|3.50|9.50|
|50k - 75k |3.50|9.50|
|75k - 100k|3.50|9.50|

\* Isso inclui os núcleos físicos, não os núcleos com hyper-threading.  
\*\* Memória RAM

Quando determinar o dimensionamento, observe os seguintes itens:

- Número total de núcleos a serem usados pelo serviço de sensor.  
Recomendamos não trabalhar com núcleos hyper-threaded. Trabalhar com núcleos com hyper-threading pode resultar em problemas de integridade do sensor do ATP do Azure.
- Número total de memória a ser usada pelo serviço de sensor.
- Se o controlador de domínio não tiver os recursos exigidos pelo sensor do ATP do Azure, o desempenho do controlador de domínio não será afetado, mas o sensor do ATP do Azure poderá não operar conforme o esperado.
- Na execução como uma máquina virtual, toda a memória precisa ser alocada para a máquina virtual em todos os momentos.
- Para ter um melhor desempenho, defina a **Opção de Energia** do sensor do Azure ATP como **Alto Desempenho**.
- São necessários no mínimo dois núcleos e
- 6 GB de espaço no disco rígido. No entanto, recomendamos 10 GB, incluindo o espaço necessário para os binários e logs do ATP do Azure.

### <a name="dynamic-memory"></a>Memória dinâmica

> [!NOTE]
> Na execução como uma VM (máquina virtual), toda a memória precisa ser alocada para a VM em todos os momentos.

|VM em execução em|Descrição|
|------------|-------------|
|Hyper-V|Garanta que a opção **Habilitar Memória Dinâmica** não esteja habilitada para a VM.|
|VMWare|Verifique se a quantidade de memória configurada e a memória reservada são iguais ou selecione a seguinte opção na configuração da VM – **Reservar toda a memória de convidado (Tudo bloqueado)** .|
|Outro host de virtualização|Confira a documentação fornecida pelo fornecedor sobre como garantir que a memória seja totalmente alocada para a VM em todos os momentos. |

## <a name="domain-controller-traffic-estimation"></a><a name="manual-sizing"></a> Estimativa de tráfego do controlador de domínio

Se, por alguma razão, não for possível usar a ferramenta de dimensionamento do ATP do Azure, reúna manualmente as informações do contador de pacotes/s de todos os controladores de domínio. Reúna as informações durante 24 horas com um pequeno intervalo de coleta de aproximadamente cinco segundos. Em seguida, calcule a média diária e a média mais ocupada do período (15 minutos) de cada controlador de domínio. As seções a seguir apresentam instruções de como coletar o contador de pacotes/s de um controlador de domínio.

Há várias ferramentas que você pode usar para descobrir a média de pacotes por segundo dos controladores de domínio. Caso não tenha as ferramentas que controlam este contador, use o monitor de desempenho para coletar as informações necessárias.

Para determinar os pacotes por segundo, faça os seguintes procedimentos em cada controlador de domínio:

1. Abra o Monitor de Desempenho.

    ![Imagem do monitor de desempenho](media/atp-traffic-estimation-1.png)

1. Expanda **Conjuntos de Coletores de Dados**.

    ![Imagem dos conjuntos de coletores de dados](media/atp-traffic-estimation-2.png)

1. Clique com botão direito do mouse em **Usuário Definido** e selecione **Novo** &gt; **Conjunto de Coletores de Dados**.

    ![Imagem do novo conjunto de coletores de dados](media/atp-traffic-estimation-3.png)

1. Insira um nome para o conjunto de coletores e selecione **Criar Manualmente (Avançado)** .

1. Em **Que tipo de dados deseja incluir?** , selecione **Criar logs de dados e Contador de desempenho**.

    ![Imagem do tipo de dados do novo conjunto de coletores de dados](media/atp-traffic-estimation-5.png)

1. Em **Que contadores de desempenho deseja registrar em log?** , clique em **Adicionar**.

1. Expanda **Adaptador de Rede**, selecione **Pacotes/s** e escolha a instância apropriada. Se não tiver certeza, selecione **&lt;Todas as instâncias&gt;** , clique em **Adicionar** e em **OK**.

    > [!NOTE]
    > Para executar essa operação em uma linha de comando, execute `ipconfig /all` para ver o nome do adaptador e a configuração.

    ![Adicionar imagem dos contadores de desempenho](media/atp-traffic-estimation-7.png)

1. Altere o **Intervalo de amostragem** para **cinco segundos**.

1. Defina o local onde você deseja que os dados sejam salvos.

1. Em **Criar conjunto de coletores de dados**, selecione **Iniciar conjunto de coletores de dados agora** e clique em **Concluir**.

    Agora, você deverá ver o conjunto de coletores de dados criado com um triângulo verde, indicando que ele está funcionando.

1. Após 24 horas, pare o conjunto de coletores de dados clicando com o botão direito do mouse no conjunto de coletores de dados e selecionando **Parar**.

    ![Imagem ao parar o conjunto de coletores de dados](media/atp-traffic-estimation-12.png)

1. No Explorador de Arquivos, navegue até a pasta em que o arquivo .blg foi salvo e clique duas vezes nele para abri-lo no Monitor de Desempenho.

1. Selecione o contador Pacotes/s e registre os valores médio e máximo.

    ![Imagem do contador de pacotes por segundo](media/atp-traffic-estimation-14.png)

## <a name="next-steps"></a>Próximas etapas

Neste guia de início rápido, você determinou quantos sensores do ATP do Azure são necessários. Determinou também o dimensionamento dos sensores. Avance para o guia de início rápido seguinte para criar uma instância do ATP do Azure.

> [!div class="nextstepaction"]
> [Criar sua instância do ATP do Azure](install-step1.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://aka.ms/azureatpcommunity) hoje mesmo!
