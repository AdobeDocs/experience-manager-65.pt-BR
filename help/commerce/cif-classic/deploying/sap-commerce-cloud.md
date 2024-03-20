---
title: Implantação do comércio eletrônico com o SAP Commerce Cloud
description: Saiba como implantar o Adobe Experience Manager eCommerce com Commerce Cloud SAP.
contentOwner: Guillaume Carlino
topic-tags: e-commerce
content-type: reference
exl-id: ecbd0097-c407-4581-bab2-4729a71df4a3
solution: Experience Manager,Commerce
source-git-commit: 1751bfb32386685e3a159939113b9667b5e17f0e
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---

# COMMERCE CLOUD SAP{#sap-commerce-cloud}

>[!NOTE]
>
>Esta página contém links para o site da hybris. Para determinadas páginas, é necessário ter uma conta para fazer logon.

## Implantação do comércio eletrônico com o SAP Commerce Cloud {#deploying-ecommerce-with-sap-commerce-cloud}

>[!NOTE]
>
>Os procedimentos a seguir usam o seguinte catálogo de demonstração para ilustrar a implantação:
>
>`Geometrixx Outdoors Site English (US)`

Implantar o [pacotes de comércio eletrônico necessários](#packages-needed-for-ecommerce-with-hybris) O fornece a funcionalidade completa da estrutura de comércio eletrônico, juntamente com uma implementação de referência da funcionalidade de comércio eletrônico, conforme fornecido com uma implementação hybris (incluindo um catálogo de demonstração)

Está disponível na ramificação em inglês (EUA) ( `/content/geometrixx-outdoors/en_US`) do local da Geometrixx Outdoors:

* [Informações do produto](#productinformationwithcolorvariants) (com variantes de cor, quando apropriado)

* [Visão geral do conteúdo do carrinho de compras](#shoppingcartcontentoverview)
* [Inscrição do cliente](#customersignup) e [Logon do cliente](#customersignin)

* [Acesso ao console de gerenciamento híbrido](#accesstothehybrismanagementconsole)

### Requisitos técnicos - hybris Server {#technical-requirements-hybris-server}

A extensão hybris da Estrutura de integração de comércio eletrônico foi atualizada para oferecer suporte ao Hybris 5 (como padrão), mantendo a compatibilidade com versões anteriores com o [Hybris 4](/help/commerce/cif-classic/developing/sap-commerce-cloud.md#developing-for-hybris).

>[!NOTE]
>
>* Oferece suporte às versões 18.11 e posteriores.
>* Você precisa do Java™ 7 para executar o [hybris 5 server.](https://www.sap.com/products/crm.html)
>* O complemento hybris, a variável [Acelerador Telco](https://www.sap.com/products/crm.html), não é compatível com a extensão AEM.
>

### Pacotes necessários para comércio eletrônico com hybris {#packages-needed-for-ecommerce-with-hybris}

Para instalar a funcionalidade de comércio eletrônico, é necessário:

* Seu servidor hybris
* Estrutura de comércio eletrônico AEM:

   * isto é parte de uma instalação padrão do AEM

* Pacote para AEM Geometrixx-all:

   * `cq-geometrixx-all-pkg`

* Pacotes de conteúdo do AEM hybris:

   * `cq-hybris-content-6.3.2`
   * implementação da API específica do hybris
   * `cq-geometrixx-hybris-content-6.3.2`
   * uma implementação de referência para ilustrar o uso de hybris ( `geometrixx-outdoors/en_US`)

### Instalação do eCommerce com hybris {#installation-of-ecommerce-with-hybris}

Para instalar uma configuração completa (usando o catálogo de demonstração, Geometrixx Outdoors), as etapas básicas são:

1. [Instalar AEM](/help/sites-deploying/deploy.md).
1. Instale o pacote Geometrixx-all

   1. ` [cq-geometrixx-all-pkg](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq60/product/cq-geometrixx-all-pkg)`

1. Instale os pacotes de conteúdo de demonstração usando o [Gerenciador de pacotes](/help/sites-administering/package-manager.md):

   1. ` [cq-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-hybris-content)`
   1. ` [cq-geometrixx-hybris-content-6.3.2](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq630/product/cq-geometrixx-hybris-content)`

1. [Baixe e crie seu servidor hybris](#download-and-build-your-hybris-server).
1. Construa seu catálogo no mecanismo de comércio eletrônico:

   1. [Configurar a loja de outdoor do Geometrixx](#setup-the-geometrixx-outdoors-store).

1. [Autor](/help/sites-authoring/qg-page-authoring.md) qualquer página suplementar que você precise no AEM.

>[!CAUTION]
>
>O uso do servidor hybris requer uma licença hybris separada.

>[!NOTE]
>
>Para desenvolvedores, [Documentação da API](/help/commerce/cif-classic/developing/ecommerce.md#api-documentation) O também está disponível para download.

### Baixe e crie seu servidor hybris {#download-and-build-your-hybris-server}

As etapas neste procedimento baixam e criam o servidor hybris. Também faz as configurações iniciais necessárias para as conexões entre hybris e cq. A extensão pode ser usada com as configurações padrão.

>[!CAUTION]
>
>As versões do Hybris anteriores à 5.5.1 não são compatíveis.

>[!NOTE]
>
>Para concluir isso, é necessário [Groovy](https://groovy-lang.org/) instalado no sistema.

1. Baixe o **hybris Commerce Suite** distribuição do site de download do hybris.

   >[!CAUTION]
   >
   >Você precisa de uma conta (do hybris) para acessar isso.

1. Descompacte o arquivo de distribuição no local desejado (referido como &lt;hybris-root-directory>).
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

1. Baixe os arquivos a seguir para a pasta raiz da distribuição hybris extraída,

   ```
       <hybris-root-directory>
   ```


[Obter arquivo](/help/sites-deploying/assets/setup.groovy)

   >[!NOTE]
   >
   >Para o hybris 5.6.0 e versões posteriores, use o seguinte setup.groovy.

   5.6.0 e posterior

[Obter arquivo](/help/sites-deploying/assets/setup-1.groovy)

1. Na linha de comando, execute o seguinte para:

   * atualizar a configuração do servidor hybris (conforme exigido pela extensão)
   * reconstruir o servidor hybris com a configuração modificada
   * iniciar o servidor

   ```shell
   groovy setup.groovy
   cd bin/platform
   ant clean all
   sh hybrisserver.sh
   ```

   >[!NOTE]
   >
   >Dependendo do sistema, várias dessas etapas podem levar vários minutos para serem concluídas.

1. Em seu navegador, navegue até o **console de administração hybris** em:

   [http://localhost:9002](http://localhost:9002)

1. Clique em **Inicializar** e, em seguida, confirme a ação de inicialização (ao excluir os dados existentes).

   O progresso é mostrado no console, com `FINISHED` indicando a conclusão.

   >[!NOTE]
   >
   >Dependendo do sistema, isso pode levar vários minutos para ser concluído.

### Configurar a loja de Geometrixx Outdoors {#setup-the-geometrixx-outdoors-store}

Este procedimento carrega e configura a loja de demonstração - Geometrixx Online.

1. Inicie a instância do hybris. Na linha de comando, execute o seguinte:

   ```shell
   cd <hybris-root-directory>/bin/platform
   sh hybrisserver.sh
   ```

1. Em seu navegador, navegue até o **hybris management console** em:

   [https://localhost:9002/backoffice](https://localhost:9002/backoffice)

   Usar estas credenciais:
   * nome de usuário: admin
   * senha: nimda

1. Na navegação da barra lateral, expanda **Sistema** e **Ferramentas**. Em seguida, selecione **Importar** para abrir o **Assistente: importação de CSV** janela.
1. No **Configuração** guia, **Carregar** o seguinte **Importar arquivo**:

[Obter arquivo](/help/sites-deploying/assets/geometrixx-outdoors-export.csv)

1. Defina o **Configuração de local** para:

   `en_US - English (United States)`

1. Abra o **Recursos** guia.
1. **Carregar** o seguinte **Media-Zip**:

[Obter arquivo](/help/sites-deploying/assets/geometrixx-outdoors-images.zip)

1. Clique em **Início** para importar os arquivos especificados. A variável **Resultado** mostra todas as entradas de log.

1. Clique em **Concluído** para fechar a janela de importação.

1. Na barra lateral, selecione **Sistema**, depois **Ferramentas**, depois **Importar**.

1. **Carregar** o seguinte **Importar arquivo**:

[Obter arquivo](/help/sites-deploying/assets/base-store.csv)

   Para o hybris 5.7, use o seguinte:

[Obter arquivo](/help/sites-deploying/assets/base-store-5_7.csv)

1. Defina o **Configuração de local** para:

   `en_US - English (United States)`

1. Clique em **Início** para importar os arquivos especificados. A variável **Resultado** mostra todas as entradas de log.

1. Clique em **Concluído** para fechar a janela de importação.

1. Agora você pode usar o cockpit do produto para exibir os catálogos e produtos importados:

   [http://localhost:9002/productcockpit](http://localhost:9002/productcockpit)
