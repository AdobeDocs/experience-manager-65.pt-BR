---
title: Configuração de uma impressora de rede PDFG (somente Windows)
seo-title: Configuração de uma impressora de rede PDFG (somente Windows)
description: Saiba como configurar uma impressora de rede PDFG ( somente Windows )
seo-description: Saiba como configurar uma impressora de rede PDFG ( somente Windows )
uuid: 13b8481e-5ef0-4a07-9602-7bc4d9e05dd4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7620e5e4-022e-49b2-8cfe-d5eec8ab99d7
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Configuração de uma impressora de rede PDFG (somente Windows) {#setting-up-a-pdfg-network-printer-windows-only}

A impressora de rede PDFG permite que os usuários gerem um documento PDF a partir de qualquer aplicativo compatível com impressão. Depois que um usuário instala a impressora de rede PDFG, uma nova impressora chamada gerador *de* PDF é exibida na seção Impressoras do Painel de controle do Windows. Se uma impressora com o mesmo nome já existir, o usuário será solicitado a fornecer outro nome.

A impressão nesta impressora a partir de qualquer aplicativo envia o documento (em formato PostScript) para o Gerador de PDF, que converte o arquivo PostScript em PDF. Dependendo de como você configurou o Gerador de PDF, ele envia o documento PDF para o usuário como um anexo para uma mensagem de email, encaminha o documento PDF para um serviço ou processo de formulários AEM especificado ou executa ambas as ações.

As etapas a seguir são necessárias para configurar uma impressora de rede PDFG:

1. Defina as configurações de email. (Consulte [Definir configurações de email para a impressora](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer)de rede PDFG.)
1. No console de administração, defina as configurações da impressora de rede PDFG. (Consulte [Configurar as configurações](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings)da impressora de rede PDFG.)
1. Certifique-se de que seus usuários estejam configurados com um endereço de email válido no banco de dados de formulários AEM e atribua PDFGUserPermission a cada usuário. <!-- Fix broken link See Setting up and organizing users -->
1. Verifique se o JRE6 de 32 bits está instalado nos computadores dos usuários.
1. Instale a impressora nos computadores dos usuários. (Consulte [Instalar impressora de rede PDFG no computador](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer)do usuário.)

## Definir configurações de email para impressora de rede PDFG {#configure-email-settings-for-pdfg-network-printer}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviços, clique em provider.email_sendmail_service, especifique as configurações de SMTP e clique em Salvar.

## Defina as configurações da impressora de rede PDFG {#configure-the-pdfg-network-printer-settings}

1. No console de administração, clique em Serviços > Gerador de PDF > Impressora de rede PDFG
1. Nas listas Configurações do Adobe PDF e Configurações de segurança, selecione as opções a serem aplicadas ao PDF gerado. Para obter detalhes sobre essas configurações, consulte [Definição das configurações](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) do Adobe PDF e [Definição das configurações](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings)de segurança.
1. Para enviar os PDFs convertidos de volta aos usuários, selecione a opção Enviar o arquivo PDF convertido de volta para o usuário por email e especifique as seguintes informações:

   * O endereço de email para enviar PDFs aos usuários
   * O assunto da mensagem de email
   * O cabeçalho, o corpo e o rodapé da mensagem de email. Na mensagem de e-mail, o &lt;receiptName> é substituído pelo nome completo do usuário que imprimiu o documento.

1. Para enviar os PDFs convertidos para um serviço ou processo de formulários AEM, selecione a opção Encaminhar o PDF convertido para o serviço ou processo de formulários AEM especificado e especifique as seguintes informações:

   * O nome do serviço a ser chamado
   * O nome da operação do serviço a ser chamado
   * O nome do parâmetro de entrada, conforme especificado no arquivo component.xml do serviço ou processo. O documento PDF será usado como um valor para esse parâmetro de entrada.

1. Clique em Salvar.

Se desejar reverter para o texto padrão original do email, clique em Restaurar conteúdo do email.

## Instale a impressora de rede PDFG no computador de um usuário {#install-pdfg-network-printer-on-a-user-s-computer}

Os usuários que têm a função Administrador do PDFG ou Usuário do PDFG podem instalar uma impressora de rede PDFG. Você deve ter um JDK de 32 bits instalado no computador.

1. (Administradores PDFG) No console de administração, clique em Serviços > Gerador de PDF > Impressora de rede PDFG.

   (Usuários PDFG) Vá até `http(s)://[host]:'port'/pdfgui` e clique no link em PDFG Network Printer Installation (Instalação da impressora em rede PDFG).

1. Em Instalação da impressora em rede PDFG, clique no link. Quando solicitado a fornecer informações de conta de usuário, especifique o nome de usuário e a senha usados na etapa 1 para fazer logon. Será exibida uma mensagem informando que a impressora foi instalada com êxito.

   ***observação **: Se a senha do usuário for alterada, os usuários precisarão reinstalar a impressora de rede PDFG em seus computadores. Não é possível atualizar a senha do console de administração.*

1. Clique em OK.

