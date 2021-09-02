---
title: Plataformas compatíveis com AEM Forms no JEE
seo-title: Supported Platforms for AEM Forms on JEE
description: Lista de componentes de infraestrutura necessários e compatíveis para instalar o AEM Forms no JEE
seo-description: List of infrastructure components required and supported for installing AEM Forms on JEE
uuid: 777f943b-4cb4-444e-a036-8032b9fce5be
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f777865e-d4a8-40ef-87b0-130c19eb1b91
docset: aem65
role: Admin
exl-id: 74d22cf4-56b2-48f5-92d9-928eaa134866
source-git-commit: f0caaaf72a75aff3099f4a9184653353639035e4
workflow-type: tm+mt
source-wordcount: '3458'
ht-degree: 1%

---

# Plataformas compatíveis com AEM Forms no JEE{#supported-platforms-for-aem-forms-on-jee}

## Plataformas compatíveis {#supported-platforms}

### Níveis de suporte {#support-levels}

O AEM Forms no servidor JEE pode ser configurado usando qualquer combinação de sistemas operacionais suportados, servidores de aplicativos, bancos de dados, drivers de banco de dados, JDK, servidores LDAP e servidores de email.

Este documento lista as plataformas de cliente e servidor compatíveis com o AEM Forms no JEE. O Adobe fornece vários níveis de suporte, tanto para as configurações recomendadas quanto para outras configurações. O documento também lista outros softwares suportados e suas versões, exceções, definições de patch e políticas de suporte a patches de software de terceiros.

>[!NOTE]
>
>* Para obter uma lista completa de exceções para plataformas de servidor compatíveis, consulte [Exceções para plataformas de servidor compatíveis](../../forms/using/aem-forms-jee-supported-platforms.md#p-exceptions-to-supported-server-platforms-p).
>* O AEM Forms no JEE é compatível somente com as versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos compatíveis.
>


### Configurações recomendadas {#recommendedconfigurations}

O Adobe recomenda essas configurações e oferece suporte total ou restrito como parte do contrato padrão de manutenção de software:

<table>
 <tbody>
  <tr>
   <th>Nível de suporte</th>
   <th>Descrição</th>
  </tr>
  <tr>
   <td>A: Suportado<br /> </td>
   <td>O Adobe oferece suporte e manutenção completos para essa configuração. Essa configuração é coberta pelo processo de garantia de qualidade do Adobe.</td>
  </tr>
  <tr>
   <td>R: Suporte restrito</td>
   <td>O Adobe fornece suporte total para essa configuração após atender a determinados pré-requisitos. Entre em contato com o suporte empresarial do Adobe para saber mais sobre os pré-requisitos e solicitar o suporte.</td>
  </tr>
  <tr>
   <td>L: Apoio limitado</td>
   <td>O Adobe oferece suporte e manutenção completos para essas configurações após determinados pré-requisitos serem atendidos. Nem todos os recursos estão disponíveis na configuração. Entre em contato com o suporte empresarial do Adobe para saber mais sobre os pré-requisitos e solicitar o suporte.<br /> </td>
  </tr>
 </tbody>
</table>

### Configurações não suportadas {#unsupported-configurations}

| Nível de suporte | Descrição |
|---|---|
| E: Espera-se que funcione | Espera-se que a configuração funcione, e não há relatórios em contrário. |
| Z: Não suportado | A configuração não é suportada. O Adobe não faz declarações sobre se a configuração funciona e não oferece suporte a ela. |

>[!NOTE]
>
>Para ajudar os clientes da AEM Forms a reduzir o custo de propriedade, simplificar a arquitetura de implantação e modernizar a pilha de desenvolvimento, a plataforma corporativa Adobe Experience Manager está se afastando das implantações baseadas em servidor de aplicativos em favor de implantações independentes baseadas em OSGi. O Adobe continua a oferecer suporte à pilha AEM Forms JEE com uma matriz reduzida de componentes de infraestrutura.
>
>Com o lançamento da versão 6.5, os componentes de infraestrutura que têm o menor uso entre nossos clientes não são mais suportados, como a seguir:
>・ Banco de dados IBM DB2
>・ Sistemas operacionais IBM AIX e Sun Solaris
>
>Para novas instalações, quando possível, é recomendável implantar o AEM Forms na pilha OSGi moderna para aproveitar as inovações mais recentes em relação à adaptável Forms para dispositivos móveis, comunicações interativas multicanais e integrações de dados de back-end usando o Modelo de dados de formulário.
>
>Reconhecemos que os usuários existentes precisam continuar implantando o AEM Forms na pilha JEE. Nesses cenários, o Adobe requer a implantação do AEM Forms JEE na infraestrutura compatível, conforme descrito nesta documentação. Se você estiver atualizando para o AEM 6.5 Forms e estiver usando uma plataforma não compatível na versão anterior do AEM Forms, entre em contato com o Suporte do Adobe para obter ajuda sobre como atualizar para uma plataforma compatível.

### Máquinas Virtuais Java (JVM) {#java-virtual-machines-jvm}

A Adobe Experience Manager Forms requer uma máquina virtual Java para execução, fornecida pela distribuição do Java Development Kit (JDK). A Adobe Experience Manager opera com as seguintes versões das máquinas virtuais Java:

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Nível de suporte</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Oracle Java™ SE 11 (64 bits)</p> </td>
   <td><p>Z: Não suportado</p> </td>
   <td><p> </p> </td>
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
   <td>IBM® J9 Virtual Machine (compilação 2.8, JRE 1.8.0)</td>
   <td>A: Suportado</td>
   <td>Versões e atualizações secundárias</td>
  </tr>
  <tr>
   <td>Máquina Virtual IBM® J9 (build 2.9, JRE 1.8.0)<br /> </td>
   <td>A: Suportado</td>
   <td>Versões e atualizações secundárias</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* É recomendável rastrear os Boletins de segurança do fornecedor do Java para garantir a segurança dos ambientes de produção e instalar as atualizações mais recentes do Java.
>* O AEM Forms no JEE suporta apenas JVMs de 64 bits em ambientes de produção.


### Bancos de dados e persistência de CRX {#databases-and-crx-persistence}

<table>
 <tbody>
  <tr>
   <td><p><strong>Plataforma</strong></p> </td>
   <td><p><strong> Descrição</strong></p> </td>
   <td><p><strong>Nível de suporte</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sistema de arquivos</p> </td>
   <td><p>Microkernel do Repositório (arquivos TAR MK)</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>MongoDB Enterprise 4.0 </p> </td>
   <td><p>Microkernel do Repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Oracle Database 12c Release 1</p> </td>
   <td><p>Microkernel do Repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
   <tr>
   <td><p>Oracle Database 12c Release 2 (12.2.0.1.0)</p> </td>
   <td><p>Microkernel do Repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td>Banco de Dados do Oracle 18c </td>
   <td>Microkernel do Repositório</td>
   <td>Compatível</td>
  </tr> 
   <tr>
   <td>Oracle Database 19c (edições Standard, Real Application Clusters (RAC) e Enterprise) </td>
   <td>Repositório Microkernal </td>
   <td>Compatível</td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2016</p> </td>
   <td><p>Microkernel do Repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td><p>Microsoft SQL Server 2019</p> </td>
   <td><p>Microkernel do Repositório</p> </td>
   <td><p>Compatível</p> </td>
  </tr>
  <tr>
   <td>IBM DB2 11.1</td>
   <td>Microkernel do Repositório</td>
   <td>R: Suporte restrito</td>
  </tr>
  <tr>
   <td>MySQL 5.7.35 </td>
   <td>-</td>
   <td>R: Suporte restrito</td>
  </tr>  
 </tbody>
</table>

* O IBM DB2 não é compatível com instalações novas. Ele é compatível somente com clientes existentes que atualizam para o AEM 6.5 Forms.
* O MongoDB é um software de terceiros e não está incluído no pacote de licenciamento AEM. Para obter mais informações, consulte a página [Política de licenciamento do MongoDB](https://www.mongodb.org/about/licensing/) .
* Para obter o máximo de sua implantação de AEM, o Adobe recomenda o licenciamento da versão MongoDB Enterprise para se beneficiar do suporte profissional.
* O Atendimento ao cliente do Adobe ajudará a solucionar problemas relacionados ao uso do MongoDB com AEM. Para obter mais informações, consulte a página [MongoDB para Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
* &#39;Sistema de Arquivos&#39; inclui armazenamento de bloco compatível com POSIX. Isso inclui a tecnologia de armazenamento de rede. Considere que o desempenho do sistema de arquivos pode variar e influencia o desempenho geral. É recomendável carregar AEM de teste em combinação com o sistema de arquivos remoto/de rede.
* Somente o MongoDB Storage Engine WiredTiger é compatível.
* A Partilha de MongoDB não é suportada no AEM.
* O AEM Forms no JEE não oferece suporte ao MySQL para persistência de RDBMK.
* O módulo Segurança de documento não usa o Repositório de conteúdo. Isso implica que, se você estiver usando apenas a Segurança de documento e não planeja usar o espaço de trabalho HTML, formulários HTML5 ou formulários adaptáveis, não instale o Repositório de conteúdo.
* O AEM Forms no JEE não oferece suporte ao uso do MySQL para Repositório AEM Persistente (CRX-Repository).


### Drivers de banco de dados {#database-drivers}

<table>
 <tbody>
  <tr>
   <th>Banco de dados </th>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td>MySQL</td>
   <td><p>MySQL Connector/J 5.7</p> <p>mysql-connector-java-5.1.44-bin.jar(versão 5.1.44)</p> </td>
   <td><p>Fornecido com AEM Forms na instalação JEE</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Driver JDBC do Microsoft® SQL Server 6.2.1.0<br /> </p> <p>sqljdbc6.jar</p> </td>
   <td><p>Fornecido com AEM Forms na instalação JEE.</p> </td>
  </tr>
  <tr>
   <td>Microsoft SQL Server<br /> </td>
   <td><p>Driver JDBC do Microsoft® SQL Server 8.2.2<br /> </p> <p>sqljdbc8.jar</p> </td>
   <td><p>Baixar do site da Microsoft.</p> </td>
  </tr>
  <tr>
   <td>Oracle</td>
   <td><p>Driver JDBC do Oracle Database 19.3.0.0.0</p> <p>ojdbc8.jar (versão 19.3.0.0.0)<br /> </p> </td>
   <td><p>Baixe de <a href="https://www.oracle.com/technetwork/database/features/jdbc/jdbc-ucp-122-3110062.html">Site do Oracle</a>.</p> </td>
  </tr>
 </tbody>
</table>

### Servidores de aplicativos {#application-servers}

<table>
 <tbody>
  <tr>
   <td><p><strong> Plataforma</strong></p> </td>
   <td><p><strong>Nível de suporte</strong></p> </td>
   <td><p><strong>Definições de patch compatíveis</strong></p> </td>
  </tr>
  <tr>
   <td>Oracle WebLogic Server 12.2.1 (12c R2)</td>
   <td>A: Suportado</td>
   <td>Service pack e atualizações críticas</td>
  </tr>
  <tr>
   <td>IBM® WebSphere® Application Server 9.0 <sup>[1] [4]</sup><br /> </td>
   <td>A: Suportado</td>
   <td>Service pack e atualizações críticas</td>
  </tr>
  <tr>
   <td><p>Plataforma de aplicativo empresarial (EAP) JBoss® 7.1.4 <sup>[2] [3] [7]</sup></p> </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Correções e correções cumulativas para a versão EAP compatível</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Os clusters IBM® WebSphere® são suportados apenas nas edições de implantação de rede.

### Sistemas operacionais para servidores {#server-operating-systems}

#### Ambientes de produção {#production-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong> Plataforma</strong></p> </th>
   <th><p><strong>Nível de suporte</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
   <tr>
   <td>Microsoft Windows Server 2019 (64 bits)</td>
   <td>A: Suportado</td>
   <td>Pacotes de serviços e atualizações críticas</td>
  </tr>
  <tr>
   <td>Ubuntu 20.04</td>
   <td>A: Suportado</td>
   <td>Pacotes de serviços e atualizações críticas</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server 2016 (64 bits) (obsoleto)</td>
   <td>A: Suportado</td>
   <td>Pacotes de serviços e atualizações críticas</td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 8 (Kernel 4.x) (64 bits)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Versões secundárias, atualizações cumulativas e atualizações críticas</p> </td>
  </tr>
  <tr>
   <td><p>Red Hat Enterprise Linux 7 (Kernel 3.x) (64 bits) (obsoleto)</td>
   <td><p>A: Suportado</p> </td>
   <td><p>Versões secundárias, atualizações cumulativas e atualizações críticas</p> </td>
  </tr>
  <tr>
   <td><p>SUSE® Linux® Enterprise Server 12 (64 bits)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Service packs, correções cumulativas e atualizações críticas de segurança</p> </td>
  </tr>
  <tr>
   <td>Oracle Linux® 7 Update 3 (64 bits)</td>
   <td>A: Suportado</td>
   <td>Service packs, correções cumulativas e atualizações críticas de segurança</td>
  </tr>
  <tr>
   <td>CentOS 7 (64 bits)<sup> [6]</sup></td>
   <td>A: Suportado</td>
   <td>Service packs, correções cumulativas e atualizações críticas de segurança</td>
  </tr>
 </tbody>
</table>

#### Ambiente virtualizado {#virtualized-environment}

Você pode executar o AEM Forms no JEE em uma máquina física ou em um ambiente virtual. No entanto, se você encontrar qualquer problema com o AEM Forms em um ambiente virtual, tente replicar o problema em uma máquina física. Se o problema persistir na máquina física, entre em contato com o Suporte do Adobe para obter uma resolução. Para os problemas que você não pode replicar em uma máquina física, entre em contato com o fornecedor do ambiente virtual.

#### Ambientes de desenvolvimento {#development-environments}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma (Versão básica)</strong></p> </th>
   <th>Nível de suporte</th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 de 64 bits</p> </td>
   <td>E: Espera-se que funcione</td>
   <td><p>Service pack e atualizações críticas</p> </td>
  </tr>
 </tbody>
</table>

### Exceções às plataformas de servidor suportadas {#exceptions-to-supported-server-platforms}

Considere as seguintes exceções ao escolher uma plataforma para configurar seu AEM Forms no servidor JEE.

1. O AEM Forms no JEE não é compatível com IBM® WebSphere® com MySQL.
1. A AEM Forms no JEE não oferece suporte e JBoss no SUSE Linux Enterprise Server 12. Somente o IBM WebSphere é compatível com o SUSE Linux Enterprise Server 12.
1. O AEM Forms no JEE não é compatível com nenhum JDK com JBoss® que não seja o Oracle Java™ SE.
1. O AEM Forms no JEE não suporta nenhum JDK com IBM® WebSphere® que não seja IBM® JDK.
1. O CRX-repository suporta persistência de tipo TarMK, MongoDB e bancos de dados relacionais (RDBMK). Não é possível ter dois sistemas de banco de dados diferentes entre o servidor de aplicativos e o repositório CRX. No entanto, em um ambiente AEM Forms no JEE, você pode usar o MongoMK com o repositório CRX e um banco de dados relacional compatível com o servidor de aplicativos.
1. O AEM Forms no JEE não é compatível com o servidor de aplicativos WebSphere no CentOS.
1. O AEM Forms no JEE não é compatível com o RBAC (controle de acesso baseado em função do JBoss).

Além disso, considere os seguintes pontos ao escolher o software para o Adobe AEM Forms em implantações JEE:

* O AEM Forms no JEE oferece suporte a atualizações, correções e pacotes de correções além da versão principal e secundária especificada do software suportado. No entanto, a atualização para a próxima versão principal ou secundária não é suportada, a menos que especificado.
* As instalações baseadas em cluster não oferecem suporte à persistência de TarMK. Para obter informações sobre a persistência suportada, consulte [Escolha de um tipo de persistência para uma instalação do AEM Forms](/help/forms/using/choosing-persistence-type-for-aem-forms.md).
* O AEM Forms no JEE é compatível com vários softwares de terceiros de acordo com a [Política de suporte de software de terceiros](../../forms/using/aem-forms-jee-supported-platforms.md#p-third-party-patch-support-policy-p).
* O AEM Forms no JEE oferece suporte a plataformas de acordo com o suporte fornecido por fornecedores terceirizados. Algumas combinações podem não ser permitidas por fornecedores terceirizados. Por exemplo, muitos fornecedores não certificaram seus servidores de aplicativos com o Oracle. Como resultado, o AEM Forms no JEE também não é compatível com essas combinações. Para garantir que você escolha as versões de software compatíveis, verifique também a matriz de suporte dos fornecedores de terceiros.
* O AEM Forms no JEE não é compatível com o TarMK Cold Standby.
* O AEM Forms no JEE não oferece suporte a clustering vertical.
* O AEM Forms no JEE não oferece suporte ao banco de dados MySQL em um ambiente em cluster.
* Para obter a lista de plataformas removidas ou atualizadas, consulte o documento [AEM 6.5 Resumo do novo recurso Forms](../../forms/using/whats-new.md).

### Servidores LDAP (opcional) {#ldap-servers-optional}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produto (Versão base)</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td>Oracle Unified Diretory (OUD) 11g Versão 2</td>
   <td>Service packs</td>
  </tr>
  <tr>
   <td>Microsoft Ative Diretory 2016</td>
   <td>Versão de manutenção e pacotes de correção</td>
  </tr>
  <tr>
   <td><p>IBM® Tivoli Diretory Server 6.4</p> </td>
   <td><p>Pacotes de recursos e correções provisórias</p> </td>
  </tr>
 </tbody>
</table>

### Servidores de email (opcional) {#email-servers-optional}

| Produto |
|---|
| IBM Lotus Domino 9.0 |
| Microsoft Exchange 2013 |
| Microsoft Office 365 |

### Gerentes de conteúdo e conectores correspondentes {#content-managers-and-corresponding-connectors}

<table>
 <tbody>
  <tr>
   <td><strong>Produto<br /> </strong></td>
   <td><strong>Versão</strong></td>
  </tr>
  <tr>
   <td>EMC Documentum</td>
   <td>7,3</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.2.</td>
  </tr>
  <tr>
   <td>IBM Filenet</td>
   <td>5.5.2</td>
  </tr>
  <tr>
   <td>Servidor IBM Content Manager</td>
   <td>8.5 Fix Pack 2</td>
  </tr>
  <tr>
   <td>Cliente IBM Content Manager</td>
   <td>8,5 </td>
  </tr>
  <tr>
   <td>Microsoft SharePoint</td>
   <td>2016<br /> </td>
  </tr>
 </tbody>
</table>

### Suporte para Cordova {#support-for-cordova}

O aplicativo AEM Forms agora é compatível com o Apache Cordova. A seguir estão as versões específicas da plataforma do Cordova que são compatíveis:

* Apache Cordova 6.4.0
* Cordova iOS 4.3.0
* Cordova Android 6.0.0
* Cordova Windows 4.4.3

### Suporte de software para o PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produto</strong></p> </th>
   <th><p><strong>Formatos compatíveis para conversão em PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2020 - </a> versão mais recente do rastreamento clássico</td>
   <td>XPS, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic </a> tracklversion mais recente (obsoleto)</td>
   <td>XPS, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 (Obsoleto)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2019<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 (Obsoleto)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 (Obsoleto)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2019<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016 (Obsoleto)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JP2, J2K, J2C, JPC), HTML, M, RTF e TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 (Obsoleto)</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JP2, J2K, J2C, JPC), HTML, M, RTF e TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
>O PDF Generator suporta apenas versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos compatíveis.
>
>Além disso:
>
>* O Gerador de PDF requer a versão de 32 bits de [Acrobat 2020 classic track version 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) para executar a conversão.
>* O PDF Generator suporta apenas a versão de varejo de 32 bits do Microsoft Office Professional Plus e outros softwares necessários para a conversão.
>* O PDF Generator não é compatível com o Microsoft Office 365.
>* As conversões do PDF Generator para OpenOffice são suportadas apenas no Windows e Linux.
>* Os recursos PDF, Optimize PDF e Export PDF do OCR são suportados apenas no Windows.
>* Uma versão do Acrobat é fornecida com o AEM Forms para ativar a funcionalidade do Gerador de PDF. A versão agrupada só deve ser acessada programaticamente com o AEM Forms, durante o período da licença do AEM Forms, para uso com o Gerador de PDF do AEM Forms. Para obter mais informações, consulte a descrição do produto AEM Forms de acordo com sua implantação ([No local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) ou [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
>
>* O serviço PDF Generator não é compatível com o Microsoft Windows 10.
>


### Exceções ao suporte de acessibilidade {#exceptions-to-accessibility-support}

Os seguintes subsistemas do AEM Forms não são compatíveis com [508](https://www.section508.gov/):

* Interface adaptável de criação do Forms
* Interface do usuário de criação do Forms Manager
* Interface do usuário de criação do Gerenciamento de correspondência
* Interface do usuário do administrador (interface do usuário do Console de administração)

## Requisitos de sistema para AEM Forms no JEE {#system-requirements-for-aem-forms-on-jee}

### Requisitos mínimos de hardware {#minimum-hardware-requirements}

<table>
 <tbody>
  <tr>
   <td>Plataforma</td>
   <td>Requisito mínimo de hardware</td>
  </tr>
  <tr>
   <td>Microsoft Windows Server</td>
   <td>Intel® Xeon® E5-2680, processador de 2,4 GHz ou equivalente<br /> VMWare ESX 5.1 ou posterior<br /> RAM: 6 GB (SO de 64 bits com JVM de 64 bits)<br /> Espaço livre em disco: 15 GB de espaço temporário mais 22 GB<br /> para AEM Forms no JEE</td>
  </tr>
  <tr>
   <td>SUSE Linux Enterprise Server</td>
   <td>Intel Xeon E5-2670v2, 1 vCPU, processador de 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM: 6 GB (SO de 64 bits com JVM de 64 bits)<br /> Espaço livre em disco: 6 GB de espaço temporário mais 22 GB<br /> para AEM Forms no JEE</td>
  </tr>
  <tr>
   <td>Red Hat Enterprise Linux</td>
   <td>Intel Xeon E5-2670v2, 1 vCPU, processador de 2,5 GHz<br /> AWS m3.medium (3 ECUs)<br /> RAM: 6 GB (SO de 64 bits com JVM de 64 bits)<br /> Espaço livre em disco: 6 GB de espaço temporário mais 22 GB<br /> para AEM Forms no JEE<br /> </td>
  </tr>
  <tr>
   <td>Requisitos de hardware para um pequeno ambiente de produção</td>
   <td>
    <ul>
     <li><strong>Ambiente</strong> alimentado pela Intel: Intel® Xeon® E5-2680, 2,4 GHz ou superior. O uso de um processador dual core melhora ainda mais o desempenho</li>
     <li><strong>Memória:  </strong>4 GB  <br /> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

Para obter requisitos adicionais, consulte:

* [Requisitos de sistema para um AEM Forms de servidor único na implantação do JEE](https://www.adobe.com/go/learn_aemforms_sysreq_single_63)
* [Requisitos de sistema para um AEM Forms em cluster na implantação JEE](https://www.adobe.com/go/learn_aemforms_sysreq_cluster_63)

## Clientes compatíveis com AEM Forms no JEE {#supported-clients-for-aem-forms-on-jee}

### Workbench {#workbench}

<table>
 <tbody>
  <tr>
   <th><p><strong>Plataforma</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft® Windows® 10 (Enterprise, Pro, Basic)</p> <p>Versão de 32 bits ou 64 bits</p> <p> </p> </td>
   <td>Pacotes de serviços e atualizações críticas</td>
  </tr>
  <tr>
   <td>Servidor Microsoft® Windows® 2016 (TBD)</td>
   <td>Pacotes de serviços e atualizações críticas</td>
  </tr>
 </tbody>
</table>

* Espaço em disco para instalação: 1,7 GB apenas para Workbench, 2,7 GB em uma única unidade para uma instalação completa do Workbench, do Designer e o conjunto de amostras de 400 MB para diretórios de instalação temporários - 200 MB no diretório temporário do usuário e 200 MB no diretório temporário do Windows. Se todos esses locais residirem em uma única unidade, deverá haver 1,5 GB de espaço disponível durante a instalação. Os arquivos copiados para os diretórios temporários são excluídos quando a instalação é concluída.

* Memória para executar o Workbench: 2 GB de RAM
* Requisito de hardware: Processador Intel® Pentium® 4 ou AMD equivalente, 1 GHz
* Resolução mínima do monitor de 1024 X 768 pixels ou superior com cor de 16 bits ou superior
* Conexão de rede TCP/IPv4 ou TCP/IPv6 ao AEM Forms no servidor JEE
* Você deve ter privilégios Administrativos para instalar o Workbench no Windows. Se você estiver instalando usando uma conta que não seja de administrador, o instalador solicitará as credenciais de uma conta apropriada.

### Designer {#designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server ou Microsoft® Windows® 10
* Processador de 1 GHz ou mais rápido com suporte para PAE, NX e SSE2.
* 1 GB de RAM para 32 bits ou 2 GB de RAM para SO de 64 bits
* 16 GB de espaço em disco para 32 bits ou 20 GB de espaço em disco para SO de 64 bits
* Memória gráfica - 128 MB de GPU (256 MB recomendados)
* 2,35 GB de espaço disponível em disco rígido
* Resolução do monitor de 1024 X 768 pixels ou superior
* Aceleração de hardware de vídeo (opcional)
* Acrobat Pro DC, Acrobat Standard DC ou Adobe Acrobat Reader DC.
* Privilégios administrativos para instalar o Designer.

### Adobe Acrobat e Adobe Reader {#adobe-acrobat-and-adobe-reader}

<table>
 <tbody>
  <tr>
   <th><p><strong>Acrobat e Adobe Reader (Base)</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td>Acrobat 2020 (rastreamento clássico)</td>
   <td>Versão 20.004.30006 ou posterior<br /> </td>
  </tr>
  <tr>
   <td>Acrobat 2017 (rastreamento clássico) (obsoleto)</td>
   <td>Versão 17.011.30078 ou posterior<br /> </td>
  </tr>

</tbody>
</table>

>[!NOTE]
>
>A família de produtos Acrobat DC apresenta duas trilhas para Acrobat e Reader, que são essencialmente produtos diferentes: &quot;Classic&quot; e &quot;Continuous.&quot; Para obter detalhes e uma comparação das duas faixas, consulte [https://www.adobe.com/go/acrobatdctracks.](https://www.adobe.com/go/acrobatdctracks)

### Navegadores {#browsers}

#### Desktops {#desktops}

<table>
 <tbody>
  <tr>
   <th><p><strong>Navegador (Base)</strong></p> </th>
   <th><p><strong>Nível de suporte</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Microsoft Edge (Evergreen)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td><p>Service packs e atualizações</p> </td>
  </tr>
  <tr>
   <td><p>Mozilla Firefox (Evergreen)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td>Todas as atualizações</td>
  </tr>
  <tr>
   <td>Microsoft Firefox ESR</td>
   <td>E: Espera-se que funcione</td>
   <td> Todas as atualizações</td>
  </tr>
  <tr>
   <td><p>Google Chrome (Evergreen)</p> </td>
   <td><p>A: Suportado</p> </td>
   <td>Todas as atualizações</td>
  </tr>
  <tr>
   <td>Google Chrome e Firefox no MAC OS X</td>
   <td>A: Suportado<br /> <br /> </td>
   <td>Todas as atualizações</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x</td>
   <td>A: Suportado</td>
   <td>Todas as atualizações</td>
  </tr>
  <tr>
   <td>Apple Safari 12.x<br /> <br /> </td>
   <td>A: Suportado</td>
   <td>Todas as atualizações</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Algumas exceções relacionadas ao navegador para desktops são as seguintes:
>
>* A maioria dos navegadores modernos não suporta mais plug-ins com base NPAPI. Para obter informações sobre como isso afeta os aplicativos e workflows do AEM Forms, consulte [Descontinuação dos plug-ins do navegador NPAPI e seu impacto](https://helpx.adobe.com/aem-forms/kb/discontinuation-of-npapi-plugins-impact-on-aem-forms.html).
>* O Safari é compatível somente no Macintosh OS X.
>* O Workspace é compatível com o Safari 5.1 no Macintosh OS X 10.6 e 10.7 com o Acrobat DC ou versões posteriores. Para obter mais informações sobre a compatibilidade do Safari 5.1 com o Adobe Reader, Acrobat, consulte [https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html](https://helpx.adobe.com/x-productkb/multi/safari-5-1-incompatible-reader.html).
>* O Console de administração não é compatível com o Safari.
>* O Gerenciamento de correspondência não é compatível com o Windows® Internet Explorer 9.0 para formulários AEM 6.1.
>* O portal Forms oferece suporte ao software de leitor de tela JAWS 14.0 no Internet Explorer 11 para acessibilidade.
>


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
   <td>Safari no iOS 11.0 e superior</td>
   <td>Todas as atualizações</td>
  </tr>
  <tr>
   <td>Microsoft Edge<br /> </td>
   <td>Todas as atualizações<br /> </td>
  </tr>
  <tr>
   <td>Navegador Android nativo no Android™ 4.4 e superior</td>
   <td>Todas as atualizações</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* O Forms Portal é compatível somente com o Safari no iPad.
>


### Aplicativo AEM Forms {#aem-forms-workspace-app}

#### Suporte a dispositivo móvel {#mobile-device-support}

O aplicativo AEM Forms está disponível nas seguintes plataformas:

| **Plataforma** | **Dispositivos compatíveis** |
|---|---|
| Apple iOS | Apple iPhone, iPad, iPad Air e iPad mini executando iOS 12 e superior. |
| Google Android | Android 5.1 e superior. O aplicativo AEM Forms é certificado em tablets Samsung Galaxy de 7 e 10 polegadas e smartphones populares. |
| Microsoft Windows | Dispositivos, tablets, laptops e desktops Microsoft Surface que executam o sistema operacional Microsoft Windows 10. |

### Flash Player Adobe {#adobe-flash-player}

<table>
 <tbody>
  <tr>
   <th><p><strong>Flash Player (Base)</strong></p> </th>
   <th><p><strong>Definições de patch compatíveis</strong></p> </th>
  </tr>
  <tr>
   <td><p>Versão mais recente do Flash Player</p> </td>
   <td><p>Versões e atualizações secundárias</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O Adobe interromperá a atualização e distribuirá o Flash Player no final de 2020](https://theblog.adobe.com/adobe-flash-update/).[

### Extensão de Segurança de Documento do Adobe para Microsoft Office {#adobe-rights-management-extension-for-microsoft-office}

Clique [aqui](https://www.adobe.com/br/products/livecycle/rightsmanagement/extension/downloads.html) para ver os requisitos do sistema para a Extensão de Segurança de Documentos do Adobe para Microsoft® Office.

### Exceções ao suporte ao cliente {#exceptions-to-client-support}

O AEM Forms no JEE oferece suporte a atualizações, correções e pacotes de correções além da versão principal e secundária especificada do software suportado. No entanto, a atualização para a próxima versão principal ou secundária não é suportada, a menos que especificado.

## Política de suporte de patch de terceiros {#third-party-patch-support-policy}

Os requisitos de software de terceiros para o AEM Forms no JEE estão documentados na seção &quot;Requisitos do sistema&quot; de seus respectivos documentos de produto. Toda a documentação pode ser acessada em [https://adobe.com/go/learn_aemforms_documentation_65](https://adobe.com/go/learn_aemforms_documentation_65) .

As plataformas de referência de terceiros da AEM Forms no JEE indicam o nível de patch específico da infraestrutura de terceiros que estava atual durante o desenvolvimento e o lançamento do AEM Forms no JEE e a partir do nível mínimo de patch/service pack da infraestrutura compatível com essa versão do AEM Forms no JEE.

O Adobe oferece suporte a patches urgentes ou recomendados emitidos por fornecedores terceirizados após sua liberação, supondo que fornecedores terceirizados garantam compatibilidade retroativa com as versões compatíveis com o AEM Forms no JEE. O Adobe só oferecerá suporte a patches lançados após o nível mínimo de patch indicado na documentação AEM Forms no JEE.

Em alguns casos, o Adobe não oferece suporte a atualizações de terceiros que alteram funcionalidades importantes e, portanto, não oferecem suporte para compatibilidade com versões anteriores. Para obter detalhes sobre as atualizações compatíveis, consulte [Definições de patch compatíveis](https://helpx.adobe.com/aem-forms/aem-forms-third-party-software-patch.html) para produtos de fornecedor específicos e os tipos de patch suportados pelo Adobe.

Sob circunstâncias fora do controle do Adobe, os patches de terceiros que reivindicam compatibilidade com versões anteriores podem ter impacto negativo nos produtos do Adobe ou nos ambientes do cliente. Nesses casos, a Adobe recomenda que os clientes avaliem o impacto de qualquer patch urgente de terceiros antes de aplicá-los a sistemas críticos. A Adobe trabalhará com terceiros usando esforços comerciais razoáveis para resolver esses problemas, seja por meio de programas normais de suporte a Adobe ou por terceiros corrigindo o problema em seu patch. Isso não garante que um patch de terceiros recém-lançado que será suportado pelo Adobe funcione conforme documentado pelo fornecedor ou com o AEM Forms no JEE.

O Adobe reserva o direito de alterar as plataformas de referência de terceiros compatíveis com uma versão do AEM Forms no JEE e suas definições de patch compatíveis em qualquer ponto determinado.

Informações adicionais sobre patches de terceiros também podem ser encontradas pesquisando artigos da base de conhecimento relacionados ao seu produto no site de Suporte Adobe Enterprise.

## Atualizações da plataforma {#platform-updates}

As seguintes plataformas são marcadas como obsoletas na versão 6.5.10.0 do AEM Forms em 2 de setembro de 2021:

* Adobe Acrobat 2017 - [O suporte principal para Adobe Acrobat 2017 termina em 6 de junho de 2022](https://helpx.adobe.com/br/support/programs/eol-matrix.html).

* Microsoft Windows Server 2016 (64 bits)

* Red Hat Enterprise Linux 7 (Kernel 3.x) (64 bits)

* Microsoft® Office 2016

* OpenOffice 4.1.2

>[!NOTE]
>
>As plataformas marcadas como [obsoletas permanecem compatíveis até o AEM Forms 6.5 Service Pack 15 (6.5.15.0), versão](https://helpx.adobe.com/support/programs/eol-matrix.html).



## Histórico de revisão {#revision-history}

* 09 de setembro de 2020
   * Alteração da versão compatível do iOS para aplicativo AEM Forms para iOS 12. A versão anterior era iOS 11.
