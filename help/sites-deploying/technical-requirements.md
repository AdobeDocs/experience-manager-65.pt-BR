---
title: Requisitos técnicos
seo-title: Requisitos técnicos
description: Uma lista das plataformas de cliente e servidor suportadas para AEM.
seo-description: Uma lista das plataformas de cliente e servidor suportadas para AEM.
uuid: 597f8fc1-9ac7-458d-a7c1-f576dd0f189b
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: platform
discoiquuid: 16c7a97d-884a-447e-9aad-18a2db1bda1d
docset: aem65
translation-type: tm+mt
source-git-commit: 7065a6b984afb18c188acd848b9b77da7da67749
workflow-type: tm+mt
source-wordcount: '3118'
ht-degree: 1%

---


# Requisitos técnicos{#technical-requirements}

O Adobe suporta Adobe Experience Manager (AEM) nas plataformas, conforme detalhado nas seguintes informações neste documento.

Para quaisquer problemas especificamente relacionados à plataforma, entre em contato com o fornecedor da plataforma.

>[!NOTE]
>
>Dependendo da plataforma na qual você instala o AEM, pode haver diferentes conjuntos de requisitos para o gerenciamento de usuários.

## Pré-requisitos {#prerequisites}

Requisitos mínimos para a instalação do Adobe Experience Manager:

* Plataforma Java instalada, JDK Standard Edition ou outras máquinas virtuais [Java suportadas](#java-virtual-machines)
* Arquivo Experience Manager Quickstart (JAR independente ou WAR de implantação de aplicativos da Web)

### Requisitos mínimos de dimensionamento {#minimum-sizing-requirements}

Requisitos mínimos para executar o Adobe Experience Manager:

* 5 GB de espaço livre em disco no diretório de instalação
* Memória de 2 GB

>[!NOTE]
>
>* Os casos de uso de ativos digitais precisam de mais memória básica. Consulte [Implantação e manutenção](/help/sites-deploying/deploy.md#default-local-install) para obter detalhes.
>* [O pacote](/help/forms/using/installing-configuring-aem-forms-osgi.md) complementar AEM Forms requer 15 GB de espaço temporário.

>



Para obter mais informações, consulte as Diretrizes [de dimensionamento de](/help/managing/hardware-sizing-guidelines.md)hardware.

### Níveis de suporte {#support-levels}

Este documento lista as plataformas de cliente e servidor suportadas para Adobe Experience Manager. O Adobe oferece vários níveis de suporte, tanto para configurações recomendadas quanto para outras configurações.

### Configurações suportadas {#supported-configurations}

A Adobe recomenda essas configurações e oferece suporte total como parte do contrato de manutenção de software padrão.

<table>
 <tbody>
  <tr>
   <td>Nível de suporte</td>
   <td>Descrição<br /> </td>
  </tr>
  <tr>
   <td><strong>A: Suportado</strong></td>
   <td>O Adobe oferece suporte e manutenção completos para essa configuração. Esta configuração é coberta pelo processo de garantia de qualidade do Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: Suporte restrito</strong></td>
   <td>Para garantir o sucesso do projeto de nossos clientes, o Adobe oferece suporte total dentro de um programa de suporte restrito, o que exige que condições específicas sejam atendidas. O suporte de nível R requer uma solicitação formal do cliente e uma confirmação por Adobe. Para obter mais informações, entre em contato com o Atendimento ao cliente do Adobe.</td>
  </tr>
 </tbody>
</table>

### Configurações não suportadas {#unsupported-configurations}

| Nível de suporte | Descrição |
|---|---|
| **Z: Não suportado** | A configuração não é suportada. O Adobe não faz declarações sobre se a configuração funciona e não oferece suporte para ela. |

## Plataformas compatíveis {#supported-platforms}

### Máquinas virtuais Java {#java-virtual-machines}

O aplicativo requer uma máquina virtual Java para execução, fornecida pela distribuição do Java Development Kit (JDK).

A Adobe Experience Manager opera com as seguintes versões das máquinas virtuais Java:

>[!CAUTION]
>
>É recomendável rastrear os Boletins de segurança do fornecedor Java para garantir a segurança dos ambientes de produção e instalar as atualizações mais recentes do Java.

<table>
 <tbody>
  <tr>
   <td>Plataforma</td>
   <td>Nível de suporte</td>
  </tr>
  <tr>
   <td>JDK do Oracle Java SE 12 [1]</td>
   <td>Z: Não suportado </td>
  </tr>
  <tr>
   <td><strong>Oracle Java SE 11 JDK - 64 bits</strong></td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>JDK do Oracle Java SE 10 [1]</td>
   <td>Z: Não suportado </td>
  </tr>
  <tr>
   <td>JDK do Oracle Java SE 9 [1]</td>
   <td>Z: Não suportado</td>
  </tr>
  <tr>
   <td>Oracle Java SE 8 JDK - 64 bits</td>
   <td>A: Suportado [3]</td>
  </tr>
  <tr>
   <td>IBM J9 VM - compilação 2.9, JRE 1.8.0 [2]</td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>IBM J9 VM - compilação 2.8, JRE 1.8.0 [2]</td>
   <td>A: Suportado</td>
  </tr>
 </tbody>
</table>

1. O Oracle migrou para um modelo de &quot;Suporte de longo prazo&quot; (LTS) dos produtos Oracle Java SE. Java 9, Java 10, and Java 12 are non-LTS releases by Oracle (see [Oracle Java SE support roadmap](https://www.oracle.com/technetwork/java/eol-135779.html)). Para implantar AEM no ambiente de produção, o Adobe fornece suporte somente para as versões LTS do Java.

1. O IBM JRE só é compatível com o WebSphere Application Server.
1. O suporte e a distribuição do JDK do Oracle Java SE, incluindo todas as atualizações de manutenção das versões LTS além do final das atualizações públicas, serão suportados pela Adobe diretamente para todos os clientes AEM que usam a tecnologia Oracle Java SE. Consulte o suporte ao [Oracle Java para perguntas e respostas](assets/adobe-oracle-java-license-agreement.pdf) da Adobe Experience Manager para obter mais informações.

### Armazenamento e persistência {#storage-persistence}

Existem várias opções para implantar o repositório da Adobe Experience Manager. Consulte a lista a seguir para obter as tecnologias e opções de armazenamento suportadas.

| **Plataforma** | **Descrição** | **Nível de suporte** |
|---|---|---|
| **Sistema de arquivos com arquivos TAR** `[1]` | Repositório | A: Suportado |
| **Sistema de arquivos com o Datastore** `[1]` | Binários | A: Suportado |
| Armazenar binários em arquivos TAR no sistema de arquivos `[1]` | Binários | Z: Não suportado para produção |
| Amazon S3 | Binários | A: Suportado |
| Armazenamento Blob do Microsoft Azure | Binários | A: Suportado |
| MongoDB Enterprise 4.0 | Repositório | A: Suportado `[2, 3]` |
| MongoDB Enterprise 3.6 | Repositório | Z: Não suportado |
| MongoDB Enterprise 3.4 | Repositório | Z: Não suportado |
| IBM DB2 10.5 | Banco de dados do Repository &amp; Forms | R: Suporte restrito `[4]` |
| Oracle Database 12c (12.1.x) | Banco de dados do Repository &amp; Forms | R: Suporte restrito |
| Microsoft SQL Server 2016 | Banco de dados Forms | A: Suportado |
| **Apache Lucene (Quickstart integrado)** | Serviço de pesquisa | A: Suportado |
| Apache Solr | Serviço de pesquisa | A: Suportado |

1. &#39;Sistema de arquivos&#39; inclui armazenamento de bloco compatível com POSIX. Isso inclui a tecnologia de armazenamentos de rede. Lembre-se de que o desempenho do sistema de arquivos pode variar e influenciar o desempenho geral. É recomendável carregar AEM de teste em combinação com o sistema de arquivos remoto/de rede.
1. O Compartilhamento MongoDB não é suportado no AEM.
1. O WiredTiger do mecanismo de Armazenamento MongoDB é compatível apenas.
1. Suportado para clientes de atualização da AEM Forms. Não suportado para novas instalações.

>[!NOTE]
>
>Consulte [Implantação de comunidades](/help/communities/deploy-communities.md) para obter mais informações sobre o recurso AEM Communities.

>[!NOTE]
>
>O MongoDB é um software de terceiros e não está incluído no pacote de licenciamento AEM. Para obter mais informações, consulte a página de política [de licenciamento do](https://www.mongodb.org/about/licensing/) MongoDB.
>
>Para obter o máximo de sua implantação AEM com o MongoDB, a Adobe recomenda licenciar a versão do MongoDB Enterprise para se beneficiar do suporte profissional. Consulte Implantações [recomendadas](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) para obter mais informações.
>
>A licença inclui um conjunto de réplicas padrão, composto por uma e duas instâncias primárias que podem ser usadas para o autor ou as implantações de publicação.
>
>Caso deseje executar o autor e publicar no MongoDB, duas licenças separadas precisam ser compradas.
>
>O Atendimento ao cliente do Adobe ajudará a solucionar problemas relacionados ao uso do MongoDB com AEM.
>
>Para obter mais informações, consulte a página [](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager)MongoDB para Adobe Experience Manager.

>[!NOTE]
>
>Os bancos de dados relacionais suportados, conforme listados acima, são softwares de terceiros e não estão incluídos no pacote de licenciamento AEM.
>
>Para executar AEM 6.5 com um banco de dados relacional suportado, é necessário um contrato de suporte separado com um fornecedor de banco de dados. O Atendimento ao cliente do Adobe ajudará a solucionar problemas relacionados ao uso de bancos de dados relacionais com o AEM 6.5.
>
>**Atualmente, a maioria dos bancos de dados relacionais é compatível com o Nível R no AEM 6.5, que vem com os critérios de suporte e um programa de suporte, conforme indicado na descrição do Nível R acima.**

### Mecanismos de Servlet / Servidores de Aplicativo {#servlet-engines-application-servers}

A Adobe Experience Manager pode ser executada como um servidor independente (o arquivo JAR de início rápido) ou como aplicativo da Web em um servidor de aplicativos de terceiros (o arquivo WAR).

A versão mínima necessária da API do servlet é o Servlet 3.1

| Plataforma | Nível de suporte |
|---|---|
| **Mecanismo Servlet integrado Quickstart (Jetty 9.4)** | A: Suportado |
| Oracle WebLogic Server 12.2 (12cR2) | Z: Não suportado |
| DELIVERY contínuo IBM WebSphere Application Server (LibertyProfile) com Perfil Web 7.0 e IBM JRE 1.8 | R: Apoio restrito a novos contratos `[2]` |
| IBM WebSphere Application Server 9.0 e IBM JRE 1.8 | R: Apoio restrito a novos contratos `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Apoio restrito a novos contratos `[2]` |
| JBoss EAP 7.2.x com JBoss Application Server | Z: Não suportado |
| JBoss EAP 7.1.4 com JBoss Application Server | R: Apoio restrito a novos contratos `[1]` `[2]` |
| JBoss EAP 7.0.x com JBoss Application Server | Z: Não suportado |

1. Recomendado para implantações com AEM Forms.
1. A partir AEM implantações 6.5 em servidores de aplicativos, o suporte é movido para Suporte restrito. Os clientes existentes podem atualizar para o AEM 6.5 e continuar usando os servidores de aplicativos. Para novos clientes, ele vem com os critérios de suporte e um programa de suporte, conforme indicado na descrição de Nível R acima.

### Sistemas operacionais de servidor {#server-operating-systems}

A Adobe Experience Manager trabalha com as seguintes plataformas de servidor para ambientes de produção:

| **Plataforma** | **Nível de suporte** |
|---|---|
| **Linux, baseado na distribuição Red Hat** | A: Suportado `[1]` `[3]` |
| Linux, baseado na distribuição Debian incl. Ubuntu | A: Suportado `[2]` |
| Linux, baseado na distribuição SUSE | A: Suportado |
| Microsoft Windows Server 2019 `[4]` | R: Apoio restrito a novos contratos |
| Microsoft Windows Server 2016 `[4]` | R: Apoio restrito a novos contratos `[5]` |
| Microsoft Windows Server 2012 R2 | Z: Não suportado |
| Oracle Solaris 11 | Z: Não suportado |
| IBM AIX 7.2 | Z: Não suportado |

1. O Linux Kernel 2.6, 3.x e 4.x inclui derivados da distribuição Red Hat, incluindo Red Hat Enterprise Linux, CentOS, Oracle Linux e Amazon Linux. Os recursos complementares do AEM Forms só são suportados no CentOS 7 e no Red Hat Enterprise Linux 7.
1. O AEM Forms é compatível apenas com Ubuntu 16.04 LTS
1. Distribuição Linux suportada pelos Serviços gerenciados da Adobe
1. As implantações de produção do Microsoft Windows são compatíveis com clientes que atualizam para a versão 6.5 e para uso sem produção. As novas implantações estão sob solicitação para AEM Sites e Assets.
1. O AEM Forms é compatível com o Microsoft Windows Server sem restrições de nível R de suporte

### Ambientes de computação virtual e em nuvem {#virtual-cloud-computing-environments}

A Adobe Experience Manager é compatível com a execução em uma máquina virtual em ambientes de computação em nuvem, como o Microsoft Azure e o Amazon Web Services (AWS), em conformidade com os requisitos técnicos listados nesta página e de acordo com os termos de suporte padrão do Adobe.

A Adobe recomenda usar os Serviços gerenciados da Adobe para implantar AEM no Azure ou AWS. Os Serviços gerenciados da Adobe fornecem aos especialistas a experiência e as habilidades de implantar e operar AEM nesses ambientes de computação em nuvem. Consulte a documentação [adicional sobre os Serviços](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t)gerenciados da Adobe.

Em todos os outros casos de implantação de AEM no Azure ou AWS, ou em qualquer outro ambiente de computação em nuvem, o suporte do Adobe será contido no ambiente de computação virtual, de acordo com as especificações técnicas listadas nesta página. Qualquer problema relatado relacionado à AEM em execução em qualquer um desses ambientes na nuvem precisará ser reprodutível independentemente de qualquer serviço de nuvem específico ao ambiente de computação em nuvem, a menos que o serviço de nuvem seja especificamente suportado como parte dos requisitos técnicos listados nesta página, por exemplo, armazenamento Blob do Azure ou AWS S3.

Para obter recomendações sobre como implantar AEM no Azure ou AWS, fora dos Serviços gerenciados da Adobe, o Adobe recomenda trabalhar diretamente com o provedor de nuvem ou parceiros Adobe com suporte à implantação de AEM no ambiente de nuvem de sua escolha. O provedor ou parceiro de nuvem selecionado será responsável pelas especificações de dimensionamento, design e implementação da arquitetura. Para atender aos seus requisitos específicos de desempenho, carga, escalabilidade e segurança.

### Plataformas do Dispatcher (Servidores Web) {#dispatcher-platforms-web-servers}

O Dispatcher é o componente de cache e balanceamento de carga. [Baixe a versão](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html)mais recente do Dispatcher. O Experience Manager 6.5 requer o Dispatcher versão 4.3.2 ou superior.

Os seguintes servidores Web são suportados para uso com o Dispatcher versão 4.3.2:

| Plataforma | Nível de suporte |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Suportado |
| Microsoft IIS 10 (Internet Information Server) | A: Suportado |
| Microsoft IIS 8.5 (Internet Information Server) | Z: Não suportado |

1. Os servidores Web criados com base no código-fonte httpd do Apache terão o mesmo nível de suporte que a versão do httpd na qual ele se baseia. Em caso de dúvida, peça à Adobe para confirmar o nível de suporte relacionado ao respectivo produto para servidor. Os seguintes casos:

   1. O servidor HTTP foi criado usando apenas distribuições oficiais de origem do Apache ou
   1. O servidor HTTP foi entregue como parte do sistema operacional no qual está sendo executado. Exemplos: IBM HTTP Server, Oracle HTTP Server

1. O Dispatcher não está disponível para o Apache 2.4.x para sistemas operacionais Windows.

## Plataformas compatíveis com o cliente {#supported-client-platforms}

### Navegadores compatíveis para criação de interface de usuário {#supported-browsers-for-authoring-user-interface}

A interface do usuário do Adobe Experience Manager funciona com as seguintes plataformas cliente. Todos os navegadores são testados com o conjunto padrão de plug-ins e suplementos.

A interface do usuário AEM é otimizada para telas maiores (geralmente notebooks e desktops) e fator de forma de tablet (como o Apple iPad ou o Microsoft Surface). O fator de forma de telefone não é suportado.

>[!NOTE]
>
>**Suporte para navegadores com ciclos de lançamento rápido:**
>
>Mozilla Firefox, Google Chrome e Microsoft Edge lançam atualizações a cada poucos meses. O Adobe tem o compromisso de fornecer atualizações para a Adobe Experience Manager manter o nível de suporte, conforme declarado abaixo, com as versões futuras desses navegadores.

<table>
 <tbody>
  <tr>
   <td><strong>Navegador</strong></td>
   <td><strong>Suporte para a interface do usuário<br /> </strong></td>
   <td><strong>Suporte para a interface clássica</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A: Suportado</td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>Microsoft Edge (Evergreen)</td>
   <td>A: Suportado</td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>Microsoft Internet Explorer 11</td>
   <td>Z: Não suportado</td>
   <td>Z: Não suportado</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: Suportado</td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>Mozilla Firefox last ESR [1]</td>
   <td>A: Suportado</td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>Apple Safari no macOS (Evergreen)</td>
   <td>A: Suportado</td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>Apple Safari 11.x no macOS</td>
   <td>Z: Não suportado</td>
   <td>Z: Não suportado</td>
  </tr>
  <tr>
   <td>Apple Safari no iOS 12.x</td>
   <td>A: Suportado [2]</td>
   <td>Z: Não suportado</td>
  </tr>
  <tr>
   <td>Apple Safari no iOS 11.x</td>
   <td>Z: Não suportado</td>
   <td>Z: Não suportado</td>
  </tr>
 </tbody>
</table>

1. Versão de suporte estendido do Firefox [Saiba mais sobre isso no mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. suporte para iPad da Apple

### Navegadores suportados para sites {#supported-browsers-for-websites}

Geralmente, o suporte de navegador para sites renderizados pela AEM Sites depende da implementação AEM modelos de página, design e saída de componente, e portanto está sob o controle da parte que implementa essas partes.

### Clientes WebDAV {#webdav-clients}

**Microsoft Windows 7+**

Para se conectar com êxito com o Microsoft Windows 7+ a uma instância AEM que não esteja protegida com SSL, a autenticação básica por rede não segura deve estar habilitada no Windows. Isso requer uma alteração no Registro do Windows do WebClient:

1. Localize a subchave do Registro:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Adicione a entrada do registro BasicAuthLevel a essa subchave usando um valor de 2 ou mais.

Para melhorar a capacidade de resposta do cliente WebDav no Windows - consulte a Base de conhecimento de suporte da [Microsoft 2445570](https://support.microsoft.com/kb/2445570)

## Notas adicionais da plataforma {#additional-platform-notes}

Esta seção fornece notas especiais e informações mais detalhadas sobre como executar o Adobe Experience Manager e seus complementos.

### IPv4 e IPv6 {#ipv-and-ipv}

Todos os elementos do Adobe Experience Manager (Instance, Dispatcher) podem ser instalados em redes IPv4 e IPv6.

A operação é contínua, pois nenhuma configuração especial é necessária. Você pode simplesmente especificar um endereço IP usando o formato adequado ao seu tipo de rede, se necessário.

Isso significa que, quando um endereço IP precisa ser especificado, você pode selecionar (conforme necessário) de:

* um endereço IPv6, por exemplo `https://[ab12::34c5:6d7:8e90:1234]:4502`

* um endereço IPv4, por exemplo `https://123.1.1.4:4502`

* um nome de servidor, por exemplo, `https://www.yourserver.com:4502`

* o caso padrão de `localhost` será interpretado para instalações de rede IPv4 e IPv6, por exemplo, `https://localhost:4502`

### Requisitos para AEM Dynamic Media Add-on {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media está desativado por padrão. Consulte aqui para [ativar o Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Com o Dynamic Media ativado, os seguintes requisitos técnicos adicionais se aplicam.

>[!NOTE]
>
>Esses requisitos do sistema **só** se aplicam se você usar o Dynamic Media - modo Híbrido; Dynamic Media - O modo híbrido tem um servidor de imagem incorporado, que só é certificado em determinados sistemas operacionais.
>
>Para clientes do Dynamic Media que executam o modo Dynamic Media - Scene7 (ou seja, **modo de execução dynamicmedia_sceno7** ), não há requisitos adicionais de sistema; apenas os mesmos requisitos de sistema AEM. Dynamic Media - A arquitetura de modo Scene7 usa o serviço de imagem baseado em nuvem e não o serviço incorporado no AEM.

#### Hardware {#hardware}

Os seguintes requisitos de hardware são aplicáveis para Linux e Windows:

* CPU Intel Xeon ou AMD Opteron com pelo menos 4 núcleos
* Pelo menos, 16 GB de RAM

#### Linux {#linux}

Se você estiver usando o Dynamic Media no Linux, os seguintes pré-requisitos precisam ser atendidos:

* RedHat Enterprise 7 ou CentOS 7 e posterior com os patches de correção mais recentes
* Sistema operacional de 64 bits
* Troca desativada (recomendado)
* SELinux desativado (consulte a observação a seguir)

>[!NOTE]
>
>Se a localidade estiver definida de modo que LC_CTYPE não seja igual a `en_US.UTF-8`, isso impedirá que o Dynamic Media funcione. Para ver qual valor é, digite &quot;locale&quot; no prompt de comando. Se ele não estiver definido como essa, defina a variável de ambiente LC_CTYPE para a string vazia digitando &quot;export LC_CTYPE=&quot; antes de executar o AEM.

>[!NOTE]
>
>**Desabilitando SELinux:** O Serviço de imagem não funciona com o SELinux ativado. Essa opção é ativada por padrão. Para resolver esse problema, edite o arquivo **/etc/selinux/config** e altere o valor do SELinux de:
>
>`SELINUX=enforcing` **para** `SELINUX=disabled`

>[!NOTE]
>
>**Arquitetura NUMA:** Os sistemas com processadores com AMD64 e Intel EM64T são normalmente configurados como plataformas de arquitetura de memória não-uniformes (NUMA), o que significa que o kernel constrói vários nós de memória no momento da inicialização em vez de construir um único nó de memória.
>
>A construção de vários nós pode resultar em exaustão de memória em um ou mais nós antes que outros nós fiquem esgotados. Quando ocorre o esgotamento da memória, o kernel pode decidir matar processos (por exemplo, o Servidor de imagens ou o Servidor de plataformas) mesmo que haja memória disponível.
>
>Portanto, a Adobe recomenda que, se você estiver executando um sistema desse tipo, desative a NUMA usando a opção de **inicialização numa=off** para evitar que o kernel acabe com esses processos.

>[!NOTE]
>
>**O nome do host do servidor deve resolver:** Verifique se o nome do host do servidor pode ser resolvido para um endereço IP. Se isso não for possível, adicione o nome de host totalmente qualificado e o endereço IP aos hosts ****/etc/hosts:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* Troque o espaço pelo menos o dobro da quantidade de memória física (RAM)

Para usar o Dynamic Media no Windows, instale os redistribuíveis do Microsoft Visual Studio 2010, 2013 e 2015 para x64 e x86.

Para Windows x64:

* Obtenha o Microsoft Visual Studio 2010 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* Obtenha o Microsoft Visual Studio 2013 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Obtenha o Microsoft Visual Studio 2015 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Para Windows x86:

* Obtenha o Microsoft Visual Studio 2010 redistribuível em [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* Obtenha o Microsoft Visual Studio 2013 redistribuível em [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Obtenha o Microsoft Visual Studio 2015 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### MacOS {#macos}

* 10.9.x e posterior
* Somente suportado para fins de avaliação e demonstração

### Requisitos para o AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produto</strong></p> </th>
   <th><p><strong>Formatos suportados para conversão em PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Versão mais recente do rastreamento</a> clássico do Acrobat 2017</td>
   <td>XPS, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>WordPerfect X7</td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Project 2016<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JP2, J2K, J2C, JPC), HTML, M, RTF e TXT</td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>O Gerador de PDF suporta apenas versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos suportados.
>
>Além disso:
>
>* O Gerador de PDF requer a versão 17.011.30078 do rastreamento clássico do [Acrobat 2017 ou posterior](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) para executar a conversão.
>* O Gerador de PDF suporta apenas a versão de 32 bits para revenda do Microsoft Office Professional Plus e outros softwares necessários para conversão.
>* O Gerador de PDF não é compatível com o Microsoft Office 365.
>* As conversões do Gerador de PDF para OpenOffice são suportadas apenas no Windows e no Linux.
>* Os recursos OCR PDF, Optimize PDF e Export PDF são suportados apenas no Windows.
>* Uma versão do Acrobat é fornecida com o AEM Forms para ativar a funcionalidade do Gerador de PDF. A versão agrupada só deve ser acessada programaticamente com a AEM Forms, durante o período da licença da AEM Forms, para uso com o AEM Forms PDF Generator. Para obter mais informações, consulte a descrição do produto AEM Forms de acordo com sua implantação ([no local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) ou [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;

   >
   >
* O serviço Gerador de PDF não é compatível com o Microsoft Windows 10.

>



### Requisitos para o AEM Assets XMP write-back de metadados {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP gravação é suportada e ativada para as seguintes plataformas e formatos de arquivo:

* **Sistemas operacionais:**

   * Linux (suporte para aplicativos de 32 bits e 32 bits em sistemas de 64 bits). Para obter etapas para instalar bibliotecas de clientes de 32 bits, consulte [Como ativar XMP extração e write-back no RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)de 64 bits.

   * Windows Server
   * Mac OS X (64 bits)

* **Formatos** de arquivo: JPEG, PNG, TIFF, PDF, INDD, AI e EPS.

### Requisitos para a AEM Assets processar ativos pesados de metadados no Linux {#assetsonlinux}

O processo XMPFilesProcessor requer a biblioteca GLIBC_2.14 para funcionar. Use um kernel Linux que contenha GLIBC_2.14, por exemplo, o kernel Linux versão 3.1.x. Ele melhora o desempenho de ativos de processamento que contêm uma grande quantidade de metadados, como arquivos PSD. O uso de uma versão anterior do GLIBC leva a erros nos registros que começam com `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
