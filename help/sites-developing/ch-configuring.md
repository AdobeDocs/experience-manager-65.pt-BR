---
title: Configuração do ContextHub
description: Saiba como configurar o Context Hub da Adobe Experience Manager para personalizar suas experiências.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
exl-id: 61208bd5-475b-40be-ba00-31bbbc952adf
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '1793'
ht-degree: 2%

---

# Configuração do ContextHub {#configuring-contexthub}

O ContextHub é uma estrutura para armazenar, manipular e apresentar dados de contexto. Para obter mais detalhes sobre o ContextHub, consulte [documentação do desenvolvedor](/help/sites-developing/contexthub.md). O ContextHub substitui [Client Context](/help/sites-administering/client-context.md) na interface para toque.

Configure o [ContextHub](/help/sites-developing/contexthub.md) barra de ferramentas para controlar se ele aparece no modo de Visualização, para criar armazenamentos do ContextHub e adicionar módulos de interface usando a interface otimizada para toque.

## Desativar o ContextHub {#disabling-contexthub}

Por padrão, o ContextHub é ativado em uma instalação do AEM. O ContextHub pode ser desativado para impedir que carregue js/css e inicialize.

<!--
There are two options to disable ContextHub:

* Edit the ContextHub's configuration and check the option **Disable ContextHub**

    1. In the rail click or tap **Tools &gt; Sites &gt; ContextHub**
    1. Click or tap the appropriate **Configuration Container**
    1. Select the **ContextHub Configuration** and click or tap **Edit Selected Element**
    1. Click or tap **Disable ContextHub** and click or tap **Save**

or
-->

* Use CRXDE Lite para definir a propriedade `disabled` para **true** em `/libs/settings/cloudsettings/legacy/contexthub`

>[!NOTE]
>
>[Devido à reestruturação dos repositórios no AEM 6.4,](/help/sites-deploying/repository-restructuring.md) o local das configurações do ContextHub alteradas em `/etc/cloudsettings` para:
>
>* `/libs/settings/cloudsettings`
>* `/conf/global/settings/cloudsettings`
>* `/conf/<tenant>/settings/cloudsettings`

## Exibição e ocultação da interface do usuário do ContextHub {#showing-and-hiding-the-contexthub-ui}

Configure o serviço OSGi do Adobe Granite ContextHub para mostrar ou ocultar o [Interface do usuário do ContextHub](/help/sites-authoring/ch-previewing.md) em suas páginas. O PID deste serviço é `com.adobe.granite.contexthub.impl.ContextHubImpl.`

Para configurar o serviço, você pode usar o [Console da Web](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console) ou use um [Nó JCR no repositório](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository):

* **Console da Web:** Para mostrar a interface do usuário do, selecione a propriedade Mostrar interface do usuário. Para ocultar a interface do usuário, desmarque a propriedade Ocultar interface do usuário.
* **Nó JCR:** Para mostrar a interface do usuário, defina o parâmetro booleano `com.adobe.granite.contexthub.show_ui` propriedade para `true`. Para ocultar a interface do usuário do, defina a propriedade como `false`.

Ao mostrar a interface do usuário do ContextHub, ela só é exibida em páginas em instâncias de autor do AEM. A interface do usuário não aparece em páginas de instâncias de publicação.

## Adição de modos e módulos da interface do usuário do ContextHub {#adding-contexthub-ui-modes-and-modules}

Configure os modos e módulos da interface do usuário exibidos na barra de ferramentas do ContextHub no modo Visualização:

* Modos de interface do usuário: grupos de módulos relacionados
* Módulos: dispositivos que expõem dados de contexto de um armazenamento e permitem que os autores manipulem o contexto

Os modos da interface são exibidos como uma série de ícones no lado esquerdo da barra de ferramentas. Quando selecionados, os módulos de um modo de interface do usuário são exibidos à direita.

![chlimage_1-319](assets/chlimage_1-319.png)

Os ícones são referências do [Biblioteca de ícones da Coral UI](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons).

### Adição de um modo de interface {#adding-a-ui-mode}

Adicione um modo de interface do usuário para agrupar módulos do ContextHub relacionados. Ao criar o modo de interface do usuário, forneça o título e o ícone que aparecem na barra de ferramentas do ContextHub.

1. No painel Experience Manager, clique ou toque em Ferramentas > Sites > Context Hub.
1. Clique ou toque no Contêiner de configuração padrão.
1. Clique ou toque em Configuração do Context Hub.
1. Clique ou toque no botão Criar e, em seguida, clique ou toque em Modo da interface do usuário do Context Hub.

   ![chlimage_1-320](assets/chlimage_1-320.png)

1. Forneça valores para as seguintes propriedades:

   * Título do modo da interface: o título que identifica o modo da interface
   * Ícone Mode: o seletor para o [Ícone da Coral UI](https://helpx.adobe.com/experience-manager/6-4/sites/developing/using/reference-materials/coral-ui/coralui3/Coral.Icon.html#availableIcons) para usar, por exemplo `coral-Icon--user`
   * Ativado: selecione para mostrar o modo de interface na barra de ferramentas do ContextHub

1. Clique ou toque em Salvar.

### Adição de um módulo de interface {#adding-a-ui-module}

Adicione um módulo da interface do usuário do ContextHub a um modo de interface do usuário para que ele seja exibido na barra de ferramentas do ContextHub para a visualização do conteúdo da página. Ao adicionar um módulo de interface do usuário, você está criando uma instância de um tipo de módulo registrado no ContextHub. Para adicionar um módulo de interface do usuário, você deve saber o nome do tipo de módulo associado.

O AEM fornece um tipo de módulo de interface do usuário base, bem como vários tipos de módulo de interface do usuário de amostra nos quais você pode basear um módulo de interface do usuário. A tabela a seguir fornece uma breve descrição de cada uma. Para obter informações sobre como desenvolver um módulo de interface personalizada, consulte [Criação de módulos de interface do usuário do ContextHub](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types).

As propriedades do módulo de interface do usuário incluem uma configuração detalhada, na qual você pode fornecer valores para propriedades específicas do módulo. Você fornece a configuração detalhada no formato JSON. A coluna Tipo de módulo na tabela fornece links para informações sobre o código JSON necessário para cada tipo de módulo de interface do usuário.

| Tipo de módulo | Descrição | Armazenar |
|---|---|---|
| [contexthub.base](/help/sites-developing/ch-samplemodules.md#contexthub-base-ui-module-type) | Um tipo de módulo de UI genérico | Configurado nas propriedades do módulo de interface do usuário |
| [contexthub.browserinfo](/help/sites-developing/ch-samplemodules.md#contexthub-browserinfo-ui-module-type) | Exibe informações sobre o navegador | surferinfo |
| [contexthub.datetime](/help/sites-developing/ch-samplemodules.md#contexthub-datetime-ui-module-type) | Exibe informações de data e hora | datetime |
| [contexthub.device](/help/sites-developing/ch-samplemodules.md#contexthub-device-ui-module-type) | Exibir o dispositivo cliente | emuladores |
| [contexthub.location](/help/sites-developing/ch-samplemodules.md#contexthub-location-ui-module-type) | Exibe a latitude e a longitude do cliente, bem como a localização em um mapa. Permite alterar o local. | localização geográfica |
| [contexthub.screen-orientation](/help/sites-developing/ch-samplemodules.md#contexthub-screen-orientation-ui-module-type) | Exibe a orientação da tela do dispositivo (paisagem ou retrato) | emuladores |
| [contexthub.tagcloud](/help/sites-developing/ch-samplemodules.md#contexthub-tagcloud-ui-module-type) | Exibe estatísticas sobre tags de página | tagcloud |
| [granite.profile](/help/sites-developing/ch-samplemodules.md#granite-profile-ui-module-type) | Exibe as informações de perfil do usuário atual, incluindo authorizableID, displayName e familyName. Você pode alterar o valor de displayName e familyName. | perfil |

1. No painel Experience Manager, clique ou toque em Ferramentas > Sites > ContextHub.
1. Clique ou toque no Contêiner de configuração ao qual você deseja adicionar um módulo de interface.
1. Clique ou digite a Configuração do ContextHub à qual você deseja adicionar o módulo de interface do usuário.
1. Clique ou toque no modo de interface do usuário ao qual você está adicionando o módulo de interface do usuário.
1. Clique ou toque no botão Criar e, em seguida, clique ou toque em Módulo de interface do usuário do ContextHub (genérico).

   ![chlimage_1-321](assets/chlimage_1-321.png)

1. Forneça valores para as seguintes propriedades:

   * Título do módulo da interface do usuário: um título que identifica o módulo da interface do usuário
   * Tipo de módulo: o tipo de módulo
   * Ativado: selecione para mostrar o módulo de interface do usuário na barra de ferramentas do ContextHub

1. (Opcional) Para substituir a configuração de armazenamento padrão, insira um objeto JSON para configurar o Módulo de interface do usuário.
1. Clique ou toque em Salvar.

## Criação de um armazenamento do ContextHub {#creating-a-contexthub-store}

Crie um armazenamento do Context Hub para manter os dados do usuário e acessar os dados conforme necessário. Os armazenamentos do ContextHub são baseados em candidatos de armazenamento registrados. Ao criar o armazenamento, é necessário o valor do storeType com o qual o candidato do armazenamento foi registrado. (Consulte [Criação de candidatos à loja personalizada](/help/sites-developing/ch-extend.md#creating-custom-store-candidates).)

### Configuração detalhada da loja {#detailed-store-configuration}

Quando você configura um armazenamento, a propriedade Detail Configuration permite fornecer valores para propriedades específicas do armazenamento. O valor é baseado na variável `config` parâmetro do repositório `init` função. Portanto, a necessidade de fornecer esse valor e o formato do valor dependem do armazenamento.

O valor da propriedade Detail Configuration é um `config` no formato JSON.

### Amostra de candidatos da loja {#sample-store-candidates}

O AEM fornece as seguintes amostras de candidatos de armazenamento nas quais você pode basear uma loja.

| Tipo de armazenamento | Descrição |
|---|---|
| [aem.segmentation](/help/sites-developing/ch-samplestores.md#aem-segmentation-sample-store-candidate) | Armazene para segmentos do ContextHub resolvidos e não resolvidos. Recupera automaticamente segmentos do ContextHub SegmentManager |
| [aem.resolvedsegments](/help/sites-developing/ch-samplestores.md#aem-resolvedsegments-sample-store-candidate) | Armazena os segmentos atualmente resolvidos. Escuta o serviço ContextHub SegmentManager para atualizar automaticamente a loja |
| [contexthub.geolocation](/help/sites-developing/ch-samplestores.md#contexthub-geolocation-sample-store-candidate) | Armazena a latitude e a longitude do local do navegador. |
| [contexthub.datetime](/help/sites-developing/ch-samplestores.md#contexthub-datetime-sample-store-candidate) | Armazena a data, a hora e a temporada atuais para o local do navegador |
| [granite.emulators](/help/sites-developing/ch-samplestores.md#granite-emulators-sample-store-candidate) | Define propriedades e recursos para vários dispositivos e detecta o dispositivo cliente atual |
| [contexthub.generic-jsonp](/help/sites-developing/ch-samplestores.md#contexthub-generic-jsonp-sample-store-candidate) | Recupera e armazena dados de um serviço JSONP |
| [granite.profile](/help/sites-developing/ch-samplestores.md#granite-profile-sample-store-candidate) | Armazena dados de perfil do usuário atual |
| [contexthub.surferinfo](/help/sites-developing/ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) | Armazena informações sobre o cliente, como informações do dispositivo, tipo de navegador e orientação da janela |
| [contexthub.tagcloud](/help/sites-developing/ch-samplestores.md#contexthub-tagcloud-sample-data-store) | Armazena tags de página e contagens de tags |

1. No painel Experience Manager, clique ou toque em Ferramentas > Sites > ContextHub.
1. Clique ou toque no container de configuração padrão.
1. Clique ou toque em Configuração do Contexthub
1. Para adicionar uma loja, clique ou toque no ícone Criar e, em seguida, clique ou toque em Configuração da loja do ContexHub.

   ![chlimage_1-322](assets/chlimage_1-322.png)

1. Forneça valores para as propriedades de configuração básica e clique ou toque em Próximo:

   * **Título da configuração:** O título que identifica o armazenamento
   * **Tipo de armazenamento:** O valor da propriedade storeType do candidato do armazenamento no qual basear o armazenamento
   * **Obrigatório:** Selecionar
   * **Ativado:** Selecionar para habilitar o armazenamento

1. (Opcional) Para substituir a configuração de armazenamento padrão, insira um objeto JSON na caixa Configuração detalhada (JSON).
1. Clique ou toque em Salvar.

## Exemplo: usando um serviço JSONP  {#example-using-a-jsonp-service}

Este exemplo ilustra como configurar um armazenamento e exibir os dados em um módulo de interface do usuário. Neste exemplo, o serviço MD5 do site jsontest.com é usado como uma fonte de dados para um armazenamento. O serviço retorna o código hash MD5 de uma determinada string, no formato JSON.

Um armazenamento contexthub.generic-jsonp é configurado para que ele armazene dados para a chamada de serviço `https://md5.jsontest.com/?text=%22text%20to%20md5%22`. O serviço retorna os seguintes dados que são exibidos em um módulo de interface do usuário:

```xml
{
   "md5": "919a56ab62b6d5e1219fe1d95248a2c5",
   "original": "\"text to md5\""
}
```

### Criação de um armazenamento contexthub.generic-jsonp {#creating-a-contexthub-generic-jsonp-store}

O candidato do armazenamento de amostra contexthub.generic-jsonp permite recuperar dados de um serviço JSONP ou um serviço da Web que retorna dados JSON. Para este candidato da loja, use a configuração da loja para fornecer detalhes sobre o serviço JSONP a ser usado.

A variável [init](/help/sites-developing/contexthub-api.md#init-name-config) função da `ContextHub.Store.JSONPStore` A classe JavaScript define um `config` objeto que inicializa este candidato de armazenamento. A variável `config` objeto contém um `service` objeto que inclui detalhes sobre o serviço JSONP. Para configurar a loja, forneça o `service` no formato JSON como o valor da propriedade Configuração detalhada.

Para salvar dados do serviço MD5 do site jsontest.com, use o procedimento em [Criação de um armazenamento do ContextHub](/help/sites-developing/ch-configuring.md#creating-a-contexthub-store) usando as seguintes propriedades:

* **Título da configuração:** md5
* **Tipo de armazenamento:** contexthub.generic-jsonp
* **Obrigatório:** Selecionar
* **Ativado:** Selecionar
* **Configuração detalhada (JSON):**

  ```xml
  {
   "service": {
   "jsonp": false,
   "timeout": 1000,
   "ttl": 1800000,
   "secure": false,
   "host": "md5.jsontest.com",
   "port": 80,
   "params":{
   "text":"text to md5"
       }
     }
   }
  ```

### Adição de um módulo de interface do usuário para os dados md5 {#adding-a-ui-module-for-the-md-data}

Adicione um módulo de interface do usuário à barra de ferramentas do ContextHub para exibir os dados armazenados no armazenamento md5 de exemplo. Neste exemplo, o módulo contexthub.base é usado para produzir o seguinte módulo de interface do usuário:

![chlimage_1-323](assets/chlimage_1-323.png)

Use o procedimento em [Adição de um módulo de interface](#adding-a-ui-module) para adicionar o módulo da interface do usuário a um Modo de interface do usuário existente, como o Modo de interface do usuário Perona de amostra. Para o Módulo de interface do usuário, use os seguintes valores de propriedade:

* **Título do módulo da interface do usuário:** MD5
* **Tipo de módulo:** contexthub.base
* **Configuração detalhada (JSON):**

  ```xml
  {
   "icon": "coral-Icon--data",
   "title": "MD5 Converstion",
   "storeMapping": { "md5": "md5" },
   "template": "<p> {{md5.original}}</p>;
                <p>{{md5.md5}}</p>"
  }
  ```

## Depuração do ContextHub {#debugging-contexthub}

Um modo de depuração para o ContextHub pode ser ativado para permitir a solução de problemas. O modo de depuração pode ser ativado por meio da configuração do ContextHub ou pelo CRXDE.

### Através da configuração {#via-the-configuration}

Edite a configuração do ContextHub e marque a opção **Depurar**

1. No painel, clique ou toque **Ferramentas > Sites > ContextHub**
1. Clique ou toque no padrão **Contêiner de configuração**
1. Selecione o **Configuração do ContextHub** e clique ou toque em **Editar elemento selecionado**
1. Clique ou toque **Depurar** e clique ou toque em **Salvar**

### Via CRXDE {#via-crxde}

Use CRXDE Lite para definir a propriedade `debug` para **true** em:

* `/conf/global/settings/cloudsettings` ou
* `/conf/<tenant>/settings/cloudsettings`

>[!NOTE]
>
>Para configurações do ContextHub ainda localizadas em seus caminhos herdados, o local para definir o `debug property` é `/libs/settings/cloudsettings/legacy/contexthub`.

### Modo silencioso {#silent-mode}

O modo silencioso suprime todas as informações de depuração. Diferentemente da opção de depuração normal, que pode ser definida independentemente para cada configuração do ContextHub, o modo silencioso é uma configuração global que tem precedência sobre qualquer configuração de depuração no nível de configuração do ContextHub.

Isso é útil para a instância de publicação, na qual você não deseja nenhuma informação de depuração. Como é uma configuração global, ela é ativada por meio do OSGi.

1. Abra o **Configuração do console da Web do Adobe Experience Manager** em `http://<host>:<port>/system/console/configMgr`
1. Pesquisar por **ContextHub do Adobe Granite**
1. Clique na configuração **ContextHub do Adobe Granite** para editar suas propriedades
1. Marque a opção **Modo silencioso** e clique em **Salvar**

## Recuperando configurações do ContextHub após a atualização {#recovering-contexthub-configurations-after-upgrading}

Quando um [atualização para AEM](/help/sites-deploying/upgrade.md) for executado, o backup das configurações do ContextHub será feito e as armazenadas em um local seguro. Durante a atualização, as configurações padrão do ContextHub são instaladas, substituindo as configurações existentes. O backup é necessário para preservar quaisquer alterações ou adições feitas.

As configurações do ContextHub são armazenadas em uma pasta chamada `contexthub` nos seguintes nós:

* `/conf/global/settings/cloudsettings`
* `/conf/<tenant>/settings/cloudsettings`

Após uma atualização, o backup é armazenado em uma pasta chamada `contexthub` abaixo de um nó chamado:

`/conf/global/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx` ou
`/conf/<tenant>/settings/cloudsettings/default-pre-upgrade_yyyymmdd_xxxxxxx`

A variável `yyyymmdd` parte do nome do nó é a data em que a atualização foi executada.

Para recuperar as configurações do ContextHub, use o CRXDE Lite para copiar os nós que representam suas lojas, modos de interface do usuário e módulos de interface do usuário abaixo do `default-pre-upgrade_yyyymmdd_xxxxxx` nó para abaixo:

* `/conf/global/settings/cloudsettings` ou
* `/conf/<tenant>/settings/cloudsettings`
