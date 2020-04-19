---
title: Definição das configurações de segurança
seo-title: Definição das configurações de segurança
description: Saiba como configurar as configurações de segurança.
seo-description: Saiba como configurar as configurações de segurança.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# Definição das configurações de segurança{#configuring-security-settings}

É possível limitar o acesso a documentos PDF configurando senhas e restringindo determinados recursos, como impressão e edição. Quando um documento PDF tem recursos restritos, as ferramentas e os itens de menu relacionados a esses recursos ficam esmaecidos. Você também pode usar outros métodos para criar documentos protegidos, como criptografia ou certificação de um documento. Uma configuração de segurança contém a senha e as opções específicas a serem usadas para determinadas conversões de PDF.

Na página Configurações de segurança, você pode fazer as seguintes tarefas:

## Criar ou editar uma configuração de segurança {#create-or-edit-a-security-setting}

Uma configuração *de* segurança controla a segurança e as permissões para arquivos convertidos com essa configuração de segurança.

1. No console de administração, clique em Serviços > Gerador de PDF > Configurações de segurança.
1. Clique em Novo ou clique no nome de uma configuração de segurança.
1. Na página Nova/Editar configurações de segurança, preencha as informações necessárias para a configuração de segurança. (Consulte [Definição das configurações](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings)de tipo de arquivo.)
1. Clique em Salvar e, na caixa de diálogo exibida, digite um nome para a configuração e clique em OK.

### Configurações de segurança {#security-settings}

Essas configurações definem a compatibilidade e a criptografia. Para obter instruções sobre como acessar as configurações de fontes, consulte [Criar ou editar uma configuração](configuring-security-settings.md#create-or-edit-a-security-setting)de segurança.

**Compatibilidade:** Define o tipo de criptografia para abrir um documento protegido por senha. A opção Acrobat 3.0 e posterior usa um nível baixo de criptografia, mas as outras opções usam um nível alto de criptografia:

**Acrobat 3.0 E Posterior:** Usa criptografia baixa (RC4 de 40 bits).

**Acrobat 5.0 E Posterior:** Usa criptografia alta (RC4 de 128 bits).

**Acrobat 6.0 E Posterior:** Usa criptografia alta (RC4 de 128 bits). Essa opção permite ativar metadados para pesquisa.

**Acrobat 7.0 E Posterior:** Usa criptografia alta (AES de 128 bits). Essa opção permite ativar metadados para pesquisa e criptografia somente de anexos de arquivo.

**Acrobat 9.0 E Posterior:** Usa criptografia alta (AES de 256 bits). Essa opção permite ativar metadados para pesquisa e criptografia somente de anexos de arquivo.

Uma versão anterior do Acrobat não pode abrir um documento PDF que tenha uma configuração de compatibilidade mais alta. Por exemplo, se você selecionar a opção Acrobat 7.0 e posterior, não poderá abrir o documento no Acrobat 6.0 ou anterior.

Verifique se o nível de compatibilidade está consistente com o nível de compatibilidade do PDF para a mesma fonte. Por exemplo, se você tiver uma pasta monitorada configurada para usar a configuração de PDF padrão, que é compatível com o Acrobat 5.0 ou posterior, seu nível de compatibilidade de segurança não deve ser superior ao Acrobat 5.0.

**Restrição de Documento:** As restrições de documento disponíveis dependem da opção Compatibilidade selecionada.

**Sem criptografia:** Não criptografa nenhuma parte do documento.

**Criptografar todo o conteúdo do Documento:** Criptografa o documento e os metadados do documento. Quando essa opção é selecionada, os mecanismos de pesquisa não podem acessar os metadados do documento.

**Criptografar Todo O Conteúdo Do Documento, Exceto Metadados (Compatível Com O Acrobat6 E Posterior):** Criptografa o conteúdo de um documento, mas ainda permite que os mecanismos de pesquisa acessem os metadados do documento. Essa opção está disponível somente quando a opção Compatibilidade estiver definida como Acrobat 6.0 ou posterior, Acrobat 7.0 ou posterior ou Acrobat 9.0 ou posterior.

**Criptografar somente anexos de arquivo (compatível com o Acrobat 7 e posterior):** Os usuários podem abrir o documento sem uma senha, mas precisam digitar uma senha para abrir anexos de arquivo. Essa opção está disponível somente quando a opção Compatibilidade estiver definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior.

Estas configurações definem a segurança da senha:

>[!NOTE]
>
>Se você esquecer uma senha, ela não poderá ser recuperada do documento. É recomendável que você armazene senhas em outro local seguro para o caso de esquecê-las. Além disso, mantenha uma cópia de backup do documento que não seja protegido por senha.

**Exigir Uma Senha Para Abrir O Documento:** Ativa as opções de senha.

**Senha de abertura do Documento:** Impede que os usuários abram o documento, a menos que digitem a senha especificada. As senhas fazem distinção entre maiúsculas e minúsculas. O Acrobat usa o método RC4 de segurança da RSA Security Inc. para proteger documentos PDF por senha. Se você estiver restringindo a impressão e edição, é recomendável adicionar uma senha de abertura de documento para melhorar a segurança.

**Digite novamente a senha de abertura do Documento:** Certifique-se de que a senha de abertura do documento está correta.

**Exigir Uma Senha Para Abrir Anexos De Arquivo:** Ativa as opções de senha. Essa opção está disponível somente quando a opção Compatibilidade estiver definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de Documento estiver definida como Criptografar somente anexos de arquivo.

**Senha de abertura do anexo de arquivo:** Certifique-se de que uma senha seja necessária para abrir um anexo de arquivo. Os usuários podem abrir o documento sem uma senha. Essa opção está disponível somente quando a opção Compatibilidade estiver definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de Documento estiver definida como Criptografar somente anexos de arquivo.

**Digite novamente o anexo do arquivo:** Certifique-se de que a senha esteja correta. Essa opção está disponível somente quando a opção Compatibilidade estiver definida como Acrobat 7.0 ou posterior ou como Acrobat 9.0 ou posterior e a opção Restrição de Documento estiver definida como Criptografar somente anexos de arquivo.

Essas opções configuram as permissões:

**Use Uma Senha Para Restringir A Impressão E Edição Do Documento E Suas Configurações De Segurança:** Habilita restrições em permissões.

**Senha de permissões:** Restringe a impressão e edição de usuários. Os usuários não podem alterar essas configurações de segurança a menos que digitem a senha especificada. Não é possível usar a mesma senha usada para a Senha de abertura do Documento. Quando você define uma senha de permissões, somente as pessoas que digitam essa senha podem alterar as configurações de segurança. Se o documento PDF tiver ambos os tipos de senhas, qualquer uma delas a abrirá. No entanto, um usuário só pode definir ou alterar os recursos restritos com a senha de permissões. Se o documento PDF tiver apenas a senha de permissão ou se um usuário abrir o documento usando a senha de abertura do documento, o prompt de senha será exibido quando o usuário tentar alterar as configurações de segurança.

**Redigite a senha de permissões:** Certifique-se de que a senha de permissões esteja correta.

**Impressão permitida:** Especifica a qualidade de impressão do documento PDF:

**Nenhum:** Impede que os usuários imprimam o documento.

**Baixa resolução (150 dpi):** Permite que os usuários imprimam o documento com resolução de não mais que 150 dpi. A impressão pode ser mais lenta porque cada página é impressa como uma imagem de bitmap. Essa opção está disponível somente se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) for selecionado.

**Alta resolução:** Permite que os usuários imprimam em qualquer resolução, direcionando a saída vetorial de alta qualidade para PostScript e outras impressoras que suportam recursos avançados de impressão de alta qualidade.

**Alterações permitidas:** Define quais ações de edição são permitidas no documento PDF:

**Nenhum:** Impede que os usuários alterem o documento, incluindo o preenchimento de campos de assinatura e de formulário.

**Inserir, Excluir E Girar Páginas:** Permite que os usuários insiram, excluam e girem páginas, além de criar marcadores e páginas de miniaturas. Essa opção está disponível somente se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) for selecionado.

**Preenchimento De Campos De Formulário E Assinatura De Campos De Assinatura Existentes:** Permite que os usuários preencham formulários e adicionem assinaturas digitais. No entanto, os usuários não podem adicionar comentários nem criar campos de formulário. Essa opção está disponível somente se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) for selecionado.

**Comentários, Preenchimento De Campos De Formulário E Assinatura De Campos De Assinatura Existentes:** Permite que os usuários preencham formulários e adicionem assinaturas digitais e comentários.

**Layout De Página, Retoque, Preenchimento De Campos De Formulário E AssinaturaCampos De Assinatura Existentes:** Permite que os usuários insiram, girem ou excluam páginas e criem marcadores ou imagens em miniatura, preencham formulários e adicionem assinaturas digitais. Essa opção não permite que os usuários criem campos de formulário. Essa opção estará disponível somente se um nível de criptografia baixo (Acrobat 3.0) for selecionado.

**Qualquer página exceto extração:** Permite que os usuários alterem o documento usando qualquer método na lista Alterações permitidas, exceto para remover páginas.

**Ative A Cópia De Texto, Imagens E Outro Conteúdo:** Permite que os usuários selecionem e copiem o conteúdo do documento PDF. Ele também permite que os utilitários que precisam acessar o conteúdo de um arquivo PDF, como o Catálogo do Acrobat, acessem esse conteúdo. Essa opção está disponível somente se um nível de criptografia alto for selecionado.

**Ative O Acesso Ao Texto De Dispositivos De Leitor De Tela Para Os Com Insuficiência Visual:** Permite que usuários portadores de deficiências visuais leiam o documento usando leitores de tela. No entanto, os usuários não podem copiar ou extrair o conteúdo do documento. Essa opção está disponível somente se um nível de criptografia alto for selecionado.

## Excluir uma configuração de segurança {#delete-a-security-setting}

Você pode excluir uma configuração de segurança se ela não for mais necessária. No entanto, as configurações de segurança pré-definidas não podem ser excluídas.

1. No console de administração, clique em **[!UICONTROL Serviços > Gerador de PDF > Configurações]** de segurança.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. É possível selecionar várias configurações.
1. Clique em **[!UICONTROL Excluir]** e, na página **[!UICONTROL Excluir confirmação]** , clique em **[!UICONTROL Excluir]** novamente.

