---
title: Atualização do Advanced Threat Analytics para o guia de migração 1,7
description: Procedimentos para atualizar o ATA para a versão 1.7
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8eefcd45-7a4b-4074-ac5b-1ffc48e6654a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4772e9cbb1e00e4bb1a4bebd5cc6e2b7821766dc
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90909885"
---
# <a name="ata-update-to-17-migration-guide"></a>Guia de migração de atualização do ATA para 1.7

[!INCLUDE [Rebranding notice](includes/rebranding.md)]
A atualização 1.7 do ATA fornece melhorias nas seguintes áreas:

- Novas detecções

- Aprimoramentos nas detecções existentes
  

## <a name="updating-ata-to-version-17"></a>Atualizando o ATA para a versão 1.7

> [!NOTE] 
> Se o ATA não estiver instalado em seu ambiente, baixe a versão completa do ATA, que inclui a versão 1,7 e siga o procedimento de instalação padrão descrito em [instalar o ATA](install-ata-step1.md).

Se você já tiver a versão 1.6 do ATA implantada, esse procedimento explicará as etapas necessárias para atualizar sua implantação.

> [!NOTE] 
> Você não pode instalar o ATA versão 1.7 diretamente sobre o ATA versão 1.4 ou 1.5. Instale primeiro o ATA versão 1.6. 

Execute estas etapas para atualizar para o ATA versão 1.7:

1.  [Baixar a atualização 1.7](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
Nessa versão, o mesmo arquivo de instalação (Microsoft ATA Center Setup.exe) é usado para instalar uma nova implantação do ATA e para atualizar as implantações existentes.

1. Atualize o Centro do ATA

1. Atualize os Gateways do ATA

    > [!IMPORTANT]
    > Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.

### <a name="step-1-update-the-ata-center"></a>Etapa 1: Atualizar o Centro do ATA

1. Faça backup do seu banco de dados: (opcional)

    - Se a Central de ATA estiver sendo executada como uma máquina virtual e você quiser fazer um ponto de verificação, desligue a máquina virtual primeiro.

    - Se o centro do ATA estiver em execução em um servidor físico, siga o procedimento recomendado para [fazer backup do MongoDB](https://docs.mongodb.org/manual/core/backups/).

1. Execute o arquivo de instalação, **Microsoft ATA Center Setup.exe**, e siga as instruções na tela para instalar a atualização.

    - Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

    - Se você não tiver habilitado as atualizações automáticas na versão 1.6, será necessário definir o ATA para usar o Microsoft Update para ATA a fim de permanecer atualizado.  Na página Microsoft Update, selecione **usar Microsoft Update quando eu verificar se há atualizações (recomendado)**.
    ![Imagem Manter o ATA atualizado](media/ata_ms_update.png) Isso ajustará as configurações do Windows para habilitar atualizações para os outros produtos da Microsoft (incluindo o ATA), como visto aqui. 
     ![Imagem de atualização automática do Windows](media/ata_installupdatesautomatically.png)

    - Na tela **Migração de dados**, selecione se deseja migrar todos os dados ou dados parciais. Se você optar por migrar apenas os dados parciais, os perfis de comportamento e tráfego de rede capturados anteriormente não serão migrados. Isso significa que são necessárias três semanas antes que a detecção de um comportamento anormal tenha um perfil completo para ativar a detecção de atividade anormal. Durante essas três semanas, todas as outras detecções do ATA funcionarão corretamente. A migração de dados **Parcial** demora muito menos para ser instalada. Se você selecionar a migração de dados **Completa**, pode demorar bastante para a instalação ser concluída. A quantidade estimada de tempo e de espaço em disco necessário, listada na tela **Migração de Dados**, dependerá da quantidade de tráfego de rede capturado anteriormente e já salvo em versões anteriores do ATA. Antes de selecionar **Parcial** ou **Completa**, verifique estes requisitos.  
    
    ![Migração de dados do ATA](media/migration-data-migration17.png)

    - Clique em **Atualizar**. Depois de clicar em Atualizar, o ATA ficará offline até que o procedimento de atualização seja concluído.

1. Após a conclusão da atualização do Centro do ATA, clique em **Iniciar** para abrir a tela **Atualizar** no console do ATA para os Gateways do ATA.
    ![Tela de atualização bem-sucedida](media/migration-center-success17.png)

1. Na tela **Atualizações**, se você já tiver configurado seus Gateways do ATA para atualizarem automaticamente, eles serão atualizados agora, caso contrário, clique em **Atualizar** ao lado de cada Gateway do ATA.
  ![Imagem de atualização dos gateways](media/migration-update-gw-17.png)

  
> [!IMPORTANT] 
> Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.
> A porta de escuta Syslog configurada em todos os Gateways será alterada para 514.
 
> [!NOTE] 
> Para instalar novos gateways do ATA, acesse a tela **gateways** e clique em **baixar a instalação do gateway** para obter o pacote de instalação do ATA 1,7 e siga as instruções para a nova instalação do gateway, conforme descrito na [etapa 4. Instale o gateway do ATA](install-ata-step4.md).



## <a name="see-also"></a>Consulte Também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
