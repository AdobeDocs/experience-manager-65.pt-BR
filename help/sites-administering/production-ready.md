---
title: Execução do AEM no modo de produção pronto
seo-title: Execução do AEM no modo de produção pronto
description: Saiba como executar o AEM no modo Pronto para produção.
seo-description: Saiba como executar o AEM no modo Pronto para produção.
uuid: f48c8bae-c72f-4772-967e-f1526f096399
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 32da99f0-f058-40ae-95a8-2522622438ce
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Execução do AEM no modo de produção pronto{#running-aem-in-production-ready-mode}

Com o AEM 6.1, a Adobe apresenta o novo `"nosamplecontent"` modo de execução destinado a automatizar as etapas necessárias para preparar uma instância do AEM para implantação em um ambiente de produção.

O novo modo de execução não só configurará automaticamente a instância para aderir às práticas recomendadas de segurança descritas na lista de verificação de segurança, como também removerá todos os aplicativos e configurações de geometrixx de amostra no processo.

>[!NOTE]
>
>Como, por motivos práticos, o AEM Production Ready Mode cobrirá apenas a maioria das tarefas necessárias para proteger uma instância, é altamente recomendável consultar a Lista de verificação [de](/help/sites-administering/security-checklist.md) segurança antes de entrar em operação com seu ambiente de produção.
>
>Além disso, observe que a execução do AEM no modo Pronto para produção desativará efetivamente o acesso ao CRXDE Lite. Se você precisar dele para depurar finalidades, consulte [Ativar o CRXDE Lite no AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Para executar o AEM no modo de produção pronto, basta adicionar o comutador do `nosamplecontent` `-r` modo de execução aos argumentos de inicialização existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por exemplo, você pode usar a produção pronta para iniciar uma instância do autor com persistência MongoDB como esta:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Altera parte do modo Production Ready {#changes-part-of-the-production-ready-mode}

Mais especificamente, as seguintes alterações de configuração serão executadas quando o AEM for executado no modo de produção pronto:

1. Por padrão, o pacote **de suporte** CRXDE ( `com.adobe.granite.crxde-support`) está desativado no modo de produção pronto. Ele pode ser instalado a qualquer momento a partir do repositório do Adobe public Maven. A versão 3.0.0 é necessária para o AEM 6.1.

1. O **pacote Apache Sling Simple WebDAV Access to repositories** ( `org.apache.sling.jcr.webdav`) só estará disponível em instâncias do **autor** .

1. Os usuários recém-criados serão solicitados a alterar a senha no primeiro login. Isso não se aplica ao usuário administrador.
1. **Gerar informações** de depuração está desabilitado para o **Apache Java Script Handler**.

1. **O conteúdo** mapeado e as informações **de depuração** Gerar estão desativadas para o **Apache Sling JSP Script Handler**.

1. O Filtro **WCM CQ** do dia está definido como `edit` no **autor** e `disabled` nas instâncias de **publicação** .

1. **O Adobe Granite HTML Library Manager** está configurado com as seguintes configurações:

   1. **** Minifique: `enabled`
   1. **** Depuração: `disabled`
   1. **** Gzip: `enabled`
   1. **** Tempo: `disabled`

1. O Servlet **** Apache Sling GET está definido para suportar configurações seguras por padrão, como segue:

| **Configuração** | **Autor** | **Publicação** |
|---|---|---|
| Execução TXT | desativado | desativado |
| Execução HTML | desativado | desativado |
| Execução JSON | ativado | ativado |
| Execução XML | desativado | desativado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desativado | desativado |

