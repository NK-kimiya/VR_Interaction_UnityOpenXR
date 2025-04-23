## 🎮 OpenXRにおける入力システムの構造

このプロジェクトでは Unity の新しい Input System を使って、VRコントローラーの操作を定義しています。

### 🔹 アクションマップ（Action Map）

アクションマップは「操作カテゴリ」のようなもので、例えば `XRI LeftHand` や `XRI RightHand` など、
左右の手ごとに使われる操作をグループ化しています。

---

### 🔸 アクション（Action）

アクションは「何をしたいか」を定義する抽象的な動作です。

| アクション名 | 意味 |
|--------------|------|
| Select       | 選択・決定（例：トリガーを押す） |
| Move         | 手の移動や移動方向の取得 |
| Activate     | オブジェクトを有効化（例：グリップ） |

---

### 🔻 コントロール（Control）

コントロールは「物理的な入力デバイス」からの信号を表します。

例えば：

- `LeftController/trigger` → 左手コントローラーのトリガーボタン
- `RightController/joystick` → 右手コントローラーのスティック

---

### ✅ 紐づけの仕組み

アクションとコントロールを紐づけることで、
**「このボタンを押したら、この動作をする」**というルールを設定できます。

例えば：

- `Select` アクション ← `RightController/trigger` にバインド
- `Move` アクション ← `RightController/joystick` にバインド

これにより、コントローラーの入力を使って直感的なVR操作が可能になります。

---

### 📁 入力設定ファイルの場所

アクション設定はプロジェクト内の `.inputactions` ファイルにまとめられています。

## 🔧 用語解説

| 用語 | 説明 |
|------|------|
| **アクションタイプ（Action Type）** | 入力の種類を指定するプロパティ（例：ボタンなのか2軸なのかなど） |
| **バインディング（Binding）** | アクションに割り当てられる物理デバイスの入力（例：トリガー、スティックなど） |

---

### 🎮 アクションマップ：CubeController

| アクション       | アクションタイプ | バインディング（入力）                     | 解説 |
|------------------|------------------|---------------------------------------------|------|
| LiftUp           | Button           | `trigger [RightHand XR Controller]`         | トリガーを押すと「持ち上げ」操作 |
| ChangeColor      | Button           | `gripPressed [RightHand XR Controller]`     | グリップを押すと色が変わる |
| Move             | Button           | `gripPressed [RightHand XR Controller]`     | グリップを押すと移動（移動用にも使用） |

---

### 🧑‍💻 アクションマップ：Head（視点トラッキング）

| アクション       | アクションタイプ | バインディング（入力）                     | 解説 |
|------------------|------------------|---------------------------------------------|------|
| Position         | Pose             | `centerEyePosition [XR HMD]`               | HMD（ヘッドマウントディスプレイ）の位置 |
| Rotation         | Pose             | `centerEyeRotation [Open XR HMD]`          | HMDの回転角度（視点の方向） |

---

### ✋ アクションマップ：RightHand（位置・姿勢）

| アクション       | アクションタイプ | バインディング（入力）                     | 解説 |
|------------------|------------------|---------------------------------------------|------|
| Position         | Pose             | `pointerPosition [RightHand XR Controller]` | 右手コントローラーの位置 |
| Rotation         | Pose             | `pointerRotation [RightHand XR Controller]` | 右手コントローラーの回転 |

---

### 🧤 アクションマップ：RightHandInteractions（操作）

| アクション        | アクションタイプ | バインディング（入力）                        | 解説 |
|-------------------|------------------|------------------------------------------------|------|
| Select            | Button           | `gripPressed [RightHand XR Controller]`        | 掴む／選択（グリップ押下） |
| Activate          | Button           | `triggerPressed [RightHand XR Controller]`     | アクティブ化／実行（トリガー） |
| UIPress           | Button           | `triggerPressed [RightHand XR Controller]`     | UIを押す（トリガー） |
| RotateAnchor      | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで回転操作 |
| TranslateAnchor   | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで移動操作 |

---

### 🕹️ アクションマップ：RightHandLocomotion（移動）

| アクション        | アクションタイプ | バインディング（入力）                        | 解説 |
|-------------------|------------------|------------------------------------------------|------|
| Move              | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで前後左右の移動 |
| Turn              | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで回転（左右） |

---

## 📘 アクションタイプの種類

| アクションタイプ | 意味 | 使用例 |
|------------------|------|--------|
| **Button**       | ボタンが押されたかを検知 | `triggerPressed`, `gripPressed` |
| **Vector2**      | 2軸の入力（スティックなど） | `primary2DAxis`（移動/回転） |
| **Pose**         | 位置と回転の両方を含む入力 | `pointerPosition`, `centerEyeRotation` |

---

## 📘 バインディングの入力パス例

| 入力 | 意味 |
|------|------|
| `trigger` | トリガーボタン（押し込み） |
| `gripPressed` | グリップボタン（握る） |
| `primary2DAxis` | スティック（上下左右） |
| `centerEyePosition` | HMD（頭部）の位置 |
| `pointerRotation` | コントローラーの回転 |

---

この構成により、コントローラーの操作とアクションが明確に分離され、デバイス変更にも柔軟に対応できます。

