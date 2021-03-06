---
title: Instalar o Advanced Threat Analytics – etapa 1
description: A primeira etapa da instalação do ATA envolve baixar e instalar o Centro do ATA em seu servidor escolhido.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/07/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3e50a48c6ffb108bee7c5b760a0368b04e3f0c61
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911511"
---
# <a name="install-ata---step-1"></a>Instalação do ATA - Etapa 1

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
> [!div class="step-by-step"]
> [Etapa 2»](install-ata-step2.md)

O procedimento de instalação fornece instruções para executar uma nova instalação do ATA 1.9. Para obter mais informações sobre como atualizar uma implantação existente do ATA de uma versão anterior, veja [o guia de migração do ATA para a versão 1.9](ata-update-1.9-migration-guide.md).

> [!IMPORTANT]
> Se você estiver usando o Windows 2012 R2, instale o KB2934520 no servidor da Central do ATA e nos servidores do Gateway do ATA antes de começar a instalação, caso contrário a instalação do ATA instalar essa atualização e exigirá uma reinicialização no meio do processo.

## <a name="step-1-download-and-install-the-ata-center"></a>Etapa 1. Baixar e instalar o Centro do ATA

Depois de verificar que o servidor atende aos requisitos, você pode prosseguir com a instalação do Centro do ATA.

> [!NOTE]
> Se você adquiriu uma licença para o Enterprise Mobility + Security (EMS) diretamente pelo portal Microsoft 365 ou por meio do modelo de licença do CSP(Cloud Solution Partner) e não tiver acesso ao ATA por meio do Microsoft VLSC (Volume Licensing Center), entre em contato com o atendimento ao cliente da Microsoft para obter o processo para ativar o ATA (Advanced Threat Analytics).

Execute as seguintes etapas no servidor do Centro do ATA.

1. Baixe o ATA no [centro de serviços de licenciamento por volume da Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx) ou no [centro de avaliação TechNet](https://www.microsoft.com/evalcenter/) ou no [msdn](/powerapps/developer/common-data-service/org-service/subscribe-sdk-assembly-updates-using-nuget).

1. Entre no computador no qual você está instalando o Centro do ATA como um usuário que seja membro do grupo Administradores local.

1. Execute **Microsoft ATA Center Setup.EXE** e siga o assistente de instalação.

    > [!NOTE]
    > Certifique-se de executar o arquivo de instalação de uma unidade local e não de um arquivo ISO montado para evitar problemas, caso uma reinicialização seja necessária como parte da instalação.

1. Se o Microsoft .NET Framework não estiver instalado, você será solicitado a instalá-lo quando iniciar a instalação. Você pode ter que reinicializar após a instalação do .NET Framework.
1. Na página de **boas-vindas** , selecione o idioma a ser usado nas telas de instalação do ATA e clique em **Avançar**.

1. Leia os Termos de Licença para Software Microsoft e, depois de aceitá-los, clique na caixa de seleção para aceitar e em **Avançar**.

1. Recomendamos configurar o ATA para atualizar automaticamente. Se a atualização automática do Windows em seu computador não estiver configurada para isso, você verá a tela **Utilizar o Microsoft Update para ajudar a manter seu computador protegido e atualizado**.
    ![Imagem Manter o ATA atualizado](media/ata_ms_update.png)

1. Selecione **Usar o Microsoft Update ao verificar atualizações (recomendado)** Isso ajusta as configurações do Windows para habilitar atualizações para outros produtos da Microsoft (incluindo o ATA).

    ![Imagem de atualização automática do Windows](media/ata_installupdatesautomatically.png)

1. Na página **Configure the Center (Configurar o Centro)** insira as informações a seguir com base em seu ambiente:

    |Campo|Descrição|Comentários|
    |---------|---------------|------------|
    |Caminho da Instalação|Esse é o local onde o Centro do ATA será instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center|Deixe o valor padrão|
    |Caminho de Dados do Banco de Dados|Esse é o local onde os arquivos de banco de dados do MongoDB estão localizados. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Altere o local para um local onde você tem espaço para crescer com base em seu tamanho. **Observação**: <ul><li>Em ambientes de produção, você deve usar uma unidade que tenha espaço suficiente com base em um planejamento de capacidade.</li><li>Para implantações de grande porte, o banco de dados deve estar em um disco físico separado.</li></ul>Confira [Planejamento de capacidade do ATA](ata-capacity-planning.md) para obter informações sobre dimensionamento.|
    |Certificado SSL do Serviço da Central|Esse é o certificado usado pelo serviço do Centro do ATA e pelo Console do ATA.|Clique no ícone de chave para selecionar um certificado instalado ou use a caixa de seleção para criar um certificado autoassinado.|

    ![Imagem de configuração do Centro do ATA](media/ATA-Center-Configuration.png)

    > [!NOTE]
    > Certifique-se de prestar atenção aos alertas de integridade referentes aos avisos de status e expiração do certificado SSL do serviço Center. Se o certificado expirar, você precisará reimplantar completamente o ATA.

1. Clique em **Instalar** para instalar o Centro do ATA e seus componentes.  
Os seguintes componentes serão instalados e configurados durante a instalação do Centro do ATA:

    - Serviço da Central do ATA

    - MongoDB

    - Conjunto de coleta de dados do Monitor de Desempenho Personalizado

    - Certificados autoassinados (se tiver sido selecionado durante a instalação)

1. Ao concluir a instalação, clique em **Iniciar** para abrir o Console do ATA e conclua a instalação na página **Configuração**.
    A página de configuração **Geral** abre automaticamente a fim de continuar a configuração e a implantação dos Gateways do ATA.
    Como você está fazendo logon no site usando um endereço IP, você recebe um aviso relacionado ao certificado e isso é normal. Clique em **Continuar neste site**.

### <a name="validate-installation"></a>Validar a instalação

1. Verifique se o serviço **Central do Microsoft Advanced Threat Analytics** está em execução.
1. Na área de trabalho, clique no atalho do **Microsoft Advanced Threat Analytics** para conectar-se ao console do ATA. Faça logon com as credenciais de usuário que você usou para instalar o ATA Center.

### <a name="set-anti-virus-exclusions"></a>Definir as exclusões de antivírus

Depois de instalar o ATA Center, exclua o diretório de banco de dados do MongoDB da análise contínua realizada pelo seu aplicativo de antivírus. A localização padrão no banco de dados é: **C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data**.

Exclua as pastas e os processos a seguir da verificação do AV:

**Pastas**  
C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\ParentKerberosAsBloomFilters  
C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\ParentKerberosTgsBloomFilters  
C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Backup  
C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\Logs

**Processos**  
mongod.exe  
Microsoft.Tri.Center.exe

Se você instalou o ATA em um diretório diferente, não deixe de alterar os caminhos de pasta de acordo com a sua instalação.

> [!div class="step-by-step"]
> [«Pré-instalação](configure-port-mirroring.md) 
>  [Etapa 2»](install-ata-step2.md)

## <a name="related-videos"></a>Vídeos Relacionados

- [Como escolher o tipo certo de Gateway do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)
- [Visão geral da implantação do ATA](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)

## <a name="see-also"></a>Consulte Também

- [Guia de implantação da POC (prova de conceito) do ATA](https://aka.ms/atapoc)
- [Ferramenta de dimensionamento do ATA](https://aka.ms/atasizingtool)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)