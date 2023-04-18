---
title: Selecionar a interface do usuário no AEM
description: Configure qual interface você usa para trabalhar no AEM.
uuid: ab127f2f-2f8a-4398-90dd-c5d48eed9e53
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: e418d330-f234-411d-8cad-3fd9906dcbee
docset: aem65
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
source-git-commit: e1a0b114ce16d0e7f6a464e9d30b8f111297bcc6
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 1%

---

# Selecionar sua interface do usuário{#selecting-your-ui}

Embora a interface habilitada para toque seja agora a interface padrão e a paridade de recursos tenha sido quase alcançada com a administração e edição de sites, pode haver momentos em que o usuário deseja alternar para a [interface clássica](/help/sites-classic-ui-authoring/classicui.md). Há várias opções para fazer isso.

>[!NOTE]
>
>Para obter detalhes sobre o status da paridade de recursos com a interface clássica, consulte o [Paridade de recursos da interface de toque](/help/release-notes/touch-ui-features-status.md) documento.

Há vários locais em que você pode definir qual interface do usuário deve ser usada:

* [Configuração da interface de usuário padrão para a sua instância](#configuring-the-default-ui-for-your-instance)
Isso definirá a interface padrão a ser exibida no logon do usuário, embora o usuário possa substituí-la e selecionar uma interface diferente para sua conta ou sessão atual.

* [Configuração da criação da interface clássica para sua conta](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Isso definirá a interface de usuário a ser usada como padrão ao editar páginas, embora o usuário possa substituí-la e selecionar uma interface de usuário diferente para sua conta ou sessão atual.

* [Alternar para a interface clássica para a sessão atual](#switching-to-classic-ui-for-the-current-session)
Isso muda para a interface clássica na sessão atual.

* No caso de [criação de página o sistema faz certas substituições em relação à interface do usuário](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Várias opções para alternar para a interface do usuário clássica não estão disponíveis imediatamente, elas devem ser configuradas especificamente para sua instância.
>
>Consulte [Ativar o acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

>[!NOTE]
>
>As instâncias atualizadas de uma versão anterior manterão a interface clássica para a criação de página.
>
>Após a atualização, a criação de página não será alternada automaticamente para a interface habilitada para toque, mas você pode configurá-la usando a variável [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de Modo de Interface do Usuário de Criação de WCM** ( `AuthoringUIMode` serviço). Consulte [Substituições da interface do usuário para o Editor](#ui-overrides-for-the-editor).

## Configuração da interface de usuário padrão para sua instância {#configuring-the-default-ui-for-your-instance}

Um administrador do sistema pode configurar a interface do usuário vista na inicialização e logon usando [Mapeamento de raiz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Isso pode ser substituído pelos padrões do usuário ou pelas configurações da sessão.

## Configuração da criação da interface clássica para sua conta {#setting-classic-ui-authoring-for-your-account}

Cada usuário pode acessar seu [preferências do usuário](/help/sites-authoring/user-properties.md#userpreferences) para definir se deseja usar a interface clássica para criação de página (em vez da interface padrão).

Isso pode ser substituído pelas configurações da sessão.

## Alternar para a interface clássica para a sessão atual {#switching-to-classic-ui-for-the-current-session}

Ao usar a interface habilitada para toque, os usuários de desktop podem querer reverter para a interface clássica (somente desktop). Há vários métodos para alternar para a interface clássica na sessão atual:

* **Links de navegação**

   >[!CAUTION]
   >
   >Essa opção para alternar para a interface clássica não está disponível imediatamente, ela deve ser configurada especificamente para sua instância.
   >
   >
   >Consulte [Ativar o acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

   Se isso estiver ativado, sempre que você passar o mouse sobre um console aplicável, um ícone será exibido (símbolo de um monitor), tocar/clicar nele abrirá o local apropriado na interface clássica.

   Por exemplo, os links de **Sites** para **siteadmin**:

   ![syui-01](assets/syui-01.png)

* **URL**

   A interface clássica pode ser acessada usando o URL da tela de boas-vindas em `welcome.html`. Por exemplo:

   `https://localhost:4502/welcome.html`

   >[!NOTE]
   >
   >A interface habilitada para toque pode ser acessada via `sites.html`. Por exemplo:
   >
   >
   >`https://localhost:4502/sites.html`

### Alternar para a interface clássica ao editar uma página {#switching-to-classic-ui-when-editing-a-page}

>[!CAUTION]
>
>Essa opção para alternar para a interface clássica não está disponível imediatamente, ela deve ser configurada especificamente para sua instância.
>
>Consulte [Ativar o acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

Se estiver ativado, **Abra a interface clássica** está disponível no **Informações da página** caixa de diálogo:

![syui-02](assets/syui-02.png)

### Substituições da interface do usuário para o Editor {#ui-overrides-for-the-editor}

As configurações definidas por um usuário ou administrador do sistema podem ser substituídas pelo sistema no caso de criação de página.

* Ao criar páginas:

   * O uso do editor clássico é forçado ao acessar a página usando `cf#` no URL. Por exemplo:
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * O uso do editor habilitado para toque é forçado ao usar `/editor.html` no URL ou ao usar um dispositivo de toque. Por exemplo:
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Qualquer ação forçada é temporária e válida somente para a sessão do navegador

   * Um conjunto de cookies será definido dependendo se ativado para toque ( `editor.html`) ou clássica ( `cf#`) é usada.

* Ao abrir páginas por meio de `siteadmin`, serão efetuados controlos da existência de:

   * O cookie
   * Uma preferência de usuário
   * Se nenhum dos dois existir, o padrão será as definições feitas na variável [Configuração do OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de Modo de Interface do Usuário de Criação de WCM** ( `AuthoringUIMode` serviço).

>[!NOTE]
>
>If [um usuário já definiu uma preferência para a criação de página](#settingthedefaultauthoringuiforyouraccount), que não será substituído pela alteração da propriedade OSGi.

>[!CAUTION]
>
>Devido ao uso de cookies, conforme já descrito, nenhuma das ações abaixo é recomendável:
>
>* Editar manualmente o URL - Um URL não padrão pode resultar em uma situação desconhecida e em falta de funcionalidade.
>* Ter ambos os editores abertos ao mesmo tempo - Por exemplo, em janelas separadas.

