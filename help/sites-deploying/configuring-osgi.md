---
title: Configuração do OSGi
seo-title: Configuração do OSGi
description: O OSGi é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos de AEM e sua configuração. Este artigo detalha como você pode gerenciar as configurações desses pacotes.
seo-description: O OSGi é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos de AEM e sua configuração. Este artigo detalha como você pode gerenciar as configurações desses pacotes.
uuid: b39059a5-dd61-486a-869a-0d7a732c3a47
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: d701e4ba-417f-4b57-b103-27fd25290736
feature: Configuring
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2014'
ht-degree: 0%

---


# Configuração do OSGi{#configuring-osgi}

[](https://www.osgi.org/) O OSGi é um elemento fundamental na pilha de tecnologia do Adobe Experience Manager (AEM). É usado para controlar os pacotes compostos de AEM e sua configuração.

O OSGi &quot;*fornece os primitivos padronizados que permitem que aplicativos sejam construídos a partir de componentes pequenos, reutilizáveis e colaborativos. Esses componentes podem ser compostos em um aplicativo e implantados*&quot;.

Isso permite o gerenciamento fácil de pacotes, pois eles podem ser interrompidos, instalados e iniciados individualmente. As interdependências são manipuladas automaticamente. Cada componente OSGi (consulte a [Especificação OSGi](https://www.osgi.org/Specifications/HomePage)) está contido em um dos vários pacotes.

Você pode gerenciar as configurações desses pacotes:

* usando o [Adobe CQ Web Console](#osgi-configuration-with-the-web-console)
* usando [arquivos de configuração](#osgi-configuration-with-configuration-files)
* configuração de [nós de conteúdo ( `sling:OsgiConfig`) no repositório](#osgi-configuration-in-the-repository)

Qualquer um dos métodos pode ser usado embora existam diferenças sutis, principalmente em relação a [Run Modes](/help/sites-deploying/configure-runmodes.md):

* [Console da Web do Adobe CQ](#osgi-configuration-with-the-web-console)

   * O Console da Web é a interface padrão para a configuração do OSGi. Ela fornece uma interface do usuário para editar as várias propriedades, onde os valores possíveis podem ser selecionados em listas predefinidas.

      Sendo assim, é o método mais fácil de usar.

   * Todas as configurações feitas com o Console da Web são aplicadas imediatamente e aplicáveis à instância atual, independentemente do modo de execução atual ou quaisquer alterações subsequentes no modo de execução.

* [arquivos de configuração](#osgi-configuration-with-configuration-files)

   * Contém as configurações definidas no console da Web.
   * Pode ser incluído em pacotes de conteúdo para uso em outras instâncias.

* [nós de conteúdo (sling:osgiConfig) no repositório](#osgi-configuration-in-the-repository)

   * Isso requer configuração manual usando o CRXDE Lite.
   * Devido às convenções de nomenclatura dos nós `sling:OsgiConfig`, é possível vincular a configuração a um [modo de execução](/help/sites-deploying/configure-runmodes.md) específico. Você ainda pode salvar configurações por mais de um modo de execução no mesmo repositório.
   * Todas as configurações apropriadas são aplicadas imediatamente (dependendo do modo de execução).

Qualquer que seja o método usado, todos esses métodos de configuração:

* Certifique-se de que copiar ou replicar o conteúdo do repositório recrie configurações idênticas.
* Permitir que você verifique as configurações no FileVault ou Subversion; para segurança ou atualizações adicionais.
* Pode ser salvo em pacotes para uso ao configurar outras instâncias.
* Permita executar implantações de configuração usando scripts para propagar os detalhes de configuração.

>[!NOTE]
>
>Detalhes de determinadas configurações importantes são listados em [Configurações do OSGi.](/help/sites-deploying/osgi-configuration-settings.md)

## Configuração do OSGi com o Console da Web {#osgi-configuration-with-the-web-console}

O [Web console](/help/sites-deploying/web-console.md) no AEM fornece uma interface padronizada para configurar os pacotes. A guia **Configuration** é usada para configurar os pacotes OSGi e, portanto, é o mecanismo subjacente para configurar AEM parâmetros do sistema.

Quaisquer alterações feitas são imediatamente aplicadas à configuração OSGi relevante, não é necessário reiniciar.

>[!NOTE]
>
>As alterações feitas no console da Web são salvas no repositório como [arquivos de configuração](#osgi-configuration-with-configuration-files). Eles podem ser incluídos em pacotes de conteúdo para reutilização em outras instalações.

>[!NOTE]
>
>No console da Web, qualquer descrição que mencione as configurações padrão está relacionada aos padrões do Sling.
>
>O Adobe Experience Manager tem seus próprios padrões e, portanto, os padrões definidos podem ser diferentes daqueles documentados no console.

Para atualizar uma configuração com o console da Web:

1. Acesse a guia **Configuration** do Console da Web:

   * Abrir o console da Web do link no menu **Ferramenta -> Operações**. Depois de fazer logon no console, você pode usar o menu suspenso de:

      **OSGi >**

   * O URL direto; por exemplo:

      `http://localhost:4502/system/console/configMgr`
   Uma lista será exibida.

1. Selecione o pacote que deseja configurar:

   * clicando no ícone **Edit** desse pacote
   * clicando no **Nome** do pacote

1. Uma caixa de diálogo abrirá. Aqui você pode editar conforme necessário; por exemplo, defina o **Nível de Log** para `INFO`:

   ![chlimage_1-140](assets/chlimage_1-140.png)

   >[!NOTE]
   >
   >As atualizações são salvas no repositório como [arquivos de configuração](#osgi-configuration-with-configuration-files). Para localizá-los posteriormente (por exemplo, para incluir em um pacote de conteúdo para uso em outra instância), você deve anotar a identidade persistente ( `PID`).

1. Clique em **Salvar**.

   Suas alterações são imediatamente aplicadas à configuração OSGi relevante do sistema em execução, não é necessário reiniciar.

   >[!NOTE]
   >
   >Agora é possível localizar o(s) arquivo(s) de configuração relacionado(s) ](#osgi-configuration-with-configuration-files); por exemplo, para incluir em um pacote de conteúdo para uso em outra instância.[

## Configuração OSGi com arquivos de configuração {#osgi-configuration-with-configuration-files}

As alterações de configuração feitas usando o Console da Web são mantidas no repositório como arquivos de configuração ( `.config`) em:

`/apps`

Eles podem ser incluídos em pacotes de conteúdo e reutilizados em outras instâncias.

>[!NOTE]
>
>O formato dos arquivos de configuração é muito específico - consulte a [Documentação do Sling Apache](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format) para obter detalhes completos.
>
>Por isso, é recomendável criar e manter o arquivo de configuração fazendo alterações reais no console da Web.

O Console da Web não mostra nenhuma indicação de onde as alterações foram salvas no repositório, mas elas podem ser facilmente localizadas:

1. Crie o arquivo de configuração fazendo uma alteração inicial no console da Web ](#osgi-configuration-with-the-web-console).[
1. Abra o CRXDE Lite.
1. No menu **Ferramentas** selecione **Consulta ...** .
1. Envie uma consulta de **Type** `SQL` para procurar o PID da configuração que você atualizou.

   Por exemplo, **Apache Felix OSGi Management Console** tem a identidade persistente (PID) de:

   `org.apache.felix.webconsole.internal.servlet.OsgiManager`

   Portanto, a consulta SQL pode ser:

   ```shell
   select * from nt:base where jcr:path like '/apps/%' and contains(*, 'org.apache.felix.webconsole.internal.servlet.OsgiManager')
   ```

1. O nó do arquivo de configuração será exibido.

   Para o exemplo acima:

   `/apps/system/config/org.apache.felix.webconsole.internal.servlet.OsgiManager.config`

   >[!CAUTION]
   >
   >É possível abrir esse arquivo para exibir suas alterações, mas para evitar erros de digitação, é recomendável fazer alterações reais com o console.

1. Agora você pode criar um pacote de conteúdo, contendo esse nó, e usar conforme necessário em suas outras instâncias.

## Configuração do OSGi no Repositório {#osgi-configuration-in-the-repository}

Além de usar o console da Web, você também pode definir detalhes de configuração no repositório. Isso permite configurar facilmente seus diferentes modos de execução.

Essas configurações são feitas criando nós `sling:OsgiConfig` no repositório para o sistema fazer referência. Esses nós espelham as configurações OSGi e formam uma interface de usuário para elas. Para atualizar os dados de configuração, atualize as propriedades do nó.

Se você modificar os dados de configuração no repositório, as alterações serão imediatamente aplicadas à configuração relevante do OSGi como se as alterações tivessem sido feitas usando o console da Web, com as verificações de validação e consistência apropriadas. Isso também se aplica à ação de copiar uma configuração de `/libs/` para `/apps/`.

Como o mesmo parâmetro de configuração pode ser localizado em vários locais, o sistema:

* procura por todos os nós do tipo `sling:OsgiConfig`
* filtros de acordo com o nome do serviço
* filtros de acordo com o modo de execução

>[!NOTE]
>
>Leia também [como definir uma configuração baseada em repositório apenas para uma instância específica](https://helpx.adobe.com/experience-manager/kb/RunModeDependentConfigAndInstall.html).

### Adicionando uma Nova Configuração ao Repositório {#adding-a-new-configuration-to-the-repository}

#### O que você precisa saber {#what-you-need-to-know}

Para adicionar uma nova configuração ao repositório, você precisa saber o seguinte:

1. A **Identidade Persistente** (PID) do serviço.

   Faça referência ao campo **Configurations** no console da Web. O nome é mostrado entre colchetes após o nome do pacote (ou nas **Informações de configuração** na parte inferior da página).

   Por exemplo, crie um nó `com.day.cq.wcm.core.impl.VersionManagerImpl.` para configurar **AEM Gerenciador de versão do WCM**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Se um [modo de execução](/help/sites-deploying/configure-runmodes.md) específico é necessário. Crie a pasta:

   * `config` - para todos os modos de execução
   * `config.author` - para o ambiente do autor
   * `config.publish` - para o ambiente de publicação
   * `config.<run-mode>` - se for caso disso

1. Se é necessário um **Configuration** ou **Fatory Configuration**.
1. Os parâmetros individuais a serem configurados; incluindo qualquer definição de parâmetro existente que precisará ser recriada.

   Faça referência ao campo de parâmetro individual no console da Web. O nome é mostrado entre parênteses para cada parâmetro.

   Por exemplo, crie uma propriedade
   `versionmanager.createVersionOnActivation` para configurar  **Criar versão na ativação**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Uma configuração já existe em `/libs`? Para listar todas as configurações em sua instância, use a ferramenta **Query** no CRXDE Lite para enviar a seguinte consulta SQL:

   `select * from sling:OsgiConfig`

   Nesse caso, essa configuração pode ser copiada para ` /apps/<yourProject>/` e depois personalizada no novo local.

#### Criando a Configuração no Repositório {#creating-the-configuration-in-the-repository}

Para realmente adicionar a nova configuração ao repositório:

1. Use o CRXDE Lite para navegar até:

   ` /apps/<yourProject>`

1. Se ainda não existir, crie a pasta `config` ( `sling:Folder`):

   * `config` - aplicável a todos os modos de execução
   * `config.<run-mode>` - específico de um modo de execução específico

1. Nesta pasta, crie um nó:

   * Tipo: `sling:OsgiConfig`
   * Nome: Identidade persistente (PID);

      por exemplo, para AEM Gerenciador de versão do WCM use `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >Ao fazer uma configuração de fábrica, anexe `-<identifier>` ao nome.
   >
   >Como em: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Em que `<identifier>` é substituído pelo texto livre que você (deve) inserir para identificar a instância (não é possível omitir essas informações); por exemplo:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Para cada parâmetro que você deseja configurar, crie uma propriedade neste nó:

   * Nome: o nome do parâmetro como mostrado no console da Web; o nome é mostrado entre parênteses no final da descrição do campo. Por exemplo, para `Create Version on Activation` use `versionmanager.createVersionOnActivation`
   * Tipo: conforme adequado.
   * Valor: conforme necessário.

   Você só precisa criar propriedades para os parâmetros que deseja configurar, outras pessoas ainda usarão os valores padrão conforme definido por AEM.

1. Salve todas as alterações.

   As alterações são aplicadas assim que o nó é atualizado, reiniciando o serviço (como nas alterações feitas no console da Web).

>[!CAUTION]
>
>Você não deve alterar nada no caminho `/libs`.

>[!CAUTION]
>
>O caminho completo de uma configuração deve estar correto para ser lido na inicialização.

## Detalhes da configuração {#configuration-details}

### Ordem de resolução na inicialização {#resolution-order-at-startup}

A seguinte ordem de precedência é usada:

1. Nós de repositório em `/apps/*/config...`.com tipo `sling:OsgiConfig` ou arquivos de propriedade.

1. Nós de repositório com tipo `sling:OsgiConfig` em `/libs/*/config...`. (definições prontas para uso).

1. Qualquer arquivo `.config` de `<*cq-installation-dir*>/crx-quickstart/launchpad/config/...`. no sistema de arquivos local.

Isso significa que uma configuração genérica em `/libs` pode ser mascarada por uma configuração específica do projeto em `/apps`.

### Ordem de resolução no tempo de execução {#resolution-order-at-runtime}

As alterações de configuração feitas enquanto o sistema está em execução acionam uma recarga com a configuração modificada.

Em seguida, aplica-se a seguinte ordem de precedência:

1. A modificação de uma configuração no console da Web terá efeito imediato, pois terá precedência no tempo de execução.
1. A modificação de uma configuração em `/apps` terá efeito imediato.
1. A modificação de uma configuração em `/libs` terá efeito imediato, a menos que seja mascarada por uma configuração em `/apps`.

### Resolução de vários modos de execução {#resolution-of-multiple-run-modes}

Para configurações específicas do modo de execução, é possível combinar vários modos de execução. Por exemplo, você pode criar pastas de configuração no seguinte estilo:

`/apps/*/config.<runmode1>.<runmode2>/`

As configurações nessas pastas serão aplicadas se todos os modos de execução corresponderem a um modo de execução definido na inicialização.

Por exemplo, se uma instância foi iniciada com os modos de execução `author,dev,emea`, os nós de configuração em `/apps/*/config.emea`, `/apps/*/config.author.dev/` e `/apps/*/config.author.emea.dev/` serão aplicados, enquanto os nós de configuração em `/apps/*/config.author.asean/` e `/config/author.dev.emea.noldap/` não serão aplicados.

Se várias configurações para o mesmo PID forem aplicáveis, a configuração com o maior número de modos de execução correspondentes será aplicada.

Por exemplo, se uma instância foi iniciada com os modos de execução `author,dev,emea` e `/apps/*/config.author/` e `/apps/*/config.emea.author/` definir uma configuração para
`com.day.cq.wcm.core.impl.VersionManagerImpl`, a configuração em `/apps/*/config.emea.author/` será aplicada.

A granularidade desta regra está em um nível PID.
Não é possível definir algumas propriedades para o mesmo PID em `/apps/*/config.author/` e outras mais específicas em `/apps/*/config.emea.author/` para o mesmo PID.
A configuração com o maior número de modos de execução correspondentes será efetiva para todo o PID.

### Configurações padrão {#standard-configurations}

A lista a seguir mostra uma pequena seleção das configurações disponíveis (em uma instalação padrão) no repositório:

* Autor - AEM filtro WCM:

   `libs/wcm/core/config.author/com.day.cq.wcm.core.WCMRequestFilter`

* Publicar - AEM filtro WCM:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.WCMRequestFilter`

* Publicar - AEM estatísticas da página WCM:

   `libs/wcm/core/config.publish/com.day.cq.wcm.core.stats.PageViewStatistics`

>[!NOTE]
>
>Como essas configurações residem em `/libs`, elas não devem ser editadas diretamente, mas copiadas para a área de seu aplicativo ( `/apps`) antes da personalização.

Para listar todos os nós de configuração em sua instância, use a funcionalidade **Query** no CRXDE Lite para enviar a seguinte consulta SQL:

`select * from sling:OsgiConfig`

### Persistência da configuração {#configuration-persistence}

* Se você alterar uma configuração por meio do console da Web, ela será (normalmente) gravada no repositório em:

   `/apps/{somewhere}`

   * Por padrão, `{somewhere}` é `system/config`, portanto, a configuração é gravada em

      `/apps/system/config`

   * No entanto, se você estiver editando uma configuração que veio inicialmente de outro lugar no repositório: por exemplo:

      /libs/foo/config/someconfig

      Em seguida, a configuração atualizada é escrita no local original; por exemplo:

      `/apps/foo/config/someconfig`

* As configurações alteradas por `admin` são salvas em `*.config` arquivos em:

   ```
      /crx-quickstart/launchpad/config
   ```

   * Esta é a área de dados privada do administrador de configuração do OSGi e mantém todos os detalhes de configuração especificados por `admin`, independentemente de como eles entraram no sistema.
   * Este é um detalhe de implementação e nunca deve editar este diretório diretamente.
   * No entanto, é útil saber a localização desses arquivos de configuração para que as cópias possam ser obtidas para backup e/ou instalação múltipla:

      * Console de Gerenciamento do Apache Felix OSGi

         `../crx/org/apache/felix/webconsole/internal/servlet/OsgiManager.config`

      * Repositório de Cliente Sling CRX

         `../com/day/crx/sling/client/impl/CRXSlingClientRepository/<pid-nr>.config`

>[!CAUTION]
>
>Você deve ***nunca*** editar as pastas ou os arquivos em:
>
>`/crx-quickstart/launchpad/config`

