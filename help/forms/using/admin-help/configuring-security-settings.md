---
title: Definição das configurações de segurança
seo-title: Configuring security settings
description: Saiba como definir configurações de segurança.
seo-description: Learn how to configure security settings.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
feature: PDF Generator
exl-id: be076477-2681-4570-953d-6c44d3c30843
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1367'
ht-degree: 0%

---

# Definição das configurações de segurança{#configuring-security-settings}

É possível limitar o acesso a documentos do PDF definindo senhas e restringindo determinados recursos, como impressão e edição. Quando um documento PDF tem recursos restritos, as ferramentas e os itens de menu relacionados a esses recursos ficam esmaecidos. Você também pode usar outros métodos para criar documentos seguros, como criptografar ou certificar um documento. Uma configuração de segurança contém a senha e as opções específicas a serem usadas em determinadas conversões de PDF.

Na página Configurações de segurança , é possível realizar as seguintes tarefas:

## Criar ou editar uma configuração de segurança {#create-or-edit-a-security-setting}

A *configuração de segurança* controla a segurança e as permissões dos arquivos convertidos com essa configuração de segurança.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações de segurança.
1. Clique em New ou clique no nome de uma configuração de segurança.
1. Na página Nova/Editar configuração de segurança, preencha as informações necessárias para a configuração de segurança. (Consulte [Definição das configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Clique em Salvar e, na caixa de diálogo exibida, digite um nome para a configuração e, em seguida, clique em OK.

### Configurações de segurança {#security-settings}

Essas configurações configuram a compatibilidade e a criptografia. Para obter instruções sobre como acessar as configurações de fontes, consulte [Criar ou editar uma configuração de segurança](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilidade:** Define o tipo de criptografia para abrir um documento protegido por senha. A opção Acrobat 3.0 e posterior usa um nível de criptografia baixo, mas as outras opções usam um nível de criptografia alto:

**Acrobat 3.0 E Posterior:** Usa baixa criptografia (RC4 de 40 bits).

**Acrobat 5.0 E Posterior:** Usa alta criptografia (RC4 de 128 bits).

**Acrobat 6.0 E Posterior:** Usa alta criptografia (RC4 de 128 bits). Essa opção permite habilitar metadados para pesquisa.

**Acrobat 7.0 E Posterior:** Usa alta criptografia (AES de 128 bits). Essa opção permite habilitar metadados para pesquisa e criptografar somente anexos de arquivo.

**Acrobat 9.0 E Posterior:** Usa alta criptografia (AES de 256 bits). Essa opção permite habilitar metadados para pesquisa e criptografar somente anexos de arquivo.

Uma versão anterior do Acrobat não pode abrir um documento PDF que tenha uma configuração de compatibilidade mais alta. Por exemplo, se você selecionar a opção Acrobat 7.0 e posterior, não será possível abrir o documento no Acrobat 6.0 ou anterior.

Verifique se o nível de compatibilidade está consistente com o nível de compatibilidade do PDF para a mesma fonte. Por exemplo, se você tiver uma pasta assistida configurada para usar a configuração PDF padrão, que é compatível com o Acrobat 5.0 ou posterior, seu nível de compatibilidade de segurança não deve ser maior que o Acrobat 5.0.

**Restrição de documento:** As restrições de documento disponíveis dependem da opção Compatibilidade selecionada.

**Sem criptografia:** Não criptografa nenhuma parte do documento.

**Criptografar todo o conteúdo do documento:** Criptografa o documento e os metadados do documento. Quando essa opção é selecionada, os mecanismos de pesquisa não podem acessar os metadados do documento.

**Criptografar Todos Os Conteúdos Do Documento Exceto Metadados (Compatível Com Acrobat 6 E Posterior):** Criptografa o conteúdo de um documento, mas ainda permite que os mecanismos de pesquisa acessem os metadados do documento. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 6.0 ou posterior, Acrobat 7.0 ou posterior ou Acrobat 9.0 ou posterior.

**Criptografar Somente Anexos De Arquivo (Compatível Com Acrobat 7 E Posterior):** Os usuários podem abrir o documento sem uma senha, mas devem digitar uma senha para abrir anexos de arquivo. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior.

Essas configurações configuram a segurança da senha:

>[!NOTE]
>
>Caso se esqueça de uma senha, ela não poderá ser recuperada do documento. É recomendável armazenar senhas em outro local seguro, caso se esqueça delas. Além disso, mantenha uma cópia de backup do documento que não é protegido por senha.

**Exigir senha para abrir o documento:** Ativa as opções de senha.

**Senha de Abertura do Documento:** Impede que os usuários abram o documento, a menos que digitem a senha especificada. As senhas diferenciam maiúsculas de minúsculas. A Acrobat usa o método RC4 de segurança da RSA Security Inc. para proteger documentos PDF de senha. Se você estiver restringindo a impressão e edição, é recomendável adicionar uma senha de abertura de documento para melhorar a segurança.

**Redigite a senha de abertura do documento:** Garante que a senha de abertura do documento esteja correta.

**Exigir senha para abrir anexos de arquivo:** Ativa as opções de senha. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de documento está definida como Criptografar somente anexos de arquivo.

**Senha de Abertura do Anexo de Arquivo:** Garante que a senha seja necessária para abrir um anexo de arquivo. Os usuários podem abrir o documento sem uma senha. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de documento está definida como Criptografar somente anexos de arquivo.

**Redigite o anexo do arquivo:** Garante que a senha esteja correta. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de documento está definida como Criptografar somente anexos de arquivo.

Essas opções configuram as permissões:

**Use Uma Senha Para Restringir A Impressão E Edição Do Documento E Suas Configurações De Segurança:** Ativa restrições em permissões.

**Senha de permissões:** Restringe a impressão e edição de usuários. Os usuários não podem alterar essas configurações de segurança a menos que digitem a senha especificada. Você não pode usar a mesma senha usada para a Senha de Abertura do Documento. Quando você define uma senha de permissões, somente as pessoas que digitam essa senha podem alterar as configurações de segurança. Se o documento PDF tiver ambos os tipos de senhas, qualquer senha a abrirá. No entanto, um usuário só pode definir ou alterar os recursos restritos com a senha de permissões. Se o documento PDF tiver apenas a senha de permissão ou se um usuário abrir o documento usando a senha de abertura do documento, o prompt de senha será exibido quando o usuário tentar alterar as configurações de segurança.

**Redigite a senha das permissões:** Garante que a senha das permissões esteja correta.

**Impressão permitida:** Especifica a qualidade de impressão do documento PDF:

**Nenhum:** Impede que os usuários imprimam o documento.

**Baixa resolução (150 dpi):** Permite que os usuários imprimam o documento com resolução de não mais do que 150 dpi. A impressão pode ser mais lenta porque cada página é impressa como uma imagem de bitmap. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) estiver selecionado.

**Alta resolução:** Permite que os usuários imprimam em qualquer resolução, direcionando saída vetorial de alta qualidade para PostScript e outras impressoras que oferecem suporte a recursos avançados de impressão de alta qualidade.

**Alterações permitidas:** Define quais ações de edição são permitidas no documento PDF:

**Nenhum:** Impede que os usuários alterem o documento, incluindo o preenchimento de campos de assinatura e de formulário.

**Inserção, Exclusão E Rotação De Páginas:** Permite aos usuários inserir, excluir e girar páginas, bem como criar marcadores e páginas de miniatura. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) estiver selecionado.

**Preenchendo Campos De Formulário E Assinando Campos De Assinatura Existentes:** Permite que os usuários preencham formulários e adicionem assinaturas digitais. No entanto, os usuários não podem adicionar comentários ou criar campos de formulário. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) estiver selecionado.

**Comentários, Preenchimentos Em Campos De Formulário E Assinatura De Campos De Assinatura Existentes:** Permite que os usuários preencham formulários e adicionem assinaturas digitais e comentários.

**Layout Da Página, Toque-Up, Preenchimento De Campos De Formulário E Assinatura De Campos De Assinatura Existentes:** Permite aos usuários inserir, girar ou excluir páginas e criar marcadores ou imagens em miniatura, preencher formulários e adicionar assinaturas digitais. Essa opção não permite que os usuários criem campos de formulário. Essa opção só estará disponível se um nível de criptografia baixo (Acrobat 3.0) estiver selecionado.

**Quaisquer páginas exceto extração:** Permite que os usuários alterem o documento usando qualquer método na Lista de permissões Alterações, exceto para remover páginas.

**Habilite A Cópia De Texto, Imagens E Outro Conteúdo:** Permite que os usuários selecionem e copiem o conteúdo do documento do PDF. Também permite que os utilitários que precisam acessar o conteúdo de um arquivo PDF, como o Acrobat Catalog, acessem esse conteúdo. Essa opção só estará disponível se um nível de criptografia alto estiver selecionado.

**Habilite O Acesso Ao Texto De Dispositivos Reader De Tela Para Os Incapacitados Visualmente:** Permite que os usuários portadores de deficiência visual leiam o documento usando leitores de tela. No entanto, os usuários não podem copiar ou extrair o conteúdo do documento. Essa opção só estará disponível se um nível de criptografia alto estiver selecionado.

## Excluir uma configuração de segurança {#delete-a-security-setting}

Você pode excluir uma configuração de segurança se ela não for mais necessária. No entanto, não é possível excluir configurações de segurança pré-configuradas.

1. No console de administração, clique em **[!UICONTROL Serviços > Gerador de PDF > Configurações de segurança]**.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. Você pode selecionar várias configurações.
1. Clique em **[!UICONTROL Excluir]** e no **[!UICONTROL Confirmação de exclusão]** página, clique em **[!UICONTROL Excluir]** novamente.
