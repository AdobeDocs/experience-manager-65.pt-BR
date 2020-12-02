---
title: COMMERCE CLOUD SAP
seo-title: COMMERCE CLOUD SAP
description: Saiba como implantar o eCommerce com o Commerce Cloud SAP.
seo-description: Saiba como implantar o eCommerce com o Commerce Cloud SAP.
uuid: a16ae42b-9c33-4da8-a130-52b72a779ec7
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: e-commerce
content-type: reference
discoiquuid: 44dfa10f-497e-473f-95d4-8dccae7ebf8e
pagetitle: Deploying eCommerce with SAP Commerce Cloud
translation-type: tm+mt
source-git-commit: 328e13eb2ce034b0b1ec7e5e0fb184de9435d1bc
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 0%

---


# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>Esta página contém links para o site hybris. Para determinadas páginas, você precisará de uma conta para fazer logon.

## Implantação do eCommerce com o SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Os procedimentos a seguir usam o seguinte catálogo de demonstração para ilustrar a implantação:
>
>`Geometrixx Outdoors Site English (US)`

A implantação dos [pacotes necessários de comércio eletrônico](#packages-needed-for-ecommerce-with-hybris) proporcionará a funcionalidade completa da estrutura de comércio eletrônico, juntamente com uma implementação de referência da funcionalidade de comércio eletrônico, conforme fornecida com uma implementação híbrida (incluindo um catálogo de demonstração)

Isso está disponível na ramificação Inglês (EUA) ( `/content/geometrixx-outdoors/en_US`) do site do Geometrixx Outdoors:

* [Informações](#productinformationwithcolorvariants)  do produto (com variantes de cor, quando apropriado)

* [Visão geral do conteúdo do carrinho de compras](#shoppingcartcontentoverview)
* [Logon do cliente ](#customersignup) e logon do  [cliente](#customersignin)

* [Acesso ao console de gerenciamento de híbridos](#accesstothehybrismanagementconsole)

### Requisitos técnicos - servidor hybris {#technical-requirements-hybris-server}

A extensão hybris do eCommerce Integration Framework foi atualizada para suportar o Hybris 5 (como padrão), mantendo a compatibilidade retroativa com [Hybris 4](/help/sites-developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Suporta as versões 18.11 e superior.
>* Você precisará do Java 7 para executar o servidor [hybris 5.](https://www.hybris.com/en/architecture-technology)
>* O complemento hybris, o [Acelerador Telco](https://www.hybris.com/en/products/telecommunication), não é suportado pela extensão AEM.

>



### Pacotes necessários para comércio eletrônico com hífen {#packages-needed-for-ecommerce-with-hybris}

Para instalar a funcionalidade de comércio eletrônico, é necessário:

* Seu servidor hybris
* AEM estrutura de comércio eletrônico:

   * isso faz parte de uma instalação padrão AEM

* Pacote de Geometrixx AEM:

   * `cq-geometrixx-all-pkg`

* Pacotes de conteúdo de AEM hips:

   * `cq-hybris-content-6.3.2`
   * implementação da API específica de hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * uma implementação de referência para ilustrar o uso de híbridos ( `geometrixx-outdoors/en_US`)

### Instalação do eCommerce com híbridos {#installation-of-ecommerce-with-hybris}

Para instalar uma configuração completa (usando o catálogo de demonstração, Geometrixx Outdoors), as etapas básicas são:

1. [Instale AEM](/help/sites-deploying/deploy.md).
1. Instale o pacote Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Instale os pacotes de conteúdo de demonstração usando o [gerenciador de pacote](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Baixe e crie seu servidor](#download-and-build-your-hybris-server) hybris.
1. Construa seu catálogo em seu mecanismo de comércio eletrônico:

   1. [Configure a Loja](#setup-the-geometrixx-outdoors-store) do Exterior da Geometrixx.

1. [](/help/sites-authoring/qg-page-authoring.md) Autorize as páginas suplementares que você precisa no AEM.

>[!CAUTION]
>
>O uso do servidor hybris requer uma licença separada de hybris.

>[!NOTE]
>
>Para desenvolvedores [A documentação da API](/help/sites-developing/ecommerce.md#api-documentation) também está disponível para download.

### Baixe e crie seu servidor hybris {#download-and-build-your-hybris-server}

As etapas neste procedimento baixarão e criarão o servidor hybris. Ele também tornará as configurações iniciais necessárias para as conexões entre hybris e cq. A extensão será então utilizável com as configurações padrão.

>[!CAUTION]
>
>Versões de hiperbrilho anteriores à versão 5.5.1 não são suportadas.

>[!NOTE]
>
>Para concluir, você precisará do [Groovy](https://groovy-lang.org/) instalado no sistema.

1. Baixe a distribuição **hybris Commerce Suite** do site de download hybris.

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
   >`ant clean all`
   >
   >Pressione `Return` quando necessário.

1. Baixe os seguintes arquivos na pasta raiz da sua distribuição de híbridos extraída,

   ```
       <hybris-root-directory>
   ```


   [Obter arquivo](assets/setup.groovy)

   >[!NOTE]
   >
   >Para o hybris 5.6.0 e posterior, use o seguinte setup.groovy.

   5.6.0 e posterior

   [Obter arquivo](assets/setup-1.groovy)

1. Na linha de comando, execute o seguinte para:

   * atualizar a configuração do servidor hybris (conforme exigido pela extensão)
   * recrie o servidor hybris com a configuração modificada
   * start do servidor

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >Dependendo do seu sistema, várias dessas etapas podem levar vários minutos para serem concluídas.

1. No seu navegador, navegue até **console de administração de híbridos** em:

   [http://localhost:9002](http://localhost:9002)

1. Clique em **Inicializar** e confirme a ação de inicialização (pois ela excluirá os dados existentes).

   O progresso será mostrado no console, com `FINISHED` indicando a conclusão.

   >[!NOTE]
   >
   >Dependendo do seu sistema, isso pode levar vários minutos para ser concluído.

### Configure a Geometrixx Outdoors Store {#setup-the-geometrixx-outdoors-store}

Este procedimento fará upload e configurará a loja de demonstração - Geometrixx Online.

1. Start sua ocorrência de hipérrimos. Na linha de comando, execute o seguinte:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. No seu navegador, navegue até **console de gerenciamento de híbridos** em:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Use estas credenciais:
   * nome de usuário: admin
   * senha: nimda

1. Na barra lateral de navegação, explique **System** e **Tools**. Em seguida, selecione **Importar** para abrir o **Assistente: Janela Importação de CSV**.
1. Na guia **Configuração**, **Carregue** o seguinte **Importar ficheiro**:

   [Obter arquivo](assets/geometrixx-outdoors-export.csv)

1. Defina **Locale Setting** como:

   `en_US - English (United States)`

1. Abra a guia **Resources**.
1. **** Carregue o seguinte  **Media-Zip**:

   [Obter arquivo](assets/geometrixx-outdoors-images.zip)

1. Clique em **Start** para importar os arquivos especificados. A guia **Resultado** mostrará quaisquer entradas de log.

1. Clique em **Done** para fechar a janela de importação.

1. Na barra lateral, selecione **Sistema**, **Ferramentas** e **Importar**.

1. **** Carregue o seguinte arquivo **** de importação:

   [Obter arquivo](assets/base-store.csv)

   Para os híbridos 5.7, use o seguinte:

   [Obter arquivo](assets/base-store-5_7.csv)

1. Defina **Locale Setting** como:

   `en_US - English (United States)`

1. Clique em **Start** para importar os arquivos especificados. A guia **Resultado** mostrará quaisquer entradas de log.

1. Clique em **Done** para fechar a janela de importação.

1. Agora você pode usar o cockpit de produtos para visualização dos catálogos e produtos importados:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)

