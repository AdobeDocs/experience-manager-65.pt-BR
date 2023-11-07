---
title: Definição das configurações de segurança
description: Saiba como definir configurações de segurança. Você pode proteger documentos do PDF limitando o acesso. Você pode criptografar, certificar ou proteger o documento por senha.
uuid: 9747f268-3551-4064-8dba-e1de4a577843
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a89ab508-173f-4b1c-88d9-ef944af4d9ae
feature: PDF Generator
exl-id: be076477-2681-4570-953d-6c44d3c30843
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 0%

---

# Definição das configurações de segurança{#configuring-security-settings}

É possível limitar o acesso a documentos do PDF definindo senhas e restringindo determinados recursos, como impressão e edição. Quando um documento PDF tem recursos restritos, as ferramentas e os itens de menu relacionados a esses recursos ficam esmaecidos. Você também pode usar outros métodos para criar documentos seguros, como criptografar ou certificar um documento. Uma configuração de segurança contém a senha e as opções específicas a serem usadas para determinadas conversões de PDF.

Na página Configurações de segurança, é possível executar as seguintes tarefas:

## Criar ou editar uma configuração de segurança {#create-or-edit-a-security-setting}

A *configuração de segurança* controla a segurança e as permissões para arquivos convertidos com essa configuração de segurança.

1. No console de administração, clique em Serviços > PDF Generator > Configurações de segurança.
1. Clique em Novo ou clique no nome de uma configuração de segurança.
1. Na página Novo/Editar configuração de segurança, preencha as informações necessárias para a configuração de segurança. (Consulte [Definição das configurações de tipo de arquivo](/help/forms/using/admin-help/configuring-file-type-settings.md#configuring-file-type-settings).)
1. Clique em Salvar e, na caixa de diálogo exibida, digite um nome para a configuração e clique em OK.

### Configurações de segurança {#security-settings}

Essas configurações definem a compatibilidade e a criptografia. Para obter instruções sobre como acessar as configurações de fontes, consulte [Criar ou editar uma configuração de segurança](configuring-security-settings.md#create-or-edit-a-security-setting).

**Compatibilidade:** Define o tipo de criptografia para abrir um documento protegido por senha. A opção Acrobat 3.0 e posterior usa um nível de criptografia baixo, mas as outras opções usam um nível de criptografia alto:

**Acrobat 3.0 E Posterior:** Usa baixa criptografia (RC4 de 40 bits).

**Acrobat 5.0 E Posterior:** Usa criptografia alta (RC4 de 128 bits).

**Acrobat 6.0 E Posterior:** Usa criptografia alta (RC4 de 128 bits). Essa opção permite ativar metadados para pesquisa.

**Acrobat 7.0 E Posterior:** Usa criptografia alta (AES de 128 bits). Essa opção permite ativar metadados para pesquisar e criptografar apenas anexos de arquivo.

**Acrobat 9.0 E Posterior:** Usa criptografia alta (AES de 256 bits). Essa opção permite ativar metadados para pesquisar e criptografar apenas anexos de arquivo.

Uma versão anterior do Acrobat não pode abrir um documento PDF com uma configuração de compatibilidade mais alta. Por exemplo, se você selecionar a opção Acrobat 7.0 e posterior, não será possível abrir o documento no Acrobat 6.0 ou anterior.

Verifique se o nível de compatibilidade é consistente com o nível de compatibilidade de PDF para a mesma fonte. Por exemplo, se você tiver uma pasta monitorada configurada para usar a configuração PDF padrão, que é compatível com o Acrobat 5.0 ou posterior, seu nível de compatibilidade de segurança não deve ser superior ao Acrobat 5.0.

**Restrição de documento:** As restrições de documento disponíveis dependem da opção Compatibilidade selecionada.

**Sem criptografia:** Não criptografa nenhuma parte do documento.

**Criptografar todo o conteúdo do documento:** Criptografa o documento e os metadados do documento. Quando essa opção é selecionada, os mecanismos de pesquisa não podem acessar os metadados do documento.

**Criptografar Todo O Conteúdo Do Documento Exceto Os Metadados (Compatível Com Acrobat 6 E Posteriores):** Criptografa o conteúdo de um documento, mas ainda permite que os mecanismos de pesquisa acessem os metadados do documento. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 6.0 ou posterior, Acrobat 7.0 ou posterior, ou Acrobat 9.0 ou posterior.

**Criptografar Somente Anexos De Arquivo (Compatível Com Acrobat 7 E Posteriores):** Os usuários podem abrir o documento sem uma senha, mas devem digitar uma senha para abrir anexos de arquivo. Essa opção está disponível somente quando a opção Compatibilidade está definida como Acrobat 7.0 ou posterior, ou Acrobat 9.0 ou posterior.

Essas configurações definem a segurança de senha:

>[!NOTE]
>
>Se você esquecer uma senha, ela não poderá ser recuperada do documento. É recomendável que você armazene as senhas em outro local seguro, caso as esqueça. Além disso, mantenha uma cópia de backup do documento que não esteja protegida por senha.

**Exigir Uma Senha Para Abrir O Documento:** Ativa as opções de senha.

**Senha para abrir o documento:** Impede que os usuários abram o documento, a menos que digitem a senha especificada. As senhas diferenciam maiúsculas de minúsculas. A Acrobat usa o método RC4 de segurança da RSA Security Inc. para proteger documentos PDF com senha. Se você estiver restringindo a impressão e a edição, é recomendável adicionar uma senha para abrir documentos para aumentar a segurança.

**Digite novamente a senha para abrir o documento:** Garante que a senha para abrir o documento esteja correta.

**Exigir Senha Para Abrir Anexos De Arquivo:** Ativa as opções de senha. Essa opção estará disponível somente quando a opção Compatibilidade estiver definida como Acrobat 7.0 ou posterior, ou Acrobat 9.0 ou posterior, e a opção Restrição de documento estiver definida como Criptografar somente anexos de arquivo.

**Senha de abertura do anexo de arquivo:** Garante que seja necessária uma senha para abrir um anexo de arquivo. Os usuários podem abrir o documento sem uma senha. Essa opção estará disponível somente quando a opção Compatibilidade estiver definida como Acrobat 7.0 ou posterior, ou Acrobat 9.0 ou posterior, e a opção Restrição de documento estiver definida como Criptografar somente anexos de arquivo.

**Digite novamente o anexo do arquivo:** Garante que a senha esteja correta. Essa opção estará disponível somente quando a opção Compatibilidade estiver definida como Acrobat 7.0 ou posterior, ou Acrobat 9.0 ou posterior, e a opção Restrição de documento estiver definida como Criptografar somente anexos de arquivo.

Essas opções configuram as permissões:

**Usar Uma Senha Para Restringir A Impressão E A Edição Do Documento E Suas Configurações De Segurança:** Ativa as restrições nas permissões.

**Senha de permissões:** Restringe a impressão e edição de usuários. Os usuários não podem alterar essas configurações de segurança, a menos que digitem a senha especificada. Não é possível usar a mesma senha usada para a Senha para abrir o documento. Ao definir uma senha de permissões, somente as pessoas que digitarem essa senha poderão alterar as configurações de segurança. Se o documento PDF tiver os dois tipos de senha, qualquer senha o abrirá. No entanto, um usuário só pode definir ou alterar os recursos restritos com a senha de permissões. Se o documento PDF tiver somente a senha de permissão ou se um usuário abrir o documento usando a senha de abertura do documento, o aviso de senha será exibido quando o usuário tentar alterar as configurações de segurança.

**Digite a senha das permissões novamente:** Verifique se a senha das permissões está correta.

**Impressão permitida:** Especifica a qualidade de impressão do documento PDF:

**Nenhum:** Impede os usuários de imprimir o documento.

**Baixa resolução (150 dpi):** Permite que os usuários imprimam o documento com uma resolução não superior a 150 dpi. A impressão pode ser mais lenta porque cada página é impressa como uma imagem bitmap. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) for selecionado.

**Alta resolução:** Permite que os usuários imprimam em qualquer resolução, direcionando a saída vetorial de alta qualidade para PostScript e outras impressoras que oferecem suporte a recursos avançados de impressão de alta qualidade.

**Alterações permitidas:** Define quais ações de edição são permitidas no documento PDF:

**Nenhum:** Impede que os usuários alterem o documento, incluindo o preenchimento de campos de assinatura e formulário.

**Inserir, Excluir E Girar Páginas:** Permite que os usuários insiram, excluam e girem páginas e criem marcadores e páginas em miniatura. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) for selecionado.

**Preencher Campos De Formulário E Assinar Campos De Assinatura Existentes:** Permite que os usuários preencham formulários e adicionem assinaturas digitais. No entanto, os usuários não podem adicionar comentários ou criar campos de formulário. Essa opção só estará disponível se um nível de criptografia alto (Acrobat 5.0, 6.0, 7.0 ou 9.0) for selecionado.

**Comentar, Preencher Campos De Formulário E Assinar Campos De Assinatura Existentes:** Permite que os usuários preencham formulários e adicionem assinaturas digitais e comentários.

**Layout Da Página, Retoque, Preencha Os Campos Do Formulário E Assine Os Campos De Assinatura Existentes:** Permite que os usuários insiram, girem ou excluam páginas e criem marcadores ou imagens em miniatura, preencham formulários e adicionem assinaturas digitais. Essa opção não permite que os usuários criem campos de formulário. Essa opção só estará disponível se um nível de criptografia baixo (Acrobat 3.0) for selecionado.

**Qualquer Página, Exceto A Extração De Páginas:** Permite que os usuários alterem o documento usando qualquer método na Lista de permissões Alterações, exceto remover páginas.

**Ativar A Cópia De Texto, Imagens E Outros Conteúdos:** Permite que os usuários selecionem e copiem o conteúdo do documento PDF. Ele também permite que os utilitários que precisam de acesso ao conteúdo de um arquivo PDF, como o Acrobat Catalog, acessem esse conteúdo. Essa opção só estará disponível se um nível de criptografia alto for selecionado.

**Ativar O Acesso Ao Texto De Dispositivos De Reader De Tela Para Deficientes Visuais:** Permite que os usuários com deficiências visuais leiam o documento usando leitores de tela. No entanto, os usuários não podem copiar ou extrair o conteúdo do documento. Essa opção só estará disponível se um nível de criptografia alto for selecionado.

## Excluir uma configuração de segurança {#delete-a-security-setting}

É possível excluir uma configuração de segurança se ela não for mais necessária. No entanto, as configurações de segurança pré-definidas não podem ser excluídas.

1. No console de administração, clique em **[!UICONTROL Serviços > PDF Generator > Configurações de segurança]**.
1. Marque a caixa de seleção ao lado da configuração a ser excluída. Você pode selecionar várias configurações.
1. Clique em **[!UICONTROL Excluir]** e no **[!UICONTROL Confirmação de exclusão]** clique em **[!UICONTROL Excluir]** novamente.
