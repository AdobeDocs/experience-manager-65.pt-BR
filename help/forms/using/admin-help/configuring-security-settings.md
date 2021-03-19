---
title: Definição das configurações de segurança
seo-title: Definição das configurações de segurança
description: Saiba como definir configurações de segurança.
seo-description: Saiba como definir configurações de segurança.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
feature: Gerador de PDF
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 0%

---


# Definir configurações de segurança{#configuring-security-settings}

É possível limitar o acesso a documentos PDF configurando senhas e restringindo determinados recursos, como impressão e edição. Quando um documento PDF tem recursos restritos, as ferramentas e os itens de menu relacionados a esses recursos ficam esmaecidos. Você também pode usar outros métodos para criar documentos seguros, como criptografar ou certificar um documento. Uma configuração de segurança contém a senha e as opções específicas a serem usadas em determinadas conversões de PDF.

Na página Configurações de segurança , é possível realizar as seguintes tarefas:

## Criar ou editar uma configuração de segurança {#create-or-edit-a-security-setting}

Uma *configuração de segurança* controla a segurança e as permissões dos arquivos convertidos com essa configuração de segurança.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações de segurança.
1. Clique em New ou clique no nome de uma configuração de segurança.
1. Na página Nova/Editar configuração de segurança, preencha as informações necessárias para a configuração de segurança. (Consulte [Definição das configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Clique em Salvar e, na caixa de diálogo exibida, digite um nome para a configuração e, em seguida, clique em OK.

### Configurações de segurança {#security-settings}

Essas configurações configuram a compatibilidade e a criptografia. Para obter instruções sobre como acessar as configurações de fontes, consulte [Criar ou editar uma configuração de segurança](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilidade:** define o tipo de criptografia para abrir um documento protegido por senha. A opção Acrobat 3.0 e posterior usa um nível de criptografia baixo, mas as outras opções usam um nível de criptografia alto:

**Acrobat 3.0 E Posterior:** Usa pouca criptografia (RC4 de 40 bits).

**Acrobat 5.0 E Posterior:** Usa criptografia alta (RC4 de 128 bits).

**Acrobat 6.0 E Posterior:** Usa criptografia alta (RC4 de 128 bits). Essa opção permite habilitar metadados para pesquisa.

**Acrobat 7.0 E Posterior:** Usa criptografia alta (AES de 128 bits). Essa opção permite habilitar metadados para pesquisa e criptografar somente anexos de arquivo.

**Acrobat 9.0 E Posterior:** Usa criptografia de alta segurança (AES de 256 bits). Essa opção permite habilitar metadados para pesquisa e criptografar somente anexos de arquivo.

Uma versão anterior do Acrobat não pode abrir um documento PDF que tenha uma configuração de compatibilidade mais alta. Por exemplo, se você selecionar a opção Acrobat 7.0 e posterior, não será possível abrir o documento no Acrobat 6.0 ou anterior.

Verifique se o nível de compatibilidade está consistente com o nível de compatibilidade do PDF para a mesma fonte. Por exemplo, se você tiver uma pasta assistida configurada para usar a configuração de PDF Padrão, que é compatível com o Acrobat 5.0 ou posterior, seu nível de compatibilidade de segurança não deve ser maior que o Acrobat 5.0.

**Restrição de documento:** as restrições de documento disponíveis dependem da opção Compatibilidade selecionada.

**Sem criptografia:** não criptografa nenhuma parte do documento.

**Criptografar todo o conteúdo do documento:** criptografa o documento e os metadados do documento. Quando essa opção é selecionada, os mecanismos de pesquisa não podem acessar os metadados do documento.

**Criptografar todos os conteúdos do documento, exceto metadados (compatível com Acrobat 6 e posterior):** criptografa o conteúdo de um documento, mas ainda permite que os mecanismos de pesquisa acessem os metadados do documento. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 6.0 ou posterior, Acrobat 7.0 ou posterior ou Acrobat 9.0 ou posterior.

**Criptografar somente anexos de arquivo (compatível com Acrobat 7 e posterior):** os usuários podem abrir o documento sem uma senha, mas devem inserir uma senha para abrir anexos de arquivo. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior.

Essas configurações configuram a segurança da senha:

>[!NOTE]
>
>Caso se esqueça de uma senha, ela não poderá ser recuperada do documento. É recomendável armazenar senhas em outro local seguro, caso se esqueça delas. Além disso, mantenha uma cópia de backup do documento que não é protegido por senha.

**Exigir senha para abrir o documento:** ativa as opções de senha.

**Senha de abertura do documento:** impede que os usuários abram o documento, a menos que digitem a senha especificada. As senhas diferenciam maiúsculas de minúsculas. A Acrobat usa o método RC4 de segurança da RSA Security Inc. para proteger documentos PDF por senha. Se você estiver restringindo a impressão e edição, é recomendável adicionar uma senha de abertura de documento para melhorar a segurança.

**Redigitar Senha de Abertura do Documento:**  Garante que a senha de abertura do documento esteja correta.

**Exigir senha para abrir anexos de arquivo:** ativa as opções de senha. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de documento está definida como Criptografar somente anexos de arquivo.

**Senha de abertura do anexo de arquivo:**  garante que uma senha seja necessária para abrir um anexo de arquivo. Os usuários podem abrir o documento sem uma senha. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de documento está definida como Criptografar somente anexos de arquivo.

**Redigitar anexo do arquivo:** garante que a senha esteja correta. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de documento está definida como Criptografar somente anexos de arquivo.

Essas opções configuram as permissões:

**Use Uma Senha Para Restringir A Impressão E A Edição Do Documento E Suas Configurações De Segurança:** Habilita Restrições Em Permissões.

**Senha de permissões:** impede que os usuários imprimam e editem. Os usuários não podem alterar essas configurações de segurança a menos que digitem a senha especificada. Você não pode usar a mesma senha usada para a Senha de Abertura do Documento. Quando você define uma senha de permissões, somente as pessoas que digitam essa senha podem alterar as configurações de segurança. Se o documento PDF tiver ambos os tipos de senhas, qualquer senha a abrirá. No entanto, um usuário só pode definir ou alterar os recursos restritos com a senha de permissões. Se o documento PDF tiver apenas a senha de permissão ou se um usuário abrir o documento usando a senha de abertura do documento, o prompt de senha será exibido quando o usuário tentar alterar as configurações de segurança.

**Redigite a senha das permissões:** garante que a senha das permissões esteja correta.

**Impressão permitida:** Especifica a qualidade de impressão do documento PDF:

**Nenhum:** impede que os usuários imprimam o documento.

**Baixa resolução (150 dpi):** Permite que os usuários imprimam o documento com resolução de não mais do que 150 dpi. A impressão pode ser mais lenta porque cada página é impressa como uma imagem de bitmap. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) estiver selecionado.

**Alta resolução:** permite que os usuários imprimam em qualquer resolução, direcionando saída vetorial de alta qualidade para PostScript e outras impressoras que suportam recursos de impressão de alta qualidade avançados.

**Alterações permitidas:** Define quais ações de edição são permitidas no documento PDF:

**Nenhum:** impede que os usuários alterem o documento, incluindo o preenchimento de campos de assinatura e de formulário.

**Inserir, Excluir E Girar Páginas:** Permite que os usuários insiram, excluam e girem páginas, bem como criar marcadores e páginas de miniatura. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) estiver selecionado.

**Preencher campos de formulário e assinar campos de assinatura existentes:** Permite que os usuários preencham formulários e adicionem assinaturas digitais. No entanto, os usuários não podem adicionar comentários ou criar campos de formulário. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) estiver selecionado.

**Comentários, Preenchimentos Em Campos De Formulário E Assinatura De Campos De Assinatura Existentes:** Permite que os usuários preencham formulários e adicionem assinaturas e comentários digitais.

**Layout de página, Retoque, Preenchimento de campos de formulário e Assinatura de campos de assinatura existentes:** Permite que os usuários insiram, giram ou excluam páginas e criem marcadores ou imagens em miniatura, preencham formulários e adicionem assinaturas digitais. Essa opção não permite que os usuários criem campos de formulário. Essa opção só estará disponível se um nível de criptografia baixo (Acrobat 3.0) estiver selecionado.

**Quaisquer páginas exceto extração:** Permite que os usuários alterem o documento usando qualquer método na Lista de permissões Alterações, exceto para remover páginas.

**Habilitar cópia de texto, imagens e outro conteúdo:** Permite que os usuários selecionem e copiem o conteúdo do documento PDF. Ele também permite que os utilitários que precisam acessar o conteúdo de um arquivo PDF, como o Acrobat Catalog, acessem esse conteúdo. Essa opção só estará disponível se um nível de criptografia alto estiver selecionado.

**Habilite o acesso de texto de dispositivos Reader de tela para os deficientes visuais:** Permite que os usuários portadores de deficiência visual leiam o documento usando leitores de tela. No entanto, os usuários não podem copiar ou extrair o conteúdo do documento. Essa opção só estará disponível se um nível de criptografia alto estiver selecionado.

## Excluir uma configuração de segurança {#delete-a-security-setting}

Você pode excluir uma configuração de segurança se ela não for mais necessária. No entanto, não é possível excluir configurações de segurança pré-configuradas.

1. No console de administração, clique em **[!UICONTROL Serviços > Gerador de PDF > Configurações de segurança]**.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. Você pode selecionar várias configurações.
1. Clique em **[!UICONTROL Delete]** e, na página **[!UICONTROL Delete Confirmation]**, clique novamente em **[!UICONTROL Delete]**.

