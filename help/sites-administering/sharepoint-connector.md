---
title: Conector SharePoint
seo-title: SharePoint Connector
description: Conector JCR do dia para Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versão 4.0.
seo-description: Learn about the Sharepoint Connector in AEM.
uuid: df650476-4e2a-486f-a007-b5ac437ff99f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 907316d1-3d23-4c46-bccb-bad6fe1bd1bb
docset: aem65
exl-id: 10ea7d2e-6e44-4d5c-a2b2-63c73b18f172
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 3%

---

# Conector SharePoint{#sharepoint-connector}

Este artigo inclui detalhes sobre o Adobe JCR Connector for Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versão 4.0.

O conector SharePoint é compatível com as seguintes funcionalidades básicas:

* Leitura de conteúdo e metadados do SharePoint.
* Confirmando as configurações de segurança do SharePoint para o conteúdo acessado aplicando a autenticação e a autorização nativas do SharePoint
* Integração de conteúdo usando o Localizador de conteúdo
* Uso de componentes AEM, como Recurso externo para exibir imagens e vídeos do SharePoint
* Sincronização do SharePoint com o AEM Assets

Todas as funcionalidades são implementadas usando os serviços Web nativos da SharePoint como interface para o conteúdo e os serviços da SharePoint.

>[!NOTE]
>
>O SharePoint Connector também é compatível com o AEM 6.1 service pack 2. O conector não oferece mais suporte à montagem do repositório virtual e, portanto, não pode ser montado. Se quiser acessar o repositório do Sharepoint usando APIs Java, use a implementação do repositório JCR do conector do Sharepoint no seu projeto.
>
>As operações de instalação, configuração, gerenciamento e TI do servidor SharePoint e da infraestrutura de TI relacionada estão fora do escopo deste documento. Consulte a documentação do fornecedor em [SharePoint](https://www.microsoft.com/sharepoint) para obter informações sobre esses tópicos. O conector requer que essas partes da infraestrutura sejam corretamente instaladas, configuradas e operadas.

## Introdução {#getting-started}

Para começar a usar o conector, faça o seguinte:

* Certifique-se de ter pelo menos o Java 7 instalado.
* Baixe o arquivo de distribuição do pacote de conectores na Distribuição do software.
* Copiar um *license.properties* para o diretório que contém a variável *cq-quickstart-6.4.0.jar* arquivo.

* Clique/toque duas vezes no arquivo .jar para iniciar o AEM ou inicie-o a partir da linha de comando.
* Instale o pacote de conectores no Gerenciador de pacotes.
* Configure as opções do conector.

## Instalação do conector SharePoint {#installing-sharepoint-connector}

O conector é um pacote de conteúdo que facilita a instalação fácil. Instale o pacote usando o Gerenciador de pacotes e, em seguida, defina o URL do servidor do SharePoint e outras opções de configuração. O conteúdo do SharePoint está disponível no repositório AEM.

### Requisitos de instalação {#installation-requirements}

O conector requer o seguinte:

* Java Runtime Environment 1.7 ou posterior
* Serviços Web da SharePoint disponíveis através da rede
* URL do servidor SharePoint
* Credenciais do usuário e permissões para repositórios CRX e SharePoint
* [Plataformas compatíveis](#supported-platforms)

O conector SharePoint está disponível para download no [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq630/featurepack/cq-6.3.0-featurepack-17673).

### Plataformas compatíveis {#supported-platforms}

O conector é compatível com o seguinte:

* AEM versões:

   * AEM 6.4, 6.3

* Versões do Microsoft SharePoint:

   * Microsoft Office SharePoint Server (MOSS) 2010
   * Microsoft Office SharePoint Server (MOSS) 2013

* Se você precisar de suporte para implantações personalizadas do conector (OEM, requisitos especiais, métodos de autenticação personalizados), entre em contato com o Adobe da sua região.

>[!NOTE]
>
>O conector só suporta configurações oficialmente compatíveis com o Microsoft. Consulte [MOSS 2010](https://technet.microsoft.com/en-us/library/cc262485(office.14).aspx) e [MOSS 2013](https://technet.microsoft.com/en-us/library/cc262485.aspx) requisitos do sistema.

### Instalação padrão {#standard-installation}

A Distribuição de software é usada para distribuir recursos do produto, exemplos e hot fixes. Para obter detalhes, consulte o [Documentação de distribuição de software](https://experienceleague.adobe.com/docs/experience-cloud/software-distribution/home.html#software-distribution).


#### Integração com AEM {#integrating-with-aem}

Para instalar o pacote de conteúdo do conector.

1. Abra um tíquete de suporte do Adobe para solicitar o pacote de recursos do conector.
1. Baixe o pacote quando ele estiver disponível e abra o Gerenciador de pacotes para sua instância do AEM.
1. Toque/clique **Instalar** na página de descrição do pacote.
1. No **Instalar pacote** , toque/clique **Instalar**.

   **Observação**: Certifique-se de estar conectado como administrador.

1. Quando o pacote estiver instalado, toque/clique em **Fechar**.

## Configuração do conector SharePoint {#configuring-sharepoint-connector}

Depois de instalar o conector do SharePoint, configure o aplicativo e as camadas do SharePoint para o conector.

Defina o URL do servidor do SharePoint para tornar seu repositório do SharePoint compatível com o JCR. Você pode definir parâmetros adicionais para configurar a conexão com o servidor do SharePoint. Além disso, configure a autenticação com o conector do SharePoint.

### Configuração da conexão com o servidor SharePoint {#configuring-the-connection-with-the-sharepoint-server}

Para definir o URL do servidor SharePoint e as opções avançadas, execute estas etapas:

1. Navegue até o Console de Gerenciamento OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Procure a variável **Conector JCR do dia para Microsoft Sharepoint** pacote.
1. Edite os valores de configuração.
1. Defina o URL do servidor do SharePoint como o valor de **Áreas de trabalho**.
1. Toque/clique **Salvar**.

![chlimage_1-62](assets/chlimage_1-62.png)

Parâmetros de &#39;Espaços de trabalho&#39; e &#39;Nome padrão do espaço de trabalho&#39;:

Por padrão, o conector expõe um único espaço de trabalho JCR. O servidor do SharePoint exposto por esse espaço de trabalho é definido por meio do parâmetro de configuração &quot;URL do servidor do Sharepoint&quot;.

O conector também pode ser configurado para vários espaços de trabalho. Nesse caso, cada espaço de trabalho é associado ao URL do respectivo servidor do SharePoint que é exposto por meio do espaço de trabalho. Para adicionar um espaço de trabalho, adicione uma definição de espaço de trabalho ao parâmetro Espaços de trabalho . Uma definição de espaço de trabalho tem o seguinte formato:
`<name>`= `<url>` em que
`<name>` é o nome do espaço de trabalho JCR e
`<url>` é o URL do servidor SharePoint para esse espaço de trabalho.

No AEM, execute mais uma etapa além das etapas de configuração acima. Lista de permissões o &#39;**com.day.cq.dam.cq-dam-jcr-connectors** Pacote &#39;.

Para lista de permissões pacotes no AEM, execute as seguintes etapas:

1. Navegue até o Console de Gerenciamento OSGi: http://localhost:4502/system/console/configMgr.
1. Procure por serviço &quot;Apache Sling Login Admin Whitelist&quot;.
1. Selecionar **Ignorar a lista de permissões**.
1. Adicionar `com.day.cq.dam.cq-dam-jcr-connectors` em pacotes de lista de permissões padrão
1. Clique em Salvar.

![chlimage_1-82](assets/chlimage_1-82a.png)

>[!NOTE]
>
>Se você configurar vários espaços de trabalho, especifique o nome do espaço de trabalho padrão no parâmetro Nome do espaço de trabalho padrão .

Para obter mais informações sobre parâmetros relacionados à autenticação, consulte [Autenticação](/help/sites-administering/sharepoint-connector.md#configuring-authentication).

### Verificar a configuração do Sharepoint {#verifying-the-sharepoint-setup}

Depois de configurar o conector, verifique o seguinte:

* O servidor do SharePoint é executado e os serviços da Web são acessíveis para a instância do conector
* As credenciais do usuário do SharePoint são válidas e o usuário tem as permissões necessárias do SharePoint
* O conector está instalado e configurado corretamente

### Configuração da sincronização DAM com o servidor do SharePoint {#configuring-dam-sync-with-the-sharepoint-server}

Para sincronizar o SharePoint Assets com o AEM, execute as seguintes etapas:

1. Navegue até o Console de Gerenciamento OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr).
1. Procure pelo serviço &quot;Default DAMAssetSynchronization&quot;.
1. Edite os valores de configuração.
1. Defina o nome de usuário e a Senha correspondente do usuário com acesso no site do SharePoint.
1. Clique em Salvar.

Ative o Serviço de sincronização DAM, que é desativado por padrão:

1. Navegue até os Componentes do console da Web OSGi: [http://localhost:4502/system/console/components](http://localhost:4502/system/console/components)
1. Procure por &quot;com.day.cq.dam.jcrconnectors.impl.AssetSynchronizationService&quot;.
1. Clique em Ativar.

Como opção, você pode configurar o atraso de sincronização entre diferentes ciclos de sincronização:

1. Navegue até o Console de Gerenciamento OSGi: [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
1. Procure por &quot;DAY CQ DAM JCR Connector Asset Synchronization Service&quot;.
1. Edite os valores de configuração.
1. Defina o valor do Período de sincronização (em segundos).
1. Clique em Salvar.

### Configurar autenticação {#configuring-authentication}

O Sharepoint inclui os métodos de autenticação Clássico e Baseado em Reivindicações , ambos com suporte para os seguintes tipos de autenticação:

* Básico
* Baseado em Forms

Em particular, os seguintes tipos de autenticação estão disponíveis:

* Classic-Basic
* Baseado no Forms clássico
* Reivindicações - Básicas
* Baseado em reivindicações Forms

O AEM JCR Connector for Microsoft SharePoint 2010 e Microsoft SharePoint 2013, versão 4.0. oferece suporte à autenticação baseada em declarações (sugerida pela Microsoft), que opera nos seguintes modos:

* **Autenticação básica/NTLM**: O conector primeiro tenta se conectar usando a autenticação básica. Se não estiver disponível, ele alternará para autenticação baseada em NTLM.
* **Autenticação baseada em Forms**: O SharePoint valida os usuários com base nas credenciais que os usuários digitam em um formulário de logon (normalmente uma página da Web). O sistema emite um token para solicitações autenticadas que contém uma chave para restabelecer a identidade de solicitações subsequentes.

**Configurar a autenticação baseada em Forms**

Vá para: [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles)

1. Clique em OSGI -> Configuração
1. Pesquise &quot;Conector Day JCR para Microsoft Sharepoint&quot;
1. Clique em &quot;Editar os valores de configuração&quot;
1. Defina o valor de &quot;Fábrica de Conexão do Sharepoint&quot; como &quot;com.day.crx.spi.sharepoint.security.FormsBasedAuthenticationConnectionFactory&quot;
1. Clique em **Salvar**.

**Configurando a Autenticação Básica (Windows)**

1. [Desativar Autenticação de Token](#disable-token-authentication).
1. Ir para [http://localhost:4502/system/console/bundles](http://localhost:4502/system/console/bundles).
1. Clique em OSGI > Configuração.
1. Procurar por **Conector JCR do dia para Microsoft Sharepoint**.
1. Clique em `Edit the configuration values`.
1. Defina o valor da Fábrica de Conexões do Sharepoint como `com.day.crx.spi.sharepoint.security.WindowsAuthenticationConnectionFactory`.
1. Clique em **Salvar**.

Somente um usuário autenticado no AEM e no SharePoint pode acessar o conteúdo do SharePoint por meio do conector.

Você também pode usar a extensão do conector para autenticação para criar um módulo de autenticação personalizado, que, por exemplo, mapeia o acesso de usuários AEM a usuários específicos do SharePoint. Crie AEM usuários correspondentes a usuários do SharePoint (o nome de usuário e a senha devem corresponder) para poder ver o conteúdo do SharePoint mapeado para a instância do conector.

Para criar um usuário no AEM:

1. Faça logon em http://localhost:9502/with o usuário administrador.
1. Clique em Ferramentas.
1. Clique em Segurança.
1. Clique em Usuários.
1. Clique em **Criar usuário**.
1. Forneça a ID do usuário (nome de usuário com acesso no SharePoint).
1. Forneça a senha correspondente.
1. Clique no símbolo de marca de verificação verde para criar o usuário.

Para adicionar o usuário no grupo de administradores:

1. Vá para Administração de grupo.
1. Clique no nó &quot;a&quot;.
1. Clique em &quot;administradores&quot;.
1. Digite a ID de usuário criada acima na caixa de texto antes de **Procurar** botão.
1. Clique no símbolo de marca de verificação verde para adicionar o usuário ao grupo de administradores.

### Desativar Autenticação de Token {#disable-token-authentication}

1. Baixe e instale o pacote `basic auth`. `zip` da Distribuição de software.

1. Feche o Início Rápido.
1. Abra o arquivo *\crx-quickstart\repository\repository.xml*.
1. Encontre a tag `<LoginModule class="com.day.crx.core.CRXLoginModule"> ... </LoginModule>.`
1. Inserir a tag `<param name="disableTokenAuth" value="true"/>` dentro da tag mencionada na etapa 4.
1. Salve e feche o arquivo xml.
1. Reinicie o QuickStart e faça logon com suas credenciais.

#### Suporte a diferentes métodos de autenticação do servidor SharePoint {#supporting-different-authentication-methods-of-the-sharepoint-server}

Em sua versão padrão, o conector é compatível com o IIS padrão **Windows** autenticação (Básica) e autenticação baseada em Forms (baseada em token). O [outros métodos de autenticação](https://technet.microsoft.com/en-us/library/cc262350.aspx#section2) O pode ser suportado pelo mecanismo de extensibilidade.

As etapas a seguir fornecem diretrizes sobre a extensão da autenticação padrão para suportar vários métodos de autenticação do servidor SharePoint:

1. Implementar `com.day.crx.spi.sharepoint.security.SharepointConnectionFactory` para lidar com o lado do cliente do seu processo de autenticação específico.
1. Instale o `SharepointConnectionFactory` implementação como um pacote de fragmentos com o host de fragmento `com.day.crx.spi.crx2sharepoint-bundle`.

   Ao usar Maven, adapte a seguinte configuração do `maven-bundle-plugin` de acordo com os requisitos do seu projeto:

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

1. Registre o `SharepointConnectionFactory` implementação na configuração do conector. Na janela de configuração do conector, clique em **Opções avançadas**. No para **Fábrica do Sharepoint Connection** , especifique o nome da implementação `com.day.crx.spi.sharepoint.auth.CustomConnectionFactory`.

1. Reinicie o conector.
