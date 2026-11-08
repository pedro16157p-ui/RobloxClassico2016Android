# Roblox Classic 2016 — Android ARM64 fan rebuild

Aplicativo Android independente e não afiliado à Roblox Corporation. Esta é uma reconstrução de preservação histórica; não acessa contas, jogos, APIs ou servidores oficiais.

## O que foi criado nesta entrega

- Projeto Android Studio nativo em Kotlin.
- Activity Android com WebView incorporada (o app abre diretamente, sem lançar o navegador).
- Arquivos HTML/CSS/JavaScript do projeto anterior empacotados em `app/src/main/assets/site/`.
- Armazenamento DOM/LocalStorage habilitado para dados locais demonstrativos.
- Navegação Voltar, viewport mobile e refinamentos de toque.
- Gradle configurado para `arm64-v8a`, `minSdk 23`, `targetSdk 35`.
- Ícone vetorial simples de identidade própria e tela sem ActionBar.

## Estado real das funcionalidades

A camada Android é um contêiner nativo funcional para a experiência web local. O conteúdo herdado atualmente oferece cadastro/login locais, perfil, catálogo demonstrativo, inventário, amizades/grupos locais e três protótipos 2D jogáveis (Natural Disaster Survival, Work at a Pizza Place e Jailbreak). Os outros sete jogos ainda não estão implementados como jogos. Não há backend compartilhado, multiplayer real, avatares R6 3D ou sincronização entre dispositivos.

As senhas novas são derivadas com PBKDF2-SHA-256 no JavaScript Web Crypto. A disponibilidade de Web Crypto no WebView deve ser confirmada no aparelho-alvo; se não estiver disponível, o cadastro/login informa o erro em vez de armazenar a senha em texto puro. Não use senhas reutilizadas nesta demonstração local.

## Abrir no Android Studio

1. Extraia o ZIP.
2. Abra a pasta `RobloxClassic2016Android` no Android Studio (versão recente compatível com AGP 8.7.3).
3. Instale Android SDK Platform 35 e Android Build Tools correspondentes pelo SDK Manager.
4. Aguarde o Gradle Sync.
5. Conecte um Android ARM64 ou inicie um emulador compatível.
6. Use **Build > Build Bundle(s) / APK(s) > Build APK(s)** ou execute no terminal:

```bash
gradle :app:assembleDebug
```

O APK de depuração será criado em:

`app/build/outputs/apk/debug/app-debug.apk`

Esse APK debug é assinado automaticamente com a chave de depuração e pode ser instalado para testes. Para instalar via ADB:

```bash
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

## Gerar APK release assinado

Crie uma keystore própria e configure `signingConfigs` no `app/build.gradle.kts` antes de publicar. Não coloque senhas de keystore no repositório. A versão atual não inclui uma chave de publicação.

## Arquitetura e ABI

`abiFilters` está definido como `arm64-v8a`. Como o app não contém bibliotecas nativas NDK, a ABI é uma restrição de empacotamento/compatibilidade; não significa que os jogos JavaScript foram convertidos em código ARM nativo. Não há APK universal nesta entrega.

## Limitações desta máquina de desenvolvimento

O ambiente usado para preparar este projeto não contém Android SDK nem Gradle instalado. Por isso, não foi possível compilar ou executar o APK aqui. O arquivo ZIP contém o projeto-fonte Android para compilação no Android Studio/ambiente com SDK 35. Nenhum APK fictício foi criado ou renomeado.
