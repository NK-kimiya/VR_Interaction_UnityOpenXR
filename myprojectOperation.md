## 入力設定ファイルの場所

使用ファイル：Assets/ActionAssets/InputActionForVR.inputactions　

## 🧭入力設定ファイルの設定 

・設定ファイルと作成したアクションマップとアクション、コントローラーの設定内容　



### 🎮 アクションマップ：CubeController

| アクション       | アクションタイプ | バインディング（入力） ：コントローラー                   | 解説 |
|------------------|------------------|---------------------------------------------|------|
| LiftUp           | Button           | `trigger [RightHand XR Controller]`         | トリガーを押すと「持ち上げ」操作 |
| ChangeColor      | Button           | `gripPressed [RightHand XR Controller]`     | グリップを押すと色が変わる |
| Move             | Button           | `gripPressed [RightHand XR Controller]`     | グリップを押すと移動（移動用にも使用） |

---

### 🧑‍💻 アクションマップ：Head（視点トラッキング）

| アクション       | アクションタイプ | バインディング（入力）： コントローラー                    | 解説 |
|------------------|------------------|---------------------------------------------|------|
| Position         | Pose             | `centerEyePosition [XR HMD]`               | HMD（ヘッドマウントディスプレイ）の位置 |
| Rotation         | Pose             | `centerEyeRotation [Open XR HMD]`          | HMDの回転角度（視点の方向） |

---

### ✋ アクションマップ：RightHand（位置・姿勢）

| アクション       | アクションタイプ | バインディング（入力）： コントローラー               | 解説 |
|------------------|------------------|---------------------------------------------|------|
| Position         | Pose             | `pointerPosition [RightHand XR Controller]` | 右手コントローラーの位置 |
| Rotation         | Pose             | `pointerRotation [RightHand XR Controller]` | 右手コントローラーの回転 |

---

### 🧤 アクションマップ：RightHandInteractions（操作）

| アクション        | アクションタイプ | バインディング（入力）：                    | 解説 |
|-------------------|------------------|------------------------------------------------|------|
| Select            | Button           | `gripPressed [RightHand XR Controller]`        | 掴む／選択（グリップ押下） |
| Activate          | Button           | `triggerPressed [RightHand XR Controller]`     | アクティブ化／実行（トリガー） |
| UIPress           | Button           | `triggerPressed [RightHand XR Controller]`     | UIを押す（トリガー） |
| RotateAnchor      | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで回転操作 |
| TranslateAnchor   | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで移動操作 |

---

### 🕹️ アクションマップ：RightHandLocomotion（移動）

| アクション        | アクションタイプ | バインディング（入力）：                        | 解説 |
|-------------------|------------------|------------------------------------------------|------|
| Move              | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで前後左右の移動 |
| Turn              | Vector2          | `primary2DAxis [RightHand XR Controller]`      | スティックで回転（左右） |

---

## 🧷 XR Controllerコンポーネントの設定

### プレハブ保存場所：Assets/Resources/XR Origin 21111

'''
XR Origin

 →Camera Offset

　　→Main Camera（HMDに連動）

　　→RightHand Controller（操作割り当て済）

　→LeftHand Controller（現在は未使用）
'''
