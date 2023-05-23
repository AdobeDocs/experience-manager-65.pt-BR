---
title: Seleção da interface do usuário no AEM
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

# Seleção da interface{#selecting-your-ui}

Embora a interface habilitada para toque agora seja a interface padrão e a paridade de recursos tenha sido quase atingida com a administração e a edição de sites, pode haver momentos em que o usuário deseje mudar para a [IU clássica](/help/sites-classic-ui-authoring/classicui.md). Há várias opções para fazer isso.

>[!NOTE]
>
>Para obter detalhes sobre o status da paridade de recursos com a interface clássica, consulte o [Paridade de recursos da interface para toque](/help/release-notes/touch-ui-features-status.md) documento.

Há vários locais em que você pode definir qual interface do usuário será usada:

* [Configuração da interface padrão para sua instância](#configuring-the-default-ui-for-your-instance)
Isso definirá a interface padrão para ser mostrada no logon do usuário, embora o usuário possa substituir isso e selecionar uma interface diferente para sua conta ou sessão atual.

* [Configuração da criação da interface clássica para sua conta](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Isso definirá a interface que será usada como padrão ao editar páginas, embora o usuário possa substituí-la e selecionar uma interface diferente para sua conta ou sessão atual.

* [Alternar para a interface clássica da sessão atual](#switching-to-classic-ui-for-the-current-session)
Isso alterna para a interface clássica da sessão atual.

* No caso de [a página que cria o sistema faz determinadas substituições em relação à interface](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Várias opções para alternar para a interface clássica não estão imediatamente disponíveis para uso imediato. Elas devem ser configuradas especificamente para sua instância.
>
>Consulte [Ativação do acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

>[!NOTE]
>
>As instâncias atualizadas de uma versão anterior manterão a interface clássica para a criação de páginas.
>
>Após a atualização, a criação de página não será alternada automaticamente para a interface habilitada para toque, mas você poderá configurá-la usando o [Configuração OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de modo de interface do usuário de criação do WCM** ( `AuthoringUIMode` serviço). Consulte [Substituições da interface do usuário para o editor](#ui-overrides-for-the-editor).

## Configuração da interface do usuário padrão para sua instância {#configuring-the-default-ui-for-your-instance}

Um administrador do sistema pode configurar a interface do usuário exibida na inicialização e no logon usando [Mapeamento de raiz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Isso pode ser substituído pelos padrões do usuário ou pelas configurações da sessão.

## Configuração da criação da interface clássica para sua conta {#setting-classic-ui-authoring-for-your-account}

Cada usuário pode acessar sua [preferências do usuário](/help/sites-authoring/user-properties.md#userpreferences) para definir se deseja usar a interface clássica para a criação de página (em vez da interface padrão).

Isso pode ser substituído pelas configurações da sessão.

## Alternar para a interface clássica da sessão atual {#switching-to-classic-ui-for-the-current-session}

Ao usar a interface habilitada para toque, os usuários de desktop podem querer reverter para a interface clássica (somente desktop). Há vários métodos para alternar para a interface clássica da sessão atual:

* **Links de navegação**

   >[!CAUTION]
   >
   >Essa opção para alternar para a interface clássica não está imediatamente disponível para uso imediato. Ela deve ser configurada especificamente para sua instância.
   >
   >
   >Consulte [Ativação do acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

   Se estiver ativado, sempre que você passar o mouse sobre um console aplicável, um ícone será exibido (símbolo de um monitor). Tocar/clicar nele abrirá o local apropriado na interface clássica.

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
>Essa opção para alternar para a interface clássica não está imediatamente disponível para uso imediato. Ela deve ser configurada especificamente para sua instância.
>
>Consulte [Ativação do acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

Se ativado, **Abrir a interface clássica** está disponível no **Informações da página** diálogo:

![syui-02](assets/syui-02.png)

### Substituições da interface do usuário para o editor {#ui-overrides-for-the-editor}

As configurações definidas por um usuário ou administrador do sistema podem ser substituídas pelo sistema no caso de criação de página.

* Ao criar páginas:

   * O uso do editor clássico é forçado ao acessar a página usando `cf#` no URL. Por exemplo:
      `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * O uso do editor habilitado para toque é forçado ao usar `/editor.html` no URL ou ao usar um dispositivo de toque. Por exemplo:
      `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Qualquer imposição é temporária e válida somente para a sessão do navegador

   * Um conjunto de cookies será definido dependendo se a opção de toque estiver ativada ( `editor.html`) ou clássico ( `cf#`) é usada.

* Ao abrir páginas por meio de `siteadmin`, será verificada a existência de:

   * O cookie
   * Uma preferência do usuário
   * Se não houver nenhuma, o padrão será as definições definidas na variável [Configuração OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de modo de interface do usuário de criação do WCM** ( `AuthoringUIMode` serviço).

>[!NOTE]
>
>Se [um usuário já definiu uma preferência para a criação de página](#settingthedefaultauthoringuiforyouraccount), que não será substituído pela alteração da propriedade OSGi.

>[!CAUTION]
>
>Devido ao uso de cookies, conforme já descrito, não é recomendável:
>
>* Editar manualmente o URL - Um URL não padrão pode resultar em uma situação desconhecida e na falta de funcionalidade.
>* Ter ambos os editores abertos ao mesmo tempo - por exemplo, em janelas separadas.

