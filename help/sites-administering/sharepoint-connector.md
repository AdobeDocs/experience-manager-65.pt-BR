---
title: SharePoint Connector
description: Conector Day JCR para Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versão 4.0.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
feature: Integration
role: Admin
source-git-commit: c4133584e9c2328b3a55042902c67770d78afcf7
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 0%

---

# SharePoint Connector{#sharepoint-connector}

Este artigo inclui detalhes sobre o Conector JCR do Adobe para Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versão 4.0.

O conector do SharePoint é compatível com as seguintes funcionalidades básicas:

* Leitura de conteúdo e metadados do SharePoint.
* Confirmar as configurações de segurança do SharePoint para o conteúdo acessado aplicando autenticação e autorização nativas do SharePoint
* Integração de conteúdo usando o Localizador de conteúdo
* Uso de componentes do AEM, como o Recurso externo, para exibir imagens e vídeos do SharePoint
* Sincronização do SharePoint com o AEM Assets

Todas as funcionalidades são implementadas usando os serviços Web nativos do SharePoint como interface para o conteúdo e os serviços do SharePoint.

>[!NOTE]
>
>O SharePoint Connector também é compatível com o AEM 6.1 service pack 2. O conector não é mais compatível com a montagem de repositório virtual e, portanto, não pode ser montado. Se quiser acessar o repositório do Sharepoint usando APIs Java, use a implementação do repositório JCR do conector do Sharepoint em seu projeto.
>
>A instalação, a configuração, o gerenciamento e as operações de TI do servidor SharePoint e a infraestrutura de TI relacionada estão fora do escopo deste documento. Consulte a documentação do fornecedor no [SharePoint](https://www.microsoft.com/sharepoint) para obter informações sobre esses tópicos. O conector exige que essas partes da infraestrutura sejam instaladas, configuradas e operadas corretamente.
>

## Introdução {#getting-started}

Para começar a usar o conector, faça o seguinte:

* Verifique se você tem pelo menos o Java 7 instalado.
* Baixe o arquivo de distribuição do pacote de conectores da Distribuição de software.
* Copie um arquivo válido *license.properties* para o diretório que contém o arquivo *cq-quickstart-6.4.0.jar*.

* Clique duas vezes no arquivo .jar para iniciar o AEM ou inicie-o a partir da linha de comando.
* Instale o pacote de conectores a partir do Gerenciador de pacotes.
* Configure as opções de conector.

## Instalação do conector do SharePoint {#installing-sharepoint-connector}

O conector é um pacote de conteúdo que facilita a instalação. Instale o pacote usando o Gerenciador de pacotes e depois defina o URL do servidor do SharePoint
e outras opções de configuração. O conteúdo do SharePoint está disponível no repositório AEM.

### Requisitos de instalação {#installation-requirements}

O conector exige o seguinte:

* Java Runtime Environment 1.7 ou posterior
* Serviços da Web da SharePoint disponíveis por meio da rede
* URL do servidor do SharePoint
* Credenciais de usuário e permissões para repositórios do CRX e SharePoint
* [Plataformas compatíveis](#supported-platforms)

O conector do SharePoint está disponível para download em [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plataformas compatíveis {#supported-platforms}

O conector é compatível com o seguinte:

* Versões do AEM:

   * AEM 6.4, 6.3

* Versões do Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Se você precisar de suporte para implantações personalizadas do conector (OEM, requisitos especiais, métodos de autenticação personalizados), entre em contato com o escritório da Adobe da sua região.

>[!NOTE]
>
>O conector é compatível apenas com configurações oficialmente compatíveis com o Microsoft. Consulte os requisitos do sistema [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) e [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx).

### Instalação padrão {#standard-installation}

A Distribuição de software é usada para distribuir recursos, exemplos e hot fixes do produto. Para obter detalhes, consulte a [documentação de Distribuição de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Integração com o AEM {#integrating-with-aem}

Para instalar o pacote de conteúdo do conector.

1. Abra um tíquete de Suporte Adobe para solicitar o pacote de recursos do conector.
1. Baixe o pacote quando ele estiver disponível e abra o Gerenciador de pacotes para sua instância do AEM.
1. Clique em **Instalar** na página de descrição do pacote.
1. Na caixa de diálogo **Instalar Pacote**, clique em **Instalar**.

   **Observação**: verifique se você está conectado como administrador.

1. Quando o pacote estiver instalado, clique em **Fechar**.

## Configuração do conector do SharePoint {#configuring-sharepoint-connector}

Depois de instalar o conector do SharePoint, configure o aplicativo e as camadas do SharePoint para o conector.

Defina o URL do servidor do SharePoint para tornar seu repositório do SharePoint compatível com JCR. Você pode definir parâmetros adicionais para configurar a conexão com o servidor do SharePoint. Além disso, configure a autenticação com o conector do SharePoint.

### Configuração da conexão com o servidor do SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Para definir o URL do servidor do SharePoint e as opções avançadas, execute estas etapas:

1. Navegue até o Console de Gerenciamento OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Procure o Conector JCR do **Day para o pacote do Microsoft Sharepoint**.
1. Edite os valores de configuração.
1. Defina a URL do SharePoint Server como o valor de **Workspaces**.
1. Clique em **Salvar**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parâmetros &quot;Espaços de trabalho&quot; e &quot;Nome padrão do Workspace&quot;:

Por padrão, o conector expõe um único espaço de trabalho JCR. O servidor do SharePoint exposto por este espaço de trabalho é definido por meio do parâmetro de configuração &#39;URL do Sharepoint Server&#39;.

O conector também pode ser configurado para vários espaços de trabalho. Nesse caso, cada espaço de trabalho é associado ao URL do respectivo servidor do SharePoint exposto por meio do espaço de trabalho. Para adicionar um espaço de trabalho, adicione uma definição de espaço de trabalho ao parâmetro Workspaces. Uma definição de espaço de trabalho tem o seguinte formato:
`<name>`= `<url>` onde
`<name>` é o nome do espaço de trabalho JCR e
`<url>` é a URL do servidor SharePoint para esse espaço de trabalho.

No AEM, execute mais uma etapa além das etapas de configuração acima. Lista de permissões o pacote &#39;**com.day.cq.dam.cq-dam-jcr-connectors**&#39;.

Para lista de permissões pacotes no AEM, execute as seguintes etapas:

1. Navegue até o Console de gerenciamento OSGi: http://localhost:4502/system/console/configMgr.
1. Procure o serviço &quot;Apache Sling Login Admin Whitelist&quot;.
1. Selecione **Ignorar a lista de permissões**.
1. Adicionar `com.day.cq.dam.cq-dam-jcr-connectors` à lista de permissões de pacotes padrão
1. Clique em Salvar.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Se você configurar vários espaços de trabalho, especifique o nome do espaço de trabalho default no parâmetro Default Workspace Name.

Para obter informações adicionais sobre parâmetros relacionados à autenticação, consulte [Autenticação](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verificando a configuração do Sharepoint {#verifying-the-sharepoint-setup}

Após configurar o conector, verifique o seguinte:

* O servidor do SharePoint é executado e os serviços da Web podem ser acessados pela instância do conector
* As credenciais de usuário do SharePoint são válidas e o usuário tem as permissões necessárias do SharePoint
* O conector está instalado e configurado corretamente

### Configuração da sincronização do DAM com o servidor do SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Para sincronizar o SharePoint Assets com AEM, execute as seguintes etapas:

1. Navegue até o Console de Gerenciamento OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Procure o serviço &quot;Default DAMAssetSynchronization&quot;.
1. Edite os valores de configuração.
1. Defina o nome de usuário e a Senha correspondente do usuário com acesso no site do SharePoint.
1. Clique em Salvar.

Habilitar o Serviço de sincronização do DAM, que está desabilitado por padrão:

1. Navegue até os Componentes do Console da Web do OSGi: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Pesquise por &quot;com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService&quot;.
1. Clique em Ativar.

Como opção, você pode configurar o atraso de sincronização entre diferentes ciclos de sincronização:

1. Navegue até o Console de Gerenciamento OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Procure por &quot;Serviço de sincronização de ativos do conector JCR DAY CQ DAM&quot;.
1. Edite os valores de configuração.
1. Defina o valor do Período de sincronização (em segundos).
1. Clique em Salvar.

### Configurando a autenticação {#configuring-authentication}

O Sharepoint inclui os métodos de autenticação Clássico e Baseado em Declarações, que oferecem suporte aos seguintes tipos de autenticação:

* Básico
* Baseado em Forms

Especificamente, os seguintes tipos de autenticação estão disponíveis:

* Classic-Basic
* Baseado em Forms clássico
* Argumentos Básicos
* Baseado em Forms para solicitações

O Conector JCR do AEM para Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versão 4.0. é compatível com autenticação baseada em declarações (sugerida pela Microsoft), que opera nos seguintes modos:

* **Autenticação básica/NTLM**: primeiro, o conector tenta se conectar usando a autenticação básica. Se não estiver disponível, ele alternará para a autenticação baseada em NTLM.
* **Autenticação com base em Forms**: o Sharepoint valida os usuários com base nas credenciais digitadas por eles em um formulário de logon (geralmente uma página da Web). O sistema emite um token para solicitações autenticadas que contém uma chave para restabelecer a identidade para solicitações subsequentes.

**Configurando a Autenticação Baseada no Forms**

Ir para: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Clique em OSGI > Configuração
1. Pesquisar &quot;Conector Day JCR para Microsoft Sharepoint&quot;
1. Clique em &quot;Editar os valores de configuração&quot;
1. Defina o valor de &#39;Sharepoint Connection Fatory&#39; como &#39;com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory&#39;
1. Clique em **Salvar**.

**Configurando Autenticação Básica (Windows)**

1. [Desabilitar Autenticação de Token](#disable-token-authentication).
1. Ir para [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Clique em OSGI > Configuração.
1. Pesquise por **Day JCR Connector para Microsoft Sharepoint**.
1. Clique em `Edit the configuration values`.
1. Defina o valor da Fábrica de Conexões do Sharepoint para `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Clique em **Salvar**.

Somente um usuário autenticado no AEM e no SharePoint pode acessar o conteúdo do SharePoint por meio do conector.

Você também pode usar a extensão do conector para autenticação a fim de criar um módulo de autenticação personalizado, que, por exemplo, mapeia o acesso de usuários do AEM a usuários específicos do SharePoint. Crie usuários do AEM correspondentes aos usuários do SharePoint (o nome de usuário e a senha devem corresponder) para poder ver o conteúdo do SharePoint mapeado para a instância do conector.

Para criar um usuário no AEM:

1. Faça logon em http://localhost:9502/with para o usuário administrador.
1. Clique em Ferramentas.
1. Clique em Segurança.
1. Clique em Usuários.
1. Clique em **Criar Usuário**.
1. Forneça a ID do usuário (nome de usuário com acesso no SharePoint).
1. Forneça a senha correspondente.
1. Clique no símbolo de marca de verificação verde para criar o usuário.

Para adicionar o usuário no grupo de administradores:

1. Vá para Administração de grupo.
1. Clique no nó &quot;a&quot;.
1. Clique em &quot;administradores&quot;.
1. Digite a ID de usuário criada acima na caixa de texto antes do botão **Procurar**.
1. Clique no símbolo de marca de seleção Verde para adicionar o usuário ao grupo de administradores.

### Desativar autenticação de token {#disable-token-authentication}

1. Baixar e instalar o pacote `basic auth`. `zip` da Distribuição de software.

1. Fechar Início Rápido.
1. Abra o arquivo *\crx-quickstart\repository\repository.xml*.
1. Localizar a marca `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Insira a tag `<param name="disableTokenAuth" value="true"/>` dentro da tag mencionada na etapa 4.
1. Salve e feche o arquivo xml.
1. Reinicie o QuickStart e faça logon com suas credenciais.

#### Suporte a diferentes métodos de autenticação do servidor do SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

Na sua versão padrão, o conector oferece suporte à autenticação padrão do IIS **Windows** (Básica) e à autenticação baseada em Forms (baseada em token). Os [outros métodos de autenticação](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) podem ter suporte por meio do mecanismo de extensibilidade.

As etapas a seguir fornecem diretrizes sobre a extensão da autenticação padrão para suportar vários métodos de autenticação do servidor SharePoint:

1. Implemente o `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` para lidar com o lado do cliente do seu processo de autenticação específico.
1. Instale a implementação `SharepointConnectionFactory` como um conjunto de fragmentos com o host de fragmento `com.day.crx.spi.crx2sharepoint-bundle`.

   Ao usar o Maven, adapte a seguinte configuração do `maven-bundle-plugin` aos requisitos do seu projeto:

   ```xml
              <plugin>
                  <groupId>org.apache.felix</groupId>
                  <artifactId>maven-bundle-plugin</artifactId>
                  <extensions>true</extensions>
                  <configuration>
                      <instructions>
                          <Export-Package />
                          <Private-Package>
                              <!-- your private package here -->
                          </Private-Package>
                          <Fragment-Host>
                              com.day.crx.spi.crx2sharepoint-bundle
                          </Fragment-Host>
                       </instructions>
                  </configuration>
              </plugin>
   ```

1. Registre a implementação `SharepointConnectionFactory` na configuração do conector. Na janela de configuração do conector, clique em **Opções avançadas**. No campo para **Fábrica de Conexões do Sharepoint**, especifique o nome da implementação `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Reinicie o conector.
