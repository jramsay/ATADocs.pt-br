---
title: Alertas de segurança de movimento lateral do ATP do Azure
description: Este artigo explica os alertas do ATP do Azure emitidos quando são detectados ataques contra a sua organização, que normalmente fazem parte dos esforços da fase de movimento lateral.
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/31/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 570bf2565ca42e7262c62f26eb368874f7d5394d
ms.sourcegitcommit: e7897436d71e253cf583ec566eca3daa9ba3cae9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2020
ms.locfileid: "91942413"
---
# <a name="tutorial-lateral-movement-alerts"></a>Tutorial: Alertas de movimento lateral

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Normalmente, os ataques cibernéticos são lançados contra alguma entidade acessível, como um usuário com poucos privilégios e, em seguida, se movem lateralmente com rapidez até que o invasor obtenha acesso a ativos valiosos. Os ativos valiosos podem ser contas confidenciais, administradores de domínio ou dados altamente confidenciais. O ATP do Azure identifica essas ameaças avançadas na origem ao longo de toda a cadeia de ataque e classifica-as nas seguintes fases:

1. [Reconhecimento](reconnaissance-alerts.md)
1. [Credenciais comprometidas](compromised-credentials-alerts.md)
1. **Movimentos laterais**
1. [Comprometimento de domínio](domain-dominance-alerts.md)
1. [Exportação](exfiltration-alerts.md)

Para entender melhor a estrutura e os componentes comuns de todos os alertas de segurança do ATP do Azure, confira [Understanding security alerts](understanding-security-alerts.md) (Entendendo os alertas de segurança). Para obter informações sobre **TP (verdadeiro positivo)** , **B-TP (verdadeiro positivo benigno)** e **FP (falso positivo)** , confira as [classificações de alertas de segurança](understanding-security-alerts.md#security-alert-classifications).

Os alertas de segurança a seguir ajudam a identificar e corrigir atividades suspeitas da fase de **Movimento lateral** detectadas pelo ATP do Azure em sua rede. Neste tutorial, você aprenderá como entender, classificar, corrigir e impedir os seguintes tipos de ataques:

> [!div class="checklist"]
>
> - Execução remota de código sobre DNS (ID 2036 externa)
> - Suspeita de roubo de identidade (Pass-the-Hash) (ID 2017 externa)
> - Suspeita de roubo de identidade (Pass-the-Ticket) (ID 2018 externa)
> - Suspeita de violação da autenticação NTLM (ID externa 2039)
> - Suspeita de ataque de retransmissão de NTLM (conta do Exchange) (ID 2037 externa)
> - Suspeita de ataque de Overpass-the-Hash (Kerberos) (ID 2002 externa)
> - Uso suspeito de certificado Kerberos invasor (ID externa 2047)
> - Suspeita de manipulação de pacote SMB (exploração de CVE-2020-0796) – (versão prévia) (ID 2406 externa)

<!-- * Suspected overpass-the-hash attack (encryption downgrade) (external ID 2008)-->

## <a name="remote-code-execution-over-dns-external-id-2036"></a>Execução remota de código sobre DNS (ID 2036 externa)

**Descrição**

Em 11/12/2018, a Microsoft publicou o anúncio [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) sobre uma vulnerabilidade de execução remota de código recém-descoberta que existe nos servidores de DNS (Sistema de Nomes de Domínio) do Windows. Nessa vulnerabilidade, os servidores falham em lidar adequadamente com solicitações. Um invasor que explorar com êxito essa vulnerabilidade poderá executar código arbitrário no contexto da Conta do Sistema Local. Servidores Windows configurados atualmente como servidores DNS estão em risco com essa vulnerabilidade.

Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando as consultas DNS suspeitas de explorar a vulnerabilidade de segurança CVE-2018-8626 são feitas em um controlador de domínio na rede.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP**

1. Os computadores de destino estão atualizados e corrigidos em relação a CVE-2018-8626?
    - Se os computadores estiverem atualizados e com as correções, **Feche** o alerta de segurança como uma atividade **FP**.
1. Foi um serviço criado ou um processo desconhecido executado no momento do ataque
    - Se nenhum novo serviço ou processo desconhecido for encontrado, opte por **Fechar** o alerta de segurança como um **FP**.
1. Esse tipo de ataque pode travar o serviço DNS antes de causar a execução do código com êxito.
    - Verifique se o serviço DNS foi reiniciado algumas vezes em torno do momento do ataque.
    - Se o DNS foi reiniciado, provavelmente foi uma tentativa de explorar a CVE-2018-8626. Considere este alerta um **TP** e siga as instruções em **Entender o escopo da violação**.

**Entender o escopo da violação**

- Investigue os [computadores de origem e de destino](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

**Remediação**

1. Conter os controladores de domínio.
    1. Corrija a tentativa de execução remota de código.
    1. Procure usuários que estavam conectados no mesmo período da atividade suspeita, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Contenha o computador de origem.
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    1. Procure usuários que estavam conectados no mesmo período da atividade suspeita, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

**Prevenção**

- Verifique se todos os servidores DNS no ambiente estão atualizados e corrigidos em relação a [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626).

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>Suspeita de roubo de identidade (Pass-the-Hash) (ID 2017 externa)

*Nome anterior:* Roubo de identidade usando o ataque de passagem de Hash

**Descrição**

Pass-the-Hash é uma técnica de movimento lateral em que os invasores roubam o hash NTLM de um usuário de um computador e o usam para acessar outro computador.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP?**
1. Determine se o hash foi usado dos computadores que o usuário está usando regularmente.
    - Se o hash foi usado dos computadores usados regularmente, **feche** o alerta como um **FP**.

**Entender o escopo da violação**

1. Investigue os [computadores de origem e destino](investigate-a-computer.md) ainda mais.
1. Investigue o [usuário comprometido](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Contêm os computadores de origem e de destino.
1. Encontre a ferramenta que realizou o ataque e remova-a.
1. Procure usuários que estavam conectados no mesmo período da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>Suspeita de roubo de identidade (Pass-the-Ticket) (ID 2018 externa)

*Nome anterior:* Roubo de identidade usando o ataque Pass-the-Ticket

**Descrição**

Pass-the-Ticket é uma técnica de movimento lateral em que os invasores roubam um tíquete Kerberos de um computador e o usam para acessar outro computador reutilizando o tíquete roubado. Nessa detecção, um tíquete Kerberos é visto sendo usado em dois (ou mais) computadores diferentes.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP?**

A resolução bem-sucedida de IPs nos computadores da organização é fundamental para identificar ataques Pass-the-Ticket de um computador para outro.

1. Verifique se o endereço IP de um ou ambos os computadores pertence a uma sub-rede alocada de um pool de DHCP subdimensionado, por exemplo, VPN, WiFi ou VDI.
1. O endereço IP é compartilhado (por exemplo, por um dispositivo NAT)?
1. O sensor não está resolvendo um ou mais dos endereços IP de destino? Se um endereço IP de destino não for resolvido, isso poderá indicar que as portas certas entre os dispositivos e o sensor não estão abertas corretamente.

    Se a resposta a uma das perguntas anteriores for **sim**, verifique se os computadores de origem e de destinos são os mesmos. Se eles forem o mesmo, esse será um **FP** e indicando que não houve nenhuma tentativa real de **Pass-the-Ticket**.

O recurso [Remote Credential Guard](/windows/security/identity-protection/remote-credential-guard) de conexões de RDP, quando usado com o Windows 10 no Windows Server 2016 e mais recentes, pode causar alertas **B-TP**.
Usando a evidência de alerta, verifique se o usuário fez uma conexão de área de trabalho remota do computador de origem para o computador de destino.

1. Verifique se há alguma evidência de correlação.
1. Se houver evidência de correlação, verifique se a conexão de RDP foi feita usando o Remote Credential Guard.
1. Se a resposta for sim, **feche** o alerta de segurança como uma atividade **T-BP**.

Há aplicativos personalizados que encaminham tíquetes em nome de usuários. Esses aplicativos têm direitos de delegação para tíquetes de usuário.

1. No momento, há um tipo de aplicativo personalizado, como aquele descrito anteriormente, nos computadores de destino? Quais serviços o aplicativo está executando? Os serviços estão atuando em nome de usuários, por exemplo, acessando bancos de dados?
    - Se a resposta for sim, **feche** o alerta de segurança como uma atividade **T-BP**.
1. O computador de destino é um servidor de delegação?
    - Se a resposta for sim, **feche** o alerta de segurança e exclua esse computador como uma atividade **T-BP**.

**Entender o escopo da violação**

1. Investigue os [computadores de origem e de destino](investigate-a-computer.md).
1. Investigue o [usuário comprometido](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Contêm os computadores de origem e de destino.
1. Encontre a ferramenta que realizou o ataque e remova-a.
1. Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Se o Microsoft Defender ATP estiver instalado – use **klist.exe purge** para excluir todos os tíquetes da sessão de logon especificada e evitar o uso dos tíquetes no futuro.

## <a name="suspected-ntlm-authentication-tampering-external-id-2039"></a>Suspeita de violação da autenticação NTLM (ID externa 2039)

Em junho de 2019, a Microsoft publicou a [Vulnerabilidade de Segurança CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040), anunciando a descoberta de uma nova vulnerabilidade de violação no Microsoft Windows, quando um ataque man-in-the-middle é capaz de ignorar com êxito a proteção de MIC (verificação de integridade da mensagem) do NTLM.

Os atores mal-intencionados que exploram com êxito essa vulnerabilidade têm a capacidade de fazer downgrade dos recursos de segurança do NTLM e podem criar sessões autenticadas com êxito em nome de outras contas. Os Windows Servers sem patch estão em risco devido a essa vulnerabilidade.

Nessa detecção, um alerta de segurança do ATP do Azure é disparado quando solicitações de autenticação do NTLM suspeitas de explorar a vulnerabilidade de segurança [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) são feitas em um controlador de domínio na rede.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP?**

1. Os computadores envolvidos, incluindo os controladores de domínio, estão atualizados e corrigidos em relação a [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040)?
    - Se os computadores estão atualizados e corrigidos, esperamos que a autenticação falhe. Se a autenticação falhou, **feche** o alerta de segurança como uma tentativa com falha.

**Entender o escopo da violação**

1. Investigue os [computadores de origem](investigate-a-computer.md).
1. Investigue a [conta de origem](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

**Remediação**

1. Conter os computadores de origem
1. Encontre a ferramenta que realizou o ataque e remova-a.
1. Procure por usuários que estavam conectados em horário próximo ao que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Force o uso do NTLMv2 selado no domínio, usando a política de grupo **Segurança de rede: nível de autenticação do LAN Manager**. Para obter mais informações, consulte as [Instruções de nível de autenticação do LAN Manager](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) para definir a política de grupo para controladores de domínio.

**Prevenção**

- Verifique se todos os dispositivos no ambiente estão atualizados e corrigidos em relação à [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040).

## <a name="suspected-ntlm-relay-attack-exchange-account-external-id-2037"></a>Suspeita de ataque de retransmissão de NTLM (conta do Exchange) (ID 2037 externa)

**Descrição**

Um Exchange Server pode ser configurado para disparar a autenticação de NTLM com a conta do Exchange Server para um servidor remoto http executado por um invasor. O servidor aguarda a comunicação do Exchange Server para retransmitir a própria autenticação confidencial para qualquer outro servidor, ou ainda mais interessante, para o Active Directory por LDAP, e captura as informações de autenticação.

Depois que o servidor de retransmissão recebe a autenticação NTLM, ele fornece um desafio que foi originalmente criado pelo servidor de destino. O cliente responde ao desafio, impedindo que um invasor obtenha a resposta e a use para continuar a negociação de NTLM com o controlador de domínio de destino.

Nessa detecção, um alerta é disparado quando o ATP do Azure identifica o uso das credenciais de conta do Exchange de uma fonte suspeita.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP?**

1. Verifique os computadores de origem por trás dos endereços IP.
    1. Se o computador de origem for um Exchange Server, **feche** o alerta de segurança como uma atividade de **FP**.
    1. Determinar se a conta de origem deve autenticar usando NTLM desses computadores? Se ela precisar se autenticar, **feche** o alerta de segurança e exclua esses computadores como uma atividade **B-TP**.

**Entender o escopo da violação**

1. Continue [investigando os computadores de origem](investigate-a-computer.md) por trás dos endereços IP envolvidos.
1. Investigue a [conta de origem](investigate-a-user.md).

**Correção sugerida e etapas de prevenção**

1. Conter os computadores de origem
    1. Encontre a ferramenta que realizou o ataque e remova-a.
    1. Procure por usuários que estavam conectados em horário próximo ao que a atividade ocorreu, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Force o uso do NTLMv2 selado no domínio, usando a política de grupo **Segurança de rede: nível de autenticação do LAN Manager**. Para obter mais informações, consulte as [Instruções de nível de autenticação do LAN Manager](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level) para definir a política de grupo para controladores de domínio.

<!--
## Suspected overpass-the-hash attack (encryption downgrade) (external ID 2008)

*Previous name:* Encryption downgrade activity

**Description**

Encryption downgrade is a method of weakening Kerberos using encryption downgrade of different fields of the protocol, normally encrypted using the highest levels of encryption. A weakened encrypted field can be an easier target to offline brute force attempts. Various attack methods utilize weak Kerberos encryption cyphers. In this detection, Azure ATP learns the Kerberos encryption types used by computers and users, and alerts you when a weaker cypher is used that is unusual for the source computer, and/or user, and matches known attack techniques.

In an over-pass-the-hash attack, an attacker can use a weak stolen hash to create a strong ticket, with a Kerberos AS request. In this detection,  instances are detected where the AS_REQ message encryption type from the source computer is downgraded, when compared to the previously learned behavior (the computer used AES).

**Learning period**

Not applicable

**TP, B-TP, or FP?**

1. Determine if the smartcard configuration recently changed.
    - Did the accounts involved recently have smartcard configurations changes?

      If the answer is yes, **Close** the security alert as a **T-BP** activity.

Some legitimate resources don't support strong encryption ciphers and may trigger this alert.

1. Do all source users share something?
    1. For example, are all of your marketing personnel accessing a specific resource that could cause the alert to be triggered?
    1. Check the resources accessed by those tickets.
       - Check this in Active Directory by checking the attribute *msDS-SupportedEncryptionTypes*, of the resource service account.
    1. If there is only one accessed resource, check if it is a valid resource for these users to access.

      If the answer to one of the previous questions is **yes**, it is likely to be a **T-BP** activity. Check if the resource can support a strong encryption cipher, implement a stronger encryption cipher where possible, and **Close** the security alert.

**Understand the scope of the breach**

1. Investigate the [source computer](investigate-a-computer.md).
1. Investigate the [compromised user](investigate-a-computer.md).

**Suggested remediation and steps for prevention**

**Remediation**

1. Reset the password of the source user and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.
1. Contain the source computer.
1. Find the tool that performed the attack and remove it.
1. Look for users logged on around the time of the activity, as they may also be compromised. Reset their passwords and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.

**Prevention**

1. Configure your domain to support strong encryption cyphers, and remove *Use Kerberos DES encryption types*. Learn more about [encryption types and Kerberos](/archive/blogs/openspecification/windows-configurations-for-kerberos-supported-encryption-type).
1. Make sure the domain functional level is set to support strong encryption cyphers.
1. Give preference to using applications that support strong encryption cyphers.
-->

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>Suspeita de ataque de Overpass-the-Hash (Kerberos) (ID 2002 externa)

*Nome anterior:* Implementação incomum de protocolo Kerberos (possível ataque de overpass-the-hash)

**Descrição**

Os invasores usam ferramentas que implementam vários protocolos como SMB e Kerberos de maneiras não padrão. Embora o Microsoft Windows aceite esse tipo de tráfego de rede sem avisos, o ATP do Azure é capaz de reconhecer possíveis casos mal-intencionados. O comportamento é uma indicação do uso de técnicas como Overpass-the-Hash, força bruta e explorações avançadas de ransomware, como o WannaCry.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP?**

Às vezes, os aplicativos implementam sua própria pilha de Kerberos, não de acordo com o RFC Kerberos.

1. Verifique se o computador de origem está executando um aplicativo com sua própria pilha Kerberos, que não esteja de acordo com o Kerberos RFC.
1. Se o computador de origem estiver executando um aplicativo desse tipo e **não** precisasse estar, corrija a configuração do aplicativo. **Feche** o alerta de segurança como uma atividade **T-BP**.
1. Se o computador de origem estiver executando esse aplicativo e deva continuar, **feche** o alerta de segurança como uma atividade **T-BP** e exclua o computador.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
1. Se houver um [usuário de origem](investigate-a-user.md), investigue.

**Correção sugerida e etapas de prevenção**

1. Redefina as senhas dos usuários comprometidos e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Contenha o computador de origem.
1. Encontre a ferramenta que realizou o ataque e remova-a.
1. Procure usuários que estavam conectados no mesmo período da atividade suspeita, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Redefina as senhas dos usuários de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.

<!-- REMOVE BOOKMARK FROM TITLE WHEN PREVIEW REMOVED -->

<a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406"></a>

## <a name="suspected-rogue-kerberos-certificate-usage-external-id-2047"></a>Uso suspeito de certificado Kerberos invasor (ID externa 2047)

**Descrição**

O ataque de certificado invasor é uma técnica de persistência usada pelos invasores depois de obter o controle sobre a organização. Os invasores comprometem o servidor de AC (autoridade de certificação) e geram certificados que podem ser usados como contas de backdoor em ataques futuros.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP**

- Determinar se a conta faz logon regularmente no computador?
  - Se o certificado é usado regularmente dos computadores, **feche** o alerta como um **FP**.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
2. Investigue o [usuário de origem](investigate-a-user.md).
3. Verificar quais recursos foram acessados com êxito e [investigue](investigate-a-computer.md).

**Correção sugerida e etapas de prevenção**

1. Redefina a senha do usuário de origem e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Conter o computador de origem
    - Encontre a ferramenta que realizou o ataque e remova-a.
    - Procure por usuários que estavam conectados em horário próximo àquele da atividade, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Localize o certificado usado no servidor de AC e revogue o certificado invalidando o TLS/SSL antes da data de expiração agendada.

## <a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation---preview-external-id-2406"></a>Suspeita de manipulação de pacote SMB (exploração de CVE-2020-0796) – (versão prévia) (ID 2406 externa)

**Descrição**

Em 12/03/2020, a Microsoft publicou o anúncio [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796), sobre uma vulnerabilidade de execução de código remota recém-descoberta na forma como o protocolo SMBv3 (Microsoft Server Message Block 3.1.1) lida com certas solicitações. Um invasor que explorou com êxito a vulnerabilidade pode executar códigos no servidor ou no cliente de destino. Os Windows Servers sem patch estão em risco devido a essa vulnerabilidade.

Nessa detecção, é disparado um alerta de segurança do ATP do Azure quando um pacote SMBv3 suspeito de explorar a vulnerabilidade de segurança CVE-2020-0796 invade um controlador de domínio na rede.

**Período de aprendizado**

Não se aplica

**TP, B-TP ou FP?**

1. Os controladores de domínio envolvidos estão atualizados e corrigidos em relação a CVE-2020-0796?
    - Se os computadores estão atualizados e corrigidos, esperamos que o ataque falhe. **Feche** o alerta de segurança como uma tentativa com falha.

**Entender o escopo da violação**

1. Investigue o [computador de origem](investigate-a-computer.md).
1. Investigue o DC (controlador de destino) de destino.

**Correção sugerida e etapas de prevenção**

**Remediação**

1. Contenha o computador de origem.
1. Encontre a ferramenta que realizou o ataque e remova-a.
1. Procure usuários que estavam conectados no mesmo período da atividade suspeita, pois eles também podem estar comprometidos. Redefina suas senhas e habilite a MFA ou, se você tiver configurado as políticas relevantes de usuário de alto risco no Azure Active Directory Identity Protection, poderá usar a ação [**Confirmar usuário comprometido**](/cloud-app-security/accounts#governance-actions) no portal de Cloud App Security.
1. Se você tem computadores cujos sistemas operacionais não dão suporte à [KB4551762](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4551762), recomendamos desabilitar o recurso de compactação do SMBv3 no ambiente, conforme descrito na seção [Soluções alternativas](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796).

**Prevenção**

1. Verifique se todos os dispositivos no ambiente estão atualizados e corrigidos em relação a [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796).

> [!div class="nextstepaction"]
> [Tutorial de alerta de comprometimento de domínio](domain-dominance-alerts.md)

## <a name="see-also"></a>Consulte Também

- [Investigar um computador](investigate-a-computer.md)
- [Trabalhando com alertas de segurança](working-with-suspicious-activities.md)
- [Trabalhando com caminhos de movimento lateral](use-case-lateral-movement-path.md)
- [Alertas de reconhecimento](reconnaissance-alerts.md)
- [Alertas de credencial comprometida](compromised-credentials-alerts.md)
- [Alertas de predominância de domínio](domain-dominance-alerts.md)
- [Alertas de exfiltração](exfiltration-alerts.md)
- [Confira o fórum do ATP do Azure!](https://aka.ms/azureatpcommunity)