---
title: Requisitos técnicos
description: Uma lista das plataformas de cliente e servidor compatíveis com o Adobe Experience Manager.
topic-tags: platform
exl-id: 47529b9a-c4e5-434f-ac26-b01714ff863b
source-git-commit: fbf056b6b7dcbfcaa27744672c45a87316c5f761
workflow-type: tm+mt
source-wordcount: '3642'
ht-degree: 1%

---

# Requisitos técnicos{#technical-requirements}

O Adobe suporta (AEM) Adobe Experience Manager nas plataformas, conforme detalhado nas informações a seguir neste documento.

Para quaisquer problemas relacionados à plataforma, entre em contato com o fornecedor da plataforma.

>[!NOTE]
>
>Dependendo da plataforma em que você instala o AEM, pode haver diferentes conjuntos de requisitos para o gerenciamento de usuários.

## Pré-requisitos {#prerequisites}

Requisitos mínimos para a instalação do Adobe Experience Manager:

* Java™ Platform, Standard Edition JDK ou outro compatível instalado [Máquinas virtuais Java™](#java-virtual-machines)
* Arquivo Experience Manager Quickstart (JAR independente ou WAR de implantação de aplicativo da Web)

### Requisitos mínimos de dimensionamento {#minimum-sizing-requirements}

Requisitos mínimos para executar o Adobe Experience Manager:

* 5 GB de espaço livre no diretório de instalação
* 2 GB de memória

>[!NOTE]
>
>* Os casos de uso de ativos digitais precisam de mais memória básica. Consulte [Implantação e manutenção](/help/sites-deploying/deploy.md#default-local-install) para obter detalhes.
>* [Pacote complementar do AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) O requer 15 GB de espaço temporário.
>

Para obter mais informações, consulte [Diretrizes de dimensionamento de hardware](/help/managing/hardware-sizing-guidelines.md).

### Níveis de suporte {#support-levels}

Este documento lista as plataformas de cliente e servidor compatíveis com o Adobe Experience Manager. O Adobe fornece vários níveis de suporte, tanto para configurações recomendadas quanto para outras configurações.

### Configurações suportadas {#supported-configurations}

A Adobe recomenda essas configurações e fornece suporte total como parte do contrato de manutenção de software padrão.

<table>
 <tbody>
  <tr>
   <td>Nível de compatibilidade</td>
   <td>Descrição<br /> </td>
  </tr>
  <tr>
   <td><strong>A: Suportado</strong></td>
   <td>O Adobe fornece suporte e manutenção completos para essa configuração. Essa configuração é coberta pelo processo de garantia de qualidade do Adobe.</td>
  </tr>
  <tr>
   <td><strong>R: Suporte restrito</strong></td>
   <td>Para garantir o sucesso do projeto do cliente, o Adobe oferece suporte total dentro de um programa de suporte restrito, o que exige que condições específicas sejam atendidas. O suporte no nível R requer uma solicitação formal do cliente e a confirmação do Adobe. Para obter mais informações, entre em contato com o Atendimento ao cliente da Adobe.</td>
  </tr>
 </tbody>
</table>

### Configurações não suportadas {#unsupported-configurations}

| Nível de compatibilidade | Descrição |
|---|---|
| **Z: Não suportado** | A configuração não é compatível. O Adobe não faz declarações sobre se a configuração funciona e não oferece suporte a ela. |

## Plataformas compatíveis {#supported-platforms}

### Máquinas virtuais Java™ {#java-virtual-machines}

O aplicativo requer uma máquina virtual Java™ para ser executada, que é fornecida pela distribuição Java™ Development Kit (JDK).

O Adobe Experience Manager opera com as seguintes versões das Máquinas Virtuais Java™:

>[!CAUTION]
>
>Rastreie os marcadores de segurança do fornecedor Java™. Isso garante a segurança dos ambientes de produção. Além disso, instale sempre as atualizações mais recentes do Java™.

| **Platform** | **Nível de suporte** | **Link** |
|---|---|---|
| JDK DO Oracle Java™ SE 17 | Z: Não suportado `[1]` |
| JDK do Oracle Java™ SE 11 - 64 bits | A: Suportado `[1]` | [Download](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+11*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=24&lt;td>) |
| JDK DO Oracle Java™ SE 10 | Z: Não suportado `[1]` |
| JDK DO Oracle Java™ SE 9 | Z: Não suportado `[1]` |
| JDK do Oracle Java™ SE 8 - 64 bits | A: Suportado `[1]` | [Download](https://experience.adobe.com/#/downloads/content/software-distribution/en/general.html?fulltext=Oracle*+JDK*+8*&amp;orderby=%40jcr%3Acontent%2Fjcr%3AlastModified&amp;orderby.sort=desc&amp;layout=list&amp;p.offset=0&amp;p.limit=10) |
| IBM® J9 VM - build 2.9, JRE 1.8.0 | A: Suportado `[2]` |
| IBM® J9 VM - build 2.8, JRE 1.8.0 | A: Suportado `[2]` |
| Azul Zulu OpenJDK 11 - 64 bits | A: Suportado `[3]` | |
| Azul Zulu OpenJDK 8 - 64 bits | A: Suportado `[3]` | |

1. O Oracle migrou para um modelo de &quot;Suporte a longo prazo&quot; (LTS, Long Term Support) para produtos Oracle Java™ SE. Java™ 9, Java™ 10 e Java™ 12 são versões não LTS do Oracle (consulte [Roteiro de suporte ao Oracle Java™ SE](https://www.oracle.com/technetwork/java/eol-135779.html)). Para implantar o AEM em um ambiente de produção, o Adobe fornece suporte somente para as versões LTS do Java™. O suporte e a distribuição do JDK do Java™ SE do Oracle, incluindo todas as atualizações de manutenção de versões LTS além do fim das atualizações públicas, são suportados pelo Adobe diretamente para todos os clientes do AEM que usam a tecnologia Oracle Java™ SE. Consulte a [Política de suporte Java™ para Adobe Experience Manager](assets/Java_Policy_for_Adobe_Experience_Manager.pdf).
   **Importante: o Oracle Java™ 11 é compatível no mínimo até setembro de 2026. O suporte para o Oracle Java™ 17 está em preparação.**

1. O IBM® JRE só é suportado com o WebSphere® Application Server.

1. As versões do Azul Zulu OpenJDK LTS são compatíveis com implantações locais de AEM a partir da versão 6.5 SP9. O suporte e a distribuição das versões LTS do Azul Zulu JDK devem ser licenciados diretamente da Azul pelos clientes do Adobe.


### Armazenamento e persistência {#storage-persistence}

Existem várias opções para implantar o repositório do Adobe Experience Manager. Consulte a lista a seguir para conhecer as tecnologias compatíveis e as opções de armazenamento.

| **Platform** | **Descrição** | **Nível de suporte** |
|---|---|---|
| **Sistema de arquivos com arquivos TAR** `[1]` | Repositório | A: Suportado |
| **Sistema de arquivos com armazenamento de dados** `[1]` | Binários | A: Suportado |
| Armazenar binários em arquivos TAR no sistema de arquivos `[1]` | Binários | Z: Não suportado para produção |
| Amazon S3 | Binários | A: Suportado |
| Armazenamento Microsoft® Azure Blob | Binários | A: Suportado |
| MongoDB Enterprise 6.0 | Repositório | A: Suportado `[3, 4]` |
| MongoDB Enterprise 5.0 | Repositório | A: Suportado `[3, 4]` |
| MongoDB Enterprise 4.4 | Repositório | A: Suportado `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.2 | Repositório | A: Suportado `[2, 3, 4, 7]` |
| MongoDB Enterprise 4.0 | Repositório | Z: Não suportado |
| MongoDB Enterprise 3.6 | Repositório | Z: Não suportado |
| MongoDB Enterprise 3.4 | Repositório | Z: Não suportado |
| IBM® DB2® 10.5 | Repositório e banco de dados Forms | R: Suporte restrito `[5]` |
| Banco de Dados do Oracle 12c (12.1.x) | Repositório e banco de dados Forms | R: Suporte restrito |
| Microsoft® SQL Server 2016 | Banco de dados Forms | A: Suportado |
| **Apache Lucene (Quickstart incorporado)** | Serviço de pesquisa | A: Suportado |
| Apache Solr | Serviço de pesquisa | A: Suportado |

1. &#39;Sistema de Arquivos&#39; inclui armazenamento em bloco compatível com POSIX. Inclui tecnologia de armazenamento em rede. Lembre-se de que o desempenho do sistema de arquivos pode variar e influencia o desempenho geral. Carregue o AEM de teste com o sistema de arquivos remoto/de rede.
1. As versões 4.2 e 4.4 do MongoDB Enterprise requerem o AEM 6.5 SP9 como mínimo.
1. A fragmentação de MongoDB não é compatível com o AEM.
1. O WiredTiger do Mecanismo de Armazenamento MongoDB é compatível somente.
1. Compatível com clientes de atualização do AEM Forms. Não suportado para novas instalações.
1. Aplicável somente ao AEM Forms:
   * Remoção do suporte ao Oracle Database 12c e adição do suporte ao Oracle Database 19c.
   * Remoção do suporte ao Microsoft® SQL Server 2016 e adição de suporte ao Microsoft® SQL Server 2019.
1. Não compatível com o AEM Forms.

>[!NOTE]
>
Consulte [Implantação de comunidades](/help/communities/deploy-communities.md) para obter informações adicionais sobre o recurso AEM Communities.

>[!NOTE]
>
MongoDB é um programa de software de terceiros e não está incluído no pacote de licenciamento AEM. Para obter mais informações, consulte [Política de licenciamento do MongoDB](https://www.mongodb.com/licensing/server-side-public-license/faq) página.
>
Para aproveitar ao máximo sua implantação do AEM com o MongoDB, a Adobe recomenda licenciar a versão MongoDB Enterprise para se beneficiar de suporte profissional. Consulte [Implantações recomendadas](/help/sites-deploying/recommended-deploys.md#prerequisites-and-recommendations-when-deploying-aem-with-mongomk) para obter mais informações.
>
A licença inclui um conjunto de réplicas padrão, que é composto por uma instância primária e duas secundárias que podem ser usadas para as implantações do autor ou de publicação.
>
Caso deseje executar o Author e o Publish no MongoDB, duas licenças separadas devem ser compradas.
>
O Atendimento ao cliente do Adobe auxilia na qualificação de problemas relacionados ao uso do MongoDB com AEM.
>
Para obter mais informações, consulte o [MongoDB para Adobe Experience Manager página](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).

>[!NOTE]
>
Os bancos de dados relacionais compatíveis, conforme listado acima, são softwares de terceiros e não são incluídos no pacote de licenciamento AEM.
>
Para executar o AEM 6.5 com um banco de dados relacional compatível, é necessário um contrato de suporte separado com um fornecedor de banco de dados. O Atendimento ao cliente do Adobe auxilia na qualificação de problemas relacionados ao uso de bancos de dados relacionais com AEM 6.5.
>
**A maioria dos bancos de dados relacionais são suportados atualmente no Nível-R no AEM 6.5, que vem com critérios de suporte e um programa de suporte, conforme declarado na descrição do Nível-R acima.**

### Mecanismos de Servlet / Servidores de Aplicativos {#servlet-engines-application-servers}

O Adobe Experience Manager pode ser executado como um servidor independente (o arquivo JAR de início rápido) ou como um aplicativo da Web em um servidor de aplicativos de terceiros (o arquivo WAR).

A versão mínima da API de Servlet necessária é a 3.1

| Platform | Nível de compatibilidade |
|---|---|
| **Mecanismo Servlet integrado Quickstart (Jetty 9.4)** | A: Suportado |
| Oracle WebLogic Server 12.2 (12cR2) | Z: Não suportado |
| Entrega contínua do IBM® WebSphere® Application Server (LibertyProfile) com Web Profile 7.0 e IBM® JRE 1.8 | R: Suporte restrito para novos contratos `[2]` |
| IBM® WebSphere® Application Server 9.0 e IBM® JRE 1.8 | R: Suporte restrito para novos contratos `[1]` `[2]` |
| Apache Tomcat 8.5.x | R: Suporte restrito para novos contratos `[2]` |
| JBoss® EAP 7.2.x com JBoss® Application Server | Z: Não suportado |
| JBoss® EAP 7.1.4 com JBoss® Application Server | R: Suporte restrito para novos contratos `[1]` `[2]` |
| JBoss® EAP 7.0.x com JBoss® Application Server | Z: Não suportado |

1. Recomendado para implantações com o AEM Forms.
1. A partir de implantações do AEM 6.5 em servidores de aplicativos, você será transferido para o Suporte restrito. Os clientes existentes podem atualizar para o AEM 6.5 e continuar usando servidores de aplicativos. Para novos clientes, ele vem com critérios de suporte e um programa de suporte, conforme declarado na descrição do Nível-R acima.
1. Somente AEM Forms aplicável:
   * Remoção do suporte para JBoss® EAP 7.1.4 e adição do suporte para JBoss® EAP 7.4.10.

### Sistemas operacionais de servidor {#server-operating-systems}

O Adobe Experience Manager funciona com as seguintes plataformas de servidor para ambientes de produção:

| **Platform** | **Nível de suporte** |
|---|---|
| **Linux®, baseado na distribuição Red Hat®** | A: Suportado `[1]` `[3]` |
| Linux®, baseado na distribuição Debian incl. Ubuntu | A: Suportado `[1]` `[2]` |
| Linux®, baseado na distribuição SUSE® | A: Suportado `[1]` |
| Microsoft® Windows Server 2019 `[4]` | R: Suporte restrito para novos contratos `[5]` |
| Microsoft® Windows Server 2016 `[4]` | R: Suporte restrito para novos contratos `[5]` |
| Microsoft® Windows Server 2012 R2 | Z: Não suportado |
| Oracle Solaris™ 11 | Z: Não suportado |
| IBM® AIX® 7.2 | Z: Não suportado |

1. Kernel Linux® 2.6, 3. x, 4. x e 5. x inclui derivados da distribuição Red Hat®, incluindo Red Hat® Enterprise Linux®, CentOS, Oracle Linux® e Amazon Linux®. Os recursos complementares da AEM Forms são suportados apenas no CentOS 7, Red Hat® Enterprise Linux® 7, Red Hat® Enterprise Linux® 8 e Red Hat® Enterprise Linux® 9.
1. O AEM Forms é compatível com o Ubuntu 20.04 LTS.
1. Distribuição Linux® suportada pela Adobe Managed Services.

   >[!NOTE]
   >
   Para servidores baseados em Linux (OSGI e pilha JEE), o complemento do AEM Forms requer dependências de tempo de execução como:
   * glibc.x86_64 (2.17-196)
   * libX11.x86_64 (1.6.7-4)
   * zlib.x86-64 (1.2.7-17)
   * libxcb.x86_64 (1.13-1.el7)
   * libXau.x86_64 (1.0.8-2.1.el7)

1. As implantações de produção do Microsoft® Windows são suportadas para clientes que estão atualizando para a versão 6.5 e para uso fora da produção. Novas implantações são feitas sob solicitação para o AEM Sites e o Assets.
1. O AEM Forms é suportado no Microsoft® Windows Server sem as restrições do nível de suporte R.
1. A AEM Forms removeu o suporte ao Microsoft® Windows Server 2016.

>[!NOTE]
>
Se estiver instalando o AEM Forms 6.5, certifique-se de ter instalado o seguinte Microsoft® Visual C++ de 32 bits redistribuível.
>
* Microsoft® Visual C++ 2008 redistribuível
* Microsoft® Visual C++ 2010 redistribuível
* Microsoft® Visual C++ 2012 redistribuível
* Microsoft® Visual C++ 2013 redistribuível
* Microsoft® Visual C++ 2019(VC14.28 ou superior) redistribuível


### Ambientes de computação virtual e em nuvem {#virtual-cloud-computing-environments}

O Adobe Experience Manager é compatível com a execução em uma máquina virtual em ambientes de computação em nuvem. Esses ambientes incluem o Microsoft® Azure e o Amazon Web Services (AWS), executados em conformidade com os requisitos técnicos listados nesta página e de acordo com os termos de suporte padrão do Adobe.

Para um ambiente nativo em nuvem, analise a oferta mais recente da linha de produtos AEM: Adobe Experience Manager as a Cloud Service. Consulte [Documentação do Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html?lang=pt-BR) para obter detalhes.

O Adobe também oferece o Adobe Managed Services para implantar o AEM no Azure ou no AWS. O Adobe Managed Services fornece aos especialistas experiência e habilidades de implantação e operação do AEM nesses ambientes de computação em nuvem. Consulte [documentação adicional sobre o Adobe Managed Services](https://business.adobe.com/products/experience-manager/managed-services.html?aemClk=t).

Em todos os outros casos de implantação do AEM no Azure, no AWS ou em qualquer outro ambiente de computação em nuvem, o suporte do Adobe está contido no ambiente de computação virtual. Esse ambiente virtual deve ser executado em conformidade com as especificações técnicas listadas nesta página. Qualquer problema relatado relacionado ao AEM em execução em qualquer um desses ambientes de nuvem deve ser reproduzível independentemente de qualquer serviço de nuvem específico do ambiente de computação em nuvem. Ou seja, a menos que o serviço em nuvem seja compatível como parte dos requisitos técnicos listados nesta página, por exemplo, armazenamento Azure Blob ou AWS S3.

Para obter recomendações sobre como implantar o AEM no Azure ou no AWS, fora do Adobe Managed Services, o Adobe recomenda trabalhar diretamente com o provedor de nuvem. Ou trabalhar com parceiros de Adobe para apoiar a implantação do AEM no ambiente de nuvem de sua escolha. O provedor ou parceiro de nuvem selecionado é responsável pelas especificações de dimensionamento, design e implementação da arquitetura, para atender aos seus requisitos específicos de desempenho, carga, escalabilidade e segurança.

### Plataformas do Dispatcher (servidores da Web) {#dispatcher-platforms-web-servers}

O Dispatcher é o componente de balanceamento de carga e cache. [Baixe a versão mais recente do Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/release-notes.html). O Experience Manager 6.5 exige a versão 4.3.2 ou superior do Dispatcher.

Os seguintes servidores da Web são compatíveis para uso com o Dispatcher versão 4.3.2:

| Platform | Nível de compatibilidade |
|---|---|
| **Apache httpd 2.4.x** `[1,2]` | A: Suportado |
| Microsoft® IIS 10 (Servidor de Informações da Internet) | R: Suportado |
| Microsoft® IIS 8.5 (Servidor de Informações da Internet) | Z: Não suportado |

1. Os servidores web criados com base no código-fonte httpd do Apache têm tanto suporte quanto a versão do httpd na qual se baseia. Em caso de dúvida, peça ao Adobe a confirmação do nível de suporte relacionado ao respectivo produto de servidor. Os seguintes casos:

   1. O servidor HTTP foi criado usando apenas distribuições de origem oficiais do Apache, ou
   1. O servidor HTTP foi entregue como parte do sistema operacional no qual está sendo executado. Exemplos: IBM® HTTP Server, Oracle HTTP Server

1. O Dispatcher não está disponível para o Apache 2.4.x para sistemas operacionais Windows.

## Plataformas de cliente compatíveis {#supported-client-platforms}

### Navegadores compatíveis com a interface de criação de usuário {#supported-browsers-for-authoring-user-interface}

A interface do usuário do Adobe Experience Manager funciona com as seguintes plataformas de cliente. Todos os navegadores são testados com o conjunto padrão de plug-ins e complementos.

A interface do usuário do AEM é otimizada para telas maiores (normalmente notebooks e desktops) e o fator de forma do tablet (como Apple iPad ou Microsoft® Surface). O fator de forma do telefone não é compatível.

>[!NOTE]
>
**Suporte para navegadores com ciclos de lançamento rápidos:**
>
O Mozilla Firefox, o Google Chrome e o Microsoft® Edge lançam atualizações a cada poucos meses. O Adobe tem o compromisso de fornecer atualizações para que o Adobe Experience Manager mantenha o nível de suporte conforme declarado abaixo com as próximas versões desses navegadores.

<table>
 <tbody>
  <tr>
   <td><strong>Navegador</strong></td>
   <td><strong>Suporte para IU<br /> </strong></td>
   <td><strong>Suporte para IU Clássica</strong></td>
  </tr>
  <tr>
   <td><strong>Google Chrome (Evergreen)</strong></td>
   <td>A: Suportado</td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>Microsoft® Edge (Evergreen)</td>
   <td>A: Suportado</td>
   <td>A: Suportado</td>
  </tr>
  <tr>
   <td>Microsoft® Internet Explorer 11</td>
   <td>Z: Não suportado</td>
   <td>Z: Não suportado</td>
  </tr>
  <tr>
   <td>Mozilla Firefox (Evergreen)</td>
   <td>A: Suportado</td>
   <td>R: Suportado</td>
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
   <td>R: Suportado [2]</td>
   <td>Z: Não suportado</td>
  </tr>
  <tr>
   <td>Apple Safari no iOS 11.x</td>
   <td>Z: Não suportado</td>
   <td>Z: Não suportado</td>
  </tr>
 </tbody>
</table>

1. Versão de suporte estendido do Firefox [Saiba mais em mozilla.org](https://www.mozilla.org/en-US/firefox/enterprise/)
1. suporte para Apple iPad

### Navegadores compatíveis com sites {#supported-browsers-for-websites}

Geralmente, o suporte a navegadores para sites renderizados pelo AEM Sites depende da implementação de modelos de página AEM, do design e da saída de componentes e, portanto, está sob o controle da parte que implementa essas partes.

### Clientes WebDAV {#webdav-clients}

**Microsoft® Windows 7+**

Ao conectar com o Microsoft® Windows 7+ a uma instância AEM que não é protegida por SSL, a autenticação básica em uma rede não segura deve ser ativada no Windows. Ela requer uma alteração no Registro do Windows do WebClient:

1. Localize a sub-tecla do registro:

   * HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\WebClient\Parameters

1. Adicione a entrada de registro BasicAuthLevel a esta subchave usando um valor de 2 ou mais.

## Notas adicionais da plataforma {#additional-platform-notes}

Esta seção fornece notas especiais e informações mais detalhadas sobre a execução do Adobe Experience Manager e seus complementos.

### IPv4 e IPv6 {#ipv-and-ipv}

Todos os elementos de Adobe Experience Manager (Instância, Dispatcher) podem ser instalados nas redes IPv4 e IPv6.

A operação é perfeita, pois nenhuma configuração especial é necessária. Você especifica um endereço IP usando o formato apropriado ao seu tipo de rede, se necessário.

Quando um endereço IP deve ser especificado, você pode selecionar (conforme necessário) a seguir:

* Um endereço IPv6. Por exemplo, `https://[ab12::34c5:6d7:8e90:1234]:4502`

* Um endereço IPv4. Por exemplo, `https://123.1.1.4:4502`

* Um nome de servidor. Por exemplo, `https://www.yourserver.com:4502`

* O caso padrão de `localhost` é interpretado para instalações de rede IPv4 e IPv6. Por exemplo, `https://localhost:4502`

### Requisitos para o complemento AEM Dynamic Media {#requirements-for-aem-dynamic-media-add-on}

O AEM Dynamic Media está desativado por padrão. Consulte aqui para [ativar o Dynamic Media](/help/assets/config-dynamic.md#enabling-dynamic-media).

Com o Dynamic Media habilitado, os seguintes requisitos técnicos adicionais se aplicam.

>[!NOTE]
>
Esses requisitos de sistema **somente** se você usar o Dynamic Media - Modo híbrido; Dynamic Media - O modo híbrido tem um servidor de imagem incorporado, certificado somente em determinados sistemas operacionais.
>
Para clientes do Dynamic Media que executam o Dynamic Media - Modo Scene7 (ou seja, **dynamicmedia_scene7** modo de execução), não há requisitos de sistema adicionais; apenas os mesmos requisitos de sistema do AEM. Dynamic Media - A arquitetura de modo Scene7 usa o serviço de imagem baseado em nuvem e não o serviço incorporado no AEM.

#### Hardware {#hardware}

Os seguintes requisitos de hardware são aplicáveis ao Linux® e ao Windows:

* CPU Intel Xeon® ou AMD® Opteron com pelo menos quatro núcleos
* Pelo menos 16 GB de RAM

#### Linux® {#linux}

Se você estiver usando Dynamic Media no Linux®, os seguintes pré-requisitos devem ser atendidos:

* Red Hat® Enterprise 7 ou CentOS 7 e posterior com os patches de correção mais recentes
* Sistema operacional de 64 bits
* Troca desabilitada (recomendado)
* SELinux desativado (consulte a observação a seguir)

>[!NOTE]
>
Se o local for definido de modo que LC_CTYPE não seja igual a `en_US.UTF-8`, impede o funcionamento do Dynamic Media. Para ver seu valor, digite &quot;locale&quot; no prompt de comando. Se não estiver definido corretamente, defina a variável de ambiente LC_CTYPE como a string vazia digitando &quot;export LC_CTYPE=&quot; antes de executar o AEM.

>[!NOTE]
>
**Desativar o SELinux:** O Servidor de imagens não funciona com o SELinux ativado. Essa opção está ativada por padrão. Para corrigir esse problema, edite o **/etc/selinux/config** e altere o valor de SELinux de:
>
`SELINUX=enforcing` **para** `SELINUX=disabled`

>[!NOTE]
>
**Arquitetura NUMA:** sistemas com processadores AMD64 e Intel® EM64T são normalmente configurados como plataformas de arquitetura de memória não uniforme (NUMA). Ou seja, o kernel constrói vários nós de memória no momento da inicialização, em vez de construir uma única memória nó.
>
As múltiplas nó construção podem resultar em exaustão de memória em um ou mais nós antes que outros nós se esgotem. Quando ocorre esgotamento da memória, o kernel pode decidir eliminar processos (por exemplo, o Servidor de imagens ou o Servidor da plataforma) mesmo que haja memória disponível.
>
Portanto, a Adobe recomenda que, se você estiver executando um sistema desse tipo, desative o NUMA usando o **numa=off** opção de inicialização para evitar que o kernel mate esses processos.

>[!NOTE]
>
**O host nome do servidor deve resolver:** verifique se o host nome do servidor pode ser resolvido em um endereço IP. Se isso não for possível, adicione o nome da host totalmente qualificado e o endereço IP em **/etc/hosts**:
>
`<ip address> <fully qualified hostname>`

#### Windows {#windows}

* Microsoft® Windows Server 2016
* Trocar espaço igual a pelo menos o dobro da quantidade de memória física (RAM)

Para usar o Dynamic Media no Windows, instale o Microsoft® Visual Studio 2010, 2013 e 2015 redistribuível para x64 e x86.

Para Windows x64:

* Faça com que o Microsoft® Visual Studio 2010 fique redistribuível a [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Faça com que o Microsoft® Visual Studio 2013 fique redistribuível a [https://www.microsoft.com/en-us/download/details.aspx?id=40784](https://www.microsoft.com/en-us/download/details.aspx?id=40784)
* Receba a redistribuição do Microsoft® Visual Studio 2015 à [https://www.microsoft.com/en-us/download/details.aspx?id=48145](https://www.microsoft.com/en-us/download/details.aspx?id=48145)

Para Windows x86:

* Obtenha o Microsoft® Visual Studio 2010 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=26999](https://www.microsoft.com/en-us/download/details.aspx?id=26999)
* Obtenha o Microsoft® Visual Studio 2013 redistribuível em [https://www.microsoft.com/en-in/download/details.aspx?id=40769](https://www.microsoft.com/en-in/download/details.aspx?id=40769)
* Obtenha o Microsoft® Visual Studio 2015 redistribuível em [https://www.microsoft.com/en-us/download/details.aspx?id=52685](https://www.microsoft.com/en-us/download/details.aspx?id=52685)

#### macOS {#macos}

* 10.9.x e posterior
* Compatível somente com fins de avaliação e demonstração

### Requisitos para AEM Forms PDF Generator {#requirements-for-aem-forms-pdf-generator}

### Suporte de software para PDF Generator {#software-support-for-pdf-generator}

<table>
 <tbody>
  <tr>
   <th><p><strong>Produto</strong></p> </th>
   <th><p><strong>Formatos compatíveis para conversão em PDF</strong></p> </th>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Faixa clássica do Acrobat 2020</a> versão mais recente</td>
   <td>XPS, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html">Acrobat versão mais recente do classic faixa</a> de 2017 (obsoleta)</td>
   <td>XPS, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, DWG, DXF e DWF</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2019</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>Microsoft® Office 2016 (obsoleto)</td>
   <td>DOC, DOCX, XLS, XLSX, PPT, PPTX, RTF e TXT</td>
  </tr>
  <tr>
   <td>WordPerfect 2020<br /> </td>
   <td>WP, WPD</td>
  </tr>
  <tr>
   <td>Microsoft® Office Visio 2016 (obsoleto)<br /> </td>
   <td>VSD, VSDX</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2019<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Microsoft® Publisher 2016 (obsoleto)<br /> </td>
   <td>PUB</td>
  </tr>
  <tr>
   <td>Projeto Microsoft® 2016 (obsoleto)<br /> </td>
   <td>MPP</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.10</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF e TXT</td>
  </tr>
  <tr>
   <td>OpenOffice 4.1.2 (obsoleto)</td>
   <td>ODT, ODP, ODS, ODG, ODF, SXW, SXI, SXC, SXD, XLS, XLSX, DOC, DOCX, PPT, PPTX, formatos de imagem (BMP, GIF, JPEG, JPG, TIF, TIFF, PNG, JPF, JPX, JP2, J2K, J2C, JPC), HTML, HTM, RTF e TXT</td>
  </tr>  
 </tbody>
</table>

>[!NOTE]
>
O PDF Generator suporta apenas versões em inglês, francês, alemão e japonês dos sistemas operacionais e aplicativos suportados.
>
Além disso,
>
* O PDF Generator requer uma versão de 32 bits do [Faixa clássica do Acrobat 2020 versão 20.004.30006](https://helpx.adobe.com/acrobat/release-note/release-notes-acrobat-reader.html) ou Acrobat 2017 versão 17.011.30078 para executar a conversão.
* As conversões de PDF Generator para OpenOffice são suportadas apenas no Windows e no Linux®.
* O PDF Generator suporta apenas a versão comercial de 32 bits do Microsoft® Office Professional Plus e outros softwares necessários para a conversão no sistema operacional Windows.
* O PDF Generator suporta as versões de 32 e 64 bits do OpenOffice no sistema operacional Linux®.
* PDF Generator não suporta Microsoft® Office 365.
* Os recursos PDF, Optimize PDF e Export PDF de OCR são suportados apenas no Windows.
* Uma versão do Acrobat é fornecida com o AEM Forms para ativar a funcionalidade PDF Generator. Acesse programaticamente a versão agrupada somente com o AEM Forms, durante o prazo da licença do AEM Forms, para uso com o AEM Forms PDF Generator. Para obter mais informações, consulte a Descrição do produto AEM Forms de acordo com a implantação ([No local](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-on-premise.html) ou [Managed Services](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-manager-managed-services.html))
* O serviço PDF Generator não suporta Microsoft® Windows 10.
* Falha do PDF Generator ao converter arquivos usando o Microsoft® Visio 2019. Você pode continuar a usar o Microsoft® Visio 2016 para converter `.VSD` e `.VSDX` arquivos.
* Falha do PDF Generator ao converter arquivos usando o Microsoft® Project 2019. Você pode continuar a usar o Microsoft® Project 2016 para converter `.VSD` e `.VSDX` arquivos.
>

### Requisitos para o AEM Forms Designer {#requirements-for-aem-forms-designer}

* Microsoft® Windows® 2016 Server, Microsoft® Windows® 2019 Server ou Microsoft® Windows® 10
* Processador 1 GHz ou mais rápido com suporte para PAE, NX e SSE2.
* 1 GB de RAM para 32 bits ou 2 GB de RAM para SO de 64 bits
* Espaço em disco de 16 GB para espaço em disco de 32 ou 20 GB para sistema operacional de 64 bits
* Memória gráfica - 128 MB de GPU (recomendado de 256 MB)
* 2,35 GB de espaço disponível em disco rígido
* Resolução do monitor de 1024 X 768 pixels ou superior
* Aceleração de hardware de vídeo (opcional)
* Acrobat Pro DC, Acrobat Standard DC ou Adobe Acrobat Reader DC
* Privilégios administrativos para instalar o Designer
* Microsoft Visual C++ 2019 (VC 14.28 ou superior) tempo de execução de 32 bits para AEM Forms Designer de 32 bits
* Microsoft Visual C++ 2019 (VC 14.28 ou superior) Runtime de 64 bits para AEM Forms Designer de 64 bits (para pilha OSGI e JEE)

### Requisitos para write-back de metadados do AEM Assets XMP {#requirements-for-aem-assets-xmp-metadata-write-back}

XMP write-back é compatível e ativado para as seguintes plataformas e formatos de arquivo:

* **Sistemas operacionais:**

   * Linux® (suporte para aplicativos de 32 e 32 bits em sistemas de 64 bits). Para ver as etapas de instalação de bibliotecas de clientes de 32 bits, consulte [Como habilitar a extração e a gravação do XMP no Red Hat® Linux® de 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).

   * Windows Server
   * macOS X (64 bits)

* **Formatos de arquivo**: JPEG, PNG, TIFF, PDF, INDD, AI e EPS.

### Requisitos para a AEM Assets processar ativos com muitos metadados no Linux® {#assetsonlinux}

O processo XMPFilesProcessor exige que o biblioteca GLIBC_2.14 funcione. Use um kernel do Linux® que contém GLIBC_2.14, por exemplo, o kernel do Linux® versão 3.1.x. Melhora o desempenho do processamento de ativos que contêm uma grande quantidade de metadados, curtir arquivos PSD. A utilização de uma versão anterior do GLIBC resulta em erros em logs que começam com `com.day.cq.dam.core.impl.handler.xmp.NCommXMPHandler Failed to read XMP`.