---
title: SAP Commerce Cloud
seo-title: SAP Commerce Cloud
description: Saiba como implantar o eCommerce com a SAP Commerce Cloud.
seo-description: Saiba como implantar o eCommerce com a SAP Commerce Cloud.
uuid: 26ace49c-02d2-4b49-a959-e033def89bd4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: c5dcc90a-05d2-4701-a625-2b655ad0b458
docset: aem65
pagetitle: Deploying eCommerce with hybris
translation-type: tm+mt
source-git-commit: 9e39868768d2fc70f587b18d36042e742d5fae45

---


# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>Esta página contém links para o site hybris. Para determinadas páginas, você precisará de uma conta para fazer logon.

## Implantação do eCommerce com a SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>O conector para o AEM 6.5 não está pronto.

>[!NOTE]
>
>Os procedimentos a seguir usam o seguinte catálogo de demonstração para ilustrar a implantação:
>
>`Geometrixx Outdoors Site English (US)`

A implantação dos pacotes [de eCommerce](#packages-needed-for-ecommerce-with-hybris) necessários proporcionará a funcionalidade completa da estrutura de eCommerce, juntamente com uma implementação de referência da funcionalidade de eCommerce, conforme fornecido com uma implementação de hybris (incluindo um catálogo de demonstração)

Este documento está disponível na seção ( `/content/geometrixx-outdoors/en_US`) em inglês (EUA) do site Geometrixx Outdoors:

* [Informações](#productinformationwithcolorvariants) do produto (com variantes de cor, quando apropriado)

* [Visão geral do conteúdo do carrinho de compras](#shoppingcartcontentoverview)
* [Inscrição](#customersignup) do cliente e logon do [cliente](#customersignin)

* [Acesso ao console de gerenciamento de híbridos](#accesstothehybrismanagementconsole)

### Requisitos técnicos - servidor hybris {#technical-requirements-hybris-server}

A extensão hybris do eCommerce Integration Framework foi atualizada para suportar o Hybris 5 (como padrão), mantendo a compatibilidade retroativa com o Hybris 4 <!--[Hybris 4](/help/sites-developing/hybris.md#developing-for-hybris). -->

>[!NOTE]
>
>* Suporta até hybris 6.4 com OCC versão 2.
>* Você precisará do Java 7 para executar o servidor [hybris 5.](https://www.hybris.com/en/architecture-technology)
>* O complemento hybris, o Acelerador [Telco](https://www.hybris.com/en/products/telecommunication), não é suportado pela extensão AEM.
>



### Pacotes necessários para o comércio eletrônico com hiperligações {#packages-needed-for-ecommerce-with-hybris}

Para instalar a funcionalidade de comércio eletrônico, é necessário:

* Seu servidor hybris, disponível a partir de [hybris](#configureandbuildthehybrisserver).
* Estrutura de eCommerce do AEM:

   * isso é parte de uma instalação padrão do AEM

* Pacote AEM Geometrixx-all:

   * `cq-geometrixx-all-pkg`

* Pacotes de conteúdo HTML do AEM: &quot;

   * 
       &quot;
 cq-hybris-content-6.3.2     
     
     &quot;
   
   * implementação da API específica de hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * uma implementação de referência para ilustrar o uso de híbridos ( `geometrixx-outdoors/en_US`)


### Instalação do eCommerce com híbridos {#installation-of-ecommerce-with-hybris}

Para instalar uma configuração completa (usando o catálogo de demonstração, Geometrixx Outdoors), as etapas básicas são:

1. [Instale o AEM](/help/sites-deploying/deploy.md).
1. Instale o pacote Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Instale os pacotes de conteúdo de demonstração usando o gerenciador de [pacotes](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Baixe e crie seu servidor](#download-and-build-your-hybris-server)hybris.
1. Construa seu catálogo em seu mecanismo de comércio eletrônico:

   1. [Configure a loja](#setup-the-geometrixx-outdoors-store)do Geometrixx Outdoor.

1. [Crie](/help/sites-authoring/page-authoring.md) quaisquer páginas suplementares que você precisar no AEM.

>[!CAUTION]
>
>O uso do servidor hybris requer uma licença separada de hybris.

>[!NOTE]
>
>A documentação [da](/help/sites-developing/ecommerce.md#api-documentation) API de desenvolvedores também está disponível para download.

### Baixe e crie seu servidor hybris {#download-and-build-your-hybris-server}

As etapas neste procedimento baixarão e criarão o servidor hybris. Ele também tornará as configurações iniciais necessárias para as conexões entre hybris e cq. A extensão será então utilizável com as configurações padrão.

>[!CAUTION]
>
>Versões de hiperbrilho anteriores à versão 5.5.1 não são suportadas.

>[!NOTE]
>
>Para concluir, você precisará do [Groovy](https://groovy-lang.org/) instalado no sistema.

1. Baixe a distribuição **hybris Commerce Suite **do site de download hybris.

   >[!CAUTION]
   >
   >Você precisará de uma conta (de híbridos) para acessar isso.

1. Descompacte o arquivo de distribuição no local desejado (conhecido como &lt;hybris-root-diretory>).
1. Na linha de comando, execute o seguinte:

   ```shell
   cd <hybris-root-directory>/bin/platform
   . ./setantenv.sh
   ant clean all
   cd ../..
   ```

   >[!NOTE]
   >
   >Ao executar:
   >
   >
   >`ant clean all`
   >
   >
   >Pressione `Return` quando necessário.

1. Baixe os seguintes arquivos na pasta raiz da sua distribuição de híbridos extraída,

   ```
       <<i>hybris-root-directory</i>>
   ```

   :

   [Obter arquivo](assets/setup.groovy)

   >[!NOTE]
   >
   >Para o hybris 5.6.0 e posterior, use o seguinte setup.groovy.

   5.6.0 e posterior

   [Obter arquivo](assets/setup-1.groovy)

1. Na linha de comando, execute o seguinte para:

   * atualizar a configuração do servidor hybris (conforme exigido pela extensão)
   * recrie o servidor hybris com a configuração modificada
   * iniciar o servidor

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >Dependendo do seu sistema, várias dessas etapas podem levar vários minutos para serem concluídas.

1. No seu navegador, navegue até o console **de administração de** hybris em:

   [https://localhost:9002](https://localhost:9002)

1. Clique em **Inicializar** e confirme a ação de inicialização (pois ela excluirá os dados existentes).

   O progresso será mostrado no console, com a `FINISHED` indicação de conclusão.

   >[!NOTE]
   >
   >Dependendo do seu sistema, isso pode levar vários minutos para ser concluído.

### Configuração da loja Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Este procedimento fará upload e configurará a loja de demonstração - Geometrixx Online.

1. Inicie sua ocorrência de hipérrimos. Na linha de comando, execute o seguinte:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. No seu navegador, navegue até o console **de gerenciamento de** híbridos em:

   [https://localhost:9002/hmc/hybris](https://localhost:9002/hmc/hybris)

1. Na barra lateral de navegação, explique **Sistema** e **Ferramentas**. Em seguida, selecione **Importar** para abrir o **Assistente: Janela Importação** CSV.
1. Na guia **Configuração** , **carregue** o seguinte arquivo **de** importação:

   [Obter arquivo](assets/geometrixx-outdoors-export.csv)

1. Defina **Locale Setting** como:

   `en_US - English (United States)`

1. Open the **Resources** tab.
1. **Carregue** o seguinte **Media-Zip**:

   [Obter arquivo](assets/geometrixx-outdoors-images.zip)

1. Clique em **Iniciar** para importar os arquivos especificados. A guia **Resultado** mostrará quaisquer entradas de log.

1. Clique em **Concluído** para fechar a janela de importação.

1. Na barra lateral, selecione **Sistema**, **Ferramentas** e, em seguida, **Importar**.

1. **Carregue** o seguinte arquivo **** de importação:

   [Obter arquivo](assets/base-store.csv)para hybris 5.7, use o seguinte:

   [Obter arquivo](assets/base-store-5_7.csv)

1. Defina **Locale Setting** como:

   `en_US - English (United States)`

1. Clique em **Iniciar** para importar os arquivos especificados. A guia **Resultado** mostrará quaisquer entradas de log.

1. Clique em **Concluído** para fechar a janela de importação.

1. Agora você pode usar o cockpit de produtos para exibir os catálogos e produtos importados:

   [https://localhost:9002/productcockpit](https://localhost:9002/productcockpit)

