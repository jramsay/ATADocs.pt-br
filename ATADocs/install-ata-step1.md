---
title: "Instalação do Advanced Threat Analytics – Etapa 1 | Microsoft Docs"
description: "A primeira etapa da instalação do ATA envolve baixar e instalar o Centro do ATA em seu servidor escolhido."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 97fa1522ca43cf92416ac845b8886f2905e9981b
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*


<a id="install-ata---step-1" class="xliff"></a>

# Instalação do ATA - Etapa 1

>[!div class="step-by-step"]
[Etapa 2 »](install-ata-step2.md)

O procedimento de instalação fornece instruções para executar uma nova instalação do ATA 1.8. Para saber mais sobre como atualizar uma implantação do ATA existente de uma versão anterior, confira [o guia de migração do ATA versão 1.8](ata-update-1.8-migration-guide.md).

> [!IMPORTANT] 
> Se você estiver usando o Windows 2012 R2, instale o KB2934520 no servidor da Central do ATA e nos servidores do Gateway do ATA antes de começar a instalação, caso contrário a instalação do ATA instalar essa atualização e exigirá uma reinicialização no meio do processo.

<a id="step-1-download-and-install-the-ata-center" class="xliff"></a>

## Etapa 1. Baixar e instalar o Centro do ATA
Depois de verificar que o servidor atende aos requisitos, você pode prosseguir com a instalação do Centro do ATA.
    
> [!NOTE]
>Se você tiver adquirido uma licença para EMS (Enterprise Mobility + Security) diretamente pelo portal do Office 365 ou pelo modelo de licenciamento CSP (Parceiro de Solução de Nuvem) e não tiver acesso ao ATA pelo VLSC (Centro de Licenciamento por Volume da Microsoft), entre em contato com o Atendimento ao Cliente Microsoft para obter o processo para ativar o ATA (Advanced Threat Analytics).

Execute as seguintes etapas no servidor do Centro do ATA.

1.  Baixe o ATA no [Centro de Serviços de Licenciamento por Volume da Microsoft](https://www.microsoft.com/Licensing/servicecenter/default.aspx), no [Centro de avaliação do TechNet](http://www.microsoft.com/evalcenter/) ou no [MSDN](https://msdn.microsoft.com/subscriptions/downloads).

2.  Entre no computador no qual você está instalando o Centro do ATA como um usuário que seja membro do grupo Administradores local.

3.  Execute **Microsoft ATA Center Setup.EXE** e siga o assistente de instalação.

> [!NOTE]   
> Certifique-se de executar o arquivo de instalação de uma unidade local e não de um arquivo ISO montado para evitar problemas, caso uma reinicialização seja necessária como parte da instalação.   

4.  Se o Microsoft .NET Framework não estiver instalado, você precisará instalá-lo ao iniciar a instalação. Você pode ter que reinicializar após a instalação do .NET Framework.
5.  Na página de **Boas-vindas**, selecione o idioma a ser usado nas telas de instalação do ATA e clique em **Avançar**.

6.  Leia os Termos de Licença para Software Microsoft e, se aceitá-los, clique na caixa de seleção e em **Avançar**.

7.  É recomendável que você defina o ATA para atualizar automaticamente. Se o Windows não estiver configurado para fazer isso no seu computador, você verá a tela **Utilizar o Microsoft Update para ajudar a manter seu computador protegido e atualizado**. 
    ![Imagem Manter o ATA atualizado](media/ata_ms_update.png)

8. Selecione **Usar o Microsoft Update ao verificar atualizações (recomendado)** Isso ajustará as configurações do Windows para habilitar atualizações para outros produtos da Microsoft (incluindo o ATA), como visto aqui. 

    ![Imagem de atualização automática do Windows](media/ata_installupdatesautomatically.png)

8.  Na página **Configure the Center (Configurar o Centro)** insira as informações a seguir com base em seu ambiente:

    |Campo|Descrição|Comentários|
    |---------|---------------|------------|
    |Caminho da Instalação|Esse é o local onde o Centro do ATA será instalado. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center|Mantenha o valor padrão|
    |Caminho de Dados do Banco de Dados|Esse é o local onde os arquivos de banco de dados do MongoDB estarão localizados. Por padrão, é %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|Altere o local para um local onde você tem espaço para crescer com base em seu tamanho. **Observação:** <ul><li>Em ambientes de produção, você deve usar uma unidade que tenha espaço suficiente com base em um planejamento de capacidade.</li><li>Para implantações de grande porte, o banco de dados deve estar em um disco físico separado.</li></ul>Confira [Planejamento de capacidade do ATA](ata-capacity-planning.md) para obter informações sobre dimensionamento.|
    |Certificado SSL do Serviço da Central|Esse é o certificado que será usado pelo serviço da Central do ATA e pelo Console do ATA.|Clique no ícone de chave para selecionar um certificado instalado ou verificar o certificado autoassinado durante a implantação em um ambiente de laboratório. Observe que você tem a opção de criar um certificado autoassinado.|
        
    ![Imagem de configuração do Centro do ATA](media/ATA-Center-Configuration.png)

10.  Clique em **Instalar** para instalar o Centro do ATA e seus componentes.
    Os seguintes componentes serão instalados e configurados durante a instalação do Centro do ATA:

    -   Serviço da Central do ATA

    -   MongoDB

    -   Conjunto de coleta de dados do Monitor de Desempenho Personalizado

    -   Certificados autoassinados (se tiver sido selecionado durante a instalação)

11.  Quando a instalação for concluída, clique em **Iniciar** para abrir o Console do ATA e conclua a instalação na página **Configuração**.
Neste ponto, você será levado automaticamente para a página de configuração **Geral** a fim de continuar a configuração e a implantação dos Gateways do ATA.
Como você está fazendo logon no site usando um endereço IP, você recebe um aviso relacionado ao certificado e isso é normal. Clique em **Continuar neste site**.

<a id="validate-installation" class="xliff"></a>

### Validar a instalação

1.  Verifique se o serviço chamado **Central do Microsoft Advanced Threat Analytics** está em execução.
2.  Na área de trabalho, clique no atalho do **Microsoft Advanced Threat Analytics** para se conectar ao Console do ATA. Faça logon com as mesmas credenciais de usuário que você usou para instalar o Centro do ATA.



>[!div class="step-by-step"]
[« Pré-instalação](configure-port-mirroring.md)
[Etapa 2 »](install-ata-step2.md)

<a id="see-also" class="xliff"></a>

## Consulte Também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Pré-requisitos do ATA](ata-prerequisites.md)
