---
title: Executando AEM no modo Pronto para produção
seo-title: Running AEM in Production Ready Mode
description: Saiba como executar o AEM no Modo de preparação para produção.
seo-description: Learn how to run AEM in Production Ready Mode.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
exl-id: 3c342014-f8ec-4404-afe5-514bdb651aae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 3%

---

# Executando AEM no modo Pronto para produção{#running-aem-in-production-ready-mode}

Com o AEM 6.1, o Adobe apresenta o novo `"nosamplecontent"` runmode destinado a automatizar as etapas necessárias para preparar uma instância de AEM para implantação em um ambiente de produção.

O novo modo de execução não somente configurará automaticamente a instância para aderir às práticas recomendadas de segurança descritas na lista de verificação de segurança, como também removerá todos os aplicativos e configurações de geometrixx de amostra no processo.

>[!NOTE]
>
>Como, por motivos práticos, o AEM Production Ready Mode só cobrirá a maioria das tarefas necessárias para proteger uma instância, é altamente recomendável consultar o [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) antes de entrar em contato com seu ambiente de produção.
>
>Além disso, observe que a execução de AEM no Modo de Pronto para Produção desativará efetivamente o acesso ao CRXDE Lite. Se for necessário para fins de depuração, consulte [Ativar o CRXDE Lite AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Para executar o AEM no modo de produção pronto, basta adicionar o `nosamplecontent` através da `-r` comutador runmode para os argumentos de arranque existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por exemplo, você pode usar a produção pronta para iniciar uma instância de autor com a persistência de MongoDB desta forma:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Altera parte do Modo de Pronto para Produção {#changes-part-of-the-production-ready-mode}

Mais especificamente, as seguintes alterações de configuração serão executadas quando o AEM for executado no modo pronto para produção:

1. O **Pacote de suporte CRXDE** ( `com.adobe.granite.crxde-support`) é desativado por padrão no modo de produção pronto. Ele pode ser instalado a qualquer momento a partir do repositório Maven do Adobe public. A versão 3.0.0 é necessária para o AEM 6.1.

1. O **Apache Sling Acesso WebDAV Simples a Repositórios** ( `org.apache.sling.jcr.webdav`) só estará disponível em **autor** instâncias.

1. Os usuários recém-criados serão solicitados a alterar a senha no primeiro logon. Isso não se aplica ao usuário administrador.
1. **Gerar informações de depuração** está desativado para a variável **Manipulador de script Java do Apache Sling**.

1. **Conteúdo mapeado** e **Gerar informações de depuração** estão desativadas para a variável **Manipulador de script JSP do Apache Sling**.

1. O **Filtro Day CQ WCM** está definida como `edit` on **autor** e `disabled` on **publicar** instâncias.

1. O **Gerenciador de biblioteca de HTML do Adobe Granite** é configurado com as seguintes configurações:

   1. **Minimizar:** `enabled`
   1. **Depuração:** `disabled`
   1. **Gzip:** `enabled`
   1. **Tempo:** `disabled`

1. O **Servlet de GET Apache Sling** O está configurado para suportar configurações seguras por padrão, da seguinte maneira:

| **Configuração** | **Autor** | **Publicação** |
|---|---|---|
| Representação TXT | desativado | desativado |
| HTML rendition | desativado | desativado |
| Representação JSON | ativado | ativado |
| Representação XML | desativado | desativado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desativado | desativado |
