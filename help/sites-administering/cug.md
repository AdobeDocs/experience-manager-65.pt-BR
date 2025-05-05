---
title: Criação de um grupo fechado de usuários
description: Saiba como criar um Grupo de usuários fechado.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
docset: aem65
exl-id: 9efba91d-45e8-42e1-9db6-490d21bf7412
solution: Experience Manager, Experience Manager Sites
feature: Security
role: Admin
source-git-commit: 6f3c4f4aa4183552492c6ce5039816896bd67495
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 1%

---

# Criação de um grupo fechado de usuários{#creating-a-closed-user-group}

Grupos de usuários fechados (CUGs) são usados para limitar o acesso a páginas específicas que residem em um site da Internet publicado. Essas páginas exigem que os membros atribuídos façam logon e forneçam credenciais de segurança.

Para configurar essa área no seu site, você:

* [criar o grupo de usuários realmente fechado e atribuir membros](#creating-the-user-group-to-be-used).

* [aplique este grupo às páginas necessárias](#applying-your-closed-user-group-to-content-pages) e selecione (ou crie) a página de logon a ser usada pelos membros do CUG; também especificada ao aplicar um CUG a uma página de conteúdo.

* [criar um link, de algum formulário, para pelo menos uma página dentro da área protegida](#linking-to-the-cug-pages); caso contrário, ele não estará visível.

* [configure o Dispatcher](#configure-dispatcher-for-cugs) se estiver em uso.

>[!CAUTION]
>
>Grupos de usuários fechados (CUGs) devem ser sempre criados tendo o desempenho em mente.
>
>Embora o número de usuários e grupos em um CUG não seja limitado, um alto número de CUGs em uma página pode retardar o desempenho da renderização.
>
>O impacto dos CUGs deve sempre ser considerado ao realizar testes de desempenho.

## Criação Do Grupo De Usuários A Ser Usado {#creating-the-user-group-to-be-used}

Para criar um grupo de usuários fechado:

1. Vá para **Ferramentas - Segurança** na tela inicial do AEM.

   >[!NOTE]
   >
   >Consulte [Gerenciando Usuários e Grupos](/help/sites-administering/security.md#managing-users-and-groups) para obter informações completas sobre como criar e configurar usuários e grupos.

1. Selecione o cartão **Grupos** na próxima tela.

   ![captura_de_tela_2018-10-30at145502](assets/screenshot_2018-10-30at145502.png)

1. Pressione o botão **Criar** no canto superior direito para criar um grupo.
1. Dê um nome ao novo grupo; por exemplo, `cug_access`.

   ![captura_de_tela_2018-10-30at151459](assets/screenshot_2018-10-30at151459.png)

1. Vá para a guia **Membros** e atribua os usuários necessários a este grupo.

   ![captura_de_tela_2018-10-30at151808](assets/screenshot_2018-10-30at151808.png)

1. Ative todos os usuários que você atribuiu ao seu CUG; neste caso, todos os membros de `cug_access`.
1. Ative o grupo de usuários fechado para que ele fique disponível no ambiente de publicação; neste exemplo, `cug_access`.

## Aplicar O Grupo De Usuários Fechado Às Páginas De Conteúdo {#applying-your-closed-user-group-to-content-pages}

Para aplicar o CUG a uma ou mais páginas:

1. Navegue até a página raiz da seção restrita que você deseja atribuir ao seu CUG.
1. Selecione a página clicando em sua miniatura e selecionando **Propriedades** na barra de ferramentas superior.

   ![captura_de_tela_2018-10-30at162632](assets/screenshot_2018-10-30at162632.png)

1. Na janela a seguir, abra a guia **Avançado**.

1. Role para baixo até a seção **Requisito de autenticação**.

   1. Ative a caixa de seleção **Habilitar**.

   1. Adicione o caminho à sua **Página de Logon**.
Isso é opcional; se deixado em branco, a página de logon padrão será usada.

   ![CUG adicionado](assets/cug-authentication-requirement.png)

1. Em seguida, vá para a guia **Permissões** e selecione **Editar grupo de usuários fechado**.

   ![captura_de_tela_2018-10-30at163003](assets/screenshot_2018-10-30at163003.png)

   >[!NOTE]
   >
   >Observe que os CUGs na guia Permissões não podem ser implantados em Live Copies de blueprints. Planeje isso ao configurar a Live Copy.
   >
   >Para obter mais informações, consulte [Grupos de usuários fechados no AEM - Livecopy](closed-user-groups.md#aem-livecopy).

1. A caixa de diálogo **Editar Grupo de Usuários Fechado** é aberta. Aqui você pode pesquisar e selecionar seu CUG, e confirmar a seleção do grupo com **Salvar**.

   O grupo será adicionado à lista; por exemplo, o grupo **cug_access**.

   ![CUG adicionado](assets/cug-added.png)

1. Confirme as alterações com **Salvar e fechar**.

>[!NOTE]
>
>Consulte [Identity Management](/help/sites-administering/identity-management.md) para obter informações sobre perfis no ambiente de publicação e fornecer formulários para entrar e sair.

## Vinculação às páginas CUG {#linking-to-the-cug-pages}

Como o destino de qualquer link para as páginas CUG não está visível para o usuário anônimo, o linkchecker removerá esses links.

Para evitar isso, é aconselhável criar páginas de redirecionamento não protegidas que apontem para páginas dentro da área CUG. As entradas de navegação são renderizadas sem causar problemas ao linkchecker. Somente ao acessar a página de redirecionamento o usuário será redirecionado dentro da área CUG - após fornecer suas credenciais de logon com êxito.

## Configurar o Dispatcher para CUGs {#configure-dispatcher-for-cugs}

Se estiver usando o Dispatcher, você precisará definir um farm do Dispatcher com as seguintes propriedades:

* [virtualhosts](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#identifying-virtual-hosts-virtualhosts): corresponde ao caminho para as páginas às quais o CUG se aplica.
* \sessionmanagement: veja abaixo.
* [cache](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#configuring-the-dispatcher-cache-cache): um diretório de cache dedicado aos arquivos aos quais o CUG se aplica.

### Configuração do Gerenciamento de sessão do Dispatcher para CUGs {#configuring-dispatcher-session-management-for-cugs}

Configure o [gerenciamento de sessão no arquivo dispatcher.any](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#enabling-secure-sessions-sessionmanagement) para o CUG. O manipulador de autenticação usado quando o acesso é solicitado para páginas CUG determina como você configura o gerenciamento de sessão.

```xml
/sessionmanagement
    ...
    /header "Cookie:login-token"
    ...
```

>[!NOTE]
>
>Quando um farm do Dispatcher tem o gerenciamento de sessão ativado, todas as páginas manipuladas pelo farm não são armazenadas em cache. Para armazenar em cache páginas que estejam fora do CUG, crie um segundo farm no dispatcher.any
>que manipula as páginas que não são CUG.

1. Configure [/sessionmanagement](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#enabling-secure-sessions-sessionmanagement) definindo `/directory`; por exemplo:

   ```xml
   /sessionmanagement
     {
     /directory "/usr/local/apache/.sessions"
     ...
     }
   ```

1. Definir [/allowAuthorized](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html?lang=pt-BR#caching-when-authentication-is-used) para `0`.
