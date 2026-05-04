# Unity + C# RPG 遊戲開發 — 初學者完整教學

> 適合對象：完全沒有 Unity 或遊戲開發經驗的初學者  
> 目標：從零開始，製作一款包含地圖、角色移動、戰鬥、道具的 2D RPG 遊戲

---

## 目錄

1. [學習路線圖總覽](#1-學習路線圖總覽)
2. [環境安裝與設定](#2-環境安裝與設定)
3. [Unity 編輯器基礎](#3-unity-編輯器基礎)
4. [C# 基礎語法速成](#4-c-基礎語法速成)
5. [第一個 RPG 專案：角色移動](#5-第一個-rpg-專案角色移動)
6. [地圖設計（Tilemap）](#6-地圖設計tilemap)
7. [角色動畫（Animator）](#7-角色動畫animator)
8. [攝影機跟隨](#8-攝影機跟隨)
9. [碰撞偵測與物理系統](#9-碰撞偵測與物理系統)
10. [NPC 與對話系統](#10-npc-與對話系統)
11. [回合制戰鬥系統](#11-回合制戰鬥系統)
12. [物品與背包系統](#12-物品與背包系統)
13. [場景切換與存檔](#13-場景切換與存檔)
14. [UI 介面設計](#14-ui-介面設計)
15. [專案實戰練習清單](#15-專案實戰練習清單)
16. [推薦學習資源](#16-推薦學習資源)

---

## 1. 學習路線圖總覽

```
第 1 週    安裝 Unity、學 C# 基礎 (變數/函式/類別)
第 2 週    Unity 編輯器操作、建立第一個場景
第 3 週    角色移動 + Sprite 顯示
第 4 週    Tilemap 地圖 + 碰撞
第 5 週    動畫 Animator
第 6 週    攝影機跟隨 + 場景切換
第 7 週    NPC 對話系統
第 8 週    回合制戰鬥
第 9 週    背包道具系統
第 10 週   UI + 存讀檔
第 11-12 週 整合測試 + 發布
```

> **建議**：每天花 1~2 小時，一邊看教學一邊動手做，不要只看不做。

---

## 2. 環境安裝與設定

### 2.1 安裝 Unity Hub

1. 前往 [https://unity.com/download](https://unity.com/download)
2. 下載並安裝 **Unity Hub**
3. 建立免費帳號（Personal 授權即可）

### 2.2 安裝 Unity Editor

1. 開啟 Unity Hub → **Installs** → **Install Editor**
2. 選擇 **LTS（長期支援）版本**（例如 Unity 6 LTS 或 2022.3 LTS）
3. 安裝時勾選：
   - ✅ **Windows Build Support**
   - ✅ **WebGL Build Support**（可選，之後可發布網頁版）
   - ✅ **Visual Studio Community**（IDE，用來寫 C#）

### 2.3 建立第一個專案

```
Unity Hub → Projects → New Project
→ 選擇 2D (Core) 範本
→ 專案名稱：MyFirstRPG
→ 儲存位置：選擇你的資料夾
→ 點擊 Create Project
```

### 2.4 設定 Visual Studio

1. 在 Unity 選單：**Edit → Preferences → External Tools**
2. External Script Editor 選擇 **Visual Studio Community**
3. 點擊 **Regenerate project files**

---

## 3. Unity 編輯器基礎

### 3.1 五大視窗介紹

| 視窗 | 功能 |
|------|------|
| **Scene View** | 設計遊戲場景的地方（可拖拉物件） |
| **Game View** | 模擬玩家視角（按 Play 後顯示） |
| **Hierarchy** | 場景中所有物件的清單 |
| **Inspector** | 查看/修改選取物件的屬性 |
| **Project** | 管理遊戲所有素材（圖片/音效/腳本） |

### 3.2 常用快捷鍵

| 快捷鍵 | 功能 |
|--------|------|
| `W` | 移動工具 |
| `E` | 旋轉工具 |
| `R` | 縮放工具 |
| `Ctrl + S` | 儲存場景 |
| `Ctrl + Z` | 復原 |
| `F` | 聚焦到選取物件 |
| `Alt + 拖曳` | 旋轉 Scene View |
| `Space` | 切換最大化視窗 |

### 3.3 GameObject 與 Component 概念

Unity 的核心概念：

```
GameObject（遊戲物件）
├── Transform Component（位置/旋轉/縮放，每個物件都有）
├── Sprite Renderer（顯示圖片）
├── Rigidbody 2D（物理引擎）
├── Collider 2D（碰撞範圍）
└── Script（你寫的 C# 腳本）
```

> **比喻**：GameObject 像是一個「空盒子」，Component 是你放進去的「功能模組」。

---

## 4. C# 基礎語法速成

> 你不需要精通 C#，但要懂基本概念才能寫 Unity 腳本。

### 4.1 變數與型別

```csharp
// 整數
int hp = 100;
int level = 1;

// 小數
float speed = 3.5f;    // Unity 常用 float，記得加 f

// 文字
string playerName = "勇者";

// 布林值
bool isAlive = true;
```

### 4.2 條件判斷

```csharp
if (hp <= 0)
{
    Debug.Log("遊戲結束！");
}
else if (hp < 30)
{
    Debug.Log("血量危險！");
}
else
{
    Debug.Log("狀態良好");
}
```

### 4.3 迴圈

```csharp
// for 迴圈：攻擊 3 次
for (int i = 0; i < 3; i++)
{
    Debug.Log("攻擊第 " + i + " 次");
}

// while 迴圈：敵人存活時持續戰鬥
while (enemyHP > 0)
{
    enemyHP -= 10;
}
```

### 4.4 方法（函式）

```csharp
// 定義方法
void TakeDamage(int damage)
{
    hp -= damage;
    if (hp < 0) hp = 0;
}

// 呼叫方法
TakeDamage(20);
```

### 4.5 類別（Class）

```csharp
public class Player
{
    public string name;
    public int hp;
    public int attack;

    public void Attack(Enemy enemy)
    {
        enemy.hp -= attack;
    }
}
```

### 4.6 Unity MonoBehaviour 腳本結構

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    // 在 Inspector 可見的變數
    public float speed = 5f;

    // 遊戲開始時執行一次
    void Start()
    {
        Debug.Log("遊戲開始！");
    }

    // 每一幀都執行（約每秒 60 次）
    void Update()
    {
        // 在這裡處理玩家輸入
    }
}
```

---

## 5. 第一個 RPG 專案：角色移動

### 5.1 匯入角色圖片

1. 下載免費 RPG Sprite（推薦：[LPC Character Generator](https://sanderfrenken.github.io/Universal-LPC-Spritesheet-Character-Generator/) 或 [itch.io 免費素材](https://itch.io/game-assets/free/tag-rpg)）
2. 將圖片拖進 Project 視窗的 `Assets` 資料夾
3. 在 Inspector 設定：
   - **Texture Type**：`Sprite (2D and UI)`
   - **Pixels Per Unit**：`16`（依圖片大小調整）
   - 點擊 **Apply**

### 5.2 建立玩家物件

```
Hierarchy → 右鍵 → 2D Object → Sprite
→ 命名為 "Player"
→ 在 Inspector 的 Sprite Renderer 選擇你的角色圖片
```

### 5.3 撰寫移動腳本

在 `Assets/Scripts/` 資料夾建立 `PlayerController.cs`：

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    [Header("移動設定")]
    public float moveSpeed = 5f;

    private Rigidbody2D rb;
    private Vector2 movement;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // 取得玩家輸入（WASD 或方向鍵）
        float moveX = Input.GetAxisRaw("Horizontal"); // -1, 0, 1
        float moveY = Input.GetAxisRaw("Vertical");   // -1, 0, 1

        movement = new Vector2(moveX, moveY).normalized;
    }

    // FixedUpdate 用於物理計算，比 Update 更穩定
    void FixedUpdate()
    {
        rb.MovePosition(rb.position + movement * moveSpeed * Time.fixedDeltaTime);
    }
}
```

### 5.4 設定 Rigidbody 2D

1. 選取 Player 物件
2. Inspector → **Add Component** → 搜尋 `Rigidbody 2D`
3. 設定：
   - **Gravity Scale**：`0`（RPG 俯視角不需要重力）
   - **Collision Detection**：`Continuous`
   - **Freeze Rotation Z**：✅（防止角色旋轉）

4. 再加入 **Box Collider 2D** 或 **Capsule Collider 2D**
5. 將 `PlayerController.cs` 拖到 Player 物件上

### 5.5 測試

按 **Play** 鍵，用 WASD 移動角色！

---

## 6. 地圖設計（Tilemap）

### 6.1 建立 Tilemap

```
Hierarchy → 右鍵 → 2D Object → Tilemap → Rectangular
```

這會同時建立：
- `Grid`（網格父物件）
- `Tilemap`（地板圖層）

建議建立多個圖層：

```
Grid
├── Ground（地板）
├── Obstacles（障礙物/牆壁）
└── Decorations（裝飾，樹/草）
```

### 6.2 匯入 Tileset 素材

1. 將 Tileset 圖片拖進 Assets
2. Inspector 設定：
   - **Texture Type**：`Sprite (2D and UI)`
   - **Sprite Mode**：`Multiple`
   - **Pixels Per Unit**：`16`
3. 點擊 **Sprite Editor** → **Slice**
   - Type：`Grid By Cell Size`
   - Pixel Size：`16 x 16`
4. **Apply**

### 6.3 使用 Tile Palette 繪製地圖

```
選單 → Window → 2D → Tile Palette
```

1. 建立新的 Tile Palette
2. 將切好的 Sprite 拖進 Palette
3. 選擇筆刷工具，在 Scene View 畫地圖

### 6.4 設定牆壁碰撞

1. 選取 **Obstacles** 這個 Tilemap 物件
2. **Add Component** → `Tilemap Collider 2D`
3. 勾選 **Used By Composite**
4. 再加入 `Composite Collider 2D`（自動加入 Rigidbody 2D，設 Kinematic）

---

## 7. 角色動畫（Animator）

### 7.1 切割行走動畫幀

假設你的角色 Sprite Sheet 格式如下：

```
行走下 → 行走左 → 行走右 → 行走上（每方向 3~4 幀）
```

在 Sprite Editor 切割後，依方向建立 Animation Clip。

### 7.2 建立 Animator Controller

```
Assets → 右鍵 → Create → Animator Controller
命名為 PlayerAnimator
```

雙擊開啟 Animator 視窗：

```
新增 Parameters（參數）：
  moveX : Float
  moveY : Float
  isMoving : Bool
```

### 7.3 設定動畫狀態機

```
Idle（靜止）
├── → Walk_Down   條件: isMoving = true, moveY < 0
├── → Walk_Up     條件: isMoving = true, moveY > 0
├── → Walk_Left   條件: isMoving = true, moveX < 0
└── → Walk_Right  條件: isMoving = true, moveX > 0
```

每個 Walk 狀態都加回 Idle 的過渡：`isMoving = false`

### 7.4 在腳本中控制動畫

```csharp
using UnityEngine;

public class PlayerController : MonoBehaviour
{
    public float moveSpeed = 5f;

    private Rigidbody2D rb;
    private Animator animator;
    private Vector2 movement;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
        animator = GetComponent<Animator>();
    }

    void Update()
    {
        float moveX = Input.GetAxisRaw("Horizontal");
        float moveY = Input.GetAxisRaw("Vertical");
        movement = new Vector2(moveX, moveY).normalized;

        // 更新動畫參數
        animator.SetFloat("moveX", moveX);
        animator.SetFloat("moveY", moveY);
        animator.SetBool("isMoving", movement != Vector2.zero);
    }

    void FixedUpdate()
    {
        rb.MovePosition(rb.position + movement * moveSpeed * Time.fixedDeltaTime);
    }
}
```

---

## 8. 攝影機跟隨

### 8.1 安裝 Cinemachine（推薦）

```
Unity 選單 → Window → Package Manager
→ 搜尋 Cinemachine → Install
```

### 8.2 設定虛擬攝影機

```
Hierarchy → 右鍵 → Cinemachine → 2D Camera
```

1. 選取 `CM vcam1`
2. Inspector → **Follow**：拖入 Player 物件
3. **Body** → `Framing Transposer`
4. 調整 **Dead Zone** 和 **Lookahead** 讓攝影機移動更流暢

### 8.3 設定攝影機邊界（Confiner）

防止攝影機超出地圖邊界：

1. 建立一個 `Empty GameObject` 命名 `CameraBounds`
2. 加入 **Polygon Collider 2D**，圍住整個地圖
3. 在 CM vcam1 加入 Extension → **CinemachineConfiner2D**
4. 將 `CameraBounds` 的 Collider 拖入 **Bounding Shape 2D**

---

## 9. 碰撞偵測與物理系統

### 9.1 Layer 設定

```
Edit → Project Settings → Tags and Layers
新增：
  Layer 6: Player
  Layer 7: Enemy
  Layer 8: NPC
  Layer 9: Item
```

### 9.2 觸發偵測範例（拾取道具）

```csharp
// 道具腳本 ItemPickup.cs
using UnityEngine;

public class ItemPickup : MonoBehaviour
{
    public string itemName = "草藥";
    public int healAmount = 30;

    // 當有 Trigger Collider 的物件進入時觸發
    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            // 讓玩家回血
            PlayerStats player = other.GetComponent<PlayerStats>();
            if (player != null)
            {
                player.Heal(healAmount);
            }

            Debug.Log("拾取了：" + itemName);
            Destroy(gameObject); // 銷毀道具
        }
    }
}
```

### 9.3 玩家屬性腳本

```csharp
// PlayerStats.cs
using UnityEngine;

public class PlayerStats : MonoBehaviour
{
    [Header("基本屬性")]
    public string playerName = "勇者";
    public int maxHP = 100;
    public int currentHP = 100;
    public int attack = 15;
    public int defense = 5;
    public int level = 1;
    public int exp = 0;

    public void TakeDamage(int damage)
    {
        int actualDamage = Mathf.Max(damage - defense, 1); // 最少受1點傷害
        currentHP -= actualDamage;
        currentHP = Mathf.Clamp(currentHP, 0, maxHP);

        if (currentHP <= 0)
        {
            Die();
        }
    }

    public void Heal(int amount)
    {
        currentHP = Mathf.Min(currentHP + amount, maxHP);
    }

    public void GainExp(int amount)
    {
        exp += amount;
        if (exp >= level * 100) // 簡單升級公式
        {
            LevelUp();
        }
    }

    private void LevelUp()
    {
        level++;
        exp = 0;
        maxHP += 20;
        currentHP = maxHP;
        attack += 3;
        defense += 1;
        Debug.Log("升級！現在是 Lv." + level);
    }

    private void Die()
    {
        Debug.Log("遊戲結束");
        // TODO: 顯示 Game Over 畫面
    }
}
```

---

## 10. NPC 與對話系統

### 10.1 建立對話資料

```csharp
// DialogueData.cs
using UnityEngine;

[System.Serializable]
public class DialogueLine
{
    public string speakerName;
    [TextArea(2, 5)]
    public string text;
}
```

### 10.2 NPC 腳本

```csharp
// NPCDialogue.cs
using UnityEngine;

public class NPCDialogue : MonoBehaviour
{
    [Header("對話內容")]
    public DialogueLine[] dialogueLines;

    private bool isPlayerNearby = false;
    private int currentLine = 0;

    void Update()
    {
        // 按下 F 鍵或 Space 鍵對話
        if (isPlayerNearby && Input.GetKeyDown(KeyCode.F))
        {
            ShowNextLine();
        }
    }

    void ShowNextLine()
    {
        if (currentLine < dialogueLines.Length)
        {
            DialogueManager.Instance.ShowDialogue(
                dialogueLines[currentLine].speakerName,
                dialogueLines[currentLine].text
            );
            currentLine++;
        }
        else
        {
            DialogueManager.Instance.HideDialogue();
            currentLine = 0; // 重置對話
        }
    }

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            isPlayerNearby = true;
            // TODO: 顯示「按 F 對話」提示
        }
    }

    void OnTriggerExit2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            isPlayerNearby = false;
            DialogueManager.Instance.HideDialogue();
            currentLine = 0;
        }
    }
}
```

### 10.3 對話管理器（Singleton 模式）

```csharp
// DialogueManager.cs
using UnityEngine;
using TMPro; // 需要安裝 TextMeshPro

public class DialogueManager : MonoBehaviour
{
    public static DialogueManager Instance; // Singleton

    [Header("UI 參考")]
    public GameObject dialoguePanel;
    public TextMeshProUGUI speakerText;
    public TextMeshProUGUI dialogueText;

    void Awake()
    {
        // Singleton 設定：確保只有一個 DialogueManager
        if (Instance == null)
            Instance = this;
        else
            Destroy(gameObject);
    }

    public void ShowDialogue(string speaker, string text)
    {
        dialoguePanel.SetActive(true);
        speakerText.text = speaker;
        dialogueText.text = text;
    }

    public void HideDialogue()
    {
        dialoguePanel.SetActive(false);
    }
}
```

---

## 11. 回合制戰鬥系統

### 11.1 戰鬥流程設計

```
玩家碰到敵人
    ↓
切換到戰鬥場景
    ↓
顯示戰鬥 UI（玩家 HP、敵人 HP、行動選單）
    ↓
玩家選擇行動（攻擊/道具/逃跑）
    ↓
計算傷害
    ↓
敵人回合 → 敵人攻擊玩家
    ↓
判斷勝負：
  ├── 敵人 HP = 0 → 玩家獲勝，獲得 EXP + 道具
  ├── 玩家 HP = 0 → 遊戲結束
  └── 繼續下一回合
```

### 11.2 戰鬥管理腳本

```csharp
// BattleManager.cs
using UnityEngine;
using System.Collections;

public enum BattleState { START, PLAYER_TURN, ENEMY_TURN, WON, LOST }

public class BattleManager : MonoBehaviour
{
    public static BattleManager Instance;

    [Header("戰鬥設定")]
    public BattleState currentState;

    // 戰鬥資料（從場景傳入）
    private PlayerStats player;
    private EnemyData enemy;
    private int enemyCurrentHP;

    void Awake()
    {
        if (Instance == null) Instance = this;
    }

    public void StartBattle(PlayerStats playerStats, EnemyData enemyData)
    {
        player = playerStats;
        enemy = enemyData;
        enemyCurrentHP = enemy.maxHP;
        currentState = BattleState.START;

        StartCoroutine(SetupBattle());
    }

    IEnumerator SetupBattle()
    {
        // 顯示開場訊息
        BattleUI.Instance.ShowMessage("遭遇了 " + enemy.enemyName + "！");
        yield return new WaitForSeconds(1.5f);

        // 進入玩家回合
        currentState = BattleState.PLAYER_TURN;
        BattleUI.Instance.ShowPlayerTurnUI();
    }

    // 玩家選擇「攻擊」
    public void OnPlayerAttack()
    {
        if (currentState != BattleState.PLAYER_TURN) return;

        int damage = Mathf.Max(player.attack - enemy.defense, 1);
        enemyCurrentHP -= damage;
        enemyCurrentHP = Mathf.Max(enemyCurrentHP, 0);

        BattleUI.Instance.ShowMessage("對 " + enemy.enemyName + " 造成 " + damage + " 點傷害！");
        BattleUI.Instance.UpdateEnemyHP(enemyCurrentHP, enemy.maxHP);

        if (enemyCurrentHP <= 0)
        {
            currentState = BattleState.WON;
            StartCoroutine(EndBattle());
        }
        else
        {
            currentState = BattleState.ENEMY_TURN;
            StartCoroutine(EnemyTurn());
        }
    }

    IEnumerator EnemyTurn()
    {
        BattleUI.Instance.HidePlayerTurnUI();
        yield return new WaitForSeconds(1f);

        int damage = Mathf.Max(enemy.attack - player.defense, 1);
        player.TakeDamage(damage);

        BattleUI.Instance.ShowMessage(enemy.enemyName + " 攻擊！造成 " + damage + " 點傷害！");
        BattleUI.Instance.UpdatePlayerHP(player.currentHP, player.maxHP);

        yield return new WaitForSeconds(1f);

        if (player.currentHP <= 0)
        {
            currentState = BattleState.LOST;
            StartCoroutine(EndBattle());
        }
        else
        {
            currentState = BattleState.PLAYER_TURN;
            BattleUI.Instance.ShowPlayerTurnUI();
        }
    }

    IEnumerator EndBattle()
    {
        if (currentState == BattleState.WON)
        {
            BattleUI.Instance.ShowMessage("勝利！獲得 " + enemy.expReward + " EXP！");
            player.GainExp(enemy.expReward);
            yield return new WaitForSeconds(2f);
            // 切換回探索場景
            SceneManager.LoadScene("MapScene");
        }
        else
        {
            BattleUI.Instance.ShowMessage("你被打倒了...");
            yield return new WaitForSeconds(2f);
            // 顯示 Game Over
            SceneManager.LoadScene("GameOverScene");
        }
    }
}
```

### 11.3 敵人資料（ScriptableObject）

```csharp
// EnemyData.cs
using UnityEngine;

[CreateAssetMenu(fileName = "New Enemy", menuName = "RPG/Enemy Data")]
public class EnemyData : ScriptableObject
{
    public string enemyName;
    public Sprite sprite;
    public int maxHP = 50;
    public int attack = 10;
    public int defense = 3;
    public int expReward = 30;
    public int goldReward = 20;
}
```

> 建立方式：Assets → 右鍵 → Create → RPG → Enemy Data

---

## 12. 物品與背包系統

### 12.1 物品資料（ScriptableObject）

```csharp
// ItemData.cs
using UnityEngine;

public enum ItemType { Consumable, Weapon, Armor, KeyItem }

[CreateAssetMenu(fileName = "New Item", menuName = "RPG/Item Data")]
public class ItemData : ScriptableObject
{
    public string itemName;
    public Sprite icon;
    public ItemType itemType;
    [TextArea] public string description;

    [Header("消耗品設定")]
    public int healAmount;    // 回血量
    public int mpRestore;     // 回魔量

    [Header("武器/防具設定")]
    public int attackBonus;
    public int defenseBonus;
}
```

### 12.2 背包管理器

```csharp
// InventoryManager.cs
using UnityEngine;
using System.Collections.Generic;

public class InventoryManager : MonoBehaviour
{
    public static InventoryManager Instance;

    [Header("背包設定")]
    public int maxSlots = 20;
    private List<ItemData> items = new List<ItemData>();

    void Awake()
    {
        if (Instance == null)
        {
            Instance = this;
            DontDestroyOnLoad(gameObject); // 切換場景不銷毀
        }
        else
        {
            Destroy(gameObject);
        }
    }

    public bool AddItem(ItemData item)
    {
        if (items.Count >= maxSlots)
        {
            Debug.Log("背包已滿！");
            return false;
        }
        items.Add(item);
        Debug.Log("獲得道具：" + item.itemName);
        return true;
    }

    public void RemoveItem(ItemData item)
    {
        items.Remove(item);
    }

    public void UseItem(ItemData item, PlayerStats player)
    {
        if (item.itemType == ItemType.Consumable)
        {
            player.Heal(item.healAmount);
            RemoveItem(item);
            Debug.Log("使用了 " + item.itemName + "，回復 " + item.healAmount + " HP");
        }
    }

    public List<ItemData> GetItems() => items;
}
```

---

## 13. 場景切換與存檔

### 13.1 場景切換

```csharp
// SceneTransition.cs
using UnityEngine;
using UnityEngine.SceneManagement;
using System.Collections;

public class SceneTransition : MonoBehaviour
{
    public string targetScene;
    public Vector2 playerSpawnPosition;

    void OnTriggerEnter2D(Collider2D other)
    {
        if (other.CompareTag("Player"))
        {
            StartCoroutine(LoadScene());
        }
    }

    IEnumerator LoadScene()
    {
        // 可加入淡入淡出效果
        yield return new WaitForSeconds(0.5f);

        // 儲存玩家出生點
        PlayerPrefs.SetFloat("SpawnX", playerSpawnPosition.x);
        PlayerPrefs.SetFloat("SpawnY", playerSpawnPosition.y);

        SceneManager.LoadScene(targetScene);
    }
}
```

> 記得在 **Build Settings**（`File → Build Settings`）加入所有場景！

### 13.2 簡易存檔系統（PlayerPrefs）

```csharp
// SaveSystem.cs
using UnityEngine;

public class SaveSystem : MonoBehaviour
{
    // 儲存遊戲
    public static void SaveGame(PlayerStats player)
    {
        PlayerPrefs.SetString("PlayerName", player.playerName);
        PlayerPrefs.SetInt("PlayerHP", player.currentHP);
        PlayerPrefs.SetInt("PlayerMaxHP", player.maxHP);
        PlayerPrefs.SetInt("PlayerLevel", player.level);
        PlayerPrefs.SetInt("PlayerExp", player.exp);
        PlayerPrefs.SetInt("PlayerAttack", player.attack);
        PlayerPrefs.SetFloat("PlayerPosX", player.transform.position.x);
        PlayerPrefs.SetFloat("PlayerPosY", player.transform.position.y);
        PlayerPrefs.SetString("CurrentScene", UnityEngine.SceneManagement.SceneManager.GetActiveScene().name);
        PlayerPrefs.Save();

        Debug.Log("遊戲已儲存！");
    }

    // 讀取遊戲
    public static void LoadGame(PlayerStats player)
    {
        if (!PlayerPrefs.HasKey("PlayerLevel")) return; // 沒有存檔

        player.playerName = PlayerPrefs.GetString("PlayerName");
        player.currentHP = PlayerPrefs.GetInt("PlayerHP");
        player.maxHP = PlayerPrefs.GetInt("PlayerMaxHP");
        player.level = PlayerPrefs.GetInt("PlayerLevel");
        player.exp = PlayerPrefs.GetInt("PlayerExp");
        player.attack = PlayerPrefs.GetInt("PlayerAttack");

        float x = PlayerPrefs.GetFloat("PlayerPosX");
        float y = PlayerPrefs.GetFloat("PlayerPosY");
        player.transform.position = new Vector3(x, y, 0);

        Debug.Log("遊戲已讀取！");
    }

    public static bool HasSaveData()
    {
        return PlayerPrefs.HasKey("PlayerLevel");
    }
}
```

---

## 14. UI 介面設計

### 14.1 建立 HUD（遊戲中的狀態列）

```
Hierarchy → 右鍵 → UI → Canvas
Canvas 下建立：
├── HPBar（Image - 血條背景）
│   └── HPBarFill（Image - 實際血條填充）
├── LevelText（TextMeshPro - 顯示等級）
├── GoldText（TextMeshPro - 顯示金幣）
└── MiniMap（RawImage - 小地圖，進階功能）
```

### 14.2 血條 UI 腳本

```csharp
// UIHealthBar.cs
using UnityEngine;
using UnityEngine.UI;
using TMPro;

public class UIHealthBar : MonoBehaviour
{
    public Image hpBarFill;
    public TextMeshProUGUI hpText;
    public TextMeshProUGUI levelText;

    private PlayerStats player;

    void Start()
    {
        player = FindObjectOfType<PlayerStats>();
    }

    void Update()
    {
        if (player == null) return;

        // 更新血條（0.0 ~ 1.0）
        float ratio = (float)player.currentHP / player.maxHP;
        hpBarFill.fillAmount = ratio;

        // 更新文字
        hpText.text = player.currentHP + " / " + player.maxHP;
        levelText.text = "Lv." + player.level;
    }
}
```

### 14.3 主選單設計

```csharp
// MainMenu.cs
using UnityEngine;
using UnityEngine.SceneManagement;

public class MainMenu : MonoBehaviour
{
    public void NewGame()
    {
        PlayerPrefs.DeleteAll(); // 清除舊存檔
        SceneManager.LoadScene("MapScene");
    }

    public void ContinueGame()
    {
        if (SaveSystem.HasSaveData())
        {
            string savedScene = PlayerPrefs.GetString("CurrentScene", "MapScene");
            SceneManager.LoadScene(savedScene);
        }
        else
        {
            Debug.Log("沒有存檔！");
        }
    }

    public void QuitGame()
    {
        Application.Quit();
    }
}
```

---

## 15. 專案實戰練習清單

依照以下順序完成，每個都是可測試的里程碑：

- [ ] **Milestone 1**：角色可以用 WASD 在空白場景移動
- [ ] **Milestone 2**：加入 Tilemap 地圖，角色碰到牆壁會被阻擋
- [ ] **Milestone 3**：角色有行走動畫（4個方向）
- [ ] **Milestone 4**：攝影機跟隨角色移動
- [ ] **Milestone 5**：地圖上放一個 NPC，靠近按 F 觸發對話框
- [ ] **Milestone 6**：地圖上放一個道具，碰到可以拾取，顯示在背包
- [ ] **Milestone 7**：碰到敵人觸發戰鬥場景，可以攻擊/使用道具/逃跑
- [ ] **Milestone 8**：勝利/失敗後正確切換場景
- [ ] **Milestone 9**：加入主選單、存檔/讀檔功能
- [ ] **Milestone 10**：加入 HUD 血條顯示
- [ ] **Bonus**：加入 BGM 和音效

---

## 16. 推薦學習資源

### 免費教學影片

| 資源 | 說明 |
|------|------|
| [Unity Learn](https://learn.unity.com) | Unity 官方教學，有 2D RPG 系列 |
| [Brackeys (YouTube)](https://www.youtube.com/@Brackeys) | 最受歡迎的 Unity 教學頻道（英文） |
| [Code Monkey (YouTube)](https://www.youtube.com/@CodeMonkeyUnity) | 高品質 Unity 教學（英文） |
| [Unity Taiwan 官方社群](https://www.facebook.com/groups/UnityTaiwan) | 中文 Unity 社群 |

### 免費遊戲素材

| 資源 | 說明 |
|------|------|
| [itch.io 免費素材](https://itch.io/game-assets/free/tag-rpg) | 大量免費 RPG 素材 |
| [OpenGameArt](https://opengameart.org) | 免費素材（音效/音樂/圖片） |
| [LPC Spritesheet Generator](https://sanderfrenken.github.io/Universal-LPC-Spritesheet-Character-Generator/) | 自訂 RPG 角色 Sprite |
| [Kenney.nl](https://kenney.nl/assets) | 高品質免費遊戲素材包 |

### 推薦書籍

- *Unity in Action*（Manning 出版）
- *Game Programming Patterns*（免費線上閱讀：gameprogrammingpatterns.com）

---

## 附錄：常見錯誤與解決方法

| 錯誤 | 原因 | 解決方法 |
|------|------|----------|
| 角色不移動 | 忘記掛腳本或 Rigidbody 2D | 確認 PlayerController 已掛到物件上 |
| 角色穿過牆壁 | 沒有 Collider | 對牆壁 Tilemap 加 `Tilemap Collider 2D` |
| 攝影機不跟隨 | Cinemachine Follow 未設定 | 把 Player 拖入 Cinemachine 的 Follow 欄位 |
| `NullReferenceException` | 變數沒有初始化 | 用 `GetComponent<>()` 在 `Start()` 中取得參考 |
| 動畫不播放 | Animator 狀態機設定錯誤 | 檢查 Transition 條件是否正確 |
| 場景切換後資料消失 | 物件被銷毀 | 在 `Awake()` 加入 `DontDestroyOnLoad(gameObject)` |

---

> **記住**：製作遊戲的關鍵是「持續做」。從小功能開始，測試成功後再加新功能。不要一開始就想把整個遊戲做完。先讓你的角色動起來，其他的一步一步來！

**祝你開發順利！🎮**
