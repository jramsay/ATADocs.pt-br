---
title: "Novidades na versão 1.8 do ATA | Microsoft Docs"
description: "Lista as novidades na nova versão 1.8 do ATA e seus problemas conhecidos"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 9592d413-df0e-4cec-8e03-be1ae00ba5dc
ms.reviewer: 
ms.suite: ems
ms.openlocfilehash: f2a4ed151db38497a6cec977f1090faf2eb4133e
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2017
---
<a id="whats-new-in-ata-version-18" class="xliff"></a>

# Novidades na versão 1.8 do ATA
Essas notas de versão fornecem informações sobre atualizações, novos recursos, correções de bug e problemas conhecidos nesta versão da Advanced Threat Analytics.



<a id="new--updated-detections" class="xliff"></a>

## Detecções novas e atualizadas

- A implementação de protocolo incomum foi aperfeiçoada para ser capaz de detectar malware WannaCry.

- NOVO! **Modificação anormal de grupos confidenciais** – Como parte da fase de elevação de privilégio, os invasores modificam grupos com altos privilégios para obter acesso a recursos confidenciais. Agora o ATA detecta quando há uma alteração anormal em um grupo com privilégios elevados.
- NOVO! **Falhas de autenticação suspeitas** (força bruta comportamental) – Os invasores tentam usar força bruta em credenciais para comprometer contas. Agora o ATA emite um alerta quando o comportamento de autenticação com falha anormal é detectado.   

- **Tentativa de execução remota – execução WMI** – Os invasores podem tentar controlar sua rede executando códigos remotamente em seu controlador de domínio. O ATA aprimorou a detecção de execução remota para incluir a detecção de métodos WMI para executar código remotamente.

- Reconhecimento usando consultas de serviço de diretório – Essa detecção foi aprimorada para poder capturar consultas em uma única entidade confidencial e reduzir o número de falsos positivos gerados na versão anterior. Se você tiver desabilitado isso na versão 1.7, instalar a versão 1.8 agora o habilitará automaticamente.

- Atividade Golden Ticket do Kerberos – O ATA 1.8 inclui uma técnica adicional para detectar ataques de golden ticket.
    - Agora, o ATA detecta atividades suspeitas em que o tempo de vida do golden ticket expirou. Se um tíquete Kerberos é usado por mais do que o tempo de vida permitido, o ATA detecta isso como uma atividade suspeita em que um Golden ticket provavelmente foi criado.
- Melhorias foram feitas nas seguintes detecções para remover falsos positivos conhecidos:  
    - Detecção de elevação de privilégios (PAC forjado) 
    - Atividade de downgrade de criptografia (Skeleton Key)
    - Implementação de protocolo incomum
    - Confiança quebrada

<a id="improved-triage-of-suspicious-activities" class="xliff"></a>

## Triagem de atividades suspeitas aprimorada

-   NOVO! O ATA 1.8 permite que você execute as seguintes atividades suspeitas durante o processo de triagem: 
    - **Excluir entidades** de gerar futuras atividades suspeitas para impedir que o ATA alerte quando detectar verdadeiros positivos benignos (como um administrador executando código remoto ou detectando scanners de segurança).
    - **Impedir que atividades suspeitas recorrentes** gerem alertas.
    - **Excluir atividades suspeitas** da linha do tempo de ataque.
-   O processo para acompanhar alertas de atividade suspeita agora é mais eficiente. A linha do tempo de atividades suspeitas foi redefinida. No ATA 1.8, você poderá ver muito mais atividades suspeitas em uma única tela, que contém as melhores informações para fins de triagem e investigação. 

<a id="new-reports-to-help-you-investigate" class="xliff"></a>

## Novos relatórios para ajudá-lo a investigar 
-   NOVO! O **relatório de resumo** foi adicionado para permitir que você veja todos os dados resumidos do ATA, incluindo atividades suspeitas, problemas de integridade e muito mais. Você pode até mesmo definir um relatório personalizado que é gerado automaticamente de forma recorrente.
-   NOVO! O **relatório de grupos confidenciais** foi adicionado para que você possa ver todas as alterações feitas em grupos confidenciais durante um certo período.


<a id="infrastructure-improvements" class="xliff"></a>

## Melhorias na infraestrutura

-   O desempenho do Centro do ATA foi aprimorado. No ATA 1.8 o Centro do ATA pode lidar com mais de um milhão de pacotes por segundo.
-   O Gateway Lightweight do ATA poderá ler eventos localmente, sem a necessidade de configurar o encaminhamento de eventos.
-   Incremento de acessibilidade – O ATA agora está de acordo com a Microsoft no fornecimento de um produto acessível para todos. 
-   Agora você pode configurar separadamente um email para alertas de monitoramento e para atividades suspeitas.

<a id="security-improvements" class="xliff"></a>

## Aprimoramentos de segurança

-   NOVO! **Logon único para o gerenciamento do ATA**. O ATA dá suporte ao logon único integrado com a autenticação do Windows – se você já fez logon em seu computador, o ATA usará esse token para fazer o logon no Console do ATA. Você também pode fazer logon usando um cartão inteligente. Scripts de instalação silenciosa para o Gateway de ATA e para o Gateway Lightweight do ATA agora usam o contexto do usuário conectado, sem a necessidade de fornecer credenciais.
-   Os privilégios do sistema local foram removidos do processo do Gateway do ATA, portanto, agora você pode usar contas virtuais (disponíveis apenas em Gateways do ATA autônomos), contas de serviço gerenciadas e contas de serviço gerenciado de grupo para executar o processo do Gateway do ATA.   
-   Foram adicionados logs de auditoria para o Centro do ATA e para os Gateways do ATA e todas as ações agora podem ser registradas no Log de Eventos do Windows.
-   Foi adicionado suporte para certificados KSP para o Centro do ATA.




<a id="see-also" class="xliff"></a>

## Consulte também
[Confira o fórum do ATA!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[Atualizar o ATA para a versão 1.8 — guia de migração](ata-update-1.8-migration-guide.md)
