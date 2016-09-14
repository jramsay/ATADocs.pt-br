---
title: "Guia de migração de atualização do ATA para 1.7 | Microsoft ATA"
description: "Procedimentos para atualizar o ATA para a versão 1.7"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 5c20c41c3fe587f18087d64f4f84c1df65072fde


---

# Guia de migração de atualização do ATA para 1.7
A atualização 1.7 do ATA fornece melhorias nas seguintes áreas:

-   Novas detecções

-   Aprimoramentos nas detecções existentes
  

## Atualizando o ATA para a versão 1.7
> [!NOTE] 
> Se o ATA não estiver instalado em seu ambiente, baixe a versão completa do ATA que inclui a versão 1.7 e siga o procedimento de instalação padrão descrito em [Instalar o ATA](/advanced-threat-analytics/deploy-use/install-ata).

Se você já tiver a versão 1.6 do ATA implantada, esse procedimento explicará as etapas necessárias para atualizar sua implantação.

> [!NOTE] 
> Você não pode instalar o ATA versão 1.7 diretamente sobre o ATA versão 1.4 ou 1.5. Instale primeiro o ATA versão 1.6. 

Execute estas etapas para atualizar para o ATA versão 1.7:

1.  [Baixe a atualização 1.7](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
Nessa versão, o mesmo arquivo de instalação (Microsoft ATA Center Setup.exe) é usado para instalar uma nova implantação do ATA e para atualizar as implantações existentes.

2.  Atualize o Centro do ATA

4.  Atualize os Gateways do ATA

    > [!IMPORTANT]
    > Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.

### Etapa 1: Atualizar o Centro do ATA

1.  Faça backup do seu banco de dados: (opcional)

    -   Se a Central de ATA estiver sendo executada como uma máquina virtual e você quiser fazer um ponto de verificação, desligue a máquina virtual primeiro.

    -   Se a Central de ATA estiver em execução em um servidor físico, siga o procedimento recomendado para [fazer backup do MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Execute o arquivo de instalação, **Microsoft ATA Center Setup.exe**, e siga as instruções na tela para instalar a atualização.

    -  Na página **Boas-vindas**, selecione seu idioma e clique em **Avançar**.

    -  Se você não tiver habilitado as atualizações automáticas na versão 1.6, será necessário definir o ATA para usar o Microsoft Update para ATA a fim de permanecer atualizado.  Na página do Microsoft Update, selecione **Usar o Microsoft Update ao verificar se há atualizações (recomendado)**.
    ![Imagem Manter o ATA atualizado](media/ata_ms_update.png) Isso ajusta as configurações do Windows para habilitar atualizações para os outros produtos da Microsoft (incluindo o ATA), como visto aqui. 
     ![Imagem de atualização automática do Windows](media/ata_installupdatesautomatically.png)

    -  Na tela **Migração de dados**, selecione se deseja migrar todos os dados ou dados parciais. Se você optar por migrar apenas os dados parciais, os perfis de comportamento e tráfego de rede capturados anteriormente não serão migrados. Isso significa que serão necessárias três semanas antes que a detecção de um comportamento anormal tenha um perfil completo para ativar a detecção de atividade anormal. Durante essas três semanas, todas as outras detecções do ATA funcionarão corretamente. A migração de dados **Parcial** demora muito menos para ser instalada. Se você selecionar a migração de dados **Completa**, pode demorar bastante para a instalação ser concluída. A quantidade estimada de tempo e de espaço em disco necessário, listada na tela **Migração de Dados**, dependerá da quantidade de tráfego de rede capturado anteriormente e já salvo em versões anteriores do ATA. Antes de selecionar **Parcial** ou **Completa**, verifique estes requisitos.  
    
    ![Migração de dados do ATA](media/migration data migration.png)

    -  Clique em **Atualizar**. Depois de clicar em Atualizar, o ATA ficará offline até que o procedimento de atualização seja concluído.

4.  Após a conclusão da atualização do Centro do ATA, clique em **Iniciar** para abrir a tela **Atualizar** no console do ATA para os Gateways do ATA.
    ![Tela de sucesso da atualização](media/migration center success.png)

5.  Na tela **Atualizações**, se você já tiver configurado seus Gateways do ATA para atualizarem automaticamente, eles serão atualizados agora, caso contrário, clique em **Atualizar** ao lado de cada Gateway do ATA.
  ![Imagem de atualização dos gateways](media/migration update gw.png)

  
> [!IMPORTANT] 
> Atualize todos os Gateways do ATA para ter certeza de o ATA funciona corretamente.
> A porta de escuta Syslog configurada em todos os Gateways será alterada para 514.
 
    > [!NOTE] 
    > To install new ATA Gateways, go the **Gateways** screen and click **Download Gateway Setup** to get the ATA 1.7 installation package and follow the instructions for new Gateway installation as described in [Step 4. Install the ATA Gateway](/advanced-threat-analytics/deploy-use/install-ata-step4) .



## Consulte também

- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->

