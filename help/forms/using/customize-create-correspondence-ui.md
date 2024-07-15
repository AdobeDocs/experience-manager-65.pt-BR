---
title: Personalizar criar interface de correspondência
description: Saiba como personalizar uma interface do usuário de correspondência, como o logotipo, no ambiente do AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
docset: aem65
feature: Correspondence Management
exl-id: 9593ca2a-7f9e-4487-a1a5-ca44114bff17
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# Personalizar criar interface de correspondência{#customize-create-correspondence-ui}

## Visão geral {#overview}

O Gerenciamento de correspondência permite que você renove a marca do modelo da solução para obter melhor valor da marca e aderir aos padrões de marca da sua organização. A reformulação da marca da interface do usuário inclui a alteração do logotipo da organização, que é exibido no canto superior esquerdo da interface Criar correspondência.

Você pode alterar o logotipo na interface de Criar correspondência com o logotipo da sua organização.

![O ícone personalizado na interface para Criar Correspondência](assets/0_1_introscreenshot.png)

O ícone personalizado na interface de Criar correspondência

### Alteração do logotipo na interface de Criar correspondência {#changing-the-logo-in-the-create-correspondence-ui}

Para configurar uma imagem de logotipo de sua escolha, faça o seguinte:

1. Crie a [estrutura de pastas apropriada no CRX](#creatingfolderstructure).
1. [Carregar o novo arquivo de logotipo](#uploadlogo) na pasta criada no CRX.

1. [Configure o CSS](#createcss) no CRX para fazer referência ao novo logotipo.
1. Limpar o histórico do navegador e [atualizar a interface do usuário Criar Correspondência](#refreshccrui).

## Criação da estrutura de pastas necessária {#creatingfolderstructure}

Crie a estrutura de pastas, conforme explicado abaixo, para hospedar a imagem de logotipo personalizada e a folha de estilos. A nova estrutura de pastas com a pasta raiz /apps é semelhante à estrutura da pasta /libs.

Para qualquer personalização, crie uma estrutura de pastas paralela, conforme explicado abaixo, na ramificação /apps.

A ramificação `/apps` (estrutura de pastas):

* Garante a segurança dos arquivos se houver uma atualização do sistema. Se houver uma atualização, um pacote de recursos ou um hot fix, a ramificação `/libs` será atualizada e, se você hospedar suas alterações na ramificação `/libs`, elas serão substituídas.
* Ajuda a não perturbar o sistema/ramificação atual, o que você pode desfazer por engano se usar os locais padrão para armazenar os arquivos personalizados.
* Ajuda os seus recursos a obter uma prioridade mais alta quando o AEM procura recursos. O AEM está configurado para pesquisar primeiro a ramificação `/apps` e depois a ramificação `/libs` para encontrar um recurso. Esse mecanismo significa que o sistema usa sua sobreposição (e as personalizações definidas lá).

Use as etapas a seguir para criar a estrutura de pasta necessária na ramificação `/apps`:

1. Vá para `https://'[server]:[port]'/[ContextPath]/crx/de` e faça logon como Administrador.
1. Na pasta de aplicativos, crie uma pasta chamada `css` com caminho/estrutura semelhante à pasta css (na pasta ccrui).

   Etapas para criar a pasta css:

   1. Clique com o botão direito na pasta **css** no seguinte caminho e selecione **Sobrepor Nó**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      ![Sobrepor nó](assets/1_overlaynode_css.png)

   1. Certifique-se de que a caixa de diálogo Sobrepor nó tenha os seguintes valores:

      **Caminho:** `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css`

      **Local de Sobreposição:** `/apps/`

      **Corresponder Tipos De Nó:** Marcado

      ![Caminho do nó de sobreposição](assets/0_1_5ioverlaynodedialog.png)

      >[!NOTE]
      >
      >Não altere a ramificação `/libs`. As alterações feitas podem ser perdidas, pois essa ramificação é responsável por qualquer alteração sempre que você:
      >
      >    
      >    
      >    * Atualizar na sua instância
      >    * Aplicar um hot fix
      >    * Instalar um pacote de recursos
      >    
      >

   1. Clique em **OK**. A pasta css é criada no caminho especificado.

1. Na pasta de aplicativos, crie uma pasta chamada `imgs` com caminho/estrutura semelhante à pasta `imgs` (na pasta de competência).

   1. Clique com o botão direito do mouse na pasta **imgs** no seguinte caminho e selecione **Sobrepor Nó**: `/libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs`
   1. Certifique-se de que a caixa de diálogo Sobrepor nó tenha os seguintes valores:

      **Caminho:** /libs/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs

      **Local de Sobreposição:** /apps/

      **Corresponder Tipos De Nó:** Marcado

   1. Clique em **OK**.

      >[!NOTE]
      >
      >Você também pode criar manualmente a estrutura de pastas na pasta /apps.

1. Clique em **Salvar tudo** para salvar as alterações no servidor.

## Carregar o novo logotipo no CRX {#uploadlogo}

Faça upload do seu arquivo de logotipo personalizado para o CRX. As regras de HTML padrão regem a renderização do logotipo. Os formatos de arquivo de imagem compatíveis são de acordo com o navegador usado para acessar o AEM Forms. Todos os navegadores suportam JPEG, GIF e PNG. Para obter mais informações, consulte a documentação específica do navegador sobre os formatos de imagem compatíveis.

* As dimensões padrão da imagem do logotipo são 48 px &#42; 48 px. Verifique se a imagem é semelhante a este tamanho ou maior que 48 px &#42; 48 px.
* Se a altura da imagem do logotipo for superior a 50 px, a interface de usuário Criar correspondência dimensionará a imagem para uma altura máxima de 50 px, pois essa é a altura do cabeçalho. Ao reduzir a imagem, a interface do usuário Criar correspondência mantém a proporção da imagem.
* A interface de usuário Criar correspondência não aumenta a escala da imagem se ela for pequena. Portanto, use uma imagem de logotipo com pelo menos 48 px de altura e largura suficiente para maior clareza.

Use as seguintes etapas para fazer upload do arquivo de logotipo personalizado para o CRX:

1. Ir para `https://'[server]:[port]'/[contextpath]/crx/de`. Se necessário, efetue login como Administrador.
1. No CRXDE, clique com o botão direito do mouse na pasta **imgs** no seguinte caminho e selecione **Criar > Criar arquivo**:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/imgs/`

   ![Criar novo nó na pasta imgs](assets/2_contentexplorernewnode.png)

1. Na caixa de diálogo Criar arquivo, digite o nome do arquivo como CustomLogo.png (ou o nome do arquivo de logotipo).

   ![CustomLogo.png como novo nó](assets/3_contentexplorernewnode_customlogo.png)

1. Clique em **Salvar tudo**.

   No novo arquivo criado (aqui, CustomLogo.png), a propriedade jcr:content é exibida.

1. Clique em jcr:content na estrutura de pastas.

   jcr:propriedades do conteúdo são exibidas.

   ![jcrcontentproperties](assets/jcrcontentproperties.png)

1. Clique duas vezes na propriedade **jcr:data**.

   A caixa de diálogo Editar jcr:data é exibida.

   Agora clique na pasta newlogo.png, clique duas vezes em jcr:content (opção dim) e defina o tipo nt:resource. Se não estiver presente, crie uma propriedade com o nome jcr:content.

1. Na caixa de diálogo Editar jcr:data, clique em **Procurar** e selecione o arquivo de imagem que deseja usar como logotipo (aqui CustomLogo.png).

   Os formatos de arquivo de imagem compatíveis são de acordo com o navegador usado para acessar o AEM Forms. Todos os navegadores suportam JPEG, GIF e PNG. Para obter mais informações, consulte a documentação específica do navegador sobre os formatos de imagem compatíveis.

   ![Arquivo de logotipo personalizado de exemplo](assets/geometrixx-outdoors.png)

   Exemplo: CustomLogo.png para ser usado como o logotipo personalizado

1. Clique em **Salvar tudo**.

## Criar o CSS para renderizar o logotipo com a interface {#createcss}

A imagem de logotipo personalizada requer que uma folha de estilos adicional seja carregada no contexto de conteúdo.

Use as etapas a seguir para criar a folha de estilos para renderizar o logotipo com a interface do usuário:

1. Ir para `https://'[server]:[port]'/[contextpath]/crx/de`. Se necessário, efetue login como Administrador.
1. Crie um arquivo chamado customcss.css (você não pode usar um nome de arquivo diferente) no seguinte local:

   `/apps/fd/cm/ccr/gui/components/admin/clientlibs/ccrui/css/`

   Etapas para criar o arquivo customcss.css:

   1. Clique com o botão direito na pasta **css** e selecione **Criar > Criar arquivo**.
   1. Na caixa de diálogo Novo Arquivo, especifique o nome do CSS como `customcss.css` (você não pode usar um nome de arquivo diferente) e clique em **OK**.
   1. Adicione o seguinte código ao arquivo css recém-criado. Em content:url no código, especifique o nome da imagem carregada na pasta imgs no CRXDE.

      ```css
      .logo, .logo:after {
      content:url("../imgs/CustomLogo.png");
      }
      ```

   1. Clique em **Salvar tudo**.

## Atualize a interface de Criar correspondência para exibir o logotipo personalizado {#refreshccrui}

Limpe o cache do navegador e abra a instância da interface Criar correspondência no navegador para que você possa ver seu logotipo personalizado.

![Criar interface de usuário de correspondência com logotipo personalizado](assets/0_1_introscreenshot-1.png)

O ícone personalizado na interface de Criar correspondência
