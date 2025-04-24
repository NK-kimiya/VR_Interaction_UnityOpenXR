## 🎮 OpenXR + Input System の基本的な手順

UnityのOpenXR環境でVRアプリを構築する際は、Input Systemを使ってアクションベースの入力制御を行います。  
以下に、その基本的な手順をまとめます。

---

### ✅ STEP 1：アクションマップの定義（Action Map）

アクションマップとは、「操作カテゴリ」をまとめたものです。  
例として、以下のようなマップを作成します：

- `XRI LeftHand`（左手コントローラー用）
- `XRI RightHand`（右手コントローラー用）
- `Head`（HMDカメラの位置と回転）
- `UI`（UI操作用）

---

### ✅ STEP 2：アクション（Action）の定義

アクションは、「どのような操作を行いたいか」を表す抽象的な定義です。

| アクション名 | 意味・用途例                      |
|--------------|-----------------------------------|
| Select       | 選択・決定（オブジェクトを掴むなど） |
| Move         | 移動（スティック移動など）        |
| Activate     | アクティブ化（実行・発射）        |

アクションには「アクションタイプ」も設定します。これにより、**どのような形式の入力（ボタン・位置・スティックなど）を扱うか**を定義します。

---

### 📘 アクションタイプの種類

| アクションタイプ | 内容                             | 使用例                             |
|------------------|----------------------------------|------------------------------------|
| Button           | ボタンが押されたかの検出         | `triggerPressed`, `gripPressed`   |
| Value / Vector2  | 数値入力（スティックなど）       | `primary2DAxis`（移動/回転）       |
| Pose             | 位置と回転の取得（トラッキング） | `pointerPosition`, `centerEyeRotation` |

---

### ✅ STEP 3：コントロール（物理入力）との紐づけ

アクションに対して、**どの物理入力（コントローラーのボタンやHMD位置など）を使うか**を設定します。  
これにより、「このボタンを押したらこの操作を行う」といったルールが構築されます。

#### 📍 よく使われる入力例

| 入力デバイス         | 意味                                 |
|----------------------|--------------------------------------|
| `trigger`            | トリガーボタン（押し込み）           |
| `gripPressed`        | グリップボタン（握る）               |
| `primary2DAxis`      | スティック（上下左右）               |
| `centerEyePosition`  | HMD（視点）の位置                     |
| `pointerRotation`    | コントローラーの回転                 |

#### 🔁 紐づけの例

- `Select` アクション ← `RightController/trigger`
- `Move` アクション ← `RightController/joystick`

---

### ✅ STEP 4：`XR Controller (Action-based)` にアクションを割り当て

`XR Controller` コンポーネントに、作成したアクションを割り当てます。  
これにより、Unityの `XR Interaction Toolkit` によって、基本的な掴む・押すといった動作が自動で処理されます。

| XR Controllerの変数             | 機能概要                       | 対応アクション（例）                      |
|--------------------------------|--------------------------------|-------------------------------------------|
| Position Action                | コントローラーの位置取得       | `Position`（RightHand）                  |
| Rotation Action                | コントローラーの回転取得       | `Rotation`（RightHand）                  |
| Tracking State Action          | トラッキングの有効状態         | `TrackingState`（RightHand）             |
| Select Action                  | 掴む・選択                      | `Select`（RightHandInteractions）        |
| Activate Action                | 実行・アクティブ化             | `Activate`（RightHandInteractions）      |
| UI Press Action                | UIを押す                        | `UIPress`（RightHandInteractions）       |
| Rotate Anchor Action           | アンカーを回転                 | `RotateAnchor`（RightHandInteractions）  |
| Translate Anchor Action        | アンカーを移動                 | `TranslateAnchor`（RightHandInteractions）|

---

### ✅ STEP 5：必要に応じてスクリプトで処理を実装

掴む・押すなどの操作は Unity が自動で処理してくれますが、**移動・回転・テレポートなどはスクリプトが必要**です。

```csharp
// 例：スティック移動処理
[SerializeField] private InputActionReference moveAction;
[SerializeField] private CharacterController controller;
[SerializeField] private Transform cameraTransform;

void Update() {
    Vector2 input = moveAction.action.ReadValue<Vector2>();
    Vector3 move = cameraTransform.forward * input.y + cameraTransform.right * input.x;
    move.y = 0;
    controller.Move(move * Time.deltaTime * 2f);
}

