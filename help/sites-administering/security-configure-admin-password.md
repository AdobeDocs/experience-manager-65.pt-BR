---
title: Configurar a senha do administrador na instalação
description: Saiba como alterar a senha de administrador na instalação do Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Configurar a senha do administrador na instalação{#configure-the-admin-password-on-installation}

## Visão geral {#overview}

Desde a versão 6.3, o Adobe Experience Manager (AEM) permite que a senha do administrador seja definida usando a linha de comando ao instalar uma nova instância.

Com versões anteriores do AEM, a senha da conta de administrador, juntamente com a senha de vários outros consoles, tinham de ser alteradas após a instalação.

Esse recurso adiciona a facilidade de definir uma nova senha de administrador para o repositório e o Mecanismo Servlet durante a instalação de uma instância do AEM, eliminando assim a necessidade de fazer isso manualmente posteriormente.

>[!CAUTION]
>
>O recurso não abrange o Felix Console, para o qual a senha deve ser alterada manualmente. Para obter mais informações, consulte as [seção Lista de Verificação de Segurança](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts).

## Como Usá-Lo? {#how-do-i-use-it}

Esse recurso será acionado automaticamente se você optar por instalar o AEM por meio da linha de comando, em vez de clicar duas vezes no JAR em um explorador de sistema de arquivos.

A sintaxe geral para executar uma instância AEM a partir da linha de comando é:

```shell
java -jar aem6.3.jar
```

Depois de executar a instância na linha de comando, você verá a opção de alterar a senha do administrador durante o processo de instalação:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>O prompt para alterar a senha do administrador é exibido apenas durante a instalação de uma nova instância do AEM.

## Uso do Sinalizador -nointerativo {#using-the-nointeractive-flag}

Você também pode optar por especificar a senha a partir de um arquivo de propriedades. Isso é feito usando o `-nointeractive` sinalizador combinado com o `-Dadmin.password.file` propriedade do sistema.

Veja um exemplo abaixo:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

A senha dentro do `passwordfile.properties` O arquivo deve ter o formato abaixo:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Se você simplesmente usar o `-nointeractive` parâmetro sem o `-Dadmin.password.file` propriedade do sistema, o AEM usa a senha padrão do administrador sem solicitar que você a altere, basicamente replicando o comportamento de versões anteriores. Esse modo não interativo pode ser usado para instalações automatizadas usando a linha de comando em um script de instalação.
