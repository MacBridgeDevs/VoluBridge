# VoluBridge

**言語:** [English](README.md) | 日本語

**公式サイト:** [VoluBridge 公式サイト](https://bridgedevs.com/ja/volubridge)

**ダウンロード:** [最新 DMG](https://bridgedevs.com/volubridge/releases/latest) | [FAQ](https://bridgedevs.com/ja/volubridge/faq) | [リファレンス](https://bridgedevs.com/ja/volubridge/reference)

VoluBridge は、Apple Silicon Mac 向けの CoreAudio ベースの音量ブリッジです。HDMI / DisplayPort モニター、USB-C ディスプレイ、USB DAC、オーディオインターフェイス、ヘッドホンなどを、通常の Mac 音量キーで扱えるようにします。

DDC に依存しません。アプリを常に開いておく前提でもありません。音声ブリッジはドライバレベルで動作し、アプリは出力選択、EQ、VU メーター、FFT、RT 診断、ドライバ管理のための操作パネルです。

![VoluBridge の音量操作、メーター、OPTIMIZER 画面](https://bridgedevs.com/VoluBridgeCapture.png)

## 試してほしい理由

- 外部モニターから音は出るが、Mac の音量キーで自然に操作できない。
- USB DAC やオーディオインターフェイスを、標準の音量キーで扱いたい。
- DDC 制御が不安定、使えない、音量の刻みが粗い、または音声経路に合っていない。
- ミキサーや音声ユーティリティのウィンドウを開きっぱなしにしたくない。
- メーター、スペクトラム表示、RT 診断で、音声経路の状態を見たい。
- 購入前に 14 日間の試用で、自分のモニター、DAC、ドック、アプリ、日常環境で確認したい。

## VoluBridge がすること

VoluBridge は `VoluBridgeRT` という仮想 CoreAudio 出力デバイスを追加します。macOS はその仮想デバイスへ音声を送り、VoluBridge が選択された実際のスピーカー、モニター、DAC、インターフェイスへルーティングします。

通常の使い方は次の通りです。

- macOS の出力先として `VoluBridge` を選ぶ
- VoluBridge のメニューバーパネルで実際に鳴らすデバイスを選ぶ
- いつも通りキーボードの音量キーを使う

macOS 側で物理デバイスを直接選んだ場合、VoluBridge はその経路をダイレクト出力として扱い、無理にブリッジ経由へ戻しません。

![VoluBridge の出力ルーティングとチャンネル選択](https://bridgedevs.com/assets/volubridge-output-routing.png)

## 主な特徴

- HDMI、DisplayPort、USB などの外部出力をキーボード音量キーで操作
- `System Output` と `VoluBridge Output` を分けたメニューバー操作パネル
- アプリ内からインストール、更新、削除できる同梱 CoreAudio HAL ドライバ
- より細かく調整できる音量ステップ
- マルチチャンネル機器向けの出力チャンネルペア選択
- スリープ復帰、再接続、出力切り替え、サンプルレート変更への自動対応
- リアルタイム VU メーター、スペクトラム表示、OPTIMIZER
- 同期、アンダーフロー、バッファ、クロック、ルーティング状態を確認できる RT 診断
- 英語 / 日本語 UI
- 14 日間の試用とライセンス認証

## VoluBridge が向いている場面

DDC で安定して音量調整できる環境では、DDC 制御アプリで十分な場合があります。VoluBridge は、DDC では扱いにくい外部オーディオ環境や、USB DAC / オーディオインターフェイスを Mac の標準音量キーで扱いたい場合に向いています。

| 比較軸 | VoluBridge | DDC 制御アプリ | 一般的な音声ユーティリティ |
|---|---|---|---|
| 外部モニター音量の操作 | 対応 | 対応環境では可能 | アプリ内ミキサーでの調整が中心 |
| USB DAC / オーディオ IF の音量キー操作 | 対応 | 基本的に対象外 | アプリ内音量や EQ が中心 |
| DDC 依存 | なし | あり | なし |
| HDMI / DisplayPort 環境 | 対応 | モニター依存 | CoreAudio 出力として扱うが、モニター音量制御は主目的ではない |
| 標準音量キー / HUD | 対応 | モニター制御へ置き換える方式が中心 | 独自 UI やアプリ内操作が中心になりやすい |
| 最小音量 / 音量の刻み | Mac 側の音量操作として扱う | モニター側の最小音量や刻み幅に依存 | アプリ内の音量処理に依存 |
| アプリ常駐への依存 | 基本音声出力はドライバレベルで動作 | 常駐アプリで制御する方式が中心 | 音声処理のために常駐アプリが前提になりやすい |
| 低遅延ブリッジ設計 | 重視 | 対象外 | ミキサー / EQ / ルーティング処理が中心 |
| VU / FFT / RT 診断 | 統合 | 基本なし | メーターや EQ 表示が中心で、RT 診断は少ない |
| 主な用途 | 外部オーディオ出力ブリッジ | モニター制御 | 音声ミキサー / EQ |

## 従来モデルとの比較

VoluBridgeRT は、音を単純に FIFO キューへ溜めてから後で再生する設計ではありません。Producer の予定時刻と Render の出力時刻を固定ターゲットへ揃えることで、長時間利用で仮想経路の遅延が積み上がりにくい構造を目指しています。

| 観点 | 一般的な FIFO 型 | VoluBridgeRT |
|---|---|---|
| 安定化の主な考え方 | キュー在庫を持つ | 出力タイムラインへ追従する |
| 遅延の挙動 | バッファに溜まった在庫量で変わる | 固定ターゲットを中心に管理する |
| 長時間利用 | キューが厚くなると遅延が増えやすい | 遅延を溜め込まない方向で制御する |
| Underflow 復帰 | キュー状態が崩れ、遅延を引きずりやすい | ターゲットタイムラインへ再同期する |
| 診断で見えるもの | バッファやアプリ状態が中心 | Fixed Cursor、Real Add Latency、missing、underflow、clock、routing state |

これは物理的な遅延が消えるという意味ではありません。VoluBridge は、直接ハードウェアへ出力した場合に対して、不要な待ち時間を増やさないことを目指す設計です。

## OPTIMIZER と可視化

VoluBridge は出力切り替えだけのアプリではありません。実際に聞いている出力を確認し、必要に応じて整えるための機能を備えています。

- 7 バンド EQ、プリセット、SoftClipper を備えた `OPTIMIZER`
- 音量調整時に確認しやすい Peak / RMS メーター
- 音声入力を確認できるスペクトラム表示
- 日常利用向けのコンパクトな出力切り替え
- 同期、アンダーフロー、バッファ、クロック、ルーティング状態を確認できる RT 診断

## 確認済みの環境

現在の確認例には、M1 MacBook Air、Mac Studio M4 Max、ASUS PG42UQ、M1 MacBook Air 内蔵オーディオ、RME UFX、Roland Fantom 08、Cubase、Parallels Desktop、Spotify、YouTube が含まれます。デバイス固有の挙動は変わるため、14 日間の試用で自分の環境を確認することをおすすめします。

## 動作環境

- macOS 11 以降
- Apple Silicon Mac
- 初回ドライバインストール、またはドライバ更新時の管理者パスワード

## インストール

1. リリースパッケージから VoluBridge の DMG をダウンロードします。
2. `VoluBridge.app` を `/Applications` にドラッグします。
3. `VoluBridge.app` を起動します。
4. 初回起動時の案内に従って、同梱の `VoluBridgeRT.driver` をインストールします。
5. macOS に求められたら管理者パスワードを入力します。

ドライバはアプリ内に同梱されています。別の companion プロセスを手動で起動する必要はありません。

## 基本的な使い方

1. メニューバーの VoluBridge アイコンを開きます。
2. `System Output` で `VoluBridge` を選択します。
3. `VoluBridge Output` で実際に音を出したいデバイスを選択します。
4. キーボードの音量キー、または macOS の音量スライダーを使います。

上部のステータスには現在の経路が表示されます。

- `<device name> (VoluBridge)` は、音声が VoluBridge 経由でルーティングされている状態です。
- `<device name> (Direct)` は、macOS がそのデバイスへ直接出力している状態です。

## 高度な設定

ほとんどのユーザーは標準設定のままで使えます。DAW、動画編集環境、不安定な HDMI 経路、特殊なバッファ挙動を持つデバイスなどでは、Advanced Settings から明示的に調整できます。

高度な設定には、サンプルレート動作、クロックモード、固定ターゲット、仮想バッファとデバイスバッファ、報告レイテンシとセーフティ値、省電力動作、RT 診断カウンターなどが含まれます。

## ライセンス

VoluBridge には 14 日間の試用期間があります。購入後はアプリ内の `Enter License Key` からフルバージョンを有効化できます。現在の価格とライセンス条件は [公式サイト](https://bridgedevs.com/ja/volubridge/buy) を確認してください。

ライセンス認証では、シート管理とサポートのために Machine ID を使用します。音声ルーティングと解析は Mac 上でローカルに処理されます。

## サポート

トラブルシューティング手順と問い合わせ時に含める情報は [SUPPORT.ja.md](SUPPORT.ja.md) を参照してください。

## 変更履歴

リリースノートは [CHANGELOG.ja.md](CHANGELOG.ja.md) を参照してください。
