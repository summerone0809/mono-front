##必要なソフトウェアのインストール

以下、ソフトウェアをインストールする
・Chocolatey (Windows Only)
・Git
・Node.js
・pnpm
・Docker
・VSCode

##インストール手順（Windows）

1.Windows PowerShell を管理者として起動し、以下のコマンドを実行する。

    Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol =
    [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

2.コマンドプロンプトを管理者として起動し、以下のコマンドを実行する

    choco install -y git
    choco install -y docker-desktop
    choco install -y vscode
    choco install -y pnpm
    choco install -y nodejs-lts

3.VSCode 拡張機能

    code --install-extension dbaeumer.vscode-eslint
    code --install-extension josevseb.google-java-format-for-vs-code
    code --install-extension vscjava.vscode-lombok
    code --install-extension mhutchie.git-graph
    code --install-extension ms-vscode.js-debug
    code --install-extension svelte.svelte-vscode
    code --install-extension redhat.vscode-quarkus
    code --install-extension sonarsource.sonarlint-vscode
    code --install-extension vscjava.vscode-java-pack

##開発環境実行手順

1.クローンしたプロジェクトを VSCode で起動
　コマンドプロンプトで以下コマンド実行

    code {クローンしたプロジェクトを配置したフォルダパス}/mono-cl

2.VSCode の Terminal で以下のコマンドを実行する。

    pnpm dev --open

3.ブラウザが起動する（http://localhost:5173）

4.mono-sv プロジェクトをクローンし、README に従って、サーバーの開発環境手順を実施する。
