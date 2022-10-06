---
title: Configurando uma impressora de rede PDFG (somente Windows)
seo-title: Setting up a PDFG Network Printer (Windows only)
description: Saiba como configurar uma impressora de rede PDFG ( somente Windows )
seo-description: Learn how to set up a PDFG Network Printer ( Windows only )
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# Configurando uma impressora de rede PDFG (somente Windows) {#setting-up-a-pdfg-network-printer-windows-only}

A impressora de rede PDFG permite que os usuários gerem um documento PDF de qualquer aplicativo que suporte impressão. Depois que um usuário instala a impressora de rede PDFG, uma nova impressora chamada *gerador de PDF* é exibida na seção Impressoras do Painel de controle do Windows. Se uma impressora com o mesmo nome já existir, será solicitado ao usuário que forneça outro nome.

A impressão nesta impressora a partir de qualquer aplicativo envia o documento (em formato PostScript) para o PDF Generator, que converte o arquivo PostScript para o PDF. Dependendo de como você configurou o PDF Generator, ele envia o documento PDF para o usuário como um anexo de uma mensagem de email, encaminha o documento PDF para um serviço ou processo de formulários AEM especificado, ou executa ambas as ações.

As etapas a seguir são necessárias para configurar uma impressora de rede PDFG:

1. Defina as configurações de email. (Consulte [Definir configurações de email para a impressora de rede PDFG](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. No console de administração, defina as configurações da impressora de rede PDFG. (Consulte [Defina as configurações da impressora de rede PDFG](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. Certifique-se de que os usuários estejam configurados com um endereço de email válido no banco de dados de formulários AEM e atribua o PDFGUserPermission a cada usuário. <!-- Fix broken link See Setting up and organizing users -->
1. Certifique-se de que o JRE6 de 32 bits esteja instalado nos computadores dos usuários.
1. Instale a impressora nos computadores dos usuários. (Consulte [Instale a impressora de rede PDFG no computador de um usuário](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## Definir configurações de email para a impressora de rede PDFG {#configure-email-settings-for-pdfg-network-printer}

1. No console de administração, clique em Serviços > Aplicativos e Serviços > Gerenciamento de Serviços.
1. Na página Gerenciamento de serviços , clique em provider.email_sendmail_service, especifique as configurações SMTP e clique em Salvar.

## Defina as configurações da impressora de rede PDFG {#configure-the-pdfg-network-printer-settings}

1. No console de administração, clique em Serviços > Gerador de PDF > Impressora de rede PDFG
1. Nas listas Configurações do Adobe PDF e Configurações de segurança , selecione as opções a serem aplicadas ao PDF gerado. Para obter detalhes sobre essas configurações, consulte [Definição das configurações do Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) e [Definição das configurações de segurança](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Para enviar os PDF convertidos de volta aos usuários, selecione a opção Enviar email para o arquivo de PDF convertido de volta ao usuário e especifique as seguintes informações:

   * O endereço de email a ser usado para enviar PDF aos usuários
   * O assunto da mensagem de email
   * O cabeçalho, o corpo e o rodapé da mensagem de email. Na mensagem de email, &lt;receivername> é substituído pelo nome completo do usuário que imprimiu o documento.

1. Para enviar os PDF convertidos para um serviço ou processo de formulários AEM, selecione a opção Encaminhar o PDF convertido para o serviço ou processo de AEM especificados e especifique as seguintes informações:

   * O nome do serviço a ser chamado
   * O nome da operação do serviço a ser chamado
   * O nome do parâmetro de entrada, conforme especificado no arquivo component.xml do serviço ou processo. O documento PDF será usado como um valor para esse parâmetro de entrada.

1. Clique em Salvar.

Para reverter para o texto de email padrão original, clique em Restaurar conteúdo de email.

## Instale a impressora de rede PDFG no computador de um usuário {#install-pdfg-network-printer-on-a-user-s-computer}

Os usuários que tiverem a função Administrador PDFG ou Usuário PDFG poderão instalar uma impressora de rede PDFG. Você deve ter um JDK de 32 bits instalado no computador.

1. (Administradores PDFG) No console de administração, clique em Serviços > Gerador de PDF > Impressora de rede PDFG.

   (Usuários do PDFG) Vá para `http(s)://[host]:'port'/pdfgui` e clique no link em PDFG Network Printer Installation (Instalação da impressora de rede PDFG).

1. Em PDFG Network Printer Installation (Instalação da impressora de rede PDFG), clique no link . Quando solicitado a fornecer informações da conta de usuário, especifique o nome de usuário e a senha usados na etapa 1 para fazer logon. Será exibida uma mensagem informando que a impressora foi instalada com êxito.

   ***observação **: Se a senha do usuário mudar, os usuários precisarão reinstalar a impressora de rede PDFG em seus computadores. Não é possível atualizar a senha do console de administração.*

1. Clique em OK.
