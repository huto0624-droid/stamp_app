# 11月 週2チャレンジ スタンプカード（シンプル版）

`Nvstamp.jpg` をカードの背景にして、光っている ○ をタップするとスタンプが押せるアプリです。
Flutter（Web）で動きます。

## 1. はじめて作る（5分）

PowerShell を開いて、アプリを作りたい場所で次を実行します。

```
flutter create stamp_app --platforms=web
cd stamp_app
mkdir assets
```

つづいて、エクスプローラーでファイルを置きます。

| 置くもの | 置き場所 |
|---|---|
| `Nvstamp.jpg` | `stamp_app\assets\` の中 |
| `main.dart`（このフォルダのもの） | `stamp_app\lib\main.dart` に **上書き** |
| `pubspec.yaml`（このフォルダのもの） | `stamp_app\pubspec.yaml` に **上書き** |

`stamp_app\test` フォルダは、最初から入っている見本のテストが古いコードを見ているので、**フォルダごと削除**してください（アプリの動作には関係ありません）。

最後に、実行します。

```
flutter pub get
flutter run -d chrome
```

**成功の目安**：カードの絵が出て、1 番の ○ がオレンジ色に光っていれば成功です。
「Hello World」や、数字を +1 するカウンターが出たら、`main.dart` が上書きできていません。置き場所（`stamp_app\lib\main.dart`）をもう一度確認してください。

## 2. 遊びかた

1. 光っている ○ をタップして、「押す」を選ぶとスタンプが押されます。
2. 押せるのは 1 番から順番です。飛ばしてタップすると、「次は ○ 番」と教えてくれます。
3. 4 番と 8 番はご褒美つきです。押すと紙吹雪が出ます。
4. 画面の下に「いま何回目か」「次に何をするか」「あと何回でご褒美か」が出ます。
5. 記録は端末に保存され、アプリを閉じても残ります。
6. 消したいときは、画面下の「はじめからやり直す」を押します。

## 3. インターネットに公開する（Firebase）

前のプロジェクトにあった `firebase.json` と `.firebaserc` を `stamp_app` フォルダにコピーしてから、次を実行します。

```
flutter build web
firebase deploy
```

Firebase は `build\web` の中身をそのまま配信します。**`flutter build web` をやり直さないと、変更は公開されません。**
公開したのに古い画面が出るときは、ブラウザで `Ctrl + Shift + R` を押してください。

## 4. 来月のカードにするとき

`lib\main.dart` の「1. 設定」だけ直します。

- `kCardImage`：新しい画像のファイル名（`pubspec.yaml` の `assets` も同じ名前に）
- `kImageW` / `kImageH`：新しい画像の横幅・縦幅（ピクセル）
- `kSaveKey`：`'stamps_2026_12'` のように変える（記録がまっさらで始まります）
- `kSlots`：○ の中心の位置と、ご褒美の名前

## 5. うまくいかないとき

| 症状 | 見ること |
|---|---|
| 「Hello World」や古い画面のまま | `lib\main.dart` を上書きしたか。実行中なら、いったん止めて `flutter run -d chrome` をやり直す |
| 「assets/Nvstamp.jpg が見つかりません」 | `stamp_app\assets\Nvstamp.jpg` があるか。`pubspec.yaml` の `assets:` に書いてあるか |
| `flutter pub get` でエラー | `pubspec.yaml` の字下げ（スペース）が崩れていないか |
| ○ の位置が絵とずれる | 画像のサイズが `kImageW` / `kImageH` と同じか |
