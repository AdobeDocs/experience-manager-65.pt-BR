---
title: Execução de AEM no modo de produção pronto
seo-title: Execução de AEM no modo de produção pronto
description: Saiba como executar AEM no modo Production Ready.
seo-description: Saiba como executar AEM no modo Production Ready.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 730a690bcbf5935ca00ed69c27ce108cb2664c22
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 3%

---


# Execução de AEM no modo de produção pronto{#running-aem-in-production-ready-mode}

Com o AEM 6.1, o Adobe apresenta o novo `"nosamplecontent"` runmode, que tem como objetivo automatizar as etapas necessárias para preparar uma instância AEM para implantação em um ambiente de produção.

O novo modo de execução não só configurará automaticamente a instância para aderir às práticas recomendadas de segurança descritas na lista de verificação de segurança, como também removerá todos os aplicativos e configurações de geometrixx de amostra no processo.

>[!NOTE]
>
>Como, por motivos práticos, o AEM Production Ready Mode (Modo pronto para produção) cobrirá somente a maioria das tarefas necessárias para proteger uma instância, é altamente recomendável consultar a [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) antes de entrar em operação com o ambiente de produção.
>
>Além disso, observe que a execução de AEM no modo de produção pronto desativará efetivamente o acesso ao CRXDE Lite. Se você precisar dele para fins de depuração, consulte [Ativando CRXDE Lite no AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Para executar o AEM no modo de produção pronto, basta adicionar o `nosamplecontent` por meio do switch `-r` runmode aos argumentos de inicialização existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por exemplo, você pode usar a produção pronta para iniciar uma instância do autor com persistência MongoDB como esta:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Altera parte do Production Ready Mode {#changes-part-of-the-production-ready-mode}

Mais especificamente, as seguintes alterações de configuração serão executadas quando o AEM for executado no modo de produção pronto:

1. O **pacote de suporte CRXDE** ( `com.adobe.granite.crxde-support`) está desativado por padrão no modo de produção pronto. Ele pode ser instalado a qualquer momento a partir do repositório Adobe public Maven. A versão 3.0.0 é necessária para o AEM 6.1.

1. O pacote **Apache Sling Simple WebDAV Access to repositories** ( `org.apache.sling.jcr.webdav`) só estará disponível em instâncias **author**.

1. Os usuários recém-criados serão solicitados a alterar a senha no primeiro login. Isso não se aplica ao usuário administrador.
1. **Gerar** infois de depuração desabilitados para o  **Apache Sling Java Script Handler**.

1. **Conteúdo mapeado** e  **Gerar** infoare de depuração desabilitados para o  **Apache Sling JSP Script Handler**.

1. O **Filtro de WCM do Day CQ** está definido para `edit` em **autor** e `disabled` nas instâncias **publish**.

1. O **Gerenciador de biblioteca HTML de Adobe Granite** está configurado com as seguintes configurações:

   1. **Minifique:** `enabled`
   1. **Depuração:** `disabled`
   1. **Gzip:** `enabled`
   1. **Tempo:** `disabled`

1. O **Servlet de GET Apache Sling** está definido para suportar configurações seguras por padrão, da seguinte maneira:

| **Configuração** | **Autor** | **Publicação** |
|---|---|---|
| Execução TXT | desativado | desativado |
| Execução HTML | desativado | desativado |
| Execução JSON | ativado | ativado |
| Execução XML | desativado | desativado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desativado | desativado |

