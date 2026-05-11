# サポート

**言語:** [English](SUPPORT.md) | 日本語

このページは、VoluBridge の問題を報告する前に確認してほしい項目をまとめたものです。

## 対応環境

VoluBridge は Apple Silicon / Intel Mac の macOS 11 以降に対応しています。

アプリは `VoluBridgeRT.driver` という CoreAudio HAL ドライバをインストールします。このドライバのインストール、更新、削除には管理者承認が必要で、CoreAudio が一時的に再起動される場合があります。

## まず確認すること

### 音が出ない

1. VoluBridge のメニューバーパネルを開きます。
2. `System Output` が `VoluBridge` になっていることを確認します。
3. `VoluBridge Output` が実際に鳴らしたいモニター、DAC、スピーカー、ヘッドホン、インターフェイスになっていることを確認します。
4. 上部ステータスが `<device name> (VoluBridge)` になっていることを確認します。
5. アプリから `Reset Audio Connection` を実行します。

### VoluBridge 出力が表示されない

1. VoluBridge を開き、`Driver:` 行を確認します。
2. ドライバが未インストールの場合は `Install Driver` を選びます。
3. 更新がある場合は、ドライバ更新項目を選びます。
4. それでも表示されない場合は、VoluBridge を終了して再度開きます。

### 音量キーが効かない

`Fine-grained Volume Steps` を有効にしている場合、macOS のアクセシビリティ許可が必要です。

アプリ更新後、macOS 側に古い許可状態が残ることがあります。VoluBridge の `Reset Accessibility Permission` を実行し、システム設定でアクセシビリティ許可を再度付与してください。

### クリック音、音切れ、復帰遅延がある

多くの設定を変更する前に、`RT Diagnostics` を開いて診断テキストをコピーしてください。特に、underflow count、fixed cursor state、last underflow context、device buffer、reported latency/safety、phase precision、output switch errors が有用です。

不安定な HDMI ディスプレイや高負荷環境では、次を試してください。

- `Reset Audio Connection`
- fixed target または device buffer を大きくする
- テストとして power saving を無効にする
- ディスプレイ、ドック、DAC、オーディオインターフェイスを再接続する

## 問い合わせ時に含める情報

問題を報告するときは、次の情報を含めてください。

- macOS バージョン
- Mac のモデルと CPU 種別
- VoluBridge アプリのバージョンとビルド
- VoluBridge ドライバのバージョンとビルド
- 出力デバイス名と接続方式、例: HDMI、DisplayPort、USB、Bluetooth、ドック、インターフェイス
- ステータスが `(VoluBridge)` か `(Direct)` のどちらか
- 問題がスリープ復帰、再接続、アプリ起動、出力切り替え、サンプルレート変更、ライセンス認証の後に起きるか
- 音声の問題では、コピーした `RT Diagnostics` テキスト
- 問題を再現する具体的な手順

ライセンスキー全体は送らないでください。ライセンス問題の調査が必要な場合は、表示されている Machine ID と正確なエラーメッセージだけを含めてください。

## プライバシーとセキュリティ

音声ルーティング、音量制御、メーター、スペクトラム解析、RT 診断は Mac 上でローカルに実行されます。

ライセンス認証と検証では、ライセンス状態とシート管理のためにネットワーク通信を行います。アプリ内のアップデート確認を使用した場合、VoluBridge はアップデート確認用エンドポイントにもアクセスします。

## アンインストール

可能な場合は VoluBridge の `Remove App Completely` を使用してください。アプリ、ドライバ、関連設定、アクセシビリティ許可状態を削除します。

アプリと設定を残して `VoluBridgeRT.driver` だけ削除したい場合は、`Remove Driver Only` を使用してください。
