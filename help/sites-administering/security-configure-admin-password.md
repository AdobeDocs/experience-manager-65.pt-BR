---
title: Configure a senha do administrador na instalação
seo-title: Configure a senha do administrador na instalação
description: Saiba como alterar a senha de administrador na instalação do AEM.
seo-description: Saiba como alterar a senha de administrador na instalação do AEM.
uuid: 06da9890-ed63-4fb6-88d5-fd0e16bc4ceb
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 00806e6e-3578-4caa-bafa-064f200a871f
translation-type: tm+mt
source-git-commit: 1c1ade947f2cbd26b35920cfd10b1666b132bcbd

---


# Configure a senha do administrador na instalação{#configure-the-admin-password-on-installation}

## Visão geral {#overview}

Desde a versão 6.3, o AEM permite que a senha do administrador seja definida usando a linha de comando ao instalar uma nova instância.

Com as versões anteriores do AEM, a senha da conta do administrador, juntamente com a senha de vários outros consoles, precisavam ser alteradas após a instalação.

Esse recurso adiciona a facilidade de definir uma nova senha de administrador para o repositório e o Mecanismo Servlet durante a instalação de uma instância do AEM, eliminando a necessidade de fazê-lo manualmente depois.

>[!CAUTION]
>
>Observe que o recurso não abrange o Console do Felix, para o qual a senha precisa ser alterada manualmente. Para obter mais informações, consulte a seção [Lista de verificação de](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts)segurança relevante.

## Como Usá-La? {#how-do-i-use-it}

Esse recurso será acionado automaticamente se você optar por instalar o AEM pela linha de comando, em vez de clicar duas vezes no JAR de um explorador de sistemas de arquivos.

A síntese geral para executar uma instância do AEM a partir da linha de comando é:

```shell
java -jar aem6.3.jar
```

Ao executar a instância a partir da linha de comando, você terá a opção de alterar a senha do administrador durante o processo de instalação:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>O prompt para alterar a senha do administrador só será exibido durante a instalação de uma nova instância do AEM.

## Usando o sinalizador -nointerativo {#using-the-nointeractive-flag}

Você também pode especificar a senha de um arquivo de propriedades. Isso é feito usando o `-nointeractive` sinalizador combinado com`-Dadmin.password.file` a propriedade system.

Veja abaixo um exemplo:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

A senha dentro do `passwordfile.properties` arquivo precisa ter o formato abaixo:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Se você simplesmente usar o `-nointeractive` parâmetro sem a propriedade `-Dadmin.password.file` do sistema, o AEM usará a senha de administrador padrão sem solicitar que você a altere, essencialmente replicando o comportamento de versões anteriores. Esse modo não interativo pode ser usado para instalações automatizadas usando a linha de comando em um script de instalação.

