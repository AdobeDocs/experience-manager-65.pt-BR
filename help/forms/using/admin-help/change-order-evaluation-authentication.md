---
title: Alterar a ordem de avaliação para autenticação
description: Você pode alterar a ordem em que os formulários AEM avaliam vários provedores de autenticação.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_user_management
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 7e29c9d4-fb82-4308-aac7-0f5cb1f4aef2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Alterar a ordem de avaliação para autenticação {#change-the-order-of-evaluation-for-authentication}

Se você configurou vários provedores de autenticação, é possível alterar a ordem em que os formulários AEM os avaliam para autenticação. A ordem dos provedores de autenticação listados no arquivo config.xml determina a ordem de avaliação para autenticação.

1. No console de administração, clique em Configurações > Gerenciamento de usuários > Configuração > Importar e exportar arquivos de configuração.
1. Para exportar a definição da configuração atual para um arquivo, clique em Exportar e salve o arquivo de configuração em outro local.
1. Localize o seguinte nó no arquivo:

   ```xml
    <node name="AuthSchemes">
        <map />
            <node name="CertificateAuth">
                <map>
                    <entry key="order" value="3" />
                    <entry key="name" value="edc.server.auth.scheme.certificate" />
                </map>
        </node>
        <node name="Kerberos">
            <map>
                <entry key="kerberosSPN" value="defaultSPN" />
                <entry key="order" value="1" />
                <entry key="name" value="edc.server.auth.scheme.kerberos" />
            </map>
    </node>
   ```

   Entrada `<entry key="order" value="3" />`, edite o valor de cada nó para definir a ordem da avaliação de autenticação.

1. Para importar o arquivo atualizado, no Gerenciamento de usuários, clique em Configuração > Importar e exportar arquivos de configuração.
1. Clique em Procurar para localizar o arquivo, clique em Importar e em OK.
