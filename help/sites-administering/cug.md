---
title: Criando um grupo de usuários fechado
seo-title: Criando um grupo de usuários fechado
description: Saiba como criar um Grupo de usuários fechado.
seo-description: Saiba como criar um Grupo de usuários fechado.
uuid: dc3c7dbd-2e86-43f9-9377-3b75053203b3
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: 6ae57874-a9a1-4208-9001-7f44a1f57cbe
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
translation-type: tm+mt
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# Criando um Grupo de Usuários Fechado{#creating-a-closed-user-group}

Grupos de usuários fechados (CUGs) são usados para limitar o acesso a páginas específicas que residem em um site da Internet publicado. Essas páginas exigem que os membros atribuídos façam logon e forneçam credenciais de segurança.

Para configurar essa área no seu site, você:

* [crie o grupo de usuários fechado e atribua membros](#creating-the-user-group-to-be-used).

* [aplique este grupo às ](#applying-your-closed-user-group-to-content-pages) páginas necessárias e selecione (ou crie) a página de logon para usar pelos membros do CUG; também especificado ao aplicar um CUG a uma página de conteúdo.

* [crie um link, de algum formulário, para pelo menos uma página dentro da área](#linking-to-the-realm) protegida; caso contrário, ele não estará visível.
* [configure o ](#configure-dispatcher-for-cugs) Dispatcherif em uso.

>[!CAUTION]
>
>Os grupos de usuários fechados (CUGs) devem sempre ser criados tendo em mente o desempenho.
>
>Embora o número de usuários e grupos em um CUG não seja limitado, um alto número de CUGs em uma página pode retardar o desempenho de renderização.
>
>O impacto dos CUGs deve ser sempre considerado ao realizar testes de desempenho.

## Criando O Grupo De Usuários A Ser Usado {#creating-the-user-group-to-be-used}

Para criar um grupo de usuários fechado:

1. Vá para **Tools - Security** a partir da tela inicial AEM.

   >[!NOTE]
   >
   >Consulte [Gerenciar usuários e grupos](/help/sites-administering/security.md#managing-users-and-groups) para obter informações completas sobre como criar e configurar usuários e grupos.

1. Selecione o cartão **Grupos** na próxima tela.

   ![captura de tela_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Pressione o botão **Create** no canto superior direito para criar um novo grupo.
1. Dê um nome ao novo grupo; por exemplo, `cug_access`.

   ![captura de tela_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Vá para a guia **Members** e atribua os usuários necessários a esse grupo.

   ![captura de tela_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Ative quaisquer usuários que você tenha atribuído ao CUG; nesse caso, todos os membros de `cug_access`.
1. Ative o grupo de usuários fechado para que ele esteja disponível no ambiente de publicação; neste exemplo, `cug_access`.

## Aplicando seu grupo de usuários fechado às páginas de conteúdo {#applying-your-closed-user-group-to-content-pages}

Para aplicar o CUG a uma página:

1. Navegue até a página raiz da seção restrita que deseja atribuir ao CUG.
1. Selecione a página clicando em sua miniatura e depois em **Propriedades** no painel superior.

   ![captura de tela_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. Na janela a seguir, vá para a guia **Advanced**.
1. Role para baixo e ative a caixa de seleção na seção **Requisito de autenticação**.

1. Adicione o caminho de configuração abaixo e pressione Salvar.
1. Em seguida, vá para a guia **Permissions** e pressione o botão **Edit Closed User Group**.

   ![captura de tela_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[OBSERVAÇÃO!]
   >
   > Observe que os CUGs na guia Permissões não podem ser implantados em Live Copies de Blueprints. Planeje isso ao configurar a Live Copy.
   >
   > Para obter mais informações, consulte [esta página](closed-user-groups.md#aem-livecopy).

1. Procure e adicione seu CUG na janela a seguir - neste caso, adicione o grupo chamado **cug_access**. Finalmente, pressione **Save**.
1. Clique em **Ativado** para definir que esta página (e quaisquer páginas secundárias) pertença a um CUG.
1. Especifique a **Página de Logon** que os membros do grupo usarão; por exemplo:

   `/content/geometrixx/en/toolbar/login.html`

   Isso é opcional, se deixado em branco, a página de logon padrão será usada.

1. Adicione o **Grupos aceitos**. Use + para adicionar grupos ou - para remover. Somente os membros desses grupos poderão fazer logon e acessar as páginas.
1. Atribua um **Realm** (um nome para os grupos de páginas), se necessário. Deixe em branco para utilizar o título da página.
1. Clique em **OK** para salvar a especificação.

Consulte [Identity Management](/help/sites-administering/identity-management.md) para obter informações sobre perfis no ambiente de publicação e fornecer formulários para fazer logon e sair.

## Vincular Ao Realm {#linking-to-the-realm}

Como o target de qualquer link para o Realm CUG não é visível para o usuário anônimo, o linkchecker removerá esses links.

Para evitar isso, é aconselhável criar páginas de redirecionamento não protegidas que apontem para páginas dentro do Realm CUG. As entradas de navegação são renderizadas sem causar problemas ao linkchecker. Somente quando realmente acessar a página de redirecionamento o usuário será redirecionado dentro do território CUG - depois de fornecer com sucesso suas credenciais de logon.

## Configurar o Dispatcher para CUGs {#configure-dispatcher-for-cugs}

Se você estiver usando o Dispatcher, precisará definir um farm do Dispatcher com as seguintes propriedades:

* [virtualhosts](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#identifying-virtual-hosts-virtualhosts): Corresponde ao caminho para as páginas às quais o CUG se aplica.
* \sessionmanagement: veja abaixo.
* [cache](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#configuring-the-dispatcher-cache-cache): Um diretório de cache dedicado aos arquivos aos quais o CUG se aplica.

### Configurando o Gerenciamento de Sessão do Dispatcher para CUGs {#configuring-dispatcher-session-management-for-cugs}

Configure [o gerenciamento de sessão no arquivo dispatcher.any](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) para o CUG. O manipulador de autenticação usado quando o acesso é solicitado para páginas CUG determina como configurar o gerenciamento de sessões.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Quando um farm do Dispatcher tem o gerenciamento de sessão ativado, todas as páginas que os identificadores de farm não são armazenadas em cache. Para armazenar páginas em cache fora do CUG, crie um segundo farm no dispatcher.any
>que manipula as páginas que não são CUG.

1. Configure [/sessionmanagement](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#enabling-secure-sessions-sessionmanagement) definindo `/directory`; por exemplo:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Defina [/allowAuthorized](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-configuration.html#caching-when-authentication-is-used) para `0`.
