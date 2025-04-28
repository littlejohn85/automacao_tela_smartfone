# automacao_tela_smartfone

Automação de Smartphone por Voz usando ADB via Termux
Este projeto foi desenvolvido diretamente no Termux (um terminal Linux para Android), utilizando Python para capturar comandos de voz e executar ações na tela do smartphone via ADB. A ideia é simples: você fala, o sistema entende e simula um toque na tela automaticamente.

Como Funciona
O script escuta sua voz, reconhece comandos como "Aceito" ou "Negar", e envia comandos ADB para clicar em pontos específicos da tela. Tudo isso sem tocar fisicamente no aparelho.

Pré-requisitos
Smartphone Android com:

Opções de Desenvolvedor ativadas

Depuração USB e Depuração via Wi-Fi ativadas

Aplicativo Termux instalado

Pacotes instalados no Termux:

bash
Copiar
Editar
pkg install python
pip install SpeechRecognition
pip install PyAudio
pkg install termux-api
pkg install adb
Conectando o ADB via Wi-Fi no Termux
Ative a Depuração USB e Depuração via Wi-Fi no seu Android (em Opções de Desenvolvedor).

Conecte o celular ao PC ou ative o ADB interno no Termux usando:

bash
Copiar
Editar
adb tcpip 5555
Descubra o IP do celular no Wi-Fi (configurações > Wi-Fi > Detalhes).

Conecte:

bash
Copiar
Editar
adb connect IP_DO_SEU_CELULAR:5555
Exemplo:

bash
Copiar
Editar
adb connect 192.168.1.100:5555
A resposta deve ser: connected to IP.

Após isso, o Termux consegue enviar comandos ADB direto para o smartphone via rede Wi-Fi!

Descobrindo as Coordenadas da Tela
Para saber onde clicar:

Ative "Mostrar Toques" nas Opções de Desenvolvedor.

Use o comando:

bash
Copiar
Editar
adb shell getevent
ou tire prints da tela:

bash
Copiar
Editar
adb shell screencap /sdcard/screen.png
adb pull /sdcard/screen.png
e veja manualmente no PC.

Aplicativos como Touch Coordinates também ajudam a ver X/Y em tempo real.

Estrutura do Script
ouvir_comando(): Usa o microfone para escutar e transformar sua voz em texto.

clicar_na_tela(x, y): Envia um comando ADB simulando um toque no ponto X/Y da tela.

processar_comando(comando): Analisa se você falou "aceito" ou "negar" e executa o clique correto.

Loop infinito para ficar ouvindo comandos continuamente.

