---
title: Requisitos técnicos
seo-title: Technical Requirements
description: Uma lista das plataformas de cliente e servidor compatíveis com o AEM.
seo-description: A list of the supported client and server platforms for AEM.
content-type: reference
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: 3643534fa0f24a1c2ea00c35853a2671b156bf9a
workflow-type: tm+mt
source-wordcount: '3329'
ht-degree: 1%

---

# Requisitos técnicos{#technical-requirements}

O Adobe oferece suporte ao Adobe Experience Manager (AEM) nas plataformas, conforme detalhado nas seguintes informações deste documento.

Para qualquer problema relacionado especificamente à plataforma, entre em contato com o fornecedor da plataforma.

>[!NOTE]
>
>Dependendo da plataforma na qual você instala o AEM, pode haver diferentes conjuntos de requisitos para o gerenciamento de usuários.

## Pré-requisitos {#prerequisites}

Requisitos mínimos para instalar o Adobe Experience Manager:

* Plataforma Java instalada, JDK Standard Edition ou outro suporte [Máquinas Virtuais Java](#java-virtual-machines)
* Arquivo Experience Manager Quickstart (JAR autônomo ou WAR de implantação de aplicativo Web)

### Requisitos mínimos de dimensionamento {#minimum-sizing-requirements}

Requisitos mínimos para executar o Adobe Experience Manager:

* 5 GB de espaço livre em disco no diretório de instalação
* Memória de 2 GB

>[!NOTE]
>
>* Os casos de uso de ativos digitais precisam de mais memória básica. Consulte [Implantação e manutenção](/help/sites-deploying/deploy.md#default-local-install) para obter detalhes.
>* [Pacote do complemento AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) requer 15 GB de espaço temporário.
>


Para obter mais informações, consulte o [Diretrizes de dimensionamento do hardware](/help/managing/hardware-sizing-guidelines.md).

### Níveis de suporte {#support-levels}

Este documento lista as plataformas de cliente e servidor compatíveis com o Adobe Experience Manager. O Adobe fornece vários níveis de suporte, tanto para configurações recomendadas quanto para outras configurações.

### Configurações suportadas {#supported-configurations}

A Adobe recomenda essas configurações e oferece suporte total como parte do contrato padrão de manutenção de software.

<table>
 <tbody>
  <tr>
   <td>Nível de compatibilidade</td>
   <td>Descrição<br /> </td>
  </tr>
  <tr>
   <td><strong>A: Suportado</strong></td>
   <td>O Adobe oferece suporte e manutenção completos para essa configuração. Essa configuração é coberta pelo processo de garantia de qualidade do Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: Suporte restrito</strong></td>
   <td>Para garantir o sucesso do projeto de nossos clientes, o Adobe oferece suporte total em um programa de suporte restrito, o que requer que condições específicas sejam atendidas. O suporte de nível R requer uma solicitação formal do cliente e a confirmação pela Adobe. Para obter mais informações, entre em contato com o Atendimento ao cliente do Adobe.</td>
  </tr>
 </tbody>
</table>

### Configurações não suportadas {#unsupported-configurations}

| Nível de compatibilidade | Descrição |
|---|---|
| **Z: Não suportado** | A configuração não é suportada. O Adobe não faz declarações sobre se a configuração funciona e não oferece suporte a ela. |

## Plataformas compatíveis {#supported-platforms}

### Máquinas Virtuais Java {#java-virtual-machines}

O aplicativo requer uma Máquina Virtual Java para execução, fornecida pela distribuição do Java Development Kit (JDK).

A Adobe Experience Manager opera com as seguintes versões das máquinas virtuais Java:

>[!CAUTION]
>
>É recomendável rastrear os Boletins de segurança do fornecedor do Java para garantir a segurança dos ambientes de produção e instalar as Atualizações mais recentes do Java.

| **Plataforma** | **Nível de compatibilidade** | **Link** |
|---|---|---|
| JDK Java SE 11 do Oracle - 64 bits | A: Suportado `[1]` | [Download](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| JDK Java SE 10 do Oracle | Z: Não suportado `[1]` |
| JDK Java SE 9 do Oracle | Z: Não suportado `[1]` |
| JDK Java SE 8 do Oracle - 64 bits | A: Suportado `[1]` | [Baixar](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM J9 VM - compilação 2.9, JRE 1.8.0 | A: Suportado `[2]` |
| IBM J9 VM - compilação 2.8, JRE 1.8.0 | A: Suportado `[2]` |
| Azul Zulu OpenJDK 11 - 64 bits | A: Suportado `[3]` |  |
| Azul Zulu OpenJDK 8 - 64 bits | A: Suportado `[3]` |  |

1. O Oracle migrou para um modelo de &quot;Suporte de longo prazo&quot; (LTS) dos produtos Oracle Java SE. O Java 9, o Java 10 e o Java 12 são versões não LTS do Oracle (consulte [Roteiro de suporte do Oracle Java SE](https://www.oracle.com/technetwork/java/eol-135779.html)). Para implantar AEM no ambiente de produção, o Adobe fornece suporte somente para as versões LTS do Java. O suporte e a distribuição do JDK Java SE do Oracle, incluindo todas as atualizações de manutenção de versões LTS além do fim das atualizações públicas, serão suportados pelo Adobe diretamente para todos os clientes AEM que usam a tecnologia Oracle Java SE. Consulte a [Política de suporte Java para Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf) para obter mais informações.


1. O IBM JRE só é compatível com o WebSphere Application Server.

1. As versões do Azul Zulu OpenJDK LTS são compatíveis com implantações locais de AEM a partir da versão 6.5 SP9. O suporte e a distribuição das versões do Azul Zulu JDK LTS devem ser licenciados diretamente do Azul por nossos clientes.


### Armazenamento e persistência {#storage-persistence}

Existem várias opções para implantar o repositório do Adobe Experience Manager. Consulte a lista a seguir para conhecer as tecnologias e opções de armazenamento suportadas.

| **Plataforma** | **Descrição** | **Nível de compatibilidade** |
|---|---|---|
| **Sistema de arquivos com arquivos TAR** `[1]` | Repositório | A: Suportado |
| **Sistema de arquivos com armazenamento de dados** `[1]` | Binários | A: Suportado |
| Armazenar binários em arquivos TAR no sistema de arquivos `[1]` | Binários | Z: Não suportado para produção |
| Amazon S3 | Binários | A: Suportado |
| Armazenamento de blobs do Microsoft Azure | Binários | A: Suportado |
| MongoDB Enterprise 4.2 | Repositório | A: Suportado `[2, 3, 4]` |
| MongoDB Enterprise 4.0 | Repositório | Z: Não suportado |
| MongoDB Enterprise 3.6 | Repositório | Z: Não suportado |
| MongoDB Enterprise 3.4 | Repositório | Z: Não suportado |
| IBM DB2 10.5 | Banco de dados do Repositório e Forms | R: Suporte restrito `[5]` |
| Oracle Database 12c (12.1.x) | Banco de dados do Repositório e Forms | R: Suporte restrito |
| Microsoft SQL Server 2016 | Banco de dados Forms | A: Suportado |
| **Apache Lucene (Quickstart integrado)** | Serviço de pesquisa | A: Suportado |
| Apache Solr | Serviço de pesquisa | A: Suportado |

1. O &#39;Sistema de Arquivos&#39; inclui o armazenamento de blocos compatível com POSIX. Isso inclui a tecnologia de armazenamento de rede. Considere que o desempenho do sistema de arquivos pode variar e influencia o desempenho geral. É recomendável carregar AEM de teste em combinação com o sistema de arquivos remoto/de rede.
1. O MongoDB Enterprise 4.2 requer AEM 6.5 SP9 como mínimo.
1. A Partilha de MongoDB não é suportada no AEM.
1. O MongoDB Storage Engine WiredTiger é compatível somente.
1. Suportado para clientes de atualização do AEM Forms. Não suportado para novas instalações.

>[!NOTE]
>
>Consulte [Implantação de comunidades](/help/communities/deploy-communities.md) para obter informações adicionais sobre o recurso AEM Communities.

>[!NOTE]
>
>O MongoDB é um software de terceiros e não está incluído no pacote de licenciamento AEM. Para obter mais informações, consulte [Política de licenciamento do MongoDB](https://www.mongodb.org/about/licensing/) página.
>
>Para aproveitar ao máximo sua implantação de AEM com o MongoDB, o Adobe recomenda o licenciamento da versão MongoDB Enterprise para se beneficiar do suporte profissional. Consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) para obter mais informações.
>
>A licença inclui um conjunto de réplicas padrão, composto por uma instância primária e duas instâncias secundárias que podem ser usadas para o autor ou para as implantações de publicação.
>
>Caso deseje executar o autor e publicar no MongoDB, duas licenças separadas precisam ser compradas.
>
>O Atendimento ao cliente do Adobe ajudará a solucionar problemas relacionados ao uso do MongoDB com AEM.
>
>Para obter mais informações, consulte o [MongoDB para página do Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
>Os bancos de dados relacionais compatíveis, conforme listado acima, são softwares de terceiros e não estão incluídos no pacote de licenciamento AEM.
>
>Para executar o AEM 6.5 com um banco de dados relacional suportado, é necessário um contrato de suporte separado com um fornecedor de banco de dados. O Atendimento ao cliente do Adobe ajudará a qualificar problemas relacionados ao uso de bancos de dados relacionais com o AEM 6.5.
>
>**Atualmente, a maioria dos bancos de dados relacionais é compatível com o Nível-R no AEM 6.5, que vem com critérios de suporte e um programa de suporte, conforme indicado na descrição de Nível-R acima.**

### Mecanismos de Servlet/Servidores de Aplicativos {#servlet-engines-application-servers}

O Adobe Experience Manager pode ser executado como um servidor independente (o arquivo JAR de início rápido) ou como um aplicativo da Web em um servidor de aplicativos de terceiros (o arquivo WAR).

A versão mínima necessária da API de servlet é o Servlet 3.1

| Plataforma | Nível de compatibilidade |
|---|---|
| **Mecanismo de Servlet integrado do Quickstart (Jetty 9.4)** | A: Suportado |
| Oracle WebLogic Server 12.2 (12cR2) | Z: Não suportado |
| Entrega contínua do IBM WebSphere Application Server (LibertyProfile) com o Perfil da Web 7.0 e IBM JRE 1.8 | R: Apoio limitado a novos contratos `[2]` |
| IBM WebSphere Application Server 9.0 e IBM JRE 1.8 | R: Apoio limitado a novos contratos `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Apoio limitado a novos contratos `[2]` |
| JBoss EAP 7.2.x com JBoss Application Server | Z: Não suportado |
| JBoss EAP 7.1.4 com JBoss Application Server | R: Apoio limitado a novos contratos `[1]` `[2]` |
| JBoss EAP 7.0.x com JBoss Application Server | Z: Não suportado |

1. Recomendado para implantações com o AEM Forms.
1. A inicialização AEM implantações 6.5 em servidores de aplicativos é transferida para o Suporte Restrito. Os clientes atuais podem atualizar para o AEM 6.5 e continuar usando os servidores de aplicativos. Para novos clientes, ele vem com critérios de suporte e um programa de suporte, conforme indicado na descrição de Nível-R acima.

### Sistemas operacionais do servidor {#server-operating-systems}

O Adobe Experience Manager funciona com as seguintes plataformas de servidor para ambientes de produção:

| **Plataforma** | **Nível de compatibilidade** |
|---|---|
| **Linux, baseado na distribuição Red Hat** | A: Suportado `[1]` `[3]` |
| Linux, baseado na distribuição Debian incl. Ubuntu | A: Suportado `[2]` |
| Linux, baseado na distribuição SUSE | A: Suportado |
| Microsoft Windows Server 2019 `[4]` | R: Apoio limitado a novos contratos |
| Microsoft Windows Server 2016 `[4]` | R: Apoio limitado a novos contratos `[5]` |
| Microsoft Windows Server 2012 R2 | Z: Não suportado |
| Oracle Solaris 11 | Z: Não suportado |
| IBM AIX 7.2 | Z: Não suportado |

1. O Linux Kernel 2.6, 3.x e 4.x inclui derivados da distribuição Red Hat, incluindo Red Hat Enterprise Linux, CentOS, Oracle Linux e Amazon Linux. Os recursos do complemento AEM Forms só são compatíveis com CentOS 7, Red Hat Enterprise Linux 7 e Red Hat Enterprise Linux 8.
1. O AEM Forms é compatível somente com o Ubuntu 16.04 LTS
1. Distribuição Linux suportada pelos Adobe Managed Services
1. As implantações de produção do Microsoft Windows são compatíveis com clientes que atualizam para 6.5 e para uso não relacionado à produção. Novas implantações são por solicitação do AEM Sites e do Assets.
1. O AEM Forms é compatível com o Microsoft Window Server sem as restrições do Nível de Suporte R.


### Ambientes de computação em nuvem e virtual {#virtual-cloud-computing-environments}

O Adobe Experience Manager é compatível com a execução em uma máquina virtual em ambientes de computação em nuvem, como o Microsoft Azure e o Amazon Web Services (AWS), em conformidade com os requisitos técnicos listados nesta página e de acordo com os termos de suporte padrão do Adobe.

Para um ambiente nativo em nuvem, analise a oferta mais recente da linha de produtos AEM: Adobe Experience Manager as a Cloud Service. Consulte [Documentação do Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=en) para obter detalhes.

O Adobe também oferece o Adobe Managed Services para implantar AEM no Azure ou no AWS. O Adobe Managed Services fornece aos especialistas experiência e habilidades de implantação e operação de AEM nesses ambientes de computação em nuvem. Consulte [documentação adicional sobre o Adobe Managed Services](https://www.adobe.com/marketing-cloud/enterprise-content-management/managed-services-cloud-platform.html?aemClk=t).

Em todos os outros casos de implantação de AEM no Azure ou AWS, ou em qualquer outro ambiente de computação em nuvem, o suporte do Adobe será contido no ambiente de computação virtual, em conformidade com as especificações técnicas listadas nesta página. Qualquer problema relatado relacionado à AEM em execução em qualquer um desses ambientes de nuvem precisará ser reproduzível independentemente de qualquer serviço de nuvem específico ao ambiente de computação em nuvem, a menos que o serviço de nuvem seja especificamente aceito como parte dos requisitos técnicos listados nesta página, por exemplo, o armazenamento do Azure Blob ou o AWS S3.

Para recomendações sobre como implantar AEM no Azure ou no AWS, fora do Adobe Managed Services, o Adobe recomenda trabalhar diretamente com o provedor de nuvem ou parceiros do Adobe que oferecem suporte à implantação do AEM no ambiente de nuvem de sua escolha. O provedor ou parceiro de nuvem selecionado será responsável pelas especificações de dimensionamento, design e implementação da arquitetura., para atender aos requisitos específicos de desempenho, carga, escalabilidade e segurança.

### Plataformas do Dispatcher (Servidores da Web) {#dispatcher-platforms-web-servers}

O Dispatcher é o componente de balanceamento de carga e cache. [Baixe a versão mais recente do Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/release-notes.html). O Experience Manager 6.5 requer o Dispatcher versão 4.3.2 ou superior.

Os seguintes servidores da Web são compatíveis com o Dispatcher versão 4.3.2:

| Plataforma | Nível de compatibilidade |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Suportado |
| Microsoft IIS 10 (Servidor de Informações da Internet) | A: Suportado |
| Microsoft IIS 8.5 (Servidor de Informações da Internet) | Z: Não suportado |

1. Os servidores da Web criados com base no código-fonte httpd do Apache terão o mesmo nível de suporte que a versão do httpd na qual se baseia. Em caso de dúvida, solicite ao Adobe a confirmação do nível de suporte relacionado ao respectivo produto de servidor. Os seguintes casos:

   1. O servidor HTTP foi criado usando apenas distribuições oficiais de origem do Apache ou
   1. O servidor HTTP foi entregue como parte do sistema operacional no qual está sendo executado. Exemplos: IBM HTTP Server, Oracle HTTP Server

1. O Dispatcher não está disponível para o Apache 2.4.x para sistemas operacionais Windows.

## Plataformas compatíveis de clientes {#supported-client-platforms}

### Navegadores compatíveis para criação de interface de usuário {#supported-browsers-for-authoring-user-interface}

A interface do usuário do Adobe Experience Manager funciona com as seguintes plataformas de cliente. Todos os navegadores são testados com o conjunto padrão de plug-ins e complementos.

A interface do usuário do AEM é otimizada para telas maiores (geralmente notebooks e desktops) e fator de forma de tablet (como Apple iPad ou Microsoft Surface). O fator de forma de telefone não é suportado.

>[!NOTE]
>
>**Suporte para navegadores com ciclos de lançamento rápidos:**
>
>Atualizações de versão do Mozilla Firefox, Google Chrome e Microsoft Edge a cada poucos meses. O Adobe tem o compromisso de fornecer atualizações para que o Adobe Experience Manager mantenha o nível de suporte, conforme declarado abaixo, com as versões futuras desses navegadores.

<table>
 <tbody>
  <tr>
   <td><strong>Navegador</strong></td>
   <td><strong>Suporte para interface do usuário<br /> </strong></td>
   <td><strong>Suporte para interface clássica</strong></td>
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
   <td>Mozilla Firefox último ESR [1]</td>
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

1. Versão de suporte estendida do Firefox [Saiba mais sobre isso no mozilla.org](https://www.mozilla.org/en-US/firefox/organizations/faq/)
1. suporte para Apple iPad

### Navegadores compatíveis para sites {#supported-browsers-for-websites}

Geralmente, o suporte de navegador para sites renderizados pelo AEM Sites depende da implementação de modelos de página de AEM, design e saída de componente e, portanto, está sob o controle da parte que implementa essas partes.

### Clientes WebDAV {#webdav-clients}

**Microsoft Windows 7+**

Para se conectar com êxito ao Microsoft Windows 7+ a uma instância de AEM que não esteja protegida com SSL, a autenticação básica por rede não segura deve ser ativada no Windows. Isso requer uma alteração no Registro do Windows do WebClient:

1. Localize a subchave do Registro:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Adicione a entrada do registro BasicAuthLevel a esta subchave usando um valor de 2 ou mais.

Para melhorar a capacidade de resposta do WebDav Client no Windows - consulte [Suporte Microsoft KB 2445570](https://support.microsoft.com/kb/2445570)

## Notas adicionais da plataforma {#additional-platform-notes}

Esta seção fornece observações especiais e informações mais detalhadas sobre a execução do Adobe Experience Manager e de seus complementos.

### IPv4 e IPv6 {#ipv-and-ipv}

Todos os elementos do Adobe Experience Manager (Instância, Dispatcher) podem ser instalados em redes IPv4 e IPv6.

A operação é contínua, pois nenhuma configuração especial é necessária. Você pode simplesmente especificar um endereço IP usando o formato adequado ao seu tipo de rede, se necessário.

Isso significa que, quando um endereço IP precisa ser especificado, você pode selecionar (conforme necessário) de:

* um endereço IPv6, por exemplo `https://[ab12::34c5:6d7:8e90:1234]:4502`

* um endereço IPv4, por exemplo `https://123.1.1.4:4502`

* um nome de servidor, por exemplo, `https://www.yourserver.com:4502`

* o caso padrão de `localhost` será interpretado para instalações de rede IPv4 e IPv6, por exemplo, `https://localhost:4502`

### Requisitos do AEM complemento Dynamic Media {#requirements-for-aem-dynamic-media-add-on}

AEM Dynamic Media está desativado por padrão. Veja aqui para [habilitar o Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Com o Dynamic Media ativado, os seguintes requisitos técnicos adicionais se aplicam.

>[!NOTE]
>
>Esses requisitos de sistema **only** aplicar se você usar o Dynamic Media - Modo híbrido; Dynamic Media - O modo híbrido tem um servidor de imagem incorporado, que só é certificado em determinados sistemas operacionais.
>
>Para clientes do Dynamic Media que executam o Dynamic Media - modo Scene7 (ou seja, **dynamicmedia_scene7** runmode), não existem requisitos adicionais do sistema; apenas os mesmos requisitos de sistema AEM. Dynamic Media - A arquitetura de modo Scene7 usa o serviço de imagem baseado em nuvem e não o serviço incorporado no AEM.

#### Hardware {#hardware}

Os seguintes requisitos de hardware são aplicáveis para Linux e Windows:

* CPU Intel Xeon ou AMD Opteron com pelo menos 4 núcleos
* Pelo menos, 16 GB de RAM

#### Linux {#linux}

Se você estiver usando o Dynamic Media no Linux, os seguintes pré-requisitos precisam ser atendidos:

* RedHat Enterprise 7 ou CentOS 7 e posterior com os patches de correção mais recentes
* Sistema operacional de 64 bits
* Troca desabilitada (recomendada)
* SELinux desativado (consulte a observação a seguir)

>[!NOTE]
>
>Se a localidade estiver definida de modo que LC_CTYPE não seja igual a `en_US.UTF-8`, impede que o Dynamic Media funcione. Para ver qual é o valor, digite &quot;locale&quot; no prompt de comando. Se não estiver definido como esse valor, defina a variável de ambiente LC_CTYPE como a string vazia, digitando &quot;export LC_CTYPE=&quot; antes de executar o AEM.

>[!NOTE]
>
>**Desabilitando o SELinux:** O Serviço de imagem não funciona com o SELinux ativado. Essa opção é ativada por padrão. Para solucionar esse problema, edite a **/etc/selinux/config** e altere o valor do SELinux de:
>
>`SELINUX=enforcing` **para** `SELINUX=disabled`

>[!NOTE]
>
>**Arquitetura NUMA:** Os sistemas com processadores com AMD64 e Intel EM64T são normalmente configurados como plataformas de arquitetura de memória não-uniformes (NUMA), o que significa que o kernel constrói vários nós de memória no momento da inicialização em vez de construir um único nó de memória.
>
>A construção de vários nós pode resultar no esgotamento da memória em um ou mais nós, antes que outros nós fiquem esgotados. Quando ocorre esgotamento de memória, o kernel pode decidir interromper processos (por exemplo, o Servidor de Imagem ou o Servidor de Plataforma) mesmo que haja memória disponível.
>
>Portanto, o Adobe recomenda que, se você estiver executando um sistema desse tipo, você desative o NUMA usando o **numa=off** para evitar que o kernel mate esses processos.

>[!NOTE]
>
>**O nome do host do servidor deve resolver:** Certifique-se de que o nome do host do servidor possa ser resolvido para um endereço IP. Se isso não for possível, adicione o nome de host totalmente qualificado e o endereço IP a **/etc/hosts**:
>
>`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft Windows Server 2016
* Troque o espaço igual a pelo menos o dobro da quantidade de memória física (RAM)

Para usar o Dynamic Media no Windows, instale Microsoft Visual Studio 2010, 2013 e 2015 redistribuíveis para x64 e x86.

Para Windows x64:

* Obter o Microsoft Visual Studio 2010 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=13523](https://www.microsoft.com/en-us/download/details.aspx?id=13523)
* Obtenha o Microsoft Visual Studio 2013 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Obtenha o Microsoft Visual Studio 2015 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Para Windows x86:

* Obter o Microsoft Visual Studio 2010 redistribuível em [https://www.microsoft.com/en-in/download/details.aspx?id=5555](https://www.microsoft.com/en-in/download/details.aspx?id=5555)
* Obtenha o Microsoft Visual Studio 2013 redistribuível em [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Obtenha o Microsoft Visual Studio 2015 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x e posterior
* Somente suportado para fins de avaliação e demonstração

### Requisitos para gerador de PDF AEM Forms {#requirements-for-aem-forms-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produto</strong></p> </th>
   <th><p><strong>Formatos suportados para conversão para PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat 2017 classic track</a> versão mais recente</td>
   <td>XPS, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPX, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
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
   <td>Editor Microsoft® 2016<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Projeto Microsoft® 2016<br /> </td>
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
>O PDF Generator suporta apenas versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos compatíveis.
>
>Além disso:
>
>* O PDF Generator requer a versão de 32 bits do [Acrobat 2017 classic track versão 17.011.30078 ou posterior](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) para executar a conversão.
>* O PDF Generator suporta apenas a versão de varejo de 32 bits do Microsoft Office Professional Plus e outros softwares necessários para a conversão.
>* O PDF Generator não é compatível com o Microsoft Office 365.
>* As conversões PDF Generator para OpenOffice são suportadas apenas no Windows e Linux.
>* Os recursos PDF, Optimize PDF e Export PDF do OCR são suportados apenas no Windows.
>* Uma versão do Acrobat é fornecida com o AEM Forms para habilitar a funcionalidade PDF Generator. A versão agrupada só deve ser acessada programaticamente com o AEM Forms, durante o período da licença do AEM Forms, para uso com o PDF Generator da AEM Forms. Para obter mais informações, consulte a descrição do produto AEM Forms de acordo com sua implantação ([No local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) ou [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))&quot;
>
>* O serviço PDF Generator não suporta Microsoft Windows 10.
>


### Requisitos do AEM Forms Designer {#requirements-for-aem-forms-designer}

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

### Requisitos para o write-back de metadados do AEM Assets XMP {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP gravação é suportada e ativada para as seguintes plataformas e formatos de arquivo:

* **Sistemas operacionais:**

   * Linux (suporte a aplicativos de 32 e 32 bits em sistemas de 64 bits). Para obter etapas para instalar bibliotecas de clientes de 32 bits, consulte [Como habilitar a extração e o write-back de XMP no RedHat Linux de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * Mac OS X (64 bits)

* **Formatos de arquivo**: JPEG, PNG, TIFF, PDF, INDD, AI e EPS.

### Requisitos do AEM Assets para processar ativos com metadados pesados no Linux {#assetsonlinux}

O processo XMPFilesProcessor requer a biblioteca GLIBC_2.14 para funcionar. Use um kernel Linux que contenha GLIBC_2.14, por exemplo, o kernel Linux versão 3.1.x. Melhora o desempenho para processar ativos que contêm uma grande quantidade de metadados, como arquivos PSD. Usar uma versão anterior do GLIBC leva a erros em logs que começam com `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.
