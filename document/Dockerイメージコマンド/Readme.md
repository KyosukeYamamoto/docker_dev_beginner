# Dockerイメージのビルド
アプリケーションとDockerfileが用意できたらdocker image buildコマンドでDockerイメージを作成する。

`docker image build -t イメージ名[:タグ名] Dockerfile配置ディレクトリのパス`
- **docker image build**
	- Dockerイメージを作成するためのコマンド。
	- **`-t`オプション**：任意のイメージ名を指定できるオプション。基本的につける。付けなかった場合、ハッシュ値が与えられる。今後イメージ名を使うことが多くなるため、イメージ名をつけることをおすすめする。
		- 例　`docker build -t example/echo:latest .`
			- イメージ名：example/echo
			- タグ名　　：latest
			- ディレクトリパス："."(カレントディレクトリ)
	- **-fオプション**：ビルドに必要なDockerfile名の指定。デフォルト（オプションなし）ではDockerfileというファイル名を参照する。
		- 例 `docker build -f Dockerfile-test -t example/echo:latest .`
			- Dockerfile名：Dockerfile-test
			- イメージ名：example/echo
			- タグ名　　：latest
			- ディレクトリパス："."(カレントディレクトリ)
	- **--pullオプション**：Dockerfile内で指定したベースイメージをビルドするたびにリモートのリポジトリから再取得させる。通常、一度取得したDockerイメージは削除しない限りホスト内に保持される。docker image build実行時に毎回リモートのリポジトリから取得されるわけではない。
		- 例 `docker build --pull=true -t example/echo:latest .`
			- Dockerfile内でgolangイメージをベースとしている場合、実行されるたびにそのイメージが取得される。

# イメージ操作のコマンド
- **docker image ls**
	- 作成されたイメージを一覧表示し、REPOSITORY, TAG, IMAGE ID, CREATED, SIZEを表示する。
- **docker search [option] 検索キーワード**
	- DockerHubのレジストリに登録されているリポジトリを検索できる。
	- **--limit 表示数 オプション**：一覧に一度に表示されるイメージの数を指定できる。
		- 例 `docker search --limit 5 mysql`
		- DockerHubのリモートリポジトリから"mysql"を含むイメージを"５件"表示する。
- **docker image pull**
	- DockerレジストリからDockerイメージをダウンロードする。
		- 例 `docker image pull jenkins:latest`
		- ローカルリポジトリにjenkinsイメージをダウンロードしている。
- **docker image tag**
	- Dockerイメージの特定のバージョンにタグ付けを行う。タグ付けをしなかった場合"latest"になる。
	- 同じタグのイメージが作成された場合既存のイメージが新しいイメージに上書きされてしまう。さらにローカルリポジトリには残ったままになるため、破棄されるまで容量を使用してしまう。
	- Dockerイメージのバージョンとしてタグ名をつけることによってイメージIDをそのままにバージョンを管理することができる。