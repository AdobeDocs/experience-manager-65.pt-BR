---
title: Configuração do SSL no Windows Vista
description: Saiba como configurar o SSL no Windows Vista. Use e execute a Java Keytool para gerar o certificado SSL com chaves RSA para autenticação.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_ssl
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 36c4300d-7a44-41f4-b294-06f32bb01686
solution: Experience Manager, Experience Manager Forms
feature: Document Security
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '173'
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

   `keytool -genkey -keyalg RSA -dname "CN=`*Nome do Host* `, OU=`*Nome do Grupo* `, O=`*Nome da Empresa* `,L=`*Nome da Cidade* `, S=`*Estado* `, C=`*Código do País* `" -alias`*&quot;Certificado LC&quot;* `-keypass` `key`*_* *senha* `-keystore`*keystorename* `.keystore`

   >[!NOTE]
   >
   >Substitua *`[JAVA_HOME]`pelo diretório onde o JDK está instalado e o texto em itálico por valores que correspondam ao seu ambiente.*

1. Digite `changeit` como senha. Essa senha é o padrão para uma instalação do Java e o administrador do sistema pode tê-la alterado.
