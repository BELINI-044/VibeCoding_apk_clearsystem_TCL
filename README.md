# ClearSystem TCL

**Launcher de código aberto para TCL Android TV, baseado no Free My TV, com tema escuro, barra de apps e atalhos para HDMI, TV aberta e ajustes.**

Personalização do [Free My TV](https://github.com/simbasjungles/free-my-tv), com visual inspirado nas barras de aplicativos de TVs, fundo noturno azul-petróleo e um painel que reúne entradas e ajustes da TV.

Desenvolvido a partir da experiência com uma **TCL 50P8M, Android TV 9**, mantendo o caminho de volta à interface original.

## Downloads

| Arquivo | Para que serve |
| --- | --- |
| **[Baixar atualização v3 para Windows](https://github.com/BELINI-044/VibeCoding_apk_clearsystem_TCL/raw/refs/heads/downloads/FreeMyTV-Atualizacao-v3.zip)** | Pacote com APK, ADB oficial e instalador automático. |
| [Código-fonte da personalização v3](https://github.com/BELINI-044/VibeCoding_apk_clearsystem_TCL/raw/refs/heads/downloads/FreeMyTV-ClearSystem-v3-source.zip) | Código Android, arte de fundo, scripts e arquivos do projeto-base para inspeção e compilação. Não inclui chaves privadas. |

Os pacotes ficam na branch [`downloads`](https://github.com/BELINI-044/VibeCoding_apk_clearsystem_TCL/tree/downloads). Se o navegador abrir a página do arquivo, use **Download raw file**, o botão com a seta para baixo. Os arquivos antigos dessa branch são históricos; as instruções abaixo usam a **v3**.

## O que a v3 oferece

- **Tema escuro e fundo noturno:** paisagem em azul-petróleo, com a área do relógio e da barra de aplicativos livre de detalhes fortes. A imagem é carregada localmente, sem download na TV nem animação contínua de fundo.
- **Aplicativos na barra inferior:** o selecionado cresce, recebe um contorno branco e mostra o nome abaixo do ícone.
- **UNITV primeiro, quando instalado:** o foco inicial fica no primeiro aplicativo disponível. O UNITV e outros serviços de streaming não acompanham este pacote.
- **Painel Recursos da TV:** acesso à TV aberta, entradas HDMI e menus de armazenamento, som e ajustes gerais que o Android permitir abrir. Uma opção sem acesso fica indisponível; o painel não muda os ajustes automaticamente.
- **Configuração inicial brasileira:** português, Celsius, BRL e cidade de Cianorte/PR. A cidade pode ser alterada nas configurações do Free My TV.
- **Interface mais limpa:** relógio menor e cotações ocultas inicialmente. Elas podem ser reativadas nas configurações.

Esta personalização **mantém o mapeamento existente do controle**, inclusive o controle de Xbox utilizado no aparelho de referência. Não adiciona atalhos novos aos botões do controle.

## Compatibilidade e estado da versão

| Item | Situação |
| --- | --- |
| Aparelho de referência | TCL 50P8M; o Android informa o modelo `BeyondTV`. |
| Sistema observado | Android TV 9 / API 28; apps ARM de 32 bits (`armeabi-v7a`). |
| Android mínimo do aplicativo | Android 8 / API 26, conforme o projeto-base. Isso não garante compatibilidade com todo firmware. |
| Versões anteriores desta personalização | Instaladas e observadas funcionando na TV de referência. |
| **v3** | **Compilada e verificada; a validação visual e funcional na TV ainda está pendente.** |
| Outras TCL e outras marcas | Não validadas por esta personalização. Confirme os requisitos do projeto-base. |

As verificações locais da v3 passaram: compilação com **JDK 17 e SDK 34**, assinatura APK igual à da versão anterior, catálogos de tradução com **410 chaves**, **48 verificações de controle remoto** e demais verificações do projeto. O instalador passou em **17 cenários simulados** no PowerShell 7/Linux; o pacote adaptado para escolher o IP ainda não foi executado em Windows real.

Este projeto personaliza a tela inicial e facilita o acesso a funções existentes. Não é uma ROM, não faz root, não formata a TV e não habilita capacidades físicas ausentes. O diagnóstico realizado não confirmou Picture-in-Picture nem HDR; a resolução da interface Android não deve ser confundida com a resolução do painel.

## Instalar ou atualizar pelo Windows

### 1. Preparar a TV

1. Deixe a TV ligada e o computador conectado à mesma rede.
2. Ative o modo de desenvolvedor nas configurações da TV: em **Sobre**, pressione sete vezes o item de compilação do Android. Os nomes variam conforme o firmware.
3. Em **Opções do desenvolvedor**, ative **Depuração USB**.
4. Anote o **IP da TV** nas configurações de rede. O exemplo `192.168.1.102` é do aparelho de referência; cada pessoa deve usar o IP da própria TV.

### 2. Executar o pacote

1. Baixe o ZIP da v3 e escolha **Extrair tudo → Extrair**.
2. Abra a pasta extraída e dê dois cliques em **`Atualizar-FreeMyTV.cmd`**. Não é necessário executar como administrador.
3. Informe o IP da sua TV. Pressione Enter para aceitar `192.168.1.102` **somente se esse for o IP correto**.
4. Se a TV pedir autorização de depuração, aceite e marque **Sempre permitir**. Se o instalador informar falta de autorização, abra-o novamente após aceitar.
5. Aguarde **`Success - atualizacao instalada!`** e pressione **Home** no controle da TV.

O instalador confere o SHA-256 do APK antes de instalar, verifica a conexão e executa `adb install -r`. Ele não desinstala o app nem limpa suas configurações. Ao terminar com sucesso, tenta desconectar somente essa TV do ADB do computador, liberando a conexão para a autorização do próprio Free My TV.

Não execute o arquivo de dentro do ZIP: o APK e a pasta `platform-tools` precisam estar juntos do instalador na pasta extraída. O Tailscale não é necessário para este procedimento local. O ADB incluído é o Platform Tools oficial para Windows, com o arquivo original verificado pelo checksum publicado pelo Google.

### 3. Ativar a tela inicial pela primeira vez

Se o Free My TV já estiver ativo, uma atualização não exige escolher o modo novamente. Em uma primeira instalação:

1. Na TV, abra **Free My TV → Tela inicial / Home Screen → Free My TV**.
2. Aceite a nova autorização de depuração que o próprio app pedir e marque **Sempre permitir**.
3. Aguarde o processo terminar e pressione Home.

A troca usa o mecanismo do projeto-base: muda a tela inicial e, quando configurado, o protetor de tela; alguns aplicativos promocionais podem ser desativados, conforme o firmware. Eles não são desinstalados. Em Google TV, a busca por voz de filmes e séries pode ser afetada. Consulte também o [guia original de instalação](https://github.com/simbasjungles/free-my-tv#install).

### TCL: execução em segundo plano

Alguns firmwares TCL exigem a permissão `AUTO_START` ou `APP_AUTO_START`. Se for necessário aplicá-la, abra o PowerShell na pasta extraída e execute:

```powershell
$tv = Read-Host "IP da sua TV"
.\platform-tools\adb.exe connect "${tv}:5555"
.\platform-tools\adb.exe -s "${tv}:5555" shell "appops set io.freemytv AUTO_START allow || appops set io.freemytv APP_AUTO_START allow"
.\platform-tools\adb.exe disconnect "${tv}:5555"
```

Na TCL Android 9 de referência, ambos os nomes retornaram **`Unknown operation string`**, e as versões anteriores funcionaram sem essa permissão. Essa resposta significa que o firmware não reconhece a operação; não indica falha na instalação do APK. O instalador não altera essas permissões automaticamente.

## Usar e personalizar

- **Abrir aplicativos:** navegue pela barra e confirme a seleção como já faz com seu controle.
- **Recursos da TV:** na tela inicial, pressione para baixo e escolha **Recursos da TV**. O atalho também aparece nos botões superiores quando a lista padrão está em uso.
- **Entradas HDMI:** o painel usa as entradas informadas pelo Android. Uma entrada sem sinal ainda pode ser selecionada.
- **Cidade e idioma:** abra as configurações da tela inicial e ajuste para sua localização.
- **Tema:** a v3 aplica o tema escuro uma vez na atualização. Depois, a escolha feita pelo usuário nas configurações prevalece.
- **Sugestões de filmes:** são opcionais e exigem a chave TMDB do próprio usuário, adicionada privadamente nas configurações do app. Nenhuma chave acompanha a distribuição.

## Voltar à interface original

Na TV, abra **Free My TV → Tela inicial / Home Screen → Original** e aguarde terminar.

**Volte para Original antes de desinstalar o Free My TV.** Desinstalar enquanto o modo personalizado está ativo pode deixar aplicativos do sistema desativados. O mecanismo Original e a proteção de recuperação do projeto-base foram mantidos nesta personalização.

## Resolver problemas

| Mensagem ou situação | Próximo passo |
| --- | --- |
| ADB ou APK não encontrado | Extraia o ZIP completo e abra o instalador na pasta extraída. |
| IP inválido | Informe o IPv4 local mostrado pela TV, sem `http://`, sem porta e sem espaços. |
| Sem conexão / TV offline | Confira o IP, a mesma rede e a depuração USB. |
| Falta de autorização | Aceite a depuração na TV e execute novamente. |
| APK não corresponde à atualização | Baixe novamente o pacote completo; a verificação de integridade interrompe a instalação. |
| Assinatura incompatível | Pare e verifique a origem da versão instalada. Não desinstale o app com o modo personalizado ativo. |
| Falta de espaço | Confira o armazenamento da TV antes de tentar novamente. |
| Instalação aguardando confirmação | Confira a mensagem apresentada na TV; o instalador não desativa as proteções do Android. |
| Um menu aparece indisponível | O firmware pode não expor esse menu ou pode exigir uma permissão que o app não possui. |

Para relatar um problema, informe o modelo, a versão do Android, a versão do app e a mensagem exibida. Não publique senhas, chaves de API nem relatórios pessoais sem revisar o conteúdo. O diagnóstico usado durante o desenvolvimento foi apenas de leitura; os recursos declarados pelo Android ainda exigem testes práticos.

## Integridade da v3

APK `FreeMyTV-v3.apk`, versão Android **`1.3-cianorte.3`**, código **6**:

```text
88898651cbb494677050dd287a569e13172ed2e0238f41e617eeec9205bb6249
```

ZIP `FreeMyTV-Atualizacao-v3.zip`:

```text
e0b26a59691dbd73adcc4b3228e0848a09783ae65c076cbeb243ef54096af563
```

## Código-fonte e créditos

O código desta personalização está no ZIP de fontes indicado em Downloads. A base é o commit [`a6c128da484d8824064f4be143913e9fce0b2f07`](https://github.com/simbasjungles/free-my-tv/tree/a6c128da484d8824064f4be143913e9fce0b2f07) do **Free My TV**, com alterações na interface, preferências e painel de recursos. O arquivo `PERSONALIZACAO.md` do pacote descreve o perfil desta versão; o `README.md` original e os scripts de compilação foram preservados.

Para compilar o Android, use JDK 17, SDK Platform 34 e Build Tools 34.0.0, configure seu `config.properties` e execute `bash build.sh`. Não há Gradle. A compilação própria gera sua própria chave de assinatura, que deve ser guardada privadamente; ela não substitui automaticamente uma instalação assinada por outra chave. Nenhum keystore ou segredo está incluído nos fontes.

- **Projeto-base:** [simbasjungles/free-my-tv](https://github.com/simbasjungles/free-my-tv).
- **Personalização e distribuição:** [R4f4e1-cyber](https://github.com/R4f4e1-cyber).
- **Licença do código:** [MIT](LICENSE), preservando os créditos dos colaboradores do Free My TV.
- **Demais componentes:** fontes, ícones, logos e ferramentas mantêm suas licenças e avisos próprios, incluídos nos respectivos arquivos e pacotes.

Projeto independente, sem afiliação com TCL, Google, Samsung ou os aplicativos exibidos. Assinaturas e acesso a conteúdo pertencem aos serviços utilizados.
