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

### XR Controllerコンポーネントの変数の割り当て　

| XR Controller変数       | 割り当てるアクション名 |
|------------------------|------------------------|
| Position Action         | `RightHand/Position`   |
| Rotation Action         | `RightHand/Rotation`   |
| Select Action           | `RightHandInteractions/Select` |
| Activate Action         | `RightHandInteractions/Activate` |
| UI Press Action         | `RightHandInteractions/UIPress` |
| Rotate Anchor Action    | `RightHandInteractions/RotateAnchor` |
| Translate Anchor Action | `RightHandInteractions/TranslateAnchor` |


---

## 🧪 動作検証手順（Meta Quest 2 用）

このプロジェクトは Meta Quest 2 を使用して、OpenXRベースのVR入力動作を検証できます。  
以下の手順でセットアップを行ってください。

---

### ✅ 1. Meta Quest 2 を開発者モードにする

VRビルドを行うには、Meta Quest 2 を「開発者モード」に設定する必要があります。

#### 🔗 開発者モードの有効化方法（公式ガイド）：
👉 [Meta公式ガイド：開発者モードの有効化](https://developer.oculus.com/documentation/unity/unity-enable-device/)

---

### ✅ 2. Unityでプロジェクトを開く

1. このリポジトリをクローンする
2. Unity Hub で `VR_Interaction_UnityOpenXR` プロジェクトを開く
3. `Assets/Scenes/Title Scene.unity` を開く

---

### ✅ 3. Meta Quest 2 をUSBでPCに接続

- デバイス上で USB デバッグの許可を求められたら「許可」を選択
- UnityがMeta Quest 2を認識した状態にする

---

### ✅ 4. ビルドとデプロイ

1. Unity 上部メニューから  
   `File > Build Settings` を選択  
2. Platform を `Android` に設定し `Switch Platform`
3. `Scenes In Build` に `Title Scene` が含まれていることを確認
4. Meta Quest 2 が USB 接続されていることを確認したら `Build and Run` をクリック

---

### ✅ 5. ヘッドセットを装着して動作確認

- トリガーやスティック操作が、アクションに応じて反映されるかをチェック
- 掴む・色を変える・移動するなどの処理が正常に機能するかを確認

---

## 💡 補足コントローラー入力やHMDの動作がUnityのInput Systemと連携し、正しく反映されるように設定

### ✅ UnityでOpenXRを有効にする理由と設定方法

UnityのXR開発では、対象のVRデバイス（Meta Quest 2など）に対応した「XR規格（ランタイム）」を指定する必要があります。  
本プロジェクトでは、**OpenXR** を使用します。

---

### ✅ 設定手順（Unity内で行う）

1. Unity メニューから `Edit > Project Settings` を開く  
2. 左側のメニューで `XR Plug-in Management` を選択  
3. 上部タブで `Android` を選択（Meta Quest 2 はAndroidベース）  
4. 一覧の中から `OpenXR` にチェックを入れる ✅

---

### ✅ さらに推奨設定：Meta Questサポートを明示する

OpenXR の中でも、Meta Quest に最適化された機能群を使うために：

1. `Project Settings > XR Plug-in Management > OpenXR` を開く  
2. `Feature Groups` セクションで `Meta Quest Support` にチェックを入れる ✅

> これにより、Meta Quest 2 固有の入力や最適化が有効になります。

---


