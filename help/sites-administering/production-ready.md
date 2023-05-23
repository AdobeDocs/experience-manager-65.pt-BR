---
title: Execução do AEM no modo de produção pronta
seo-title: Running AEM in Production Ready Mode
description: Saiba como executar o AEM no modo de produção pronta.
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

# Execução do AEM no modo de produção pronta{#running-aem-in-production-ready-mode}

Com o AEM 6.1, o Adobe apresenta o novo `"nosamplecontent"` runmode destinado a automatizar as etapas necessárias para preparar uma instância do AEM para implantação em um ambiente de produção.

O novo modo de execução não só configurará automaticamente a instância para seguir as práticas recomendadas de segurança descritas na lista de verificação de segurança, como também removerá todos os aplicativos e configurações de amostra do Geometrixx no processo.

>[!NOTE]
>
>Como, por motivos práticos, o AEM Production Ready Mode cobrirá apenas a maioria das tarefas necessárias para proteger uma instância, é altamente recomendável consultar o [Lista de verificação de segurança](/help/sites-administering/security-checklist.md) antes de entrar em funcionamento com seu ambiente de produção.
>
>Além disso, observe que a execução do AEM no Modo Pronto para produção desativará efetivamente o acesso ao CRXDE Lite. Se for necessário para fins de depuração, consulte [CRXDE Lite no AEM](/help/sites-administering/enabling-crxde-lite.md).

![chlimage_1-83](assets/chlimage_1-83a.png)

Para executar o AEM no modo de produção pronto, basta adicionar o `nosamplecontent` por meio da `-r` runmode alterne para seus argumentos de inicialização existentes:

```shell
java -jar aem-quickstart.jar -r nosamplecontent
```

Por exemplo, você pode usar a produção pronta para iniciar uma instância de autor com persistência MongoDB, desta forma:

```shell
java -jar aem-quickstart.jar -r author,crx3,crx3mongo,nosamplecontent -Doak.mongo.uri=mongodb://remoteserver:27017 -Doak.mongo.db=aem-author
```

## Altera parte do modo Pronto para produção {#changes-part-of-the-production-ready-mode}

Mais especificamente, as seguintes alterações de configuração serão executadas quando o AEM for executado no modo pronto para produção:

1. A variável **Pacote de suporte do CRXDE** ( `com.adobe.granite.crxde-support`) é desativado por padrão no modo de produção pronta. Ele pode ser instalado a qualquer momento no repositório Maven público do Adobe. A versão 3.0.0 é necessária para o AEM 6.1.

1. A variável **Apache Sling Simple WebDAV Acesso a repositórios** ( `org.apache.sling.jcr.webdav`) o pacote só estará disponível em **autor** instâncias.

1. Usuários recém-criados precisarão alterar a senha no primeiro logon. Isso não se aplica ao usuário administrador.
1. **Gerar informações de depuração** está desativado para o **Manipulador de script Java do Apache Sling**.

1. **Conteúdo mapeado** e **Gerar informações de depuração** estão desativados para a variável **Manipulador de script JSP do Apache Sling**.

1. A variável **Filtro WCM CQ do dia** está definida como `edit` em **autor** e `disabled` em **publicar** instâncias.

1. A variável **Gerenciador de biblioteca de HTML do Adobe Granite** O está configurado com as seguintes configurações:

   1. **Minificar:** `enabled`
   1. **Depurar:** `disabled`
   1. **Gzip:** `enabled`
   1. **Horário:** `disabled`

1. A variável **Apache Sling GET Servlet** O está definido para suportar configurações seguras por padrão, da seguinte maneira:

| **Configuração** | **Autor** | **Publicação** |
|---|---|---|
| Representação TXT | desativado | desativado |
| representação do HTML | desativado | desativado |
| Representação JSON | ativado | ativado |
| Representação XML | desativado | desativado |
| json.maximumresults | 1000 | 100 |
| Índice automático | desativado | desativado |
