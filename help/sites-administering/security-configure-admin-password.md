---
title: Configurar a senha do administrador na instalação
description: Saiba como alterar a senha de administrador na instalação do Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
exl-id: b55ff9d5-8139-4ecf-ba09-5cf88207c5c4
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: b1210526-416b-4ef6-bcc0-1692e99f30e9
    internal-label: Administration and security
subfeature_v2:
  - id: c35bc059-fd80-4a01-91a6-e48da3c76758
    internal-label: Security practices
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%
---
# Configurar a senha do administrador na instalação{#configure-the-admin-password-on-installation}

## Visão geral {#overview}

Desde a versão 6.3, o Adobe Experience Manager (AEM) permite que a senha do administrador seja definida usando a linha de comando ao instalar uma nova instância.

Com versões anteriores do AEM, a senha da conta de administrador, juntamente com a senha de vários outros consoles, tinham que ser alteradas após a instalação.

Esse recurso adiciona a facilidade de definir uma nova senha de administrador para o repositório e o Mecanismo Servlet durante a instalação de uma instância do AEM, eliminando assim a necessidade de fazer isso manualmente posteriormente.

>[!CAUTION]
>
>O recurso não abrange o Felix Console, para o qual a senha deve ser alterada manualmente. Para obter mais informações, consulte a [seção Lista de Verificação de Segurança](/help/sites-administering/security-checklist.md#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts) relevante.

## Como Usá-Lo? {#how-do-i-use-it}

Esse recurso será acionado automaticamente se você optar por instalar o AEM por meio da linha de comando, em vez de clicar duas vezes no JAR em um explorador de sistema de arquivos.

A sintaxe geral para executar uma instância do AEM a partir da linha de comando é:

```shell
java -jar aem6.3.jar
```

Depois de executar a instância na linha de comando, você verá a opção de alterar a senha do administrador durante o processo de instalação:

![chlimage_1-116](assets/chlimage_1-116a.png)

>[!NOTE]
>
>O prompt para alterar a senha do administrador é exibido apenas durante a instalação de uma nova instância do AEM.

## Uso do Sinalizador -nointerativo {#using-the-nointeractive-flag}

Você também pode optar por especificar a senha a partir de um arquivo de propriedades. Isso é feito usando o sinalizador `-nointeractive` combinado com a propriedade do sistema `-Dadmin.password.file`.

Veja um exemplo abaixo:

```shell
java -Dadmin.password.file =/path/to/passwordfile.properties -jar aem6.3.jar -nointeractive
```

A senha dentro do arquivo `passwordfile.properties` deve ter o formato abaixo:

```xml
admin.password = 12345678
```

>[!NOTE]
>
>Se você simplesmente usar o parâmetro `-nointeractive` sem a propriedade do sistema `-Dadmin.password.file`, o AEM usará a senha de administrador padrão sem solicitar que você a altere, essencialmente replicando o comportamento de versões anteriores. Esse modo não interativo pode ser usado para instalações automatizadas usando a linha de comando em um script de instalação.
