## 🎮 OpenXR + Input System の基本的な手順（初心者向け解説付き）

UnityのOpenXR環境でVRアプリを構築する際は、Input Systemを使ってアクションベースの入力制御を行います。  
以下に、その基本的な手順と設定ポイントを丁寧に説明します。

---

### ✅ STEP 1：アクションマップの定義（Action Map）

アクションマップとは、「操作カテゴリ（例：右手、左手、UIなど）」をまとめたもので、Input Systemで使用します。

#### 🔧 作成方法・ファイル場所

- Unityエディタで `.inputactions` ファイルを作成します。
  - メニュー：`Assets > Create > Input Actions`
- 一般的に、`Assets/Settings/` や `Assets/ActionAssets/` フォルダに配置されます。
- 作成後、ダブルクリックすると「アクションマップエディター」が開きます。

#### 例：アクションマップの構成

- `XRI LeftHand`（左手操作）
- `XRI RightHand`（右手操作）
- `Head`（HMDの位置/回転）
- `UI`（UI操作）

---

### ✅ STEP 2：アクション（Action）の定義

アクションは、「何をしたいか？」を表す抽象的な操作定義です。

| アクション名 | 意味・用途例                        |
|--------------|-------------------------------------|
| Select       | 掴む・選択（オブジェクトを掴むなど）|
| Move         | 移動（スティック操作）             |
| Activate     | 実行・発射（ボタンを押す、トリガー）|

#### アクションタイプとは？

アクションには、「Button」「Value」「Pose」などの**アクションタイプ**を設定します。これにより、**どの形式の入力か（押す？位置？回転？）**を指定します。

| アクションタイプ | 内容                             | 使用例                             |
|------------------|----------------------------------|------------------------------------|
| Button           | ボタンが押されたかを検知         | `triggerPressed`, `gripPressed`   |
| Vector2          | 2軸入力（スティックなど）         | `primary2DAxis`（移動/回転）       |
| Pose             | 位置と回転の両方を含む入力        | `pointerPosition`, `centerEyeRotation` |

---

### ✅ STEP 3：物理コントローラーとの紐づけ（バインディング）

定義したアクションに対して、「どのデバイスのどの入力を使うか」を割り当てます。

#### 📍 よく使われる入力例

| 入力デバイス         | 意味                                 |
|----------------------|--------------------------------------|
| `trigger`            | トリガーボタン（引き金）              |
| `gripPressed`        | グリップ（握る）                      |
| `primary2DAxis`      | スティック入力（上下左右）            |
| `centerEyePosition`  | HMDの位置                             |
| `pointerRotation`    | コントローラーの回転                  |

#### 例：

- `Select` アクション ← `RightController/trigger`
- `Move` アクション ← `RightController/joystick`

---

### ✅ STEP 4：XR Controller にアクションを割り当て

#### 🔧 XR Controller とは？

- Unityの `XR Interaction Toolkit` に含まれるコンポーネントです。
- VRコントローラーの動作（掴む・押す・移動など）を処理する**インターフェース**です。

#### 📍 どこにアタッチされている？

- `XR Origin` オブジェクトを Hierarchy に追加すると、自動的に以下の構成が生成されます：

```plaintext
XR Origin
├── Camera Offset
│   ├── RightHand Controller（←ここに XR Controller がアタッチ）
│   └── Main Camera（視点）
```
### STEP 5：スクリプトで移動や特殊処理を実装（必要に応じて）

移動や回転などの操作は、自動では処理されないため、スクリプトで処理を記述する必要があります。  
作成したスクリプトは、**一般的には `XR Origin`（プレイヤー全体のルートオブジェクト）にアタッチ**します。

###補足：VRでよく使う基本動作

| 動作カテゴリ        | 内容・目的                              | 主なアクション名    | 入力デバイス例                      |
|---------------------|-------------------------------------------|----------------------|-------------------------------------|
| 🕹️ プレイヤーの移動    | スティックで前後左右に移動                 | `Move`               | `primary2DAxis`（Vector2）         |
| 🔄 プレイヤーの回転    | スティックで左右に向きを変更               | `Turn`               | `primary2DAxis`（Vector2）         |
| 📍 テレポート移動     | 特定の場所へ一瞬で移動（瞬間移動）         | `TeleportSelect`     | トリガー or スティック押し込み     |
| ✋ オブジェクトを掴む  | 近くのオブジェクトを手で掴む               | `Select`             | `trigger` or `gripPressed`         |
| ⚡ オブジェクトの操作  | 掴んだオブジェクトを実行／有効化する       | `Activate`           | `triggerPressed`                   |
| 🖱️ UI操作             | UIボタンを押す                            | `UIPress`            | `triggerPressed`                   |
| 🎯 アンカー移動       | スティックでアンカー（移動ポイント）を移動 | `TranslateAnchor`    | `primary2DAxis`                    |
| ↻ アンカー回転       | スティックでアンカーを回転                | `RotateAnchor`       | `primary2DAxis`                    |
| 👁️ ヘッド位置の取得   | HMDの位置・回転から視点の情報を得る        | `Position`, `Rotation` | `centerEyePosition`, `centerEyeRotation` |
| 🧭 手の位置の取得     | コントローラーの位置・回転                 | `Position`, `Rotation` | `pointerPosition`, `pointerRotation` |
