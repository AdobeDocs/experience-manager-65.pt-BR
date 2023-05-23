---
title: Etapas adicionais para obter e-mail com anexo
description: Etapas adicionais para obter e-mail com anexo
exl-id: 0d0713fb-d95a-4a95-91ef-9cdaea30e343
source-git-commit: 2e9b9c40f54aa54a946e4320341ed4a760c56fd1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Não é possível obter email com anexos para AEM Forms em plataformas JEE{#unable-to-get-email-with-attachments}

O problema se aplica à seguinte versão:
* Experience Manager 6.5 Forms

## Problema {#issue}

O usuário não pode executar operações como Enviar PDF por email ou Incluir anexos com a configuração de envio.

## Solução {#solution}

1. Baixar jar como [java.mail-1.0.jar](/help/forms/using/java.mail-1.0.jar) e descompacte o arquivo jar baixado para obter o arquivo manifest.

1. Usar o arquivo de manifesto de `java.mail-1.0.jar` recuperado da Etapa 1 para criar um novo arquivo jar personalizado, diga como `java.mail-1.5.jar`.

1. Abra o arquivo de manifesto e substitua todas as ocorrências de `1.5.0` com `1.5.6` e `Bundle-Version: 1.0` com `Bundle-Version:1.5`

1. Criar um novo jar personalizado (`java.mail-1.5.jar`) usando o seguinte comando em `C:\Adobe\Adobe_Experience_Manager_Forms\java\jdk\bin` pasta como:
   `jar -cfm java.mail-1.5.jar manifest.mf`

   No comando acima, *manifest.mf* é o nome do arquivo de manifesto e *java.mail-1.5.jar* é o nome do arquivo que seria criado após a execução do comando acima.

1. Baixar [javax.mail-1.5.6.redhat-1.jar](https://mvnrepository.com/artifact/com.sun.mail/javax.mail/1.5.6.redhat-1).

1. Navegue até `http://<server name>:<port>/lc/system/console/bundles`e exclua o pacote com um nome como `JavaMail API (com.sun.mail.javax.mail) version 1.6.2`.

1. Instalar `java.mail-1.5.jar` obtido da etapa 3.  Esta etapa reinicia as propriedades sling da implantação do JEE. Aguardar os pacotes instalados em `http://<server name>:<port>/lc/system/console/bundles` para mostrar o Status como **Ativo**.

   >Observação: caso o status ainda seja **InAtive**, reiniciar   **JBoss** do **Console de serviços**.


1. Instalar `javax.mail-1.5.6.redhat-1.jar`arquivo baixado usando a etapa 5.

1. Parar **JBoss** do **Console de serviços** e anexe as seguintes propriedades a **Sling.properties** arquivo:
   * `org.osgi.framework.system.packages.extra=javax.activation; version\=1.2.0`
   * `sling.bootdelegation.activation=javax.activation.*`

1. Restart **JBoss**.
