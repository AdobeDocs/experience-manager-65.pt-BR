---
title: Configuração de uma impressora de rede PDFG (somente Windows)
description: Saiba como configurar uma impressora de rede PDFG (somente Windows )
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: c3fc159e-2677-4b71-b0b2-2feaf69e1a32
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 0%

---

# Configuração de uma impressora de rede PDFG (somente Windows) {#setting-up-a-pdfg-network-printer-windows-only}

>[!NOTE]
> 
> Verifique se o usuário tem privilégios de administrador para acessar o console do administrador.

A impressora de rede PDFG permite que os usuários gerem um documento PDF a partir de qualquer aplicativo que suporte impressão. Depois que um usuário instala a impressora de rede PDFG, uma nova impressora chamada *gerador de PDF* é exibida na seção Impressoras do Painel de Controle do Windows. Se já existir uma impressora com o mesmo nome, o usuário será solicitado a fornecer outro nome.

Imprimir para esta impressora a partir de qualquer aplicativo envia o documento (no formato PostScript) para o PDF Generator, que converte o arquivo PostScript para o PDF. Dependendo de como você configurou o PDF Generator, ele envia o documento PDF para o usuário como um anexo de uma mensagem de email, encaminha o documento PDF AEM para um serviço ou processo de formulários especificado ou executa ambas as ações.

As seguintes etapas são necessárias para configurar uma impressora de rede PDFG:

1. Defina as configurações de email. (Consulte [Definir configurações de email para a Impressora de Rede PDFG](setting-pdfg-network-printer-windows.md#configure-email-settings-for-pdfg-network-printer).)
1. No console de administração, defina as configurações de Impressora de rede PDFG. (Consulte [Definir as configurações da Impressora de Rede PDFG](setting-pdfg-network-printer-windows.md#configure-the-pdfg-network-printer-settings).)
1. Verifique se os usuários estão configurados com um endereço de email válido no banco de dados de formulários AEM e atribua o PDFGUserPermission a cada usuário. <!-- Fix broken link See Setting up and organizing users -->
1. Verifique se o JRE6 de 32 bits está instalado nos computadores dos usuários.
1. Instale a impressora nos computadores dos usuários. (Consulte [Instalar impressora de rede PDFG no computador de um usuário](setting-pdfg-network-printer-windows.md#install-pdfg-network-printer-on-a-user-s-computer).)

## Definir configurações de email para a impressora de rede PDFG {#configure-email-settings-for-pdfg-network-printer}

1. No console de administração, clique em Serviços > Aplicativos e serviços > Gerenciamento de serviços.
1. Na página Gerenciamento de serviço, clique em provider.email_sendmail_service, especifique as configurações de SMTP e clique em Salvar.

## Definir as configurações de impressora de rede PDFG {#configure-the-pdfg-network-printer-settings}

1. No console de administração, clique em Serviços > PDF Generator > Impressora de rede PDFG
1. Nas listas Configurações do Adobe PDF e Configurações de segurança, selecione as opções a serem aplicadas ao PDF gerado. Para obter detalhes sobre essas configurações, consulte [Definindo configurações do Adobe PDF](/help/forms/using/admin-help/configuring-pdf-settings.md#configuring-adobe-pdf-settings) e [Definindo configurações de segurança](/help/forms/using/admin-help/configuring-security-settings.md#configuring-security-settings).
1. Para enviar os PDF convertidos de volta aos usuários, selecione a opção Enviar o arquivo de PDF convertido de volta para o usuário e especifique as seguintes informações:

   * O endereço de email a ser usado para enviar PDF aos usuários
   * O assunto da mensagem de email
   * O cabeçalho, o corpo e o rodapé da mensagem de email. Na mensagem de email, &lt;receiverName> é substituído pelo nome completo do usuário que imprimiu o documento.

1. Para enviar os PDF convertidos para um serviço ou processo do AEM Forms, selecione a opção Encaminhar o PDF AEM convertido para o serviço ou processo do Forms especificado e especifique as seguintes informações:

   * O nome do serviço a ser chamado
   * O nome da operação do serviço a ser chamado
   * O nome do parâmetro de entrada, conforme especificado no arquivo component.xml do serviço ou processo. O documento PDF é usado como um valor para esse parâmetro de entrada.

1. Clique em Salvar.

Se quiser reverter para o texto de email padrão original, clique em Restaurar conteúdo de email.

## Instalar impressora de rede PDFG no computador de um usuário {#install-pdfg-network-printer-on-a-user-s-computer}

Usuários que possuem as funções de Administrador do PDFG ou Usuário do PDFG podem instalar uma impressora de rede PDFG. Você deve ter um JDK de 32 bits instalado no computador.

1. (Administradores de PDFG) No console de administração, clique em Serviços > PDF Generator > Impressora de rede PDFG.

   (Usuários de PDFG) Vá para `http(s)://[host]:'port'/pdfgui` e clique no link em Instalação de impressora de rede PDFG.

1. Em Instalação da impressora de rede PDFG, clique no link. Quando forem solicitadas informações da conta do usuário, especifique o nome de usuário e a senha usados na etapa 1 para efetuar login. Será exibida uma mensagem informando que a impressora foi instalada com êxito.

   ***observação **: se a senha do usuário for alterada, os usuários deverão reinstalar a Impressora de Rede PDFG em seus computadores. Não é possível atualizar a senha no console de administração.*

1. Clique em OK.
