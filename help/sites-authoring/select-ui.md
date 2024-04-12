---
title: Seleção da interface do usuário no AEM
description: Configure qual interface você usa para trabalhar no Adobe Experience Manager 6.5.
exl-id: 01cab3c3-4c0d-44d9-b47c-034de9a08cb1
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 1%

---

# Seleção da interface{#selecting-your-ui}

A interface habilitada para toque do Adobe Experience Manager (AEM) agora é a interface padrão e a paridade de recursos foi quase atingida com a administração e a edição de sites. No entanto, pode haver momentos em que o usuário deseje alternar para a variável [IU clássica](/help/sites-classic-ui-authoring/classicui.md). Há várias opções para fazer isso.

>[!NOTE]
>
>Para obter detalhes sobre o status da paridade de recursos com a interface clássica, consulte o [Paridade de recursos da interface para toque](/help/release-notes/touch-ui-features-status.md) documento.

Há vários locais em que você pode definir qual interface do usuário será usada:

* [Configuração da interface padrão para sua instância](#configuring-the-default-ui-for-your-instance)
Define a interface padrão para ser exibida no logon do usuário. O usuário pode substituir isso e selecionar uma interface diferente para sua conta ou sessão atual.

* [Configuração da criação da interface clássica para sua conta](/help/sites-authoring/select-ui.md#setting-classic-ui-authoring-for-your-account)
Isso define a interface como o padrão ao editar páginas, embora o usuário possa substituí-la e selecionar uma interface diferente para sua conta ou sessão atual.

* [Alternar para a interface clássica da sessão atual](#switching-to-classic-ui-for-the-current-session)
Alterna para a interface clássica da sessão atual.

* No caso de [criação de página, o sistema faz determinadas substituições em relação à interface](#ui-overrides-for-the-editor).

>[!CAUTION]
>
>Várias opções para alternar para a interface clássica não estão imediatamente disponíveis para uso imediato. Elas devem ser configuradas para sua instância.
>
>Consulte [Ativação do acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

>[!NOTE]
>
>As instâncias atualizadas de uma versão anterior retêm a interface clássica para a criação de página.
>
>Após a atualização, a criação de página não muda automaticamente para a interface habilitada para toque, mas você pode configurar isso usando o [Configuração OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de modo de interface do usuário de criação do WCM** ( `AuthoringUIMode` serviço). Consulte [Substituições da interface do usuário para o editor](#ui-overrides-for-the-editor).

## Configuração da interface do usuário padrão para sua instância {#configuring-the-default-ui-for-your-instance}

Um administrador do sistema pode configurar a interface do usuário exibida na inicialização e no logon usando [Mapeamento de raiz](/help/sites-deploying/osgi-configuration-settings.md#daycqrootmapping).

Isso pode ser substituído pelos padrões do usuário ou pelas configurações da sessão.

## Configuração da criação da interface clássica para sua conta {#setting-classic-ui-authoring-for-your-account}

Cada usuário pode acessar o seu próprio [preferências do usuário](/help/sites-authoring/user-properties.md#userpreferences) para definir se eles desejam usar a interface clássica para criação de página, em vez da interface padrão.

Isso pode ser substituído pelas configurações da sessão.

## Alternar para a interface clássica da sessão atual {#switching-to-classic-ui-for-the-current-session}

Ao usar a interface habilitada para toque, os usuários de desktop podem querer reverter para a interface clássica (somente desktop). Há vários métodos para alternar para a interface clássica da sessão atual:

* **Links de navegação**

  >[!CAUTION]
  >
  >Essa opção para alternar para a interface clássica não está imediatamente disponível para uso imediato. Ela deve ser configurada para sua instância.
  >
  >
  >Consulte [Ativação do acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

  Se estiver ativado, sempre que você passar o mouse sobre um console aplicável, um ícone será exibido (um símbolo de monitor). Tocar/clicar nesse ícone abre o local apropriado na interface clássica.

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
>Essa opção para alternar para a interface clássica não está imediatamente disponível para uso imediato. Ela deve ser configurada para sua instância.
>
>Consulte [Ativação do acesso à interface clássica](/help/sites-administering/enable-classic-ui.md) para obter mais informações.

Se ativado, **Abrir a interface clássica** está disponível no **Informações da página** diálogo:

![syui-02](assets/syui-02.png)

### Substituições da interface do usuário para o editor {#ui-overrides-for-the-editor}

As configurações definidas por um usuário ou administrador do sistema podem ser substituídas pelo sistema se houver criação de página.

* Ao criar páginas:

   * O uso do editor clássico é forçado ao acessar a página usando `cf#` no URL. Por exemplo:
     `https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

   * O uso do editor habilitado para toque é forçado ao usar `/editor.html` no URL ou ao usar um dispositivo de toque. Por exemplo:
     `https://localhost:4502/editor.html/content/geometrixx/en/products/triangle.html`

* Qualquer imposição é temporária e válida somente para a sessão do navegador

   * A definição de um conjunto de cookies depende da ativação ou não de toque ( `editor.html`) ou clássico ( `cf#`) é usada.

* Ao abrir páginas por meio de `siteadmin`, são efetuados controlos para verificar a existência do seguinte:

   * O cookie
   * Uma preferência do usuário
   * Se nenhum existir, o padrão será as definições definidas na variável [Configuração OSGi](/help/sites-deploying/configuring-osgi.md) do **Serviço de modo de interface do usuário de criação do WCM** ( `AuthoringUIMode` serviço).

>[!NOTE]
>
>Se [um usuário já definiu uma preferência para a criação de página](#settingthedefaultauthoringuiforyouraccount), que não é substituído pela alteração da propriedade OSGi.

>[!CAUTION]
>
>Devido ao uso de cookies, conforme já descrito, não é recomendável:
>
>* Editar manualmente o URL - Um URL não padrão pode resultar em uma situação desconhecida e na falta de funcionalidade.
>* Ter ambos os editores abertos ao mesmo tempo - por exemplo, em janelas separadas.
