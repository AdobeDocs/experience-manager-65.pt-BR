---
title: Configuração do SSL no Windows Vista
description: Saiba como configurar o SSL no Windows Vista. Use e execute a Java Keytool para gerar o certificado SSL com chaves RSA para autenticação.
uuid: 20bfcefb-ec84-4c55-bceb-6af106d883d7
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 667645a0-53d0-4f9b-a0ba-cc7e366a23a1
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# Configuração do SSL no Windows Vista {#configuring-ssl-on-windows-vista}

Para configurar o SSL no Windows Vista™, você precisa de um certificado SSL com chaves RSA para autenticação. Você pode usar a ferramenta Chave Java para criar o certificado.

>[!NOTE]
>
>O Windows Vista não funcionará com chaves DSA.

Você pode executar a ferramenta de chaves usando um único comando que inclui todas as informações necessárias para criar o certificado e o keystore.

**Criar um certificado SSL**

1. Em um prompt de comando, navegue até *`[JAVA HOME]`*/bin e digite o seguinte comando para criar o certificado e o keystore:

   `keytool -genkey -keyalg RSA -dname "CN=`*Nome do host* `, OU=`*Nome do grupo* `, O=`*Nome da empresa* `,L=`*Nome da cidade* `, S=`*Estado* `, C=`*Código do país* `" -alias`*&quot;LC Cert&quot;* `-keypass` `key`*_* *senha* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Substituir *`[JAVA_HOME]`com o diretório onde o JDK está instalado e substitua o texto em itálico por valores que correspondam ao seu ambiente.*

1. Tipo `changeit` como a senha. Essa senha é o padrão para uma instalação do Java e o administrador do sistema pode tê-la alterado.
