---
title: Configuração do OSGi
description: O OSGi é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos de AEM e sua configuração. Este artigo detalha como é possível gerenciar as definições de configuração desses pacotes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 5ecd09a3-c4be-4361-9816-03106435346f
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 0%

---

# Configuração do OSGi{#configuring-osgi}

O [OSGi](https://www.osgi.org/) é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos de AEM e sua configuração.

O OSGi &quot;*fornece os primitivos padronizados que permitem que os aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados &quot;*&quot;.

Isso permite o fácil gerenciamento de pacotes, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são tratadas automaticamente. Cada componente OSGi (consulte a [Especificação OSGi](https://docs.osgi.org/specification/)) está contido em um dos vários pacotes.

Você pode gerenciar as definições de configuração desses pacotes ao:

* usando o [Adobe CQ Web Console](#osgi-configuration-with-the-web-console)
* usando [arquivos de configuração](#osgi-configuration-with-configuration-files)
* configurando [nós de conteúdo ( `sling:OsgiConfig`) no repositório](#osgi-configuration-in-the-repository)

Qualquer um dos métodos pode ser usado, embora existam diferenças sutis, principalmente em relação aos [Modos de Execução](/help/sites-deploying/configure-runmodes.md):

* [Console da Web do Adobe CQ](#osgi-configuration-with-the-web-console)

   * O Console da Web é a interface padrão para a configuração do OSGi. Ela fornece uma interface para editar as várias propriedades, onde os valores possíveis podem ser selecionados nas listas predefinidas.

     Como tal, é o método mais fácil de usar.

   * Quaisquer configurações feitas com o Console da Web são aplicadas imediatamente e aplicáveis à instância atual, independentemente do modo de execução atual ou de qualquer alteração subsequente no modo de execução.

* [arquivos de configuração](#osgi-configuration-with-configuration-files)

   * Contêm configurações definidas no console da Web.
   * Podem ser incluídos em pacotes de conteúdo para uso em outras instâncias.

* [nós de conteúdo (sling:osgiConfig) no repositório](#osgi-configuration-in-the-repository)

   * Requer configuração manual usando CRXDE Lite.
   * Devido às convenções de nomenclatura dos nós `sling:OsgiConfig`, você pode vincular a configuração a um [modo de execução](/help/sites-deploying/configure-runmodes.md) específico. Você pode até mesmo salvar configurações para mais de um modo de execução no mesmo repositório.
   * Todas as configurações apropriadas são aplicadas imediatamente (dependendo do modo de execução).

Qualquer que seja o método usado, todos esses métodos de configuração:

* Certifique-se de que copiar ou replicar o conteúdo do repositório recrie configurações idênticas.
* Permite que você faça check-out das configurações para o FileVault ou Subversion; para segurança ou para atualizações adicionais.
* Podem ser salvas em pacotes para uso ao configurar outras instâncias.
* Permite executar implantações de configuração usando scripts para propagar os detalhes da configuração.

>[!NOTE]
>
>Detalhes de determinadas configurações importantes são listados em [Configurações OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configuração do OSGi com o console da Web {#osgi-configuration-with-the-web-console}

O [console da Web](/help/sites-deploying/web-console.md) em AEM fornece uma interface padronizada para configurar os pacotes. A guia **Configuração** é usada para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar parâmetros do sistema AEM.

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

1. Acesse a guia **Configuração** do Console da Web:

   * Abrindo o console da Web no link do menu **Ferramenta > Operações**. Depois de fazer logon no console, você pode usar o menu suspenso de:

     **OSGi >**

   * O URL direto; por exemplo:

     `http://localhost:4502/system/console/configMgr`

   Uma lista é exibida.

1. Selecione o pacote que você deseja configurar:

   * clicando no ícone **Editar** desse pacote
   * clicando no **Nome** do pacote

1. Uma caixa de diálogo é aberta. Aqui é possível editar conforme necessário. Por exemplo, defina o **Nível de Log** como `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >As atualizações estão salvas no repositório como [arquivos de configuração](#osgi-configuration-with-configuration-files). Para localizar esses arquivos posteriormente a fim de incluí-los em um pacote de conteúdo para uso em outra instância, por exemplo, anote a identidade persistente ( `PID`).

1. Clique em **Salvar**.

   Suas alterações são aplicadas imediatamente à configuração OSGi relevante do sistema em execução; não é necessário reiniciar.

   >[!NOTE]
   >
   >Agora você pode localizar os [arquivos de configuração](#osgi-configuration-with-configuration-files) relacionados. Por exemplo, para incluir em um pacote de conteúdo para uso em outra instância.

## Configuração OSGi com arquivos de configuração {#osgi-configuration-with-configuration-files}

As alterações de configuração feitas usando o Console da Web são mantidas no repositório como arquivos de configuração ( `.config`) em:

`/apps`

Esses arquivos podem ser incluídos em pacotes de conteúdo e reutilizados em outras instâncias.

>[!NOTE]
>
>O formato dos arquivos de configuração é específico - consulte a documentação do Sling Apache para:
>* detalhes completos do [Apache Sling Provisioning Model e Apache SlingStart](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>* Tutoriais e exemplos de [Obtendo Recursos e Propriedades no Sling](https://sling.apache.org/documentation/tutorials-how-tos/getting-resources-and-properties-in-sling.html).
>
>Por esse motivo, é recomendável criar e manter o arquivo de configuração fazendo alterações reais no console da Web.

O Console da Web não mostra nenhuma indicação de onde no repositório suas alterações foram salvas, mas elas podem ser facilmente localizadas:

1. Crie o arquivo de configuração [fazendo uma alteração inicial no console da Web](#osgi-configuration-with-the-web-console).
1. Abra o CRXDE Lite.
1. No menu **Ferramentas**, selecione **Consulta...** .
1. Para procurar o PID da configuração atualizada, envie uma consulta de **Tipo** `SQL`.

   Por exemplo, o **Console de Gerenciamento OSGi do Apache Felix** tem a identidade persistente (PID) de:

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

Essas configurações são feitas criando `sling:OsgiConfig` nós no repositório para que o sistema faça referência. Esses nós espelham as configurações do OSGi e uma interface do usuário é formada para eles. Para atualizar os dados de configuração, atualize as propriedades do nó.

Se você modificar os dados de configuração no repositório, as alterações serão aplicadas imediatamente à configuração OSGi relevante. É como se as alterações tivessem sido feitas usando o console da Web, com as verificações de validação e consistência apropriadas. Este fluxo de trabalho também se aplica à ação de copiar uma configuração de `/libs/` para `/apps/`.

Como o mesmo parâmetro de configuração está em vários lugares, o sistema:

* procura todos os nós do tipo `sling:OsgiConfig`
* filtros de acordo com o nome do serviço
* filtros de acordo com o modo de execução

>[!NOTE]
>
>Leia também [como definir uma configuração baseada em repositório somente para uma instância específica](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17500.html?lang=pt-BR).

### Adicionar uma nova configuração ao repositório {#adding-a-new-configuration-to-the-repository}

#### O que você precisa saber {#what-you-need-to-know}

Para adicionar uma configuração ao repositório, você deve saber o seguinte:

1. A **Identidade Persistente** (PID) do serviço.

   Referencie o campo **Configurações** no console da Web. O nome é mostrado entre parênteses depois do nome do pacote (ou nas **Informações de Configuração** em direção à parte inferior da página).

   Por exemplo, crie um nó `com.day.cq.wcm.core.impl.VersionManagerImpl.` para configurar o **Gerenciador de Versão do WCM do AEM**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. É necessário um [modo de execução](/help/sites-deploying/configure-runmodes.md) específico? Crie a pasta:

   * `config` - para todos os modos de execução
   * `config.author` - para o ambiente de criação
   * `config.publish` - para o ambiente de publicação
   * `config.<run-mode>` - conforme apropriado

1. É necessária uma **Configuração** ou uma **Configuração de Fábrica**?
1. Os parâmetros individuais a serem configurados, incluindo quaisquer definições de parâmetro existentes que devem ser recriadas.

   Faça referência ao campo de parâmetro individual no console da Web. O nome é mostrado entre parênteses para cada parâmetro.

   Por exemplo, criar uma propriedade
   `versionmanager.createVersionOnActivation` para configurar **Criar Versão na Ativação**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Existe uma configuração em `/libs`? Para listar todas as configurações na sua instância, use a ferramenta **Query** no CRXDE Lite para enviar a seguinte consulta SQL:

   `select * from sling:OsgiConfig`

   Em caso afirmativo, essa configuração pode ser copiada para ` /apps/<yourProject>/` e personalizada no novo local.

#### Criação da configuração no repositório {#creating-the-configuration-in-the-repository}

Para realmente adicionar a nova configuração ao repositório:

1. Use o CRXDE Lite para navegar até:

   ` /apps/<yourProject>`

1. Se não existir, crie a pasta `config` ( `sling:Folder`):

   * `config` - aplicável a todos os modos de execução
   * `config.<run-mode>` - específico para um determinado modo de execução

1. Nesta pasta, crie um nó:

   * Tipo: `sling:OsgiConfig`
   * Nome: a identidade persistente (PID);

     por exemplo, para AEM WCM Version Manager use `com.day.cq.wcm.core.impl.VersionManagerImpl`

   >[!NOTE]
   >
   >Ao fazer uma Configuração de Fábrica, anexe `-<identifier>` ao nome.
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

   Você só deve criar propriedades para os parâmetros que deseja configurar, outros ainda assumirão os valores padrão conforme definido pelo AEM.

1. Salve todas as alterações.

   As alterações são aplicadas quando o nó é atualizado reiniciando o serviço (como com as alterações feitas no console da Web).

>[!CAUTION]
>
>Não altere nada no caminho `/libs`.

>[!CAUTION]
>
>O caminho completo de uma configuração deve estar correto para ser lido na inicialização.

## Detalhes da configuração {#configuration-details}

### Ordem de resolução na inicialização {#resolution-order-at-startup}

A seguinte ordem de precedência é usada:

1. Nós do repositório em `/apps/*/config...`. com tipo `sling:OsgiConfig` ou arquivos de propriedade.

1. Nós do repositório com tipo `sling:OsgiConfig` em `/libs/*/config...`. (definições prontas para uso).

1. Qualquer arquivo `.config` de `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. no sistema de arquivos local.

Uma configuração genérica em `/libs` pode ser mascarada por uma configuração específica de projeto em `/apps`.

### Ordem de resolução no tempo de execução {#resolution-order-at-runtime}

Alterações de configuração feitas enquanto o sistema está em execução acionam um recarregamento com a configuração modificada.

Então, a seguinte ordem de precedência se aplica:

1. A modificação de uma configuração no console da Web tem efeito imediato, pois tem precedência no tempo de execução.
1. A modificação de uma configuração em `/apps` tem efeito imediato.
1. A modificação de uma configuração em `/libs` tem efeito imediato, a menos que seja mascarada por uma configuração em `/apps`.

### Resolução de vários modos de execução {#resolution-of-multiple-run-modes}

Para configurações específicas do modo de execução, vários modos de execução podem ser combinados. Por exemplo, você pode criar pastas de configuração no seguinte estilo:

`/apps/*/config.<runmode1>.<runmode2>/`

As configurações nessas pastas são aplicadas se todos os modos de execução corresponderem a um modo de execução definido na inicialização.

Por exemplo, se uma instância foi iniciada com os modos de execução `author,dev,emea`, os nós de configuração em `/apps/*/config.emea`, `/apps/*/config.author.dev/` e `/apps/*/config.author.emea.dev/` serão aplicados, enquanto os nós de configuração em `/apps/*/config.author.asean/` e `/config/author.dev.emea.noldap/` não serão aplicados.

Se várias configurações para o mesmo PID forem aplicáveis, a configuração com o maior número de modos de execução correspondentes será aplicada.

Por exemplo, se uma instância foi iniciada com os modos de execução `author,dev,emea`, e `/apps/*/config.author/` e `/apps/*/config.emea.author/` definem uma configuração para
`com.day.cq.wcm.core.impl.VersionManagerImpl`, a configuração em `/apps/*/config.emea.author/` é aplicada.

A granularidade dessa regra está em um nível PID.
Você não pode definir algumas propriedades para o mesmo PID em `/apps/*/config.author/` e outras mais específicas em `/apps/*/config.emea.author/` para o mesmo PID.
A configuração com o maior número de modos de execução correspondentes é válida para todo o PID.

### Configurações padrão {#standard-configurations}

A lista a seguir mostra uma pequena seleção das configurações disponíveis (em uma instalação padrão) no repositório:

* Autor - Filtro WCM para AEM:

  `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Publish - AEM Filtro WCM:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Publish - AEM Estatísticas de página do WCM:

  `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Como essas configurações residem no `/libs`, elas não devem ser editadas diretamente, mas copiadas para a área do seu aplicativo ( `/apps`) antes da personalização.

Para listar todos os nós de configuração na sua instância, use a funcionalidade **Query** no CRXDE Lite para enviar a seguinte consulta SQL:

`select * from sling:OsgiConfig`

### Persistência de configuração {#configuration-persistence}

* Se você alterar uma configuração por meio do console da Web, ela (geralmente) será gravada no repositório em:

  `/apps/{somewhere}`

   * Por padrão, `{somewhere}` é `system/config`, portanto, a configuração é gravada em

     `/apps/system/config`

   * No entanto, se você estiver editando uma configuração que veio inicialmente de outro lugar no repositório: por exemplo:

     /libs/foo/config/Someconfig

     Em seguida, a configuração atualizada é gravada no local original; por exemplo:

     `/apps/foo/config/someconfig`

* As configurações alteradas por `admin` são salvas em `*.config` arquivos em:

  ```
     /crx-quickstart/launchpad/config
  ```

   * Esta área são os dados privados do administrador de configuração OSGi e contém todos os detalhes de configuração especificados por `admin`, independentemente de como eles entraram no sistema.
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
