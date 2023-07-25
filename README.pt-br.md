**Como criar um ISO personalizado do Windows 10 com software pré-instalado.**

Software Necessário:

**Windows ADK para Windows 10 (Ferramentas de Implantação):** Certifique-se de baixar a versão correta do Windows ADK para a sua versão do Windows 10 (por exemplo, Windows 10 versão 1909, 20H2, etc.)
   - [Baixar Windows ADK](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit)

**Rufus (Para Criar uma Unidade USB Bootável):**
   - [Baixar Rufus](https://rufus.ie/)

1. **Formatar uma Máquina e Instalar o Software:**
   - Formate a máquina e crie uma conta local com o nome desejado.
   - Instale os programas necessários e remova os aplicativos desnecessários (bloatware).

2. **Executar a Limpeza de Disco:**
   - Abra a Limpeza de Disco (busque por "Limpeza de Disco" no menu Iniciar).
   - Selecione os arquivos do sistema que deseja limpar e prossiga.

3. **Reduzir o Tamanho da Unidade C:\ e Criar uma Nova Partição:**
   - Pressione a tecla Windows + X e selecione "Gerenciamento de Disco".
   - Clique com o botão direito na unidade C:\ (geralmente rotulada como "OS (C:)") e escolha "Reduzir Volume".
   - Insira o tamanho desejado para reduzir a partição e crie um espaço não alocado.
   - Clique com o botão direito no espaço não alocado e selecione "Novo Volume Simples".
   - Atribua a letra da unidade "D" e rotule-a como "Image".

4. **Criar Pastas na Unidade D:\:**
   - Abra o Explorador de Arquivos (Win + E) e navegue até a unidade D:\.
   - Clique com o botão direito em uma área vazia e escolha "Novo" > "Pasta".
   - Nomeie a pasta como "Scratch".
   - Crie outra pasta chamada "iso_files".

5. **Desligar a Máquina:**
   - Salve seu trabalho e feche todos os aplicativos.
   - Clique em Iniciar > Energia > Desligar.

6. **Iniciar a Partir da Unidade USB do Windows e Abrir o Prompt de Comando:**
   - Insira a unidade USB do Windows e reinicie a máquina.
   - Acesse a BIOS ou menu de inicialização (geralmente F2, F12, Esc ou Del) durante a inicialização.
   - Selecione a unidade USB como dispositivo de inicialização.
   - Na tela de configuração do Windows, pressione Shift + F10 para abrir o Prompt de Comando.

7. **Capturar a Imagem no Formato .wim:**
   - No Prompt de Comando, execute o seguinte comando:
     ```
     dism /capture-image /imagefile:D:\install.wim /capturedir:C:\ /ScratchDir:D:\Scratch /name:Windows10 /compress:maximum /checkintegrity /verify /bootable
     ```

8. **Montar a ISO do Windows e Copiar os Conteúdos:**
   - Monte uma ISO do Windows (correspondente à versão instalada) na sua máquina.
   - Copie o arquivo "Windows10.wim" da ISO montada para "D:\iso_files\Sources" e substitua o arquivo existente.

9. **Baixar e Instalar o Windows ADK:**
   - Baixe o Windows ADK para Windows 10 [no site da Microsoft](https://developer.microsoft.com/en-us/windows/hardware/windows-assessment-deployment-kit), caso ainda não tenha feito.

10. **Executar as Ferramentas de Implantação como Administrador:**
    - Execute o "Ambiente de Ferramentas de Implantação e Imagem" como administrador.

11. **Criar o ISO Personalizado:**
    - No prompt aberto, execute o seguinte comando:
      ```
      oscdimg.exe -m -o -u2 -udfver102 -bootdata:2#p0,e,bd:\iso_files\boot\etfsboot.com#pEF,e,bd:\iso_files\efi\microsoft\boot\efisys.bin d:\iso_files d:\Windows10Inside.iso
      ```

12. **Usar o Rufus para Criar a Unidade USB Bootável:**
    - Use a ferramenta Rufus para criar uma unidade USB bootável usando a ISO personalizada.

13. **Utilize a unidade USB bootável em suas máquinas 🙂**
