---
title: Atualização do Advanced Threat Analytics para o guia de migração 1,8
description: Procedimentos para atualizar o ATA para a versão 1.8
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/20/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e5a9718c-b22e-41f7-a614-f00fc4997682
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ed745c16bebff4eb8845cfe0ea834645f909ee1f
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911081"
---
# <a name="updating-ata-to-version-18"></a>Atualizando o ATA para a versão 1.8

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE] 
> Se o ATA não estiver instalado em seu ambiente, baixe a versão completa do ATA, que inclui a versão 1,8 e siga o procedimento de instalação padrão descrito em [instalar o ATA](install-ata-step1.md).

Se você já tiver a versão 1.7 do ATA implantada, esse procedimento explicará as etapas necessárias para atualizar sua implantação.

> [!NOTE] 
>  Somente o ATA versão 1.7 atualização 1 e 1.7 atualização 2 podem ser atualizados para a versão 1.8 do ATA, qualquer versão anterior do ATA não pode ser atualizada diretamente para a versão 1.8.

Siga essas etapas para atualizar para o ATA versão 1.8:

1.  [Baixe a versão de atualização do ATA 1.8 do Centro de Download](https://www.microsoft.com/download/details.aspx?id=55536) ou a versão completa do [Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
Na versão de migração, o arquivo pode ser usado apenas para a atualização do ATA 1.7. Na versão do Centro de Avaliação, o mesmo arquivo de instalação (Microsoft ATA Center Setup.exe) é usado para instalar uma nova implantação do ATA e para atualizar as implantações existentes.

1. Atualize o Centro do ATA

1. Atualize os Gateways do ATA

    > [!IMPORTANT]
    > Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.

### <a name="step-1-update-the-ata-center"></a>Etapa 1: Atualizar o Centro do ATA

1. Faça backup do seu banco de dados: (opcional)

   - Se a Central de ATA estiver sendo executada como uma máquina virtual e você quiser fazer um ponto de verificação, desligue a máquina virtual primeiro.

   - Se o Centro do ATA estiver em execução em um servidor físico, consulte o artigo sobre [recuperação de desastre](disaster-recovery.md) para obter informações sobre como fazer backup do banco de dados.

1. Execute o arquivo de instalação, **Microsoft ATA Center Setup.exe**, e siga as instruções na tela para instalar a atualização.

   - Na página **Boas-vindas**, escolha seu idioma e clique em **Avançar**.

   - Se você não tiver habilitado as atualizações automáticas na versão 1.7, será necessário definir o ATA para usar o Microsoft Update para ATA a fim de permanecer atualizado.  Na página Microsoft Update, selecione **usar Microsoft Update quando eu verificar se há atualizações (recomendado)**.
     ![Imagem Manter o ATA atualizado](media/ata_ms_update.png)
     
     Isso ajusta as configurações do Windows para habilitar as atualizações para o ATA. 
    
   - Na tela **Migração de dados**, selecione se deseja migrar todos os dados ou dados parciais. Se você optar por migrar apenas os dados parciais, todas as detecções funcionarão imediatamente com a exceção da detecção de comportamento anormal, que demora três semanas para criar um perfil completo.  
    
   A migração de dados **Parcial** demora muito menos para ser instalada. Se você selecionar a migração de dados **Completa**, pode demorar bastante para a instalação ser concluída. Certifique-se de examinar a quantidade estimada de tempo e de espaço em disco necessário, que são listadas na tela **Migração de Dados**. Esses números dependem da quantidade de tráfego de rede capturada anteriormente que você salvou nas versões anteriores do ATA. Por exemplo, na tela abaixo, você pode ver uma migração de dados de um banco de dados grande:
         
    ![Migração de dados do ATA](media/migration-data-migration.png)

   - Clique em **Atualizar**. Depois de clicar em Atualizar, o ATA ficará offline até que o procedimento de atualização seja concluído.

1. Após a conclusão da atualização do Centro do ATA, clique em **Iniciar** para abrir a tela **Atualizar** no console do ATA para os Gateways do ATA.

    ![Tela de sucesso da atualização](media/migration-center-success.png)

1. Na tela **Atualizações**, se você já tiver configurado seus Gateways do ATA para atualizarem automaticamente, eles serão atualizados agora, caso contrário, clique em **Atualizar** ao lado de cada Gateway do ATA.
  
![Imagem de atualização dos gateways](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.
 
> [!NOTE] 
> Para instalar novos gateways do ATA, acesse a tela **gateways** e clique em **baixar a instalação do gateway** para obter o pacote de instalação do gateway 1,8 do ATA e siga as instruções para nova instalação do gateway, conforme descrito na [etapa 4. Instale o gateway do ATA](install-ata-step4.md).


## <a name="see-also"></a>Consulte Também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
