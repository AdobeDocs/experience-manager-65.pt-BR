---
title: Configuração do OSGi
seo-title: Configuring OSGi
description: O OSGi é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos de AEM e sua configuração. Este artigo detalha como é possível gerenciar as definições de configuração desses pacotes.
seo-description: OSGi is a fundamental element in the technology stack of Adobe Experience Manager (AEM). It is used to control the composite bundles of AEM and their configuration. This article details how you can manage the configuration settings for such bundles.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 0%

---

# Configuração do OSGi{#configuring-osgi}

[OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos de AEM e sua configuração.

OSGi &quot;*O fornece as primitivas padronizadas que permitem que os aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados*&quot;.

Isso permite o fácil gerenciamento de pacotes, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são tratadas automaticamente. Cada componente OSGi (consulte a [Especificação OSGi](https://docs.osgi.org/specification/)) está contido em um dos vários pacotes.

Você pode gerenciar as definições de configuração desses pacotes ao:

* usando o [Console da Web do Adobe CQ](#osgi-configuration-with-the-web-console)
* usar [arquivos de configuração](#osgi-configuration-with-configuration-files)
* configurando [nós de conteúdo ( `sling:OsgiConfig`) no repositório](#osgi-configuration-in-the-repository)

Ambos os métodos podem ser usados, embora existam diferenças sutis, principalmente em relação a [Modos de execução](/help/sites-deploying/configure-runmodes.md):

* [Console da Web do Adobe CQ](#osgi-configuration-with-the-web-console)

   * O Console da Web é a interface padrão para a configuração do OSGi. Ela fornece uma interface para editar as várias propriedades, onde os valores possíveis podem ser selecionados nas listas predefinidas.

     Como tal, é o método mais fácil de usar.

   * Quaisquer configurações feitas com o Console da Web são aplicadas imediatamente e aplicáveis à instância atual, independentemente do modo de execução atual ou de qualquer alteração subsequente no modo de execução.

* [arquivos de configuração](#osgi-configuration-with-configuration-files)

   * Contêm configurações definidas no console da Web.
   * Podem ser incluídos em pacotes de conteúdo para uso em outras instâncias.

* [nós de conteúdo (sling:osgiConfig) no repositório](#osgi-configuration-in-the-repository)

   * Requer configuração manual usando CRXDE Lite.
   * Devido às convenções de nomenclatura do `sling:OsgiConfig` nós, é possível vincular a configuração a um [modo de execução](/help/sites-deploying/configure-runmodes.md). Você pode até mesmo salvar configurações para mais de um modo de execução no mesmo repositório.
   * Todas as configurações apropriadas são aplicadas imediatamente (dependendo do modo de execução).

Qualquer que seja o método usado, todos esses métodos de configuração:

* Certifique-se de que copiar ou replicar o conteúdo do repositório recrie configurações idênticas.
* Permite que você faça check-out das configurações para o FileVault ou Subversion; para segurança ou para atualizações adicionais.
* Podem ser salvas em pacotes para uso ao configurar outras instâncias.
* Permite executar implantações de configuração usando scripts para propagar os detalhes da configuração.

>[!NOTE]
>
>Os detalhes de determinadas configurações importantes estão listados em [Configurações do OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configuração do OSGi com o console da Web {#osgi-configuration-with-the-web-console}

A variável [Console da Web](/help/sites-deploying/web-console.md) no AEM fornece uma interface padronizada para configurar os pacotes. A variável **Configuração** é usada para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar os parâmetros do sistema AEM.

Quaisquer alterações feitas são aplicadas imediatamente à configuração OSGi relevante; não é necessário reiniciar.

>[!NOTE]
>
>As alterações feitas no console da Web são salvas no repositório como [arquivos de configuração](#osgi-configuration-with-configuration-files). Esses arquivos podem ser incluídos em pacotes de conteúdo para reutilização em instalações adicionais.

>[!NOTE]
>
>No console da Web, todas as descrições que mencionam as configurações padrão estão relacionadas aos padrões do Sling.
>
>O Adobe Experience Manager tem seus próprios padrões e, portanto, os padrões definidos podem ser diferentes dos padrões documentados no console.

Para atualizar uma configuração com o console da Web:

1. Acesse o **Configuração** do Console da Web:

   * Ao abrir o console da Web no link no **Ferramenta > Operações** menu. Depois de fazer logon no console, você pode usar o menu suspenso de:

     **OSGi >**

   * O URL direto; por exemplo:

     `http://localhost:4502/system/console/configMgr`

   Uma lista é exibida.

1. Selecione o pacote que você deseja configurar:

   * clicando no **Editar** ícone desse pacote
   * clicando no **Nome** do pacote

1. Uma caixa de diálogo é aberta. Aqui é possível editar conforme necessário. Por exemplo, defina a variável **Nível de registro** para `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >As atualizações são salvas no repositório como [arquivos de configuração](#osgi-configuration-with-configuration-files). Para localizar esses arquivos posteriormente para incluir em um pacote de conteúdo para uso em outra instância, por exemplo, anote a identidade persistente ( `PID`).

1. Clique em **Salvar**.

   Suas alterações são aplicadas imediatamente à configuração OSGi relevante do sistema em execução; não é necessário reiniciar.

   >[!NOTE]
   >
   >Agora você pode localizar o [arquivos de configuração](#osgi-configuration-with-configuration-files). Por exemplo, para incluir em um pacote de conteúdo para uso em outra instância.

## Configuração OSGi com arquivos de configuração {#osgi-configuration-with-configuration-files}

As alterações de configuração feitas usando o Console da Web são mantidas no repositório como arquivos de configuração ( `.config`) em:

`/apps`

Esses arquivos podem ser incluídos em pacotes de conteúdo e reutilizados em outras instâncias.

>[!NOTE]
>
>O formato dos arquivos de configuração é específico - consulte a documentação do Sling Apache para:
>* detalhes completos de [o modelo de provisionamento do Apache Sling e o Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>* tutoriais e exemplos de [Obtenção de recursos e propriedades no Sling](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html).
>
>Por esse motivo, é recomendável criar e manter o arquivo de configuração fazendo alterações reais no console da Web.

O Console da Web não mostra nenhuma indicação de onde no repositório suas alterações foram salvas, mas elas podem ser facilmente localizadas:

1. Criar o arquivo de configuração por [fazer uma alteração inicial no console da web](#osgi-configuration-with-the-web-console).
1. Abra o CRXDE Lite.
1. No **Ferramentas** selecione **Consulta ...** .
1. Para pesquisar o PID da configuração atualizada, envie uma consulta de **Tipo** `SQL`.

   Por exemplo, **Console de gerenciamento do Apache Felix OSGi** tem a identidade persistente (PID) de:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   Assim, a consulta SQL poderia ser:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. O nó do arquivo de configuração é mostrado.

   Para o exemplo acima:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >Você pode abrir esse arquivo para exibir as alterações, mas para evitar erros de digitação, é recomendável fazer alterações reais com o console.

1. Agora é possível criar um pacote de conteúdo com esse nó e usá-lo conforme necessário em outras instâncias.

## Configuração do OSGi no repositório {#osgi-configuration-in-the-repository}

Além de usar o console da Web, você também pode definir detalhes de configuração no repositório. Isso permite configurar facilmente seus diferentes modos de execução.

Essas configurações são feitas criando `sling:OsgiConfig` nós no repositório para o sistema fazer referência. Esses nós espelham as configurações do OSGi e uma interface do usuário é formada para eles. Para atualizar os dados de configuração, atualize as propriedades do nó.

Se você modificar os dados de configuração no repositório, as alterações serão aplicadas imediatamente à configuração OSGi relevante. É como se as alterações tivessem sido feitas usando o console da Web, com as verificações de validação e consistência apropriadas. Esse workflow também se aplica à ação de copiar uma configuração de `/libs/` para `/apps/`.

Como o mesmo parâmetro de configuração está em vários lugares, o sistema:

* pesquisa todos os nós do tipo `sling:OsgiConfig`
* filtros de acordo com o nome do serviço
* filtros de acordo com o modo de execução

>[!NOTE]
>
>Ler também [como definir uma configuração baseada em repositório somente para uma instância específica](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=en).

### Adicionar uma nova configuração ao repositório {#adding-a-new-configuration-to-the-repository}

#### O que você precisa saber {#what-you-need-to-know}

Para adicionar uma configuração ao repositório, você deve saber o seguinte:

1. A variável **Identidade persistente** do serviço.

   Referencie a **Configurações** no console da Web. O nome é mostrado entre parênteses após o nome do pacote (ou no campo **Informações de configuração** na parte inferior da página).

   Por exemplo, criar um nó `com.day.cq.wcm.core.impl.VersionManagerImpl.` para configurar **Gerenciador de versão AEM WCM**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. É um [modo de execução](/help/sites-deploying/configure-runmodes.md) obrigatório? Crie a pasta:

   * `config` - para todos os modos de execução
   * `config.author` - para o ambiente de criação
   * `config.publish` - para o ambiente de publicação
   * `config.<run-mode>` - conforme adequado

1. É um **Configuração** ou **Configuração de fábrica** necessário?
1. Os parâmetros individuais a serem configurados, incluindo quaisquer definições de parâmetro existentes que devem ser recriadas.

   Faça referência ao campo de parâmetro individual no console da Web. O nome é mostrado entre parênteses para cada parâmetro.

   Por exemplo, criar uma propriedade
   `versionmanager.createVersionOnActivation` para configurar **Criar versão na ativação**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Existe uma configuração no `/libs`? Para listar todas as configurações na sua instância, use o **Query** ferramenta no CRXDE Lite para enviar a seguinte consulta SQL:

   `select * from sling:OsgiConfig`

   Em caso afirmativo, essa configuração pode ser copiada para o ` /apps/<yourProject>/`, depois personalizado no novo local.

#### Criação da configuração no repositório {#creating-the-configuration-in-the-repository}

Para realmente adicionar a nova configuração ao repositório:

1. Use o CRXDE Lite para navegar até:

   ` /apps/<yourProject>`

1. Se não existir, crie o `config` pasta ( `sling:Folder`):

   * `config` - aplicável a todos os modos de execução
   * `config.<run-mode>` - específico para um modo de execução específico

1. Nesta pasta, crie um nó:

   * Tipo: `sling:OsgiConfig`
   * Nome: a identidade persistente (PID);

     por exemplo, para o uso do Gerenciador de versão do WCM do AEM `com.day.cq.wcm.core.impl.VersionManagerImpl`

   >[!NOTE]
   >
   >Ao fazer uma configuração de fábrica, adicione `-<identifier>` ao nome.
   >
   >Como em: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Onde `<identifier>` é substituído por texto livre que você (deve) inserir para identificar a instância (você não pode omitir essas informações); por exemplo:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Para cada parâmetro que você deseja configurar, crie uma propriedade neste nó:

   * Nome: o nome do parâmetro conforme mostrado no console da Web; o nome é mostrado entre parênteses no final da descrição do campo. Por exemplo, para `Create Version on Activation` use `versionmanager.createVersionOnActivation`
   * Tipo: conforme apropriado.
   * Value: conforme necessário.

   Você só precisa criar propriedades para os parâmetros que deseja configurar, outros ainda assumirão os valores padrão conforme definidos pelo AEM.

1. Salve todas as alterações.

   As alterações são aplicadas quando o nó é atualizado reiniciando o serviço (como com as alterações feitas no console da Web).

>[!CAUTION]
>
>Não altere nada no `/libs` caminho.

>[!CAUTION]
>
>O caminho completo de uma configuração deve estar correto para ser lido na inicialização.

## Detalhes da configuração {#configuration-details}

### Ordem de resolução na inicialização {#resolution-order-at-startup}

A seguinte ordem de precedência é usada:

1. Nós do repositório em `/apps/*/config...`.com tipo `sling:OsgiConfig` ou arquivos de propriedade.

1. Nós do repositório com tipo `sling:OsgiConfig` em `/libs/*/config...`. (definições prontas para uso).

1. Qualquer `.config` arquivos de `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. no sistema de arquivos local.

Uma configuração genérica no `/libs` pode ser mascarado por uma configuração específica do projeto no `/apps`.

### Ordem de resolução no tempo de execução {#resolution-order-at-runtime}

Alterações de configuração feitas enquanto o sistema está em execução acionam um recarregamento com a configuração modificada.

Então, a seguinte ordem de precedência se aplica:

1. A modificação de uma configuração no console da Web tem efeito imediato, pois tem precedência no tempo de execução.
1. Modificar uma configuração no `/apps` imediatamente.
1. Modificar uma configuração no `/libs` tem efeito imediato, a menos que seja mascarado por uma configuração no `/apps`.

### Resolução de vários modos de execução {#resolution-of-multiple-run-modes}

Para configurações específicas do modo de execução, vários modos de execução podem ser combinados. Por exemplo, você pode criar pastas de configuração no seguinte estilo:

`/apps/*/config.<runmode1>.<runmode2>/`

As configurações nessas pastas são aplicadas se todos os modos de execução corresponderem a um modo de execução definido na inicialização.

Por exemplo, se uma instância foi iniciada com os modos de execução `author,dev,emea`, nós de configuração em `/apps/*/config.emea`, `/apps/*/config.author.dev/`, e `/apps/*/config.author.emea.dev/` é aplicado, enquanto os nós de configuração em `/apps/*/config.author.asean/` e `/config/author.dev.emea.noldap/` não são aplicadas.

Se várias configurações para o mesmo PID forem aplicáveis, a configuração com o maior número de modos de execução correspondentes será aplicada.

Por exemplo, se uma instância foi iniciada com os modos de execução `author,dev,emea`, e ambos `/apps/*/config.author/` e `/apps/*/config.emea.author/` definir uma configuração para
`com.day.cq.wcm.core.impl.VersionManagerImpl`, a configuração em `/apps/*/config.emea.author/` é aplicada.

A granularidade dessa regra está em um nível PID.
Não é possível definir algumas propriedades para o mesmo PID no `/apps/*/config.author/` e mais específicas em `/apps/*/config.emea.author/` para o mesmo PID.
A configuração com o maior número de modos de execução correspondentes é válida para todo o PID.

### Configurações padrão {#standard-configurations}

A lista a seguir mostra uma pequena seleção das configurações disponíveis (em uma instalação padrão) no repositório:

* Autor - Filtro WCM para AEM:

  `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Publicar - Filtro WCM para AEM:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Publicar - Estatísticas de página do WCM no AEM:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Como essas configurações residem em `/libs` eles não devem ser editados diretamente, mas copiados para a área do seu aplicativo ( `/apps`) antes da personalização.

Para listar todos os nós de configuração na sua instância, use o **Query** funcionalidade no CRXDE Lite para enviar a seguinte query SQL:

`select * from sling:OsgiConfig`

### Persistência de configuração {#configuration-persistence}

* Se você alterar uma configuração por meio do console da Web, ela (geralmente) será gravada no repositório em:

  `/apps/{somewhere}`

   * Por padrão `{somewhere}` é `system/config` para que a configuração seja gravada em

     `/apps/system/config`

   * No entanto, se você estiver editando uma configuração que veio inicialmente de outro lugar no repositório: por exemplo:

     /libs/foo/config/Someconfig

     Em seguida, a configuração atualizada é gravada no local original; por exemplo:

     `/apps/foo/config/someconfig`

* Configurações alteradas por `admin` são salvos em `*.config` arquivos em:

  ```
     /crx-quickstart/launchpad/config
  ```

   * Essa área são os dados privados do administrador de configuração do OSGi e contém todos os detalhes de configuração especificados por `admin`, independentemente de como entraram no sistema.
   * Essa área é um detalhe de implementação e você nunca deve editar esse diretório diretamente.
   * No entanto, é útil saber o local desses arquivos de configuração para que as cópias possam ser feitas para backup, várias instalações ou ambas:

      * Console de gerenciamento do Apache Felix OSGi

        `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Repositório do cliente do CRX Sling

        `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Nunca edite as pastas ou arquivos em:
>
>`/crx-quickstart/launchpad/config`
