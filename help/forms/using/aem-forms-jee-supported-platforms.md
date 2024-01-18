---
title: Plataformas compatíveis com AEM Forms no JEE
description: Lista de componentes de infraestrutura necessários e compatíveis para a instalação do AEM Forms no JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: 75139b4a951269aeacc689baec1da6bf72ce65bc
workflow-type: tm+mt
source-wordcount: '4002'
ht-degree: 0%

---


# Plataformas compatíveis com AEM Forms no JEE {#supported-platforms-for-aem-forms-on-jee}

## Plataformas compatíveis {#supported-platforms}

<div class="preview">

O Adobe lançou um [instalador completo](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) com AEM 6.5 Forms Service Pack 18 (6.5.18.0) no JEE, juntamente com os instaladores de patch. O instalador completo oferece suporte a novas plataformas, enquanto o instalador de patch inclui apenas correções de erros.
Se você estiver fazendo uma nova instalação ou planejando usar o software mais recente para o seu Forms AEM 6.5 no ambiente JEE, o Adobe recomenda usar [Instalador completo do AEM 6.5.18.0 Forms no JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) lançado em 31 de agosto de 2023 em vez do instalador do Forms AEM 6.5 lançado em 08 de abril de 2019 ou do Forms Installer AEM 6.5.12 lançado em 03 de março de 2022.

</div>

### Níveis de suporte {#support-levels}

O AEM Forms no servidor JEE pode ser configurado usando qualquer combinação de sistemas operacionais, servidores de aplicativos, bancos de dados, drivers de banco de dados, JDK, servidores LDAP e servidores de email compatíveis.

Este documento lista as plataformas de cliente e servidor compatíveis com o AEM Forms no JEE. O Adobe fornece vários níveis de suporte, tanto para configurações Adobe recomendadas quanto para outras configurações. O documento também lista outros softwares compatíveis e suas versões, exceções, definições de patch e política de suporte a patches de software de terceiros.

>[!NOTE]
>
>- Para obter uma lista completa de exceções para plataformas de servidor compatíveis, consulte [Exceções às plataformas de servidor compatíveis](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>- O AEM Forms no JEE é compatível apenas com as versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos compatíveis.

### Política de atualização e suporte

#### Instalador completo

- **Suporte de atualização para instaladores completos**: Um instalador completo é lançado com cada 6ª versão do Service Pack do AEM. Por exemplo, havia um instalador completo lançado com as versões 6.5.12.0 e 6.5.18.0 do SP. O AEM Forms permite atualizações diretas exclusivamente dos dois últimos instaladores completos. Por exemplo, o AEM Forms facilita atualizações diretas para a versão 6.5.18.0 somente dos dois últimos instaladores completos, ou seja, as versões 6.5.12.0 e 6.5.6.0. Se precisar fazer upgrade de um upgrade anterior, você pode usar um upgrade multi-hop para primeiro acessar uma versão completa do instalador com suporte e, em seguida, a versão mais recente.

- **Substituição e remoção**: o suporte à plataforma é atualizado com cada versão completa do instalador. Qualquer software marcado como obsoleto na matriz de plataforma durante uma versão completa do instalador tem direito a ser removido da matriz de plataforma suportada em uma versão subsequente do instalador completo, indicando o fim do suporte para o software.

#### Service Packs

- **Cobertura do Service Pack**: o Adobe fornece suporte técnico para ambientes AEM Forms usando qualquer um dos seis service packs mais recentes. Se sua versão atual é anterior aos últimos seis service packs, a Adobe recomenda que você atualize para a versão mais recente a fim de obter desempenho ideal, segurança e suporte contínuo.

- **Diretrizes do instalador de patches**: Ao usar os instaladores de patch para atualizar, é crucial verificar se a versão subjacente do instalador completo não tem mais de duas versões. Por exemplo, durante a instalação do service pack 6.5.19.0, verifique se a versão subjacente do instalador completo é 6.5.18.0 ou 6.5.12.0.

- **Suporte para atualização de patches**: você pode continuar atualizando para o service pack mais recente até que também esteja atualizando para as plataformas compatíveis mais recentes. Por exemplo, é possível atualizar do service pack 6.5.12.0 para o 6.5.19.0, desde que você faça a transição para uma combinação de plataforma compatível com o 6.5.19.0.

### Configurações recomendadas {#recommendedconfigurations}

a Adobe recomenda essas configurações e fornece suporte total ou restrito como parte do contrato padrão de manutenção de software:

<table>
 <tbody>
  <tr>
   <th>Nível de compatibilidade</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>A: Suportado<br /> </td>
   <td>O Adobe fornece suporte e manutenção completos para essa configuração. Essa configuração é coberta pelo processo de garantia de qualidade do Adobe.</td>
  </tr>
  <tr>
   <td>R: Suporte restrito</td>
   <td>O Adobe fornece suporte total para essa configuração após o cumprimento de determinados pré-requisitos. Entre em contato com o suporte corporativo da Adobe para saber mais sobre os pré-requisitos e fazer uma solicitação para obter suporte.</td>
  </tr>
  <tr>
   <td>L: Suporte limitado</td>
   <td>O Adobe fornece suporte e manutenção completos para essa configuração após o cumprimento de determinados pré-requisitos. Nem todos os recursos estão disponíveis na configuração. Entre em contato com o suporte corporativo da Adobe para saber mais sobre os pré-requisitos e fazer uma solicitação para obter suporte.<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações não suportadas {#unsupported-configurations}

| Nível de compatibilidade | Descrição |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E: A expectativa é funcionar | Espera-se que a configuração funcione e não há relatórios em contrário. |
| Z: Não suportado | A configuração não é compatível. O Adobe não faz nenhuma declaração sobre se a configuração funciona e não oferece suporte a ela. |

>[!NOTE]
>
>Para ajudar os clientes da AEM Forms a reduzir o custo de propriedade, simplificar a arquitetura de implantação e modernizar a pilha de desenvolvimento, a plataforma corporativa da Adobe Experience Manager está se afastando das implantações baseadas em servidor de aplicativos em favor das implantações independentes baseadas em OSGi. O Adobe continua a oferecer suporte à pilha do AEM Forms JEE com uma matriz reduzida de componentes de infraestrutura.
>
>Com o lançamento da versão 6.5, os componentes da infraestrutura com menor uso entre os clientes do Adobe não serão mais suportados, como demonstrado a seguir:
>
>- banco de dados IBM® DB2®
- Sistemas operacionais IBM® AIX® e Sun Solaris™
>
Para novas instalações, quando viável, é recomendável implantar o AEM Forms na pilha OSGi moderna para usar as inovações mais recentes em torno do Adaptive Forms responsivo para comunicações móveis, comunicações interativas de vários canais e integrações de dados de back-end usando o Modelo de dados de formulário.
>
O Adobe reconhece que os usuários existentes devem continuar a implantar o AEM Forms na pilha do JEE. Nesses casos, o Adobe exige a implantação do AEM Forms JEE em uma infraestrutura compatível, conforme descrito nesta documentação. Se você estiver atualizando para o AEM 6.5 Forms e estiver usando uma plataforma não compatível na versão anterior do AEM Forms, entre em contato com o Suporte da Adobe para obter ajuda sobre como atualizar para uma plataforma compatível.

### Máquinas virtuais Java™ (JVM) {#java-virtual-machines-jvm}

O Adobe Experience Manager Forms requer uma máquina virtual Java™ para ser executada, que é fornecida pela distribuição Java™ Development Kit (JDK). O Adobe Experience Manager opera com as seguintes versões das Máquinas Virtuais Java™:

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>Nível de compatibilidade</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr> 
   <td><p>Oracle Java™ SE 11 (64 bits) <sup> [8] </sup> </p>  </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Versões e atualizações secundárias </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 11 - 64 bits</td>
   <td>Z: Não suportado</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Azul Zulu OpenJDK 8 - 64 bits</td>
   <td>Z: Não suportado</td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td>Oracle Java™ SE 8 (64 bits)</td>
   <td>A: Suportado</td>
   <td>Versões e atualizações secundárias</td>
  </tr>
  <tr>
   <td>Máquina virtual IBM® J9 (build 2.9, JRE 1.8.0) IBM® JDK SR6-FP26<br /> </td>
   <td>A: Suportado</td>
   <td>Versões e atualizações secundárias</td>
  </tr>
  <tr>
   <td>IBM® JAVA1.8.0_291(build 8.0.6.30)<br /> </td>
   <td>A: Suportado</td>
   <td>Versões e atualizações secundárias</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- Rastreie os Boletins de segurança do fornecedor Java™ para garantir a segurança dos ambientes de produção e instalar as atualizações mais recentes do Java™.
- O AEM Forms no JEE é compatível apenas com JVMs de 64 bits em ambientes de produção.

### Bancos de dados e persistência CRX {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Platform</strong></p> </td>
   <td><p><strong> Descrição</strong></p> </td>
   <td><p><strong>Nível de compatibilidade</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sistema de arquivos</p> </td>
   <td><p>Microkernel do repositório (arquivos TAR MK)</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p> MongoDB Enterprise 5.0</p> </td>
   <td><p>Microkernel do repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
    <tr>
   <td><p> MongoDB Enterprise 6.0 </p> </td>
   <td><p>Microkernel do repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
   <tr>
   <td>Oracle Database 19c (edições Standard, Real Application Clusters (RAC) e Enterprise) </td>
   <td>Microkernal do repositório </td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td><p>Microkernel do repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft® SQL Server 2019 </p> </td>
   <td><p>Microkernel do repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td>IBM® DB2® 11.1 (obsoleto)</td>
   <td>Microkernel do repositório</td>
   <td>R: Suporte restrito</td>
  </tr>
  <tr>
  <tr>
   <td>MySQL 8.0.27</td>
   <td>-</td>
   <td>R: Suporte restrito</td>
  </tr>
 </tbody>
</table>

- O IBM® DB2® não é suportado para instalações novas. Ele é compatível somente com clientes existentes que estão atualizando para o AEM 6.5 Forms.
- MongoDB é um software de terceiros e não está incluído no pacote de licenciamento AEM. Para obter mais informações, consulte [Política de licenciamento do MongoDB](https://www.mongodb.org/about/licensing/).
- Para aproveitar ao máximo a implantação do AEM, a Adobe recomenda licenciar a versão MongoDB Enterprise para se beneficiar de suporte profissional.
- O Atendimento ao cliente do Adobe auxilia na qualificação de problemas relacionados ao uso do MongoDB com AEM. Para obter mais informações, consulte [Página do MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
- &#39;Sistema de Arquivos&#39; inclui armazenamento em bloco compatível com POSIX. Isso inclui a tecnologia de armazenamento em rede. Lembre-se de que o desempenho do sistema de arquivos pode variar e influencia o desempenho geral. É recomendável carregar o AEM de teste com o sistema de arquivos remoto/de rede.
- Somente o WiredTiger do Mecanismo de Armazenamento MongoDB é compatível.
- A fragmentação de MongoDB não é compatível com o AEM.
- O AEM Forms no JEE não oferece suporte ao MySQL para persistência RDBMK.
- O módulo de Segurança de documentos não usa o Repositório de conteúdo. Isso implica que, se você estiver usando somente a Segurança de documentos e não planeja usar formulários do HTML Workspace, do HTML5 ou formulários adaptáveis, não instale o Repositório de conteúdo.
- O AEM Forms no JEE não é compatível com o uso do MySQL para o repositório AEM persistente (repositório CRX).

### Drivers de banco de dados {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Banco de dados </th>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>Conector MySQL/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar(versão 5.1.44)</p> </td>
   <td><p>Fornecido com o AEM Forms na instalação do JEE</p> </td>
  </tr>
  <tr>
   <td>Microsoft® SQL Server<br /> </td>
   <td><p>Driver JDBC do Microsoft® SQL Server 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Download do site da Microsoft® na web.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Driver JDBC do Oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (versão 19.3.0.0.0)<br /> </p> </td>
   <td><p>Baixar de <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Site do Oracle</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Servidores de aplicativos {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Platform</strong></p> </td>
   <td><p><strong>Nível de compatibilidade</strong></p> </td>
   <td><p><strong>Definições de patch compatíveis</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 12.2.1 (12c R2) (obsoleto) <sup>[9]</sup></td>
   <td>A: Suportado</td>
   <td>Service pack e atualizações críticas</td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 14c <sup>[9]</sup></td>
   <td>A: Suportado</td>
   <td>Service pack e atualizações críticas</td>
  </tr>
  <tr>
   <td>Servidor de aplicativos IBM® WebSphere® 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
   <td>A: Suportado</td>
   <td>Service pack e atualizações críticas</td>
  </tr>
  <tr>
   <td><p>JBoss® Enterprise Application Platform (EAP) 7.4 <sup>[2] [3] [7]</sup> </p> </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Patches e patches cumulativos para a versão de EAP compatível</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Os clusters do IBM® WebSphere® só são suportados nas edições de Implantação de rede.

### Sistemas operacionais de servidor {#server-operating-systems}

#### Ambientes de produção {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Platform</strong></p> </th>
   <th><p><strong>Nível de suporte</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft® Windows Server 2019 (64 bits) (obsoleto)</td>
   <td>A: Suportado</td>
   <td>Service packs e atualizações críticas</td>
  </tr>
     <tr>
   <td>Microsoft® Windows Server 2022 (64 bits)</td>
   <td>A: Suportado</td>
   <td>Service packs e atualizações críticas</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A: Suportado</td>
   <td>Service packs e atualizações críticas</td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bits)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Versões secundárias, atualizações cumulativas e atualizações críticas</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64 bits) (obsoleto)</td>
   <td><p>A: Suportado</p> </td>
   <td><p>Versões secundárias, atualizações cumulativas e atualizações críticas</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bits)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Service packs, patches cumulativos e atualizações críticas de segurança</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Atualização 3 (64 bits)</td>
   <td>A: Suportado</td>
   <td>Service packs, patches cumulativos e atualizações críticas de segurança</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bits)<sup> [6]</sup></td>
   <td>A: Suportado</td>
   <td>Service packs, patches cumulativos e atualizações críticas de segurança</td>
  </tr>
 </tbody>
</table>

#### Ambiente virtualizado {#virtualized-environment}

Você pode executar o AEM Forms no JEE em uma máquina física ou em um ambiente virtual. No entanto, se você encontrar algum problema com o AEM Forms em um ambiente virtual, tente replicar o problema em uma máquina física. Se o problema persistir na máquina física, entre em contato com o Suporte da Adobe para obter uma resolução. Para os problemas que não podem ser replicados em uma máquina física, entre em contato com o fornecedor do ambiente virtual.

#### Ambientes de desenvolvimento {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma (Versão Base)</strong></p> </th>
   <th>Nível de compatibilidade</th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 de 64 bits</p> </td>
   <td>E: A expectativa é funcionar</td>
   <td><p>Service pack e atualizações críticas</p> </td>
  </tr>
 </tbody>
</table>

### Exceções às plataformas de servidor compatíveis {#exceptions-to-supported-server-platforms}

Considere as exceções a seguir ao escolher uma plataforma para configurar o AEM Forms no servidor JEE.

1. O AEM Forms no JEE não é compatível com o IBM® WebSphere® com MySQL.
1. O AEM Forms no JEE não é compatível com o JBoss® no SUSE® Linux® Enterprise Server 12. Somente o IBM® WebSphere® é suportado no SUSE® Linux® Enterprise Server 12.
1. O AEM Forms no JEE não suporta nenhum JDK com JBoss® além do Oracle Java™ SE.
1. O AEM Forms no JEE não suporta nenhum JDK com IBM® WebSphere® diferente do IBM® JDK.
1. O repositório CRX oferece suporte à persistência do tipo TarMK, MongoDB e bancos de dados relacionais (RDBMK). Você não pode ter dois sistemas de banco de dados diferentes entre o servidor de aplicativos e o repositório CRX. No entanto, em um ambiente AEM Forms no JEE, é possível usar o MongoMK com repositório CRX e um banco de dados relacional compatível com o servidor de aplicativos.
1. O AEM Forms no JEE não é compatível com o servidor de aplicativos WebSphere® no CentOS.
1. O AEM Forms no JEE não suporta o controle de acesso baseado em função (RBAC) JBoss®.
1. O AEM Forms no JEE suporta o SDK Java™ SE 11 (64 bits) do Oracle para servidor de aplicativos somente JBoss® EAP 7.4.
1. As versões do JDK posteriores à 1.8.0_281 não são compatíveis com o servidor WebLogic. (FORMS-8498)

<!-- 
1. [!DNL Microsoft&reg; Windows Server 2019] does not support [!DNL MySQL 5.7] and [!DNL JBoss&reg; EAP 7.1], [!DNL Microsoft&reg; Windows Server 2019] does not support turnkey installations for [!DNL Experience Manager Forms Service Pack 6.5.10.0 and later]. (CQDOC-18312) 
-->

Além disso, considere os seguintes pontos ao escolher o software para Adobe AEM Forms em implantações JEE:

- Atualizações de suporte, patches e fix packs do AEM Forms no JEE sobre a versão principal e secundária especificada do software compatível. No entanto, não há suporte para a atualização para a próxima versão principal ou secundária, a menos que especificado.
- Instalações baseadas em cluster não dão suporte à persistência TarMK. Para obter informações sobre persistência compatível, consulte [Escolha de um tipo de persistência para uma instalação do AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- O AEM Forms no JEE suporta vários softwares de terceiros conforme o Adobe [Política de suporte a software de terceiros](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
- AEM Forms em plataformas de suporte JEE de acordo com o suporte fornecido por fornecedores terceirizados. Algumas combinações podem não ser permitidas por fornecedores de terceiros. Por exemplo, muitos fornecedores não certificaram seus servidores de aplicativos com o Oracle. Como resultado, o AEM Forms no JEE também não é compatível com essas combinações. Para garantir que você escolha as versões de software compatíveis, verifique também a matriz de suporte para outros fornecedores.
- O AEM Forms no JEE não é compatível com TarMK Cold Standby.
- O AEM Forms no JEE não é compatível com clustering vertical.
- O AEM Forms no JEE não é compatível com o banco de dados MySQL em um ambiente clusterizado.
- Para obter a lista de plataformas removidas ou atualizadas, consulte [Resumo dos novos recursos do AEM 6.5 Forms](../../forms/using/whats-new.md) documento.

### Servidores LDAP (opcional) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produto (Versão Base)</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td>Microsoft® Ative Diretory 2016 (obsoleto)</td>
   <td>Versão de manutenção e fix packs</td>
  </tr>
  <tr>
   <td>Diretório ativo Microsoft® 2022</td>
   <td>Versão de manutenção e fix packs</td>
  </tr>
  <tr>
   <td><p>Servidor de Diretórios IBM® Tivoli 6.4</p> </td>
   <td><p>Pacotes de recursos e correções provisórias</p> </td>
  </tr>
 </tbody>
</table>

### Servidores de e-mail (opcional) {#email-servers-optional}

| Produto |
| ----------------------- |
| Microsoft® Exchange 2013 |
| Microsoft® Office 365 |

### Gerenciadores de conteúdo e conectores correspondentes {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>Produto<br /> </strong></td>
   <td><strong>Versão</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum®</td>
   <td>7,3</td>
  </tr>
  <tr>
   <td>IBM® FileNet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>IBM® Content Manager Server (obsoleto) </td>
   <td>8.5 Fix pack 2</td>
  </tr>
  <tr>
   <td> Cliente do gerenciador de conteúdo IBM® (obsoleto)</td>
   <td>8,5 </td>
  </tr>
   <td>Microsoft® Sharepoint </td>
   <td>2019<br /> </td>
  </tr>
 </tbody>
</table>

### Suporte para Cordova {#support-for-cordova}

O aplicativo AEM Forms agora é compatível com o Apache Cordova. A seguir estão as versões específicas da plataforma do Cordova que são compatíveis:

- Apache Cordova 6.4.0
- Cordova iOS 4.3.0
- Cordova Android™ 6.0.0
- Cordova Windows 4.4.3

### Suporte de software para PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produto</strong></p> </th>
   <th><p><strong>Formatos suportados para conversão em PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Faixa clássica do Acrobat 2020</a> versão mais recente</td>
   <td>XPS, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF e TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
O PDF Generator suporta apenas versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos suportados.
>
Além disso:
>
- O PDF Generator exige a versão de 32 bits do [Faixa clássica do Acrobat 2020 versão 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) para executar a conversão.
- O PDF Generator suporta apenas a versão comercial de 32 bits do Microsoft® Office Professional Plus e outros softwares necessários para a conversão.
- PDF Generator não suporta Microsoft® Office 365.
- As conversões de PDF Generator para OpenOffice são suportadas apenas no Windows e no Linux®.
- Os recursos PDF, Optimize PDF e Export PDF de OCR são suportados apenas no Windows.
- Uma versão do Acrobat é fornecida com o AEM Forms para ativar a funcionalidade PDF Generator. A versão agrupada só deve ser acessada programaticamente com o AEM Forms, durante o prazo da licença do AEM Forms, para uso com o AEM Forms PDF Generator. Para obter mais informações, consulte a Descrição do produto AEM Forms de acordo com a implantação ([No local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) ou [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
- O serviço PDF Generator não suporta Microsoft® Windows 10.
-PDF Generator falha ao converter arquivos usando o Microsoft® Visio 2019. Você pode continuar a usar o Microsoft® Visio 2016 para converter arquivos .VSD e .VSDX.
- Falha do PDF Generator ao converter arquivos usando o Microsoft® Project 2019. Você pode continuar a usar o Microsoft® Project 2016 para converter arquivos .MPP.
- Falha do PDF Generator ao converter arquivos usando o Microsoft® Visio 2019.
- Falha do PDF Generator ao converter arquivos usando o Microsoft® Project 2019.
>

### Exceções ao suporte de acessibilidade {#exceptions-to-accessibility-support}

Os seguintes subsistemas do AEM Forms não são [508](https://www.section508.gov/) compatível:

- Interface de criação adaptável do Forms
- Interface de criação do Forms Manager
- Interface de criação do gerenciamento de correspondência
- Interface do usuário do administrador (Interface do usuário do Console de administração)

## Requisitos do sistema para AEM Forms no JEE {#system-requirements-for-aem-forms-on-jee}

### Requisitos mínimos de hardware {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Platform</td>
   <td>Requisito mínimo de hardware</td>
  </tr>
  <tr>
   <td>Microsoft® Windows Server</td>
   <td>Processador Intel Xeon® E5-2680 de 2,4 GHz ou equivalente<br /> VMWare ESX 5.1 ou posterior<br /> RAM: 6 GB (SO de 64 bits com JVM de 64 bits)<br /> Espaço livre em disco: 15 GB de espaço temporário mais 22 GB<br /> para AEM Forms no JEE</td>
  </tr>
  <tr>
   <td>SUSE® Linux® Enterprise Server</td>
   <td>Processador Intel Xeon® E5-2670v2, 1 vCPU, 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM: 6 GB (SO de 64 bits com JVM de 64 bits)<br /> Espaço livre em disco: 6 GB de espaço temporário mais 22 GB<br /> para AEM Forms no JEE</td>
  </tr>
  <tr>
   <td>Red Hat® Enterprise Linux®</td>
   <td>Processador Intel Xeon® E5-2670v2, 1 vCPU, 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM: 6 GB (SO de 64 bits com JVM de 64 bits)<br /> Espaço livre em disco: 6 GB de espaço temporário mais 22 GB<br /> para AEM Forms no JEE<br /> </td>
  </tr>
  <tr>
   <td>Requisitos de hardware para um ambiente de produção pequeno</td>
   <td>
    <ul>
     <li><strong>Ambiente equipado com a Intel®</strong>: Intel Xeon® E5-2680, 2,4 GHz ou superior. O uso de um processador dual core melhora ainda mais o desempenho</li>
     <li><strong>Memória: </strong>4 GB <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Para requisitos adicionais, consulte:

- [Requisitos de sistema para um AEM Forms de servidor único na implantação do JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [Requisitos de sistema para um AEM Forms em cluster na implantação do JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)

## Clientes compatíveis com o AEM Forms no JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Platform</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>Versão de 32 bits ou 64 bits</p> <p> </p> </td>
   <td>Service packs e atualizações críticas</td>
  </tr>
  <tr>
   <td>Microsoft® Windows® 2019 Server (obsoleto)</td>
   <td>Service packs e atualizações críticas</td>
  </tr>
  <tr>
   <td>Servidor Microsoft® Windows® 2022</td>
   <td>Service packs e atualizações críticas</td>
  </tr>
 </tbody>
</table>

- Espaço em disco para instalação: 1,7 GB apenas para o Workbench, 2,7 GB em uma única unidade para uma instalação completa do Workbench, Designer e a montagem de amostras 400 MB para diretórios de instalação temporários - 200 MB no diretório temporário do usuário e 200 MB no diretório temporário do Windows. Se todos esses locais residirem em uma única unidade, deverá haver 1,5 GB de espaço disponível durante a instalação. Os arquivos copiados para os diretórios temporários são excluídos quando a instalação é concluída.

- Memória para executar o Workbench: 2 GB de RAM
- Requisito de hardware: processador de 1 GHz Intel® Pentium® 4 ou AMD® equivalente
- Resolução mínima do monitor de 1024 X 768 pixels ou superior com cor de 16 bits ou superior
- Conexão de rede TCP/IPv4 ou TCP/IPv6 com o AEM Forms no servidor JEE
- Você deve ter privilégios Administrativos para instalar o Workbench no Windows. Se você estiver instalando usando uma conta de não administrador, o instalador solicitará as credenciais de uma conta apropriada.

### Designer {#designer}

- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server ou Microsoft® Windows® 10
- 1 GHz ou mais rápido com suporte para PAE, NX e SSE2.
- 1 GB de RAM para 32 bits ou 2 GB de RAM para SO de 64 bits
- 16 GB de espaço em disco para 32 ou 20 GB de espaço em disco para SO de 64 bits
- Memória gráfica - 128 MB de GPU (recomenda-se 256 MB)
- 2,35 GB de espaço disponível em disco rígido
- Resolução do monitor de 1024 X 768 pixels ou superior
- Aceleração de hardware de vídeo (opcional)
- Acrobat Pro DC, Acrobat Standard DC ou Adobe Acrobat Reader DC
- Privilégios administrativos para instalar o Designer
- Microsoft® Visual C++ 2019 (VC 14.28 ou superior) tempo de execução de 32 bits

### ADOBE ACROBAT e ADOBE READER {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat e Adobe Reader (Base)</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020 (faixa clássica)</td>
   <td>Versão 20.004.30006 ou posterior<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
A família de produtos Acrobat DC apresenta duas faixas para Acrobat e Reader, que são produtos diferentes: &quot;Classic&quot; e &quot;Continuous&quot;. Para obter detalhes e uma comparação das duas faixas, consulte [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

### Navegadores {#browsers}

#### Áreas de trabalho {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>Navegador (Base)</strong></p> </th>
   <th><p><strong>Nível de suporte</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Edge (Evergreen)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Service packs e atualizações</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td>Todas as atualizações</td>
  </tr>
  <tr>
   <td>Mozilla Firefox ESR</td>
   <td>E: A expectativa é funcionar</td>
   <td> Todas as atualizações</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td>Todas as atualizações</td>
  </tr>
  <tr>
   <td>Apple Safari no macOS</td>
   <td>A: Suportado</td>
   <td>Todas as atualizações</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
Algumas exceções relacionadas ao navegador para desktops são as seguintes:
>
- O Safari é compatível somente com Macintosh OS X.
- O Espaço de trabalho é compatível com o Safari 5.1 no Macintosh OS X 10.6 e 10.7 com Acrobat DC ou versões posteriores. Para obter mais informações sobre a compatibilidade do Safari 5.1 com o Adobe Reader, Acrobat, consulte [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
- O Console de administração não é compatível com o Safari.
- O Gerenciamento de correspondência não é compatível com o Windows® Internet Explorer 9.0 para formulários AEM 6.1.
- O Forms Portal oferece suporte ao software de leitor de tela JAWS 14.0 no Internet Explorer 11 para acessibilidade.

#### Clientes móveis {#mobile-clients}

<table>
 <tbody>
  <tr>
   <th><p><strong>Navegador (Base)</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Chrome no Android™ 4.1.2 e posterior</p> </td>
   <td><p>Todas as atualizações</p> </td>
  </tr>
  <tr>
   <td>Safari no iOS 15.1 e posterior</td>
   <td>Todas as atualizações</td>
  </tr>
  <tr>
   <td>Microsoft® Edge<br /> </td>
   <td>Todas as atualizações<br /> </td>
  </tr>
  <tr>
   <td>Navegador Android™ nativo no Android™ 4.4 e posterior</td>
   <td>Todas as atualizações</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
- O Forms Portal é compatível com o Safari somente no iPad.

### aplicativo AEM Forms {#aem-forms-workspace-app}

#### Suporte a dispositivo móvel {#mobile-device-support}

O aplicativo AEM Forms está disponível nas seguintes plataformas:

| **Platform** | **Dispositivos compatíveis** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone, iPad, iPad Air e iPad mini executando o iOS 15.1 e superior. |
| Google Android™ | Android™ 5.1 e superior. O aplicativo AEM Forms é certificado em tablets Samsung Galaxy de 7 e 10 polegadas e smartphones populares. |
| Microsoft® Windows | Dispositivos Microsoft® Surface, tablets, laptops e desktops com o sistema operacional Microsoft® Windows 10. |

### Extensão de segurança de documentos Adobe para o Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}

Clique em [aqui](https://www.adobe.com/br/products/livecycle/rightsmanagement/extension/downloads.html) para ver os requisitos de sistema do Adobe Document Security Extension for Microsoft® Office.

### Exceções ao suporte ao cliente {#exceptions-to-client-support}

Atualizações de suporte, patches e fix packs do AEM Forms no JEE sobre a versão principal e secundária especificada do software compatível. No entanto, não há suporte para a atualização para a próxima versão principal ou secundária, a menos que especificado.

## Política de suporte a patches de terceiros {#third-party-patch-support-policy}

Os requisitos de software de terceiros para o AEM Forms no JEE estão documentados na seção &quot;Requisitos do sistema&quot; dos respectivos documentos do produto. Acesse toda a documentação de [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

A AEM Forms nas plataformas de referência de terceiros do JEE especifica o nível de patch específico da infraestrutura de terceiros que estava em vigor durante o desenvolvimento e o lançamento do AEM Forms no JEE e a partir do nível mínimo de patch/service pack da infraestrutura compatível com essa versão do AEM Forms no JEE.

O Adobe oferece suporte a patches urgentes ou recomendados emitidos por fornecedores terceirizados após o lançamento, supondo que esses fornecedores garantam compatibilidade com versões anteriores compatíveis com o AEM Forms no JEE. O Adobe só oferecerá suporte a patches lançados após o nível mínimo de patch declarado na documentação do AEM Forms no JEE.

Às vezes, o Adobe não é compatível com atualizações de terceiros que alteram a funcionalidade principal e, portanto, não é compatível com versões anteriores completas. Para obter detalhes sobre as atualizações compatíveis, consulte [Definições de patch compatíveis](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) para produtos de fornecedores específicos e os tipos de patch compatíveis com o Adobe.

Em circunstâncias além do controle do Adobe, patches de terceiros que alegam compatibilidade com versões anteriores podem ter impacto negativo nos produtos Adobe ou ambientes do cliente. Nesses casos, a Adobe recomenda que os clientes avaliem o impacto de qualquer patch urgente de terceiros antes de aplicá-los a sistemas críticos. O Adobe trabalha com terceiros usando esforços comerciais razoáveis para resolver esses problemas, seja por meio de programas normais de suporte ao Adobe ou por terceiros que corrijam o problema em seu patch. Isso não garante que um patch de terceiros recém-lançado compatível com o Adobe funcione conforme documentado pelo fornecedor ou com o AEM Forms no JEE.

O Adobe se reserva o direito de alterar as plataformas de referência de terceiros compatíveis com uma versão do AEM Forms no JEE e suas definições de patch compatíveis em um determinado ponto.

Informações adicionais sobre patches de terceiros também podem ser encontradas no site de suporte do Adobe Enterprise para obter artigos da base de conhecimento relacionados ao seu produto.

<!--

## Platform updates {#platform-updates}

The following platforms are marked as deprecated with AEM Forms 6.5.18.0 release on August 31, 2023:

- Microsoft&reg; Windows Server 2019 (64-bit)
- Microsoft&reg; Active Directory 2016

The following platforms are marked as deprecated with AEM Forms 6.5.13.0 release on June 2, 2022:
- Microsoft&reg; SharePoint 2016

The following platforms are marked as deprecated with AEM Forms 6.5.10.0 release on September 7, 2021:

- Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/support/programs/eol-matrix.html).
- Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
- Microsoft&reg; Windows Server 2016 (64-bit) 
- Microsoft&reg; Office 2016
- OpenOffice 4.1.2

-->


## Histórico de revisão {#revision-history}

<!--

- 6.5.18.0 (Aug 31, 2023)
  - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
    - MongoDB Enterprise 4.4
    - Oracle WebLogic Server 14c
    - My SQL JDBC connector 8
    - Active Directory 2022
    - Microsoft&reg; Windows Server 2022 (64-bit)

  - **Removed support**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
    - Windows Server 2016 (64-bit)
    - MongoDB Enterprise 4.0
    - Oracle Database 12c Release 2 (12.2.0.1.0)
    - MySQL 5.7.35
    - Microsoft&reg; SQL Server 2016
    - JBoss&reg; EAP 7.1.4
    - My SQL JDBC connector 5.1.44
    - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
    - Microsoft&reg; SQL Server JDBC driver 6.2.2.0
    - Microsoft&reg; JDBC Driver 8.x for SQL Server

    The release has also removed support for the following platforms for PDF Generator and in-general:
    - Microsoft&reg; Sharepoint 2016
    - Microsoft&reg; Office 2016
    - Microsoft&reg; Office Visio 2016 
    - Microsoft&reg; Publisher 2016
    - Microsoft&reg; Project 2016
    - OpenOffice 4.1.2
    - Acrobat 2017 (Classic track) Version 17.011.30078 or later

  - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:
    - Microsoft&reg; Windows Server 2019 (64-bit)
    - Microsoft&reg; Active Directory 2016
    
- 6.5.13.0 (June 2, 2022)

  The following platforms are deprecated with AEM Forms 6.5.13.0 release on:
 
  - Microsoft&reg; SharePoint 2016

- 6.5.12.0 (March 3, 2022)

    - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has removed support for the following platforms:
      - IBM&reg; J9 Virtual Machine (build 2.8, JRE 1.8.0)
      - Oracle Database 12c Release 1
      - Oracle Database 18c
      - Oracle Unified Directory (OUD) 11g Release 2
      - IBM&reg; Lotus Domino 9.0
      - IBM&reg; FileNet 5.2
      - Adobe Flash Player

    - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:

      - MongoDB Enterprise 4.0
      - MongoDB Enterprise 4.2
      - IBM&reg; DB2&reg; 11.1
      - Oracle Database 12c Release 2
      - MySQL 5.7.35
      - Microsoft&reg; SQL Server JDBC driver 6.2.1.0
      - JBoss&reg; Enterprise Application Platform (EAP) 7.1.4
      - IBM&reg; Content Manager Server 8.5 Fix pack 2
      - IBM&reg; Content Manager Client 8.5
      - Microsoft&reg; SQL Server 2016

- 6.5.10.0 (Sep 01, 2022)

  - **Added support**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platform:
  
    - Oracle Java&trade; SE 11 (64 bit) SDK for application server JBoss&reg; EAP 7.4.
  - **Deprecated support**: [!DNL Adobe Experience Manager Forms] on JEE has deprecated the following platforms:

    - Adobe Acrobat 2017 - [Core support for Adobe Acrobat 2017 ends on June 6, 2022](https://helpx.adobe.com/support/programs/eol-matrix.html).
    - Red Hat&reg; Enterprise Linux&reg; 7 (Kernel 3.x) (64-bit)
    - Microsoft&reg; Windows Server 2016 (64-bit) 
    - Microsoft&reg; Office 2016
    - OpenOffice 4.1.2


-->

### Versão 6.5.19.1 (15 de dezembro de 2023)

| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 6.0 | MongoDB Enterprise 4.4 |  |
| MongoDB Enterprise 5.0 |  |  |
|  | |  |

### Versão 6.5.18.0 (31 de agosto de 2023)

| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 4.4 | Windows Server 2016 (64 bits) | Microsoft® Windows Server 2019 (64 bits) |
| Oracle WebLogic Server 14c | MongoDB Enterprise 4.0 | Diretório ativo Microsoft® 2016 |
| My SQL JDBC connector 8 | Oracle Database 12c Versão 2 (12.2.0.1.0) |  |
| Ative Diretory 2022 | MySQL 5.7.35 |  |
| Microsoft® Windows Server 2022 (64 bits) | Microsoft® SQL Server 2016 |  |
|  | JBoss® EAP 7.1.4 |  |
|  | Conector My SQL JDBC 5.1.44 |  |
|  | Driver JDBC do Microsoft® SQL Server 6.2.1.0 |  |
|  | Driver JDBC do Microsoft® SQL Server 6.2.2.0 |  |
|  | Driver Microsoft® JDBC 8.x para SQL Server |  |
|  |  |  |
|  | **Suporte removido (PDF Generator e Em geral):** |  |
|  | Microsoft® Sharepoint 2016 |  |
|  | Microsoft® Office 2016 |  |
|  | Microsoft® Office Visio 2016 |  |
|  | Microsoft® Publisher 2016 |  |
|  | Projeto Microsoft® 2016 |  |
|  | OpenOffice 4.1.2 |  |
|  | Acrobat 2017 (faixa clássica) versão 17.011.30078 ou posterior |  |


### Versão 6.5.13.0 (2 de junho de 2022)

| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
|  |  | Microsoft® SharePoint 2016 |


### Versão 6.5.12.0 (3 de março de 2022)

| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
|  | Máquina virtual IBM® J9 (build 2.8, JRE 1.8.0) | MongoDB Enterprise 4.0 |
|  | Oracle Database 12c Versão 1 | MongoDB Enterprise 4.2 |
|  | Oracle Database 18c | IBM® DB2® 11.1 |
|  | Oracle Unified Diretory (OUD) 11g versão 2 | Oracle Database 12c Versão 2 |
|  | IBM® Lotus Domino 9.0 | MySQL 5.7.35 |
|  | IBM® FileNet 5.2 | Driver JDBC do Microsoft® SQL Server 6.2.1.0 |
|  | Flash Player Adobe | JBoss® Enterprise Application Platform (EAP) 7.1.4 |
|  | | IBM® Content Manager Server 8.5 - Pacote de correções 2 |
|  | | Cliente do gerenciador de conteúdo IBM® 8.5 |
|  | | Microsoft® SQL Server 2016 |
|  | | Microsoft® Windows Server 2016 |

### Versão 6.5.10.0 (1 de setembro de 2022)

| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
| SDK do Java™ SE 11 (64 bits) do oracle para o servidor de aplicativos JBoss® EAP 7.4. | | [O Adobe Acrobat 2017 - Suporte principal para Adobe Acrobat 2017 termina em 6 de junho de 2022.](https://helpx.adobe.com/br/support/programs/eol-matrix.html) |
|  | | Red Hat® Enterprise Linux® 7 (Kernel 3.x) (64 bits) |
|  | | Microsoft® Windows Server 2016 (64 bits) |
|  | | Microsoft® Office 2016 |
|  | | OpenOffice 4.1.2 |


>[!NOTE]
>
As plataformas obsoletas continuarão a receber suporte até a próxima versão completa do instalador ou até que o suporte de fornecedores terceirizados para a plataforma chegue ao fim da vida útil, o que ocorrer primeiro.

<!-- 
- Oct 10, 2021

  - Changed supported version of iOS for AEM Forms App to iOS 15.1. The previous version was iOS 12.

- Sep 07, 2021
  - **Platform Updates**: [!DNL Adobe Experience Manager Forms] on JEE has added support for the following platforms:
    - [!DNL Adobe Acrobat 2020]
    - [!DNL Ubuntu 20.04]
    - [!DNL Open Office 4.1.10]
    - [!DNL Microsoft&reg;&reg; Office 2016]
    - [!DNL Microsoft&reg;&reg; Windows Server 2016]
    - [!DNL RHEL8]

- Dec 03, 2020
  - Support added with AEM Forms 6.5.7.0 or later for the following platform:
    - [!DNL Microsoft&reg;&reg; SQL Server 2019]

- Sep 09, 2020

    - Changed supported version of iOS for AEM Forms App to iOS 12. The previous version was iOS 11.

    -->

