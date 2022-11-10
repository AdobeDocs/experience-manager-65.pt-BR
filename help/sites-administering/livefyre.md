---
title: Integração com o Livefyre
seo-title: Integrating with Livefyre
description: Saiba como integrar os recursos de curadoria líderes do setor do Livefyre à sua instância do AEM 6.5, permitindo que você publique conteúdo valioso gerado pelo usuário (UGC) nas redes sociais em seu site em minutos.
seo-description: Learn how to integrate and use Livefyre with AEM 6.5.
uuid: c355705d-6e0f-4a33-aa1f-d2d1c818aac0
contentOwner: ind14750
content-type: reference
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/SITES
discoiquuid: bb3fcb53-b8c3-4b1d-9125-4715f34ceb0b
exl-id: 6327b571-4c7f-4a5e-ba93-45d0a064aa1f
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1648'
ht-degree: 5%

---

# Integração com o Livefyre{#integrating-with-livefyre}

Saiba como integrar os recursos de curadoria líderes do setor do Livefyre à sua instância do AEM 6.5, permitindo que você publique conteúdo valioso gerado pelo usuário (UGC) nas redes sociais em seu site em minutos.

## Introdução {#getting-started}

### Instale o Pacote Livefyre para AEM {#install-livefyre-package-for-aem}

O AEM 6.5 vem com o Livefyre feature package 1.2.6 pré-instalado. Este pacote inclui apenas a integração limitada do Livefyre com o AEM Sites e deve ser desinstalado antes de instalar um pacote atualizado. Com o pacote mais recente, você pode experimentar a integração completa do Livefyre com o AEM, incluindo Sites, Ativos e Comércio.

>[!NOTE]
>
>Alguns recursos do pacote AEM-LF dependem do SCF (Social Component Framework). Se você estiver usando o Livefyre feature pack como parte de um site que não é de comunidades, será necessário declarar *cq.social.scf* como uma dependência nas clientlibs do autor do site. Se você estiver usando o pacote de recursos LF como parte de um site de comunidades, essa dependência já deve ser declarada.

1. Na página inicial do AEM, clique no link **Ferramentas** no painel esquerdo.
1. Navegar para **Implantação > Pacotes**.
1. No Gerenciador de pacotes, role até ver o pacote de recursos do Livefyre pré-instalado e clique no título do pacote **cq-social-livefyre-pkg-1.2.6.zip** para expandir as opções.
1. Clique em **Mais > Desinstalar**.

   ![livefyre-aem-uninstall-64](assets/livefyre-aem-uninstall-64.png)

1. Baixe o pacote Livefyre em [Distribuição de software](https://experience.adobe.com/#/downloads/content/software-distribution/br/aem.html).

1. No Gerenciador de pacotes, instale o pacote baixado. Consulte [Como trabalhar com pacotes](/help/sites-administering/package-manager.md) para obter mais informações sobre o uso da Distribuição de software e pacotes no AEM

   ![livefyre-aem4-6-4](assets/livefyre-aem4-6-4.png)

   O pacote Livefyre-AEM agora está instalado. Antes de começar a usar os recursos de integração, você deve configurar o AEM para usar o Livefyre.

   Para obter mais informações e notas de versão sobre pacotes de recursos, consulte [Pacotes de recursos](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/home.html).

### Configure AEM para usar o Livefyre: Criar uma pasta de configuração {#configure-aem-to-use-livefyre-create-a-configuration-folder}

1. Na página inicial do AEM, clique no link **Ferramentas** no painel à esquerda, em seguida, navegue até **Geral > Navegador de configuração**.
   * Consulte a [Navegador de configuração](/help/sites-administering/configurations.md) documentação para obter mais informações.
1. Clique em **Criar** para abrir a caixa de diálogo Criar configuração .
1. Nomeie sua configuração e verifique o **Configurações da nuvem** caixa de seleção.

   Isso criará uma pasta em **Ferramentas > Implantação > Configuração do Livefyre** com o nome fornecido.

   ![livefyre-aem-create-config-folder](assets/livefyre-aem-create-config-folder.png)

### Configure AEM para usar o Livefyre: Criar uma configuração do Livefyre {#configure-aem-to-use-livefyre-create-a-livefyre-configuration}

Configure o AEM para usar as credenciais de licença do Livefyre da organização, permitindo a comunicação entre o Livefyre e o AEM.

1. Na página inicial do AEM, clique no link **Ferramentas** no painel à esquerda, em seguida, navegue até **Implantação > Configuração do Livefyre**.
1. Selecione a pasta de configuração na qual deseja criar uma nova configuração do Livefyre e clique em **Criar**.

   ![create-livefyre-configuration1](assets/create-livefyre-configuration1.png)

   >[!NOTE]
   >
   >As pastas devem ter as Configurações de nuvem ativadas em suas propriedades antes que as configurações do Livefyre possam ser adicionadas a elas. As pastas de configuração são criadas e gerenciadas na variável [Navegador de configuração.](/help/sites-administering/configurations.md)
   >
   >Não é possível criar um nome para uma configuração; ele é referenciado pelo caminho da pasta em que está. Você só pode ter uma configuração por pasta.

1. Selecione o cartão de configuração do Livefyre recém-criado e clique em **Propriedades**.

   ![create-livefyre-configuration2](assets/create-livefyre-configuration2.png)

1. Insira as credenciais do Livefyre da organização e clique em **OK**.

   ![configure-aem2](assets/configure-aem2.png)

   Para acessar essas informações, abra o estúdio do Livefyre e navegue até **Configurações > Configurações de integração > Credenciais**.

   Sua instância do AEM agora está configurada para usar o Livefyre e você pode usar os recursos de integração.

### Personalizar integração de logon único {#customize-single-sign-on-integration}

O pacote Livefyre for AEM inclui uma integração pronta para uso entre perfis do AEM Communities e o serviço SSO da Livefyre.

Quando os usuários fazem logon no site do AEM, eles também são conectados aos componentes sociais do Livefyre. Quando um usuário desconectado tenta usar um recurso do componente Livefyre que requer autenticação (como o upload de uma foto), o componente Livefyre inicia a autenticação do usuário.

A integração de autenticação padrão pode não ser perfeita para cada site. Para corresponder melhor ao fluxo de autenticação nos modelos do site, você pode substituir o Delegado de Autenticação do Livefyre padrão para atender às suas necessidades. Use estas etapas:

1. Uso do CRXDE Lite, copiar */libs/social/integrações/livefyre/components/authorizablecomponent/authclientlib* para */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib*.
1. Editar e salvar */apps/social/integrations/livefyre/components/authorizablecomponent/authclientlib/auth.js* para implementar um delegado de autenticação do Livefyre que atenda às suas necessidades.

   Para obter mais informações sobre como personalizar um representante de autenticação, consulte [Integração de identidade](https://answers.livefyre.com/developers/identity-integration/).

   Para obter mais informações sobre AEM Clientlibs, consulte [Usar bibliotecas do lado do cliente](https://experienceleague.adobe.com/docs/experience-manager-65/developing/introduction/clientlibs.html?lang=pt-BR).

## Use o Livefyre com o AEM Sites {#use-livefyre-with-aem-sites}

### Adicionar componentes do Livefyre a uma página {#add-livefyre-components-to-a-page}

Antes de adicionar componentes do Livefyre a uma página no Sites, é necessário ativar o Livefyre para a página, herdando uma configuração da nuvem do Livefyre de uma página principal ou adicionando a configuração diretamente à página. Consulte sua implementação para saber como incluir serviços em nuvem em seu site.

Quando o Livefyre é ativado para a página, os contêineres devem ser configurados para permitir os componentes do Livefyre. Consulte [Configuração de componentes no modo de design](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/siteandpage/default-components-designmode.html) para obter instruções sobre como ativar componentes diferentes.

>[!NOTE]
>
>Os aplicativos que exigem autenticação para publicação não funcionam até que a autenticação seja configurada em Personalizar integração de logon único .

1. No **Componentes** painel lateral no modo de design, selecione **Livefyre** no menu para limitar a lista aos componentes disponíveis do Livefyre.

   ![livefyre-add](assets/livefyre-add.png)

1. Selecione um componente do Livefyre e arraste-o para a posição na página.
1. Selecione se deseja criar um novo aplicativo do Livefyre ou incorporar um existente.

   Se estiver incorporando um aplicativo existente, AEM selecionar o aplicativo. Se estiver criando um novo aplicativo, o aplicativo precisará ser preenchido antes que qualquer conteúdo seja exibido. O aplicativo será criado no site e na rede do Livefyre selecionados quando a configuração da nuvem do Livefyre for ativada para a página.

   Para obter mais informações sobre como inserir componentes, consulte [Editar conteúdo da página](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/authoring/editing-content.html).

### Edite um componente do Livefyre para uma página de AEM. {#edit-a-livefyre-component-for-an-aem-page}

Você só pode configurar e editar um componente do Livefyre no Livefyre Studio. De AEM:

1. Clique no componente Livefyre para configurar.
1. Clique no botão **Configurar** ícone (chave) para abrir a caixa de diálogo de configuração.
1. Clique em **Para editar esse componente, vá para o Livefyre Studio**.
1. Edite o aplicativo no Livefyre Studio.

## Use o Livefyre com o AEM Assets {#use-livefyre-with-aem-assets}

### Solicitar direitos e importar UGC para o AEM Assets {#request-rights-and-import-ugc-into-aem-assets}

Você pode importar conteúdo gerado pelo usuário (UGC) do Twitter e do Instagram do Livefyre Studio para o AEM Assets usando o Importador de UGC. Após selecionar o conteúdo a ser importado, você deve solicitar direitos ao conteúdo antes que a importação possa ser concluída.

>[!NOTE]
>
>Antes de usar o Assets para importar o UGC, você deve configurar contas do Social e solicitações de direitos no Livefyre Studio. Consulte [Configuração: Solicitações de direitos](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html) para obter mais informações.

Para importar o UGC para o AEM Assets:

1. Na página inicial do AEM, navegue até **Ativos > Arquivos**.
1. Clique em **Criar**, depois clique em **Importar UGC.**

   ![livefyre-aem-import-ugc](assets/livefyre-aem-import-ugc.png)

1. Localizar conteúdo:

   * No Livefyre, clicando na guia Biblioteca UGC. Use os filtros e a pesquisa para encontrar conteúdo da Biblioteca UGC.
   * No Twitter e no Instagram, clicando na guia Twitter ou Instagram . Use a pesquisa ou os filtros para localizar conteúdo.

1. Selecione os ativos que deseja importar. Os ativos selecionados são contados e salvos automaticamente na variável **Selecionado** guia .
1. **Opcional**: Clique no botão **Selecionado** e revise o conteúdo UGC selecionado para importação.
1. Clique em **Avançar**.

   ![livefyre-aem-import-ugc2](assets/livefyre-aem-import-ugc2.png)

1. Para solicitações de direitos, escolha uma das seguintes opções para cada ativo:

   Para Instagram:

   * **Solicitar direitos manualmente** para obter uma mensagem que pode ser copiada, colada e enviada manualmente para os proprietários do conteúdo por meio do Instagram.
   * **Atribuir manualmente direitos de conteúdo** para substituir os direitos de ativos individuais.

   >[!NOTE]
   >
   >Devido a atualizações que afetam a agregação de conteúdo de contas de usuários não comerciais, não podemos mais postar comentários em seu nome ou verificar automaticamente as respostas do autor. [Clique aqui para saber mais](https://developers.facebook.com/blog/post/2018/04/04/facebook-api-platform-product-changes/).

   ![livefyre-aem-import-ugc3-6-4](assets/livefyre-aem-import-ugc3-6-4.png)

   Para Twitter:

   * **Autor da mensagem** para enviar uma mensagem ao proprietário do conteúdo solicitando direitos ao ativo.
   * **Atribuir manualmente direitos de conteúdo** para substituir os direitos de ativos individuais.


1. Clique em **Importar**.

   Se você enviou uma solicitação de direitos do Twitter, o proprietário do conteúdo verá a mensagem de solicitação de direitos em sua conta:

   ![livefyre-aem-rights-request-twitter](assets/livefyre-aem-rights-request-twitter.png)

   >[!NOTE]
   >
   >O twitter tem limites em solicitações idênticas provenientes da mesma conta. Ao importar mais de dois ativos, modifique as mensagens individualmente para evitar que sejam sinalizadas.

1. Clique em **Concluído** no canto superior direito para concluir o fluxo de trabalho de Solicitação de direitos.

   Você pode ver o status de uma Solicitação de direitos pendente de um ativo no Livefyre Studio. Se o conteúdo estiver pendente de uma solicitação de direitos, o ativo não será exibido no AEM Assets até que os direitos sejam concedidos. O ativo aparece automaticamente no AEM Assets quando uma Solicitação de direitos é concedida.

   Para o Instagram, você deve rastrear a resposta do proprietário do conteúdo e conceder direitos manualmente se tiver direitos ao conteúdo.

## Use o Livefyre com AEM Commerce {#use-livefyre-with-aem-commerce}

### Importar catálogos de produtos para o Livefyre com AEM Commerce {#import-product-catalogs-into-livefyre-with-aem-commerce}

AEM usuários do Commerce podem integrar facilmente seu catálogo de produtos existente ao Livefyre para impulsionar a participação do usuário nos aplicativos de visualização do Livefyre.

Após importar o catálogo de produtos, eles são exibidos em tempo real na sua instância do Livefyre. Se você editar ou excluir itens em seu catálogo de produtos do Commerce do AEM, as alterações serão automaticamente atualizadas no Livefrye.

1. Verifique se você tem o Livefyre para AEM pacote mais recente instalado em sua instância do AEM.
1. Na página inicial do AEM, navegue até **Comércio AEM**.
1. Crie uma nova coleção ou use uma coleção existente.
1. Passe o mouse sobre a coleção e clique em **Propriedades da coleção** (ícone de lápis).
1. Verificar **Sincronizar com o Livefyre**.
1. Preencha o **Prefixo da página do Livefyre** para vincular esta coleção a uma página específica no AEM.

   O prefixo da página define o caminho raiz no seu ambiente, onde a pesquisa por páginas de produtos começa. O Livefyre escolhe a primeira página que tem um produto correspondente associado a ela. Para obter páginas diferentes para produtos diferentes, várias coleções são necessárias.

## Matriz de suporte AEM para aplicativos do Livefyre {#aem-support-matrix-for-livefyre-apps}

| Aplicativos Livefyre | AEM 6.1 | AEM 6.2 | AEM 6.3 | AEM 6.4 |
|---|---|---|---|---|
| Carrossel | X | X | X | X |
| Chat | X | X | X | X |
| Comentários | X | X | X | X |
| Tira |  | X | X | X |
| LiveBlog | X | X | X | X |
| Mapa | X | X | X | X |
| Mural de mídia | X | X | X | X |
| Mosaico | X | X | X | X |
| Pesquisa |  | X | X | X |
| Revisões |  | X | X | X |
| Cartão único | X | X | X | X |
| Storify 2 |  | X | X | X |
| Em tendência |  | X | X | X |
| Botão Upload |  | X | X | X |
