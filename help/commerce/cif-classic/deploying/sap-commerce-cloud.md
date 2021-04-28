---
title: Commerce Cloud SAP
seo-title: Commerce Cloud SAP
description: Saiba como implantar o eCommerce com o SAP Commerce Cloud.
seo-description: Saiba como implantar o eCommerce com o SAP Commerce Cloud.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
translation-type: tm+mt
source-git-commit: da538dac17b4c6182b44801b4c79d6cdbf35f640
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 2%

---

# SAP Commerce Cloud{#sap-commerce-cloud}

>[!NOTE]
>
>Esta página contém links para o site de hybris. Para determinadas páginas, você precisará de uma conta para fazer logon.

## Implantação do comércio eletrônico com o SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Os procedimentos a seguir usam o seguinte catálogo de demonstração para ilustrar a implantação:
>
>`Geometrixx Outdoors Site English (US)`

A implantação dos [pacotes de comércio eletrônico necessários](#packages-needed-for-ecommerce-with-hybris) proporcionará a funcionalidade completa da estrutura de comércio eletrônico, juntamente com uma implementação de referência da funcionalidade de comércio eletrônico, conforme fornecido com uma implementação de hybris (incluindo um catálogo de demonstração)

Isso está disponível na ramificação inglesa (EUA) ( `/content/geometrixx-outdoors/en_US`) do site Geometrixx Outdoors:

* [Informações do produto](#productinformationwithcolorvariants)  (com variantes de cor, quando apropriado)

* [Visão geral do conteúdo do Carrinho de compras](#shoppingcartcontentoverview)
* [Logon ](#customersignup) no cliente - Fazer logon no  [cliente](#customersignin)

* [Acesso ao console de gerenciamento de híbridos](#accesstothehybrismanagementconsole)

### Requisitos técnicos - Servidor hybris {#technical-requirements-hybris-server}

A extensão hybris da Estrutura de Integração do eCommerce foi atualizada para oferecer suporte ao Hybris 5 (como padrão), mantendo a compatibilidade com o [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Suporta as versões 18.11 e superior.
>* Você precisará do Java 7 para executar o servidor [hybris 5.](https://www.hybris.com/en/architecture-technology)
>* O complemento hybris, o [Acelerador de Telco](https://www.hybris.com/en/products/telecommunication), não é suportado pela extensão AEM.

>



### Pacotes necessários para comércio eletrônico com híbridos {#packages-needed-for-ecommerce-with-hybris}

Para instalar a funcionalidade de comércio eletrônico, é necessário:

* Seu servidor hybris
* AEM estrutura de comércio eletrônico:

   * isso faz parte de uma instalação AEM padrão

* AEM pacote Geometrixx-all:

   * `cq-geometrixx-all-pkg`

* Pacotes de conteúdo de híbridos AEM:

   * `cq-hybris-content-6.3.2`
   * implementação de API específica de híbridos
   * `cq-geometrixx-hybris-content-6.3.2`
   * uma implementação de referência para ilustrar o uso de híbridos ( `geometrixx-outdoors/en_US`)

### Instalação do comércio eletrônico com híbridos {#installation-of-ecommerce-with-hybris}

Para instalar uma configuração completa (usando o catálogo de demonstração, Geometrixx Outdoors), as etapas básicas são:

1. [Instalar AEM](/help/sites-deploying/deploy.md).
1. Instale o pacote Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Instale os pacotes de conteúdo de demonstração usando o [gerenciador de pacotes](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Baixe e crie seu servidor hybris](#download-and-build-your-hybris-server).
1. Construa seu catálogo no seu mecanismo de comércio eletrônico:

   1. [Configure a loja](#setup-the-geometrixx-outdoors-store) do Geometrixx Outdoor.

1. [](/help/sites-authoring/qg-page-authoring.md) Autorize páginas suplementares que você precisa no AEM.

>[!CAUTION]
>
>O uso do servidor hybris requer uma licença de hybris separada.

>[!NOTE]
>
>Para desenvolvedores, a [documentação da API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) também está disponível para download.

### Baixe e crie seu servidor hybris {#download-and-build-your-hybris-server}

As etapas neste procedimento baixarão e criarão o servidor hybris. Ele também fará as configurações iniciais necessárias para as conexões entre hybris e cq. A extensão será utilizável com as configurações padrão.

>[!CAUTION]
>
>As versões Hybris anteriores à 5.5.1 não são compatíveis.

>[!NOTE]
>
>Para concluir isso, você precisará do [Groovy](https://groovy-lang.org/) instalado em seu sistema.

1. Baixe a distribuição **hybris Commerce Suite** do site de download de híbridos.

   >[!CAUTION]
   >
   >Você precisará de uma conta (de híbridos) para acessar o .

1. Descompacte o arquivo de distribuição no local necessário (referido como &lt;hybris-root-diretory>).
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

1. Baixe os seguintes arquivos para a pasta raiz da distribuição de híbridos extraídos,

   ```
       <hybris-root-directory>
   ```


   [Obter arquivo](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >Para hybris 5.6.0 e posteriores, use o seguinte setup.groovy.

   5.6.0 e posterior

   [Obter arquivo](/help/sites-deploying/assets/setup-1.groovy)

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

1. No seu navegador, navegue até o **console de administração de híbridos** em:

   [http://localhost:9002](http://localhost:9002)

1. Clique em **Initialize** e confirme a ação de inicialização (pois ela excluirá os dados existentes).

   O progresso será mostrado no console, com `FINISHED` indicando conclusão.

   >[!NOTE]
   >
   >Dependendo do sistema, isso pode levar vários minutos para ser concluído.

### Configure a Loja Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Este procedimento fará upload e configurará a loja de demonstração - Geometrixx Online.

1. Inicie sua instância de híbridos. Na linha de comando, execute o seguinte:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. No navegador, navegue até o **console de gerenciamento de híbridos** em:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Use estas credenciais:
   * nome de usuário: administrador
   * senha: nimda

1. Na navegação da barra lateral, expanda **Sistema** e **Ferramentas**. Em seguida, selecione **Importar** para abrir o **Assistente: Janela Importação de CSV**.
1. Na guia **Configuration**, **Upload** o seguinte **Import file**:

   [Obter arquivo](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Defina **Configuração de localidade** para:

   `en_US - English (United States)`

1. Abra a guia **Resources** .
1. **** Carregue o seguinte  **Media-Zip**:

   [Obter arquivo](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Clique em **Start** para importar os arquivos especificados. A guia **Result** mostrará quaisquer entradas de log.

1. Clique em **Concluído** para fechar a janela de importação.

1. Na barra lateral, selecione **Sistema**, **Ferramentas**, em seguida **Importar**.

1. **** Carregue o seguinte arquivo  **de importação**:

   [Obter arquivo](/help/sites-deploying/assets/base-store.csv)

   Para os híbridos 5.7, use o seguinte:

   [Obter arquivo](/help/sites-deploying/assets/base-store-5_7.csv)

1. Defina **Configuração de localidade** para:

   `en_US - English (United States)`

1. Clique em **Start** para importar os arquivos especificados. A guia **Result** mostrará quaisquer entradas de log.

1. Clique em **Concluído** para fechar a janela de importação.

1. Agora é possível usar o cockpit de produtos para visualizar os catálogos e produtos importados:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
