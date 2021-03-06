---
title: Tutorial do guia estratégico de Reconhecimento do ATP do Azure
description: O tutorial do guia estratégico de Reconhecimento do ATP do Azure descreve como simular ameaças de Reconhecimento para detecção pelo Azure ATP.
ms.service: azure-advanced-threat-protection
ms.topic: how-to
author: shsagir
ms.author: shsagir
ms.date: 09/01/2019
ms.reviewer: itargoet
ms.openlocfilehash: 235894040ff84fe627b4cbe4d4ecd857a7555e76
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912654"
---
# <a name="tutorial-reconnaissance-playbook"></a>Tutorial: Guia estratégico de reconhecimento

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

O segundo tutorial desta série de quatro partes para alertas de segurança do ATP do Azure é um guia estratégico de reconhecimento. A finalidade do laboratório de alerta de segurança do ATP do Azure é ilustrar os recursos do **ATP do Azure** para identificação e detecção de atividades suspeitas e possíveis ataques contra a sua rede. O guia estratégico explica como testar algumas detecções *discretas* do ATP do Azure e se concentra nos recursos baseados em *assinatura* do ATP do Azure. Este guia estratégico não inclui alertas ou detecções baseados no aprendizado de máquina avançado ou detecções comportamentais baseadas no usuário/entidade, pois isso exige um período de aprendizado de até 30 dias com tráfego de rede real. Para saber mais sobre cada tutorial desta série, consulte a [Visão geral do laboratório de alerta de segurança do ATP](playbook-lab-overview.md).

Este guia estratégico ilustra os serviços de detecções de ameaça e alertas de segurança do ATP do Azure para ataques simulados em ferramentas de ataque e invasão comuns e reais disponíveis publicamente.

Neste tutorial, você vai:
> [!div class="checklist"]
> * Simular o reconhecimento de mapeamento de rede
> * Simular o reconhecimento do serviço de diretório
> * Simular o reconhecimento de endereço IP e de usuário (SMB)
> * Examinar os alertas de segurança do reconhecimento simulado no ATP do Azure

## <a name="prerequisites"></a>Pré-requisitos

[Um laboratório de alerta de segurança completo do ATP](playbook-setup-lab.md)
  - Recomendamos seguir as instruções de configuração do laboratório com a maior fidelidade possível. Quanto mais parecido estiver o seu laboratório com a configuração de laboratório sugerida, mais fácil será para seguir os procedimentos de teste do ATP do Azure.

## <a name="simulate-a-reconnaissance-attack"></a>Simular um ataque de reconhecimento

Depois que um invasor consegue presença em seu ambiente, começa a campanha de reconhecimento. Nesta fase, o invasor normalmente gastará um tempo pesquisando. Ele tenta descobrir computadores de interesse, enumerar usuários e grupos, reunir IPs importantes e mapear os ativos e fraquezas da sua organização. As atividades de reconhecimento permitem que os invasores tenham uma compreensão detalhada e uma mapeamento completo de seu ambiente para uso posterior.

Métodos de teste do ataque de reconhecimento:

* Reconhecimento de mapeamento de rede
* Reconhecimento do serviço de diretório
* Reconhecimento de endereço IP e de usuário (SMB)

## <a name="network-mapping-reconnaissance-dns"></a>Reconhecimento de mapeamento de rede (DNS)

Uma das primeiras coisas que um invasor tentará fazer é obter uma cópia de todas as informações de DNS. Mediante o êxito, o invasor terá acesso a informações abrangentes sobre seu ambiente que podem incluir informações semelhantes sobre seus outros ambientes ou redes.

A ATP do Azure suprime a atividade de reconhecimento de mapeamento de rede da sua **linha do tempo de atividade suspeita** até que um período de aprendizado de oito dias passe. No período de aprendizado, o ATP do Azure aprende o que é normal e anormal em sua rede. Após o período de aprendizado de oito dias, os eventos de reconhecimento de mapeamento de rede anormais invocam um alerta de segurança relacionado. 

### <a name="run-nslookup-from-victimpc"></a>Executar nslookup no VictimPC

Para testar o reconhecimento de DNS, usaremos a ferramenta de linha de comando nativa, *nslookup*, para iniciar uma transferência de zona de DNS. Os servidores DNS com a configuração correta recusarão consultas desse tipo e não permitirão a tentativa de transferência de zona.  

Entre no **VictimPC** usando as credenciais comprometidas de DiogoM. Execute o seguinte comando:

``` cmd
nslookup
```

Digite **server**, depois o endereço IP ou FQDN do controlador de domínio no qual o sensor do ATP está instalado.

```nslookup
server contosodc.contoso.azure
```

Vamos tentar transferir o domínio.

```nslookup
ls -d contoso.azure
```

- Substitua contosodc.contoso.azure e contoso.azure pelo FQDN do sensor e do nome domínio do ATP do Azure, respectivamente.

 ![tentativa de comando nslookup para copiar o servidor de DNS - falha](media/playbook-recon-nslookup.png)

Se **ContosoDC** for o primeiro sensor implantado, aguarde 15 minutos para permitir que o back-end do banco de dados conclua a implantação dos microsserviços necessários.

### <a name="network-mapping-reconnaissance-dns-detected-in-azure-atp"></a>Reconhecimento de mapeamento de rede (DNS) detectado no ATP do Azure

Obter visibilidade desse tipo de tentativa (com êxito ou falha) é essencial para a proteção contra ameaças do domínio. Após a instalação recente do ambiente, você precisará ir para a linha do tempo **Atividades lógicas** para ver a atividade detectada. 

Na Pesquisa do ATP do Azure, digite **VictimPC**, depois clique para exibir a linha do tempo.

![Reconhecimento de DNS detectado pelo AATP, exibição de alto nível](media/playbook-recon-nslookupdetection1.png)

Procure a atividade "Consulta AXFR". O ATP do Azure detecta esse tipo de reconhecimento em seu DNS. 
  - Se você tiver muitas atividades, clique em **Filtrar por** e desmarque todos os tipos exceto **Consulta DNS**.

![Exibição detalhada da detecção de reconhecimento de DNS em AATP](media/playbook-recon-nslookupdetection2.png)

Se o analista de segurança determinar que essa atividade partiu de um scanner de segurança, o dispositivo específico poderá ser excluído de outros alertas de detecção. Na área superior direita do alerta, clique nos três pontos. Em seguida, selecione **Fechar e excluir MySecurityScanner**. Garantindo que esse alerta não apareça novamente quando detectado em "MySecurityScanner".

A detecção de falhas pode ser tão criteriosa quanto a detecção de ataques bem-sucedidos em um ambiente. O portal do ATP do Azure nos permite ver exatamente o resultado das ações executadas por um possível invasor. Em nossa história de ataque de reconhecimento DNS simulado, nós, atuando como os invasores, foram impedidos de despejar os registros DNS do domínio. Sua equipe de SecOps tomou conhecimento da nossa tentativa de ataque e do computador que usamos em nossa tentativa de alerta de segurança do ATP do Azure.

## <a name="directory-service-reconnaissance"></a>Reconhecimento do serviço de diretório

Atuando como invasor, o próximo objetivo de reconhecimento é uma tentativa de enumerar todos os usuários e grupos na floresta. O ATP do Azure suprime a atividade de enumeração do serviço de diretório da sua linha do tempo de Atividade Suspeita até que um período de aprendizado de 30 dias passe. No período de aprendizado, o ATP do Azure aprende o que é normal e anormal em sua rede. Após o período de aprendizado de 30 dias, os eventos de enumeração de serviço de diretório anormais invocam um alerta de segurança. Durante o período de aprendizado de 30 dias, você pode ver as detecções do ATP do Azure dessas atividades usando a linha do tempo de atividade de uma entidade em sua rede. As detecções do ATP do Azure dessas atividades aparecem neste laboratório.

Para demonstrar um método comum de reconhecimento do serviço de diretório, usaremos o binário nativo da Microsoft, o *net*. Após nossa tentativa, um exame da linha do tempo de Atividade de DiogoM, nosso usuário comprometido, mostrará o ATP do Azure detectando essa atividade.

### <a name="directory-service-enumeration-via-net-from-victimpc"></a>Enumeração do serviço de diretório por meio de *net* no VictimPC

Qualquer usuário ou computador autenticado pode enumerar outros usuários e grupos em um domínio. Essa capacidade de enumeração é necessária para que a maioria dos aplicativos funcionem corretamente. Nosso usuário comprometido, DiogoM, tem uma conta de domínio sem privilégios. Nesse ataque simulado, veremos exatamente como até mesmo uma conta de domínio sem privilégios ainda pode fornecer pontos de dados valiosos para um invasor.

1. No **VictimPC**, execute o seguinte comando:

    ``` cmd
    net user /domain
    ```

   A saída mostra todos os usuários no domínio Contoso.Azure.

    ![Enumerar todos os usuários no domínio](media/playbook-recon-dsenumeration-netusers.png)

1. Vamos tentar enumerar todos os grupos no domínio. Execute o seguinte comando:

    ``` cmd
    net group /domain
    ```

   A saída mostra todos os grupos no domínio Contoso.Azure. Observe um Grupo de Segurança que não é um grupo padrão: **Helpdesk**.

    ![Enumerar todos os grupos no domínio](media/playbook-recon-dsenumeration-netgroups.png)

1. Agora, vamos tentar enumerar somente o grupo Administradores de Domínio. Execute o seguinte comando:

    ``` cmd
    net group "Domain Admins" /domain
    ```

    ![Enumerar todos os membros do grupo Administradores de Domínio](media/playbook-recon-dsenumeration-netdomainadmins.png)

    Atuando como invasor, aprendemos que há dois membros do grupo Administradores de Domínio: **YasminC** e **ContosoAdmin** (administrador interno para o controlador de domínio). Sabendo que não há limites de segurança entre o nosso Domínio e a Floresta, nosso próximo passo é tentar enumerar os Administradores de Empresa.

1. Para tentar enumerar os Administradores de Empresa, execute o seguinte comando:

    ``` cmd
   net group "Enterprise Admins" /domain
   ```

   Aprendemos que há somente um Administrador de Empresa, ContosoAdmin. Essas informações não eram importantes, pois já sabíamos que não há um limite de segurança entre o nosso Domínio e a Floresta.

    ![Administradores de Empresa enumerados no domínio](media/playbook-recon-dsenumeration-netenterpriseadmins.png)

Com as informações coletadas em nosso reconhecimento, sabemos sobre o Grupo de Segurança Helpdesk. No entanto, essas informações *ainda* não são interessantes. Também sabemos que **YasminC** é membro do grupo Administradores de Domínio. Se pudermos coletar a credencial de YasminC, poderemos acessar o próprio Controlador de Domínio.

### <a name="directory-service-enumeration-detected-in-azure-atp"></a>Enumeração do serviço de diretório detectada no ATP do Azure

Se o nosso laboratório tivesse *atividade real por 30 dias com o ATP do Azure instalado*, a atividade que acabamos de realizar como DiogoM provavelmente seria classificada como anormal. As atividades anormais apareceriam na linha do tempo de Atividade Suspeita. No entanto, como acabamos de instalar o ambiente, precisaremos acessar a linha do tempo de Atividades Lógicas.

Na Pesquisa do ATP do Azure, vamos ver a aparência da linha do tempo de Atividade Lógica do DiogoM:

![Pesquisar uma entidade específica na linha do tempo de atividade lógica](media/playbook-recon-dsenumeration-searchlogicalactivity.png)

Podemos ver quando DiogoM entrou no VictimPC usando o protocolo Kerberos. Além disso, vemos que DiogoM, no VictimPC, enumerou todos os usuários no domínio.

![Linha do tempo de atividade lógica do DiogoM](media/playbook-recon-dsenumeration-jeffvlogicalactivity.png)

Muitas atividades são registradas na linha do tempo de Atividade Lógica, tornando-a um recurso importante para execução de DFIR (Resposta a incidente e análises forenses digitais). Você pode até ver as atividades de quando a detecção inicial não era do ATP do Azure, mas do Microsoft Defender ATP, do Microsoft 365 e de outros.

Olhando a **página do ContosoDC**, também podemos ver os computadores nos quais DiogoM entrou.

![Computadores nos quais DiogoM entrou](media/playbook-recon-dsenumeration-jeffvloggedin.png)

Também podemos obter Dados de Diretório, incluindo Associações e Controles de Acesso do DiogoM, tudo de dentro do ATP do Azure.

![Dados de diretório do DiogoM no AATP](media/playbook-recon-dsenumeration-jeffvdirectorydata.png)

Agora, nossa atenção mudará para a Enumeração de Sessão do SMB.

## <a name="user-and-ip-address-reconnaissance-smb"></a>Reconhecimento de endereço IP e de usuário (SMB)

A pasta sysvol do Active Directory Domain Services é um dos mais importantes, senão *o* mais importante, compartilhamento de rede no ambiente. Cada computador e usuário deve ser capaz de acessar esse compartilhamento de rede específico para efetuar pull das Políticas de Grupo. Um invasor pode obter muitas informações da enumeração de quem tem sessões ativas com a pasta sysvol.

Nossa próxima etapa é a Enumeração da Sessão SMB no recurso ContosoDC. Queremos saber quem mais tem sessões com o compartilhamento SMB, e *de qual IP*.

### <a name="use-joewares-netsessexe-from-victimpc"></a>Usar NetSess.exe da JoeWare no VictimPC

Execute a ferramenta **NetSess** da JoeWare no ContosoDC no contexto de um usuário autenticado, nesse caso, ContosoDC:

``` cmd
NetSess.exe ContosoDC
```

![Os invasores usam o reconhecimento de SMB para identificar os usuários e seus endereços IP](media/playbook-recon-smbrecon.png)

Já sabemos que YasminC é um Administrador de Domínio. Esse ataque nos proporcionou um endereço IP de YasminC como 10.0.24.6. Como invasor, aprendemos exatamente quem precisamos comprometer. Também conseguimos o local de rede onde essa credencial está conectada.

### <a name="user-and-ip-address-reconnaissance-smb-detected-in-azure-atp"></a>Reconhecimento de endereço IP e de usuário (SMB) detectado no ATP do Azure

Agora podemos ver o que o Azure ATP detectou para nós:

![AATP detectando o reconhecimento de SMB](media/playbook-recon-smbrecon-detection1.png)

Não só somos alertados sobre essa atividade, também somos alertados sobre as contas expostas e seus respectivos endereços IP *nesse ponto no tempo*. Como o SOC (Center de Operações de Segurança), não temos apenas a tentativa e seu status, mas também o que foi enviado de volta ao invasor. Essas informações ajudam em nossa investigação.


## <a name="next-steps"></a>Próximas etapas

Normalmente, a próxima fase na cadeia de encerramento de ataque é uma tentativa de movimentação lateral.

> [!div class="nextstepaction"]
> [Guia estratégico de Movimentação Lateral do ATP do Azure](playbook-lateral-movement.md)

## <a name="join-the-community"></a>Participe da comunidade

Tem mais perguntas ou interesse em discutir sobre o ATP do Azure e a segurança relacionada com outras pessoas? Participe da [Comunidade do ATP do Azure](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) hoje mesmo!

