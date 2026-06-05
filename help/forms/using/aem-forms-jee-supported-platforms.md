---
title: Plataformas compatíveis com AEM Forms no JEE
description: Lista de componentes de infraestrutura necessários e compatíveis para a instalação do AEM Forms no JEE
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE,Platform Matrix
source-git-commit: ca3f909f4085537a085fd4c8d92f4dcef66f1cab
workflow-type: tm+mt
source-wordcount: '3839'
ht-degree: 1%

---



# Plataformas compatíveis com AEM Forms no JEE {#supported-platforms-for-aem-forms-on-jee}


## Plataformas compatíveis {#supported-platforms}


<div class="preview">

A Adobe lançou um [instalador completo](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) com o AEM 6.5.23.0 Forms Service Pack 23 (6.5.23.0) no JEE, juntamente com os instaladores de patch. O instalador completo oferece suporte a novas plataformas, enquanto o instalador de patch inclui apenas correções de erros.

Se você estiver executando uma nova instalação ou planejando usar o software mais recente para o seu ambiente AEM 6.5.23.0 Forms no JEE, a Adobe recomenda usar o [AEM 6.5.23.0 Forms no instalador completo do JEE](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) lançado em 06 de junho de 2025 em vez do instalador do AEM 6.5.18 Forms lançado em 31 de agosto de 2023 ou do AEM 6.5.12 Forms Installer lançado em 08 de abril de 2019.


</div>


### Níveis de suporte {#support-levels}


O AEM Forms no servidor JEE pode ser configurado usando qualquer combinação de sistemas operacionais, servidores de aplicativos, bancos de dados, drivers de banco de dados, JDK, servidores LDAP e servidores de email compatíveis.


Este documento lista as plataformas de cliente e servidor compatíveis com o AEM Forms no JEE. O Adobe fornece vários níveis de suporte, tanto para configurações recomendadas do Adobe quanto para outras configurações. O documento também lista outros softwares compatíveis e suas versões, exceções, definições de patch e política de suporte a patches de software de terceiros.


>[!NOTE]
>
>- Para obter uma lista completa de exceções para plataformas de servidor compatíveis, consulte [Exceções para plataformas de servidor compatíveis](#exceptions-to-supported-server-platforms).
>- O AEM Forms no JEE é compatível apenas com as versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos compatíveis.

### Política de atualização e suporte

#### Instalador completo

- **Suporte à atualização para instaladores completos**: um instalador completo é lançado a cada sexta versão do AEM Service Pack. Por exemplo, havia um instalador completo lançado com 6.5.12.0 e 6.5.18.0 versões do SP. O AEM Forms permite atualizações diretas exclusivamente dos dois últimos instaladores completos. Por exemplo, o AEM Forms facilita atualizações diretas para a versão 6.5.23.0 somente dos dois últimos instaladores completos, ou seja, 6.5.18.0 e 6.5.12.0. Se precisar fazer upgrade de um upgrade anterior, você pode usar um upgrade multi-hop para primeiro acessar uma versão completa do instalador com suporte e, em seguida, a versão mais recente.

- **Descontinuação**: o suporte à plataforma é atualizado com cada versão completa do instalador. Qualquer software marcado como obsoleto na matriz de plataformas pode ser removido das plataformas suportadas nas versões subsequentes ou quando o software chegar ao fim do suporte.

#### Service Packs


- **Cobertura de Service Pack**: a Adobe fornece suporte técnico para ambientes AEM Forms usando qualquer um dos seis service packs mais recentes. Se sua versão atual for anterior aos últimos seis service packs, a Adobe recomenda que você atualize para a versão mais recente a fim de obter desempenho ideal, segurança e suporte contínuo.

- **Diretrizes de Atualização de Patch**: Ao usar os instaladores de patch para atualizar, é crucial verificar se a versão subjacente do instalador completo não tem mais do que duas versões antigas. Por exemplo, durante a instalação do service pack 6.5.23.0, verifique se a versão subjacente do instalador completo é 6.5.18.0 ou 6.5.12.0.

<!--
- **Patch Upgrade Support**: You can upgrade from an older service pack to a newer one (for example, from 6.5.18.0 to 6.5.23.0) using the patch installer, as long as the destination platform (OS, JDK, application server, etc.) is supported by the newer service pack.
-->

### Configurações recomendadas {#recommendedconfigurations}


A Adobe recomenda essas configurações e fornece suporte total ou restrito como parte do contrato padrão de manutenção de software:


<table>
<tbody>
 <tr>
  <th>Nível de compatibilidade</th>
  <th>Descrição</th>
 </tr>
 <tr>
  <td>A: Suportado<br /> </td>
  <td>A Adobe oferece suporte e manutenção completos para essa configuração. Essa configuração é coberta pelo processo de controle de qualidade da Adobe.</td>
 </tr>
 <tr>
  <td>R: Suporte restrito</td>
  <td>A Adobe fornece suporte total para essa configuração após o cumprimento de determinados pré-requisitos. Entre em contato com o suporte corporativo da Adobe para saber mais sobre os pré-requisitos e fazer uma solicitação para obter suporte.</td>
 </tr>
 <tr>
  <td>L: Suporte limitado</td>
  <td>A Adobe fornece suporte e manutenção completos para essa configuração após o cumprimento de determinados pré-requisitos. Nem todos os recursos estão disponíveis na configuração. Contate o suporte empresarial da Adobe para saber mais sobre os pré-requisitos e levantar uma solicitação de suporte.<br /> </td>
 </tr>
</tbody>
</table>


### Configurações não suportadas {#unsupported-configurations}


| Nível de compatibilidade | Descrição |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| E: A expectativa é funcionar | Espera-se que a configuração funcione e não há relatórios em contrário. |
| Z: Não suportado | A configuração não é compatível. A Adobe não faz nenhuma declaração sobre se a configuração funciona e não oferece suporte a ela. |


>[!NOTE]
>
>Para ajudar os clientes da AEM Forms a reduzir o custo de propriedade, simplificar a arquitetura de implantação e modernizar a pilha de desenvolvimento, a plataforma corporativa da Adobe Experience Manager está se afastando das implantações baseadas em servidor de aplicativos em favor das implantações independentes baseadas em OSGi. A Adobe continua a oferecer suporte à pilha do AEM Forms JEE com uma matriz reduzida de componentes de infraestrutura.
><br>>Com o lançamento do 6.5, os componentes de infraestrutura com uso mais baixo entre os clientes do Adobe não terão mais suporte, como mostrado a seguir:
>
> - banco de dados IBM® DB2®
> - Sistemas operacionais IBM® AIX® e Sun Solaris™
>
>
>Para novas instalações, quando viável, é recomendável implantar o AEM Forms na pilha OSGi moderna para usar as inovações mais recentes em torno do Adaptive Forms responsivo para comunicações móveis, comunicações interativas de vários canais e integrações de dados de back-end usando o Modelo de dados de formulário.
>
>A Adobe reconhece que os usuários existentes devem continuar a implantar o AEM Forms na pilha do JEE. Nesses cenários, o Adobe exige a implantação do AEM Forms JEE em uma infraestrutura compatível, conforme descrito nesta documentação. Se você estiver atualizando para o AEM 6.5 Forms e estiver usando uma plataforma não compatível na versão anterior do AEM Forms, entre em contato com o Suporte da Adobe para obter ajuda sobre como atualizar para uma plataforma compatível.

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
>- Rastreie os Boletins de segurança do fornecedor Java™ para garantir a segurança dos ambientes de produção e instalar as atualizações mais recentes do Java™.
>- O AEM Forms no JEE é compatível apenas com JVMs de 64 bits em ambientes de produção.

### Bancos de dados e persistência do CRX {#databases-and-crx-persistence}


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
  <td><p> MongoDB Enterprise 6.0 (obsoleto) </p> </td>
  <td><p>Microkernel do repositório</p> </td>
  <td><p>Compatível</p> </td>
 </tr>
 <tr>
  <td><p> MongoDB Enterprise 7.0 </p> </td>
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
  <td></td>
 </tr>
 <tr>
  <td><p>Microsoft® SQL Server 2019 (obsoleto) </p> </td>
  <td><p>Microkernel do repositório</p> </td>
  <td><p>Compatível</p> </td>
 </tr>
 <tr>
  <td><p>Microsoft® SQL Server 2022 </p> </td>
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
  <td>MySQL 8.0.27 (obsoleto) </td>
  <td>-</td>
  <td>R: Suporte restrito</td>
 </tr>
 <tr>
 <tr>
  <td>MySQL 8.4</td>
  <td>-</td>
  <td>R: Suporte restrito</td>
 </tr>
</tbody>
</table>


- O IBM® DB2® não é suportado para instalações novas. Ele é compatível somente com clientes existentes que estão atualizando para o AEM 6.5 Forms.
- MongoDB é um software de terceiros e não está incluído no pacote de licenciamento da AEM. Para obter mais informações, consulte [política de licenciamento do MongoDB](https://www.mongodb.org/about/licensing/).
- Para aproveitar ao máximo a implantação do AEM, a Adobe recomenda licenciar a versão MongoDB Enterprise para se beneficiar de suporte profissional.
@@ -242.187 +206.150 @@ O Adobe Experience Manager Forms requer uma máquina virtual Java™ para ser executada, com
- O módulo de Segurança de documentos não usa o Repositório de conteúdo. Isso implica que, se você estiver usando somente a Segurança de documentos e não planeja usar o HTML Workspace, formulários HTML5 ou formulários adaptáveis, não instale o Repositório de conteúdo.
- O AEM Forms no JEE não é compatível com o uso do MySQL para repositório AEM persistente (CRX-Repository).


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
  <td><p>MySQL Connector/J 5.7 (obsoleto)</p> </td>
  <td><p>Fornecido com o AEM Forms na instalação do JEE</p> </td>
 </tr>
 <tr>
  <td>MySQL</td>
  <td><p>Conector MySQL/J 8.4</p> </td>
  <td><p>Fornecido com o AEM Forms na instalação do JEE</p> </td>
 </tr>
 <tr>
  <td>Microsoft® SQL Server<br /> </td>
  <td><p>Driver JDBC do Microsoft® SQL Server 8.2.2 <br /> </p> <p>sqljdbc8.jar (obsoleto) </p> </td>
  <td><p>Download do site da Microsoft® na web.</p> </td>
 </tr>
 <tr>
  <td>Microsoft® SQL Server<br /> </td>
  <td><p>Driver JDBC do Microsoft® SQL Server 12.10.0 <br /> </p> <p>sqljdbc12.10.0.jar</p> </td>
  <td><p>Download do site da Microsoft® na web.</p> </td>
 </tr>
 <tr>
  <td>Oracle</td>
  <td><p>Driver JDBC do Oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (versão 19.3.0.0.0)<br /> </p> </td>
  <td><p>Baixar de <a href="https://www.oracle.com/database/technologies/appdev/jdbc-ucp-19c-downloads.html">Site da Oracle</a>.</p> </td>
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
  <td>IBM® WebSphere® Application Server 9.0.0.10 <sup>[1] [4]</sup><br /> </td>
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
>Os clusters do IBM® WebSphere® só são suportados nas edições de Implantação de rede.

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
  <td><p>Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bits) (obsoleto)</p> </td>
  <td><p>A: Suportado</p> </td>
  <td><p>Versões secundárias, atualizações cumulativas e atualizações críticas</p> </td>
 </tr>
 <tr>
  <td><p>Red Hat® Enterprise Linux® 9 (Kernel 5.x) (64 bits)</p> </td>
  <td><p>A: Suportado</p> </td>
  <td><p>Versões secundárias, atualizações cumulativas e atualizações críticas</p> </td>
 </tr>
 <tr>
  <td><p>SUSE® Linux® Enterprise Server 15 SP6 (64 bits) </p> </td>
  <td><p>A: Suportado</p> </td>
  <td><p>Service packs, patches cumulativos e atualizações críticas de segurança</p> </td>
 </tr>
 <tr>
  <td>Oracle Linux® 7 Atualização 3 (64 bits)</td>
  <td>A: Suportado</td>
  <td>Service packs, patches cumulativos e atualizações críticas de segurança</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
> Para servidores baseados em Linux®, as dependências de tempo de execução necessárias são:
>
> - glibc.x86_64 (2.17-196)
> - libX11.x86_64 (1.6.7-4)
> - zlib.x86-64 (1.2.7-17)
> - libxcb.x86_64 (1.13-1.el7)
> - libXau.x86_64 (1.0.8-2.1.el7)
> - glibc-locale.x86_64 ( 2.17 ou superior)
> - OpenSSL 3 (necessário no local padrão do SO).

Para instalação do OpenSSL 3: As bibliotecas libcrypto.so.3 e libssl.so.3 devem estar disponíveis no caminho da biblioteca padrão representado pela variável de ambiente LD_LIBRARY_PATH. Se estiverem instalados em um local não padrão, verifique se esse caminho foi adicionado a LD_LIBRARY_PATH antes de iniciar o servidor.

#### Ambiente virtualizado {#virtualized-environment}


Você pode executar o AEM Forms no JEE em uma máquina física ou em um ambiente virtual. No entanto, se você encontrar algum problema com o AEM Forms em um ambiente virtual, tente replicar o problema em uma máquina física. Se o problema persistir no computador físico, entre em contato com o Suporte da Adobe para obter uma resolução. Para os problemas que não podem ser replicados em uma máquina física, entre em contato com o fornecedor do ambiente virtual.


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
1. O AEM Forms no JEE não suporta JBoss® no SUSE® Linux® Enterprise Server 12. Somente o IBM® WebSphere® é suportado no SUSE® Linux® Enterprise Server 12.
1. O AEM Forms no JEE não suporta qualquer JDK com JBoss® além do Oracle Java™ SE.
1. O AEM Forms no JEE não suporta qualquer JDK com IBM® WebSphere® diferente do IBM® JDK.
1. O repositório do CRX oferece suporte à persistência do tipo TarMK, MongoDB e bancos de dados relacionais (RDBMK). Você não pode ter dois sistemas de banco de dados diferentes entre o servidor de aplicativos e o repositório do CRX. No entanto, em um ambiente AEM Forms no JEE, é possível usar o MongoMK com repositório do CRX e um banco de dados relacional compatível com o servidor de aplicativos.
@@ -432,12 +359,12 @@ Considere as seguintes exceções ao escolher uma plataforma para configurar seu AEM F
1. As versões do JDK posteriores à 1.8.0_281 não são compatíveis com o servidor WebLogic. (FORMS-8498)
1. O JDK 11.0.20 não é compatível com a instalação do AEM Forms no instalador do JEE. Somente o JDK 11.0.19 ou versões anteriores são compatíveis com a instalação do AEM Forms no instalador do JEE.

1. [!DNL Microsoft® Windows Server 2019] não dá suporte a [!DNL MySQL 5.7] e [!DNL JBoss® EAP 7.1], [!DNL Microsoft® Windows Server 2019] não dá suporte a instalações turnkey para [!DNL Experience Manager Forms Service Pack 6.5.10.0 and later]. (CQDOC-18312)


Além disso, considere os seguintes pontos ao escolher o software para Adobe AEM Forms em implantações JEE:


- Atualizações de suporte, patches e fix packs do AEM Forms no JEE sobre a versão principal e secundária especificada do software compatível. No entanto, não há suporte para a atualização para a próxima versão principal ou secundária, a menos que especificado.
- Instalações baseadas em cluster não dão suporte à persistência TarMK. Para obter informações sobre a persistência com suporte, consulte [Escolha de um tipo de persistência para uma instalação do AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
- O AEM Forms no JEE oferece suporte a vários softwares de terceiros de acordo com a [Política de suporte a software de terceiros](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p) da Adobe.
@@ -449,274 +376,219 @@ Além disso, considere os seguintes pontos ao escolher o software para o Adobe AEM

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
  <td>8.5 </td>
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

### Considerações para o PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produto</strong></p> </th>
   <th><p><strong>Formatos compatíveis com a conversão para o PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat Pro DC</a> (faixa contínua, versão mais recente)</td>
   <td>XPS, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML e HTM</td>
  </tr>

<tr>
   <td>Microsoft® Office 2024 Professional Plus, licenças de varejo e por volume</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>
   OpenOffice 4.1.15 </td>
   <td>
    ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF e TXT<br>

</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>- O PDF Generator suporta apenas as versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos compatíveis.
>- A PDF Generator exige uma build de 32 bits do Windows do Adobe Acrobat Pro DC (Continuous track, versão mais recente) para conversões nativas orientadas pela Acrobat e uma build de 32 bits do Microsoft® Office Professional Plus para conversões baseadas no Office no Microsoft® Windows. Ative o Acrobat por meio do Feature Restricted Licensing (FRL) ou do processo de implantação corporativa do Adobe; consulte [Instalar o Adobe Acrobat Pro DC](install-configure-document-services.md#install-adobe-acrobat-pro-dc) no artigo de instalação de serviços de documento.
>- A instalação do Microsoft® Office Professional Plus pode usar o licenciamento por volume baseado em Varejo ou MAK/KMS/AD.
>- Se a instalação do Microsoft® Office se tornar desativada ou não licenciada por qualquer motivo, como uma instalação com licença de volume que não consegue localizar um host KMS em um período especificado, as conversões podem falhar até que a instalação seja relicenciada e reativada.
>- A PDF Generator não oferece suporte ao Microsoft® Office 365.
>- As conversões do PDF Generator para OpenOffice são suportadas no Windows e no Linux®.
>- Os recursos OCR PDF, Otimizar PDF e Export PDF são suportados apenas no Windows.
>- A PDF Generator não oferece suporte ao Microsoft® Windows 11.
>- O suporte ao Microsoft® Office 2021 Professional Plus está obsoleto.

<!--
Removed lines: >- PDF Generator fails to convert files using Microsoft&reg; Visio 2019. You can continue to use Microsoft&reg; Visio 2016 to convert .VSD and .VSDX files.
>- PDF Generator fails to convert files using Microsoft&reg; Project 2019. You can continue to use Microsoft&reg; Project 2016 to convert .MPP files.
-->

### Exceções ao suporte de acessibilidade {#exceptions-to-accessibility-support}


Os seguintes subsistemas do AEM Forms não são compatíveis com [508](https://www.section508.gov/):


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
  <td>Intel Xeon® E5-2670v2, 1 vCPU, processador de 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM: 6 GB (SO de 64 bits com JVM de 64 bits)<br /> Espaço livre em disco: 6 GB de espaço temporário mais 22 GB<br /> para AEM Forms no JEE</td>
 </tr>
 <tr>
  <td>Red Hat® Enterprise Linux®</td>
  <td>Intel Xeon® E5-2670v2, 1 vCPU, processador de 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM: 6 GB (SO de 64 bits com JVM de 64 bits)<br /> Espaço livre em disco: 6 GB de espaço temporário mais 22 GB<br /> para AEM Forms no JEE<br /> </td>
 </tr>
 <tr>
  <td>Requisitos de hardware para um ambiente de produção pequeno</td>
  <td>
   <ul>
    <li><strong>Ambiente equipado com Intel®</strong>: Intel Xeon® E5-2680, 2,4 GHz ou superior. O uso de um processador dual core melhora ainda mais o desempenho</li>
    <li><strong>Memória: </strong>4 GB <br /> </li>
   </ul> </td>
 </tr>
</tbody>
</table>


Para requisitos adicionais, consulte:

- [Requisitos de sistema para um AEM Forms de servidor único na implantação do JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_65)
- [Requisitos de sistema para um AEM Forms em cluster na implantação do JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_65)


### Adobe Acrobat e Adobe Reader {#adobe-acrobat-and-adobe-reader}


<table>
<tbody>
 <tr>
  <th><p><strong>Acrobat e Adobe Reader (Base)</strong></p> </th>
  <th><p><strong>Definições de patch compatíveis</strong></p> </th>
 </tr>
 <tr>
  <td>Adobe Acrobat Pro DC (Continuous track, versão mais recente)</td>
  <td>Última versão, conforme descrito nas <a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">notas de versão do Acrobat e do Reader</a><br /> </td>
 </tr>
 </tbody>
</table>


>[!NOTE]
>
>O Adobe Acrobat 2020 (faixa clássica) não é compatível com o AEM Forms. Use o Adobe Acrobat Pro DC (Continuous track, versão mais recente).
>
>A família de produtos do Acrobat DC apresenta duas faixas para o Acrobat e o Reader, que são produtos diferentes: &quot;Clássico&quot; e &quot;Contínuo&quot;. Para obter detalhes e uma comparação das duas faixas, consulte [https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html](https://www.adobe.com/devnet-docs/acrobatetk/tools/AdminGuide/whatsnewdc.html).

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


- Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server, Microsoft® Windows® 10 ou Windows® 11
- 1 GHz ou mais rápido com suporte para PAE, NX e SSE2.
- 1 GB de RAM para 32 bits ou 2 GB de RAM para SO de 64 bits
@@ -729,49 +601,45 @@ Para requisitos adicionais, consulte:
- Privilégios administrativos para instalar o Designer
- Microsoft® Visual C++ 2019 (VC 14.28 ou superior) tempo de execução de 32 bits


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
>Algumas exceções relacionadas ao navegador para desktops são as seguintes:
>
>- O Gerenciamento de correspondência não é compatível com o Windows® Internet Explorer 9.0 para formulários do AEM 6.1.
>- O Forms Portal oferece suporte ao software de leitor de tela JAWS 14.0 no Internet Explorer 11 para acessibilidade.

#### Clientes móveis {#mobile-clients}


<table>
<tbody>
 <tr>
  <th><p><strong>Navegador (Base)</strong></p> </th>
  <th><p><strong>Definições de patch compatíveis</strong></p> </th>
 </tr>
 <tr>
  <td><p>Chrome no Android™ 4.1.2 e superior</p> </td>
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
  <td>Navegador Android™ nativo no Android™ 4.4 e superior</td>
  <td>Todas as atualizações</td>
 </tr>
</tbody>
</table>


>[!NOTE]
>
>- O Forms Portal é compatível com o Safari somente no iPad.

### aplicativo AEM Forms {#aem-forms-workspace-app}


#### Suporte a dispositivo móvel {#mobile-device-support}

O aplicativo AEM Forms está disponível nas seguintes plataformas:

| **Plataforma** | **Dispositivos com suporte** |
| ----------------- | ------------------------------------------------------------------------------------------------------------------- |
| Apple iOS | Apple iPhone, iPad, iPad Air e iPad mini executando o iOS 15.1 e superior. |
| Google Android™ | Android™ 5.1 e superior. O aplicativo AEM Forms é certificado em tablets Samsung Galaxy de 7 e 10 polegadas e smartphones populares. |
| Microsoft® Windows | Dispositivos Microsoft® Surface, tablets, laptops e desktops com o sistema operacional Microsoft® Windows 10. |


### Adobe Document Security Extension for Microsoft® Office {#adobe-rights-management-extension-for-microsoft-office}


Clique [aqui](https://www.adobe.com/br/products/livecycle/rightsmanagement/extension/downloads.html) para ver os requisitos de sistema do Adobe Document Security Extension for Microsoft® Office.


### Exceções ao suporte ao cliente {#exceptions-to-client-support}


Atualizações de suporte, patches e fix packs do AEM Forms no JEE sobre a versão principal e secundária especificada do software compatível. No entanto, não há suporte para a atualização para a próxima versão principal ou secundária, a menos que especificado.


## Política de suporte a patches de terceiros {#third-party-patch-support-policy}


Os requisitos de software de terceiros para o AEM Forms no JEE estão documentados na seção &quot;Requisitos do sistema&quot; dos respectivos documentos do produto. Acesse toda a documentação de [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65).


A AEM Forms nas plataformas de referência de terceiros do JEE especifica o nível de patch específico da infraestrutura de terceiros que estava em vigor durante o desenvolvimento e o lançamento do AEM Forms no JEE e a partir do nível mínimo de patch/service pack da infraestrutura compatível com essa versão do AEM Forms no JEE.


A Adobe oferece suporte a patches urgentes ou recomendados emitidos por fornecedores terceirizados após o lançamento, supondo que esses fornecedores garantam compatibilidade com versões anteriores compatíveis com o AEM Forms no JEE. O Adobe só oferecerá suporte a patches lançados após o nível mínimo de patch declarado na documentação do AEM Forms no JEE.


Às vezes, o Adobe não é compatível com atualizações de terceiros que alteram a funcionalidade principal e, portanto, não é compatível com versões anteriores completas. Para obter detalhes sobre as atualizações com suporte, consulte [Definições de patch com suporte](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) para produtos de fornecedores específicos e os tipos de patch para os quais a Adobe oferece suporte.


Em circunstâncias fora do controle da Adobe, patches de terceiros que alegam compatibilidade com versões anteriores podem ter impacto negativo nos produtos da Adobe ou nos ambientes dos clientes. Nesses casos, a Adobe recomenda que os clientes avaliem o impacto de qualquer patch urgente de terceiros antes de aplicá-los a sistemas críticos. A Adobe trabalha com terceiros usando esforços razoáveis dos negócios para resolver esses problemas, seja por meio de programas normais de suporte da Adobe ou por terceiros que corrijam o problema na correção. Isso não garante que um patch de terceiros recém-lançado compatível com o Adobe funcione conforme documentado pelo fornecedor ou com o AEM Forms no JEE.


A Adobe se reserva o direito de alterar as plataformas de referência de terceiros compatíveis com uma versão do AEM Forms no JEE e suas definições de patch compatíveis em qualquer ponto específico.


Informações adicionais sobre patches de terceiros também podem ser encontradas no site de suporte do Adobe Enterprise para obter artigos da base de conhecimento relacionados ao seu produto.

Para qualquer consulta relacionada a formatos ou versões de plataforma compatíveis, entre em contato com o [suporte da AEM Forms](https://business.adobe.com/in/support/main.html)

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
### Release 6.5.23.0 (June 06, 2025)
| Added Support | Removed Support | Deprecated Support |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 7.0 |    MongoDB Enterprise 5.0 | MongoDB Enterprise 6.0 |
| MYSQL 8.4 |SUSE&reg; Linux&reg; Enterprise Server 12 (64-bit) | MYSQL 8.0.27 |
| Microsoft&reg; SQL Server 2022 | |Microsoft&reg; SQL Server 2019 |
| Microsoft&reg; SQL Server JDBC driver 12.8 | | Microsoft&reg; SQL Server JDBC driver 8.2 |
| Microsoft&reg; Office 2021 | | Microsoft&reg; Office 2019 |
| Red Hat&reg; Enterprise Linux&reg; 9 (Kernel 4.x) (64-bit) | |Red Hat&reg; Enterprise Linux&reg; 8 (Kernel 4.x) (64-bit)  |

-->

### Versão 6.5.24.0 (26 de novembro de 2025)

| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
| Microsoft® Office 2024 | | Microsoft® Office 2021 |
| Adobe Acrobat Pro DC (Continuous track, última versão) para PDF Generator e serviços de documento relacionados | Adobe Acrobat 2020 (faixa clássica) |  |

### Versão 6.5.23.0 (6 de junho de 2025)

| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
| MongoDB Enterprise 7.0 | MongoDB Enterprise 5.0 | MongoDB Enterprise 6.0 |
| MYSQL 8.4 | SUSE® Linux® Enterprise Server 12 (64 bits) | MYSQL 8.0.27 |
| Microsoft® SQL Server 2022 | Centos 7 | Microsoft® SQL Server 2019 |
| Driver JDBC do Microsoft® SQL Server 12.10.0 | Red Hat® Enterprise Linux® 7 (Kernel 4.x) (64 bits) | Driver JDBC do Microsoft® SQL Server 8.2 |
| Red Hat® Enterprise Linux® 9 (Kernel 5.x) (64 bits) | | Red Hat® Enterprise Linux® 8 (Kernel 4.x) (64 bits) |

### Versão 6.5.22.0 (29 de novembro de 2024)


| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
| SUSE® Linux® Enterprise Server 15 SP6 (64 bits) | |  |

### Versão 6.5.21.0 (13 de junho de 2024)

| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
| Microsoft® Office 2021 |  |  |

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
|  | Acrobat 2017 (faixa clássica) versão 17.011.30078 ou posterior |  |

### Versão 6.5.13.0 (2 de junho de 2022)


| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
|  |  | Microsoft® SharePoint 2016 |

### Versão 6.5.12.0 (3 de março de 2022)


| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
|  | Máquina virtual IBM® J9 (build 2.8, JRE 1.8.0) | MongoDB Enterprise 4.0 |
|  | | Microsoft® SQL Server 2016 |
|  | | Microsoft® Windows Server 2016 |

### Versão 6.5.10.0 (01 de setembro de 2022)


| Suporte adicionado | Suporte removido | Suporte obsoleto |
| -------------- | --------------- | ------------------- |
| Oracle Java™ SE 11 (64 bits) SDK para servidor de aplicativos JBoss® EAP 7.4. | | [O Adobe Acrobat 2017 - Suporte principal para Adobe Acrobat 2017 termina em 6 de junho de 2022.](https://helpx.adobe.com/br/support/programs/eol-matrix.html) |
|  | | OpenOffice 4.1.2 |

>[!NOTE]
>
> As plataformas obsoletas continuarão a receber suporte até a próxima versão completa do instalador ou até que o suporte de fornecedores terceirizados para a plataforma chegue ao fim da vida útil, o que ocorrer primeiro.

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