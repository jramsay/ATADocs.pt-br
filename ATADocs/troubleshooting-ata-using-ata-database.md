---
title: "Solução de problemas do Advanced Threat Analytics usando o banco de dados | Microsoft Docs"
description: "Descreve como você pode usar o banco de dados do ATA para solucionar problemas"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 112ee57f79b20b4e42b15c6fdc4566bbdcebe29f
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2017
---
*Aplica-se a: Advanced Threat Analytics versão 1.8*



<a id="troubleshooting-ata-using-the-ata-database" class="xliff"></a>

# Solução de problemas do ATA usando o banco de dados do ATA
O ATA usa o MongoDB como seu banco de dados.
Você pode interagir com o banco de dados usando a linha de comando padrão ou usando uma ferramenta de interface de usuário para executar tarefas avançadas e solucionar problemas.

<a id="interacting-with-the-database" class="xliff"></a>

## Interação com o banco de dados
O modo padrão, e mais básico, de consultar o banco de dados é usando o shell Mongo:

1.  Abra uma janela de linha de comando e altere o caminho até a pasta bin do MongoDB. O caminho padrão é: **C:\Arquivos de Programas\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**.

2.  Execute: `mongo.exe ATA`. Digite ATA com letras maiúsculas.

|Como...|Sintaxe|Anotações|
|-------------|----------|---------|
|Verifique se há coleções no banco de dados.|`show collections`|É útil como um teste completo para verificar se o tráfego está sendo gravado no banco de dados, e se o evento 4776 está sendo recebido pelo ATA.|
|Obter detalhes de um usuário/computador/grupo (UniqueEntity), como ID do usuário.|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|Encontre o tráfego de autenticação Kerberos proveniente de um computador específico em um dia específico.|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|Para obter a &lt;ID do computador de origem&gt;, consulte as coleções UniqueEntity, conforme mostrado no exemplo.<br /><br />Cada tipo de atividade de rede, por exemplo, autenticações Kerberos, possui sua própria coleção de acordo com a data UTC.|
|Encontre o tráfego de NTLM proveniente de um computador específico relacionado a uma conta específica em um dia específico.|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|Para obter a &lt;ID do computador de origem&gt; e a &lt;ID da conta&gt;, consulte as coleções UniqueEntity, conforme mostrado no exemplo.<br /><br />Cada tipo de atividade de rede, por exemplo, autenticações NTLM, possui sua própria coleção de acordo com a data UTC.|
|Pesquise propriedades avançadas, como as datas ativas de uma conta. |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|Para obter a &lt;ID da conta&gt;, consulte as coleções UniqueEntity, conforme mostrado no exemplo.<br>O nome da propriedade que mostra as datas nas quais a conta esteve ativa é chamado: "ActiveDates". Por exemplo, talvez você queira saber se uma conta tem pelo menos 21 dias de atividade para que o algoritmo de aprendizado de máquina de comportamento anormal possa ser executado.|
|Faça alterações de configuração avançadas. Neste exemplo, alteramos o tamanho da fila de envio para todos os Gateways do ATA para 10.000.|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

O exemplo a seguir fornece código de exemplo usando a sintaxe fornecida acima. Se você estiver investigando uma atividade suspeita que ocorreu em 20/10/2015 e quiser saber mais sobre as atividades de NTLM que "John Doe" realizou nesse dia:<br /><br />Primeiro, encontre a ID de "John Doe"

`db.UniqueEntity.find({Name: "John Doe"})`<br>Anote a respectiva ID conforme indicado pelo valor de `_id` Para nosso exemplo, digamos que a ID seja `123bdd24-b269-h6e1-9c72-7737as875351`<br>Depois, pesquise pela coleção com a data mais próxima e anterior à data que você está procurando, no caso de nosso exemplo, 20/10/2015.<br>Em seguida, procure por atividades de NTLM na conta de John Doe: 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

<a id="see-also" class="xliff"></a>

## Consulte também
- [Pré-requisitos do ATA](ata-prerequisites.md)
- [Planejamento da capacidade do ATA](ata-capacity-planning.md)
- [Configurar coleta de eventos](configure-event-collection.md)
- [Configuração do encaminhamento de eventos do Windows](configure-event-collection.md#configuring-windows-event-forwarding)
- [Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)