# VPS 租用推薦：搞懂 CN2 GIA、CMIN2 與國際線路的差別，按建站、跨境或開發用途挑對機房與方案

會去搜「VPS 租用推薦」的人，通常已經知道 VPS 是什麼了，卡住的是另一些問題：租哪個機房、價格差在哪、同樣 2 核 2G 為什麼有人賣 6.9 美元有人賣 79.9 美元。

這篇不從「VPS 是什麼」講起，直接處理決策順序。價格與方案以 DMIT 這家專做中國方向優化線路的主機商為例，因為它同時提供洛杉磯、香港、東京三個機房，而且每個機房都分三種線路，剛好可以把「線路」這個變數單獨拆出來看。

不過先說一句：VPS 的庫存和價格變動很快，同一系列還會因為硬體平台換代出現價差。以下價格是近期公開資料整理，下單前請以結帳頁實際顯示為準。

## 先決定使用者在哪，再決定租哪條線路

大部分選錯的情境，順序都反了：先看到便宜的價格，再看規格，最後才想到自己的使用者在哪。

合理的順序是反過來走的：

1. 你的服務主要給誰用（中國大陸、亞太、歐美，還是只有你自己遠端連）
2. 這群人連過去，走哪條線路最穩
3. 哪些機房有這條線路
4. 最後才是核心數、記憶體、流量、預算

三個典型情境，答案差很多。

**面向中國大陸使用者的網站或應用**：線路品質比 CPU 型號重要。晚高峰掉不掉速、三網（電信／聯通／移動）是不是都走得順，會直接反映在跳出率上。

**面向海外使用者的跨境電商或 API**：國際骨幹線路就夠用，沒必要為中國優化付溢價。這類需求通常流量吃得多，反而要看端口頻寬與月流量額度。

**只有自己用的開發測試機、CI/CD、爬蟲節點**：選最便宜的入門款，拉高一點流量就好。核心數對這種用途的影響，通常小於你想像。

## CN2 GIA、CMIN2、AS9929、國際 BGP：這幾個詞到底差在哪

這些名詞不是行銷詞，而是真的指不同的承載網路。

**CN2 GIA（AS4809）** 是中國電信的高端承載網，優先級高、晚高峰相對不容易塞。代價是貴，因為頻寬成本本身就高。

**CMIN2 / CMI** 是中國移動的國際網路。行動寬頻的用戶走移動自家線路，延遲與穩定度都不錯，價格通常比 CN2 GIA 低一截。

**AS9929（聯通國際精品線路）** 走的是聯通的高品質國際出口，比一般的 4837 線路穩，晚高峰丟包率低。

**國際 BGP / Tier 1** 則是 Telia、Zayo、Cogent 這類國際骨幹，對中國大陸沒有專門優化。香港節點走這條路，回中國大陸的延遲有可能比美國西岸還高，這是新手最常踩的坑。

同樣的 2 核 2G，走 CN2 GIA 的月付 79.9 美元，走國際線路的月付 12.9 美元。差的就是這條線。

## 洛杉磯、香港、東京怎麼選

**香港**的優勢是物理距離，到中國大陸沿海延遲通常在 20–50ms 這個區間，是美西與東京做不到的。缺點也很直接：同價位給的流量明顯少，香港 Premium 入門款 500GB 月流量，月付 39.9 美元。

**洛杉磯**是最多人選的折衷點。三網回程走 CN2 GIA 的 Premium 系列，從中國大陸過去延遲大約在 150ms 內，流量給得比香港寬鬆，價格也中間。EB（Eyeball）系列同價位流量更大。

**東京**離中國大陸比洛杉磯近，價格介於兩者之間。東京 Premium 入門月付 21.9 美元，是三地 Premium 系列裡最便宜的一檔。

## 以 DMIT 為例：三個機房、三種線路的實際方案

DMIT 是美國註冊的主機商，2018 年前後開始做 VPS，機房分布在洛杉磯、香港、東京。產品線統一分成三類：Premium（.Pro，CN2 GIA）、Eyeball（.EB，CMIN2 為主）、Tier 1（.T1，國際線路）。全系 KVM 虛擬化、AMD EPYC 處理器搭配 NVMe SSD，預設給 1 個 IPv4 加 1 個 IPv6/64，支援支付寶、PayPal、信用卡付款，也有中文客服。

有個容易被忽略的變數：**同一系列會因為硬體平台換代而出現價差**。目前看得到的有 AS3（EPYC 7003）、AN4（EPYC 9004）、AN5（EPYC 9005）三個代次，規格相同但標價差幾美元，庫存也各自獨立。看到同一個 TINY 有兩個價格，八成是這個原因，不是有人標錯。

### 洛杉磯 Premium（三網回程 CN2 GIA）

| 方案 | CPU | 記憶體 | 硬碟 | 月流量／端口 | 超量後 | 價格 | 購買 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TINY | 1 核 | 2GB | 20GB | 1TB／1Gbps | 4Mbps | $9.99/月 | [ 查看 TINY 方案](https://www.dmit.io/aff.php?aff=12046) |
| Pocket | 2 核 | 2GB | 40GB | 1.5TB／4Gbps | 4Mbps | $14.90/月 | [ 查看 Pocket 方案](https://www.dmit.io/aff.php?aff=12046) |
| STARTER | 2 核 | 2GB | 80GB | 3TB／10Gbps | 4Mbps | $29.90/月 | [ 查看 STARTER 方案](https://www.dmit.io/aff.php?aff=12046) |
| MINI | 4 核 | 4GB | 80GB | 5TB／10Gbps | 8Mbps | $58.88/月 | [ 查看 MINI 方案](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 4 核 | 4GB | 160GB | 7TB／10Gbps | 8Mbps | $74.99/月 | [ 查看 MICRO 方案](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 6 核 | 8GB | 160GB | 15TB／10Gbps | 10Mbps | $168.88/月 | [ 查看 MEDIUM 方案](https://www.dmit.io/aff.php?aff=12046) |
| LARGE | 8 核 | 16GB | 320GB | 25TB／10Gbps | 10Mbps | $338.88/月 | [ 查看 LARGE 方案](https://www.dmit.io/aff.php?aff=12046) |
| GIANT | 12 核 | 24GB | 640GB | 50TB／10Gbps | 10Mbps | $619.99/月 | [ 查看 GIANT 方案](https://www.dmit.io/aff.php?aff=12046) |

### 洛杉磯 Eyeball（三網回程 CMIN2）

| 方案 | CPU | 記憶體 | 硬碟 | 月流量／端口 | 超量後 | 價格 | 購買 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TINY | 1 核 | 2GB | 20GB | 1.5TB／2Gbps | 4Mbps | $9.99/月 | [ 查看 EB TINY](https://www.dmit.io/aff.php?aff=12046) |
| Pocket | 2 核 | 2GB | 40GB | 3TB／4Gbps | 4Mbps | $14.90/月 | [ 查看 EB Pocket](https://www.dmit.io/aff.php?aff=12046) |
| STARTER | 2 核 | 2GB | 80GB | 5TB／10Gbps | 4Mbps | $29.90/月 | [ 查看 EB STARTER](https://www.dmit.io/aff.php?aff=12046) |
| MINI | 4 核 | 4GB | 80GB | 10TB／10Gbps | 8Mbps | $58.88/月 | [ 查看 EB MINI](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 4 核 | 4GB | 160GB | 14TB／10Gbps | 8Mbps | $74.99/月 | [ 查看 EB MICRO](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 6 核 | 8GB | 160GB | 30TB／10Gbps | 10Mbps | $168.88/月 | [ 查看 EB MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| LARGE | 8 核 | 16GB | 320GB | 50TB／10Gbps | 10Mbps | $338.88/月 | [ 查看 EB LARGE](https://www.dmit.io/aff.php?aff=12046) |
| GIANT | 12 核 | 24GB | 640GB | 100TB／10Gbps | 10Mbps | $619.99/月 | [ 查看 EB GIANT](https://www.dmit.io/aff.php?aff=12046) |

EB 和 Pro 同價位的差別在流量：TINY 這檔，Pro 給 1TB，EB 給 1.5TB。如果你的使用者以移動、聯通為主，又不需要電信 CN2 GIA 等級的回程，EB 是更划算的一邊。

### Tier 1（洛杉磯／香港／東京三個機房價格相同）

| 方案 | CPU | 記憶體 | 硬碟 | 月流量／端口 | 超量後 | 價格 | 購買 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| WEE | 1 核 | 1GB | 20GB | 1TB／4Gbps | 50–100Mbps | $36.90/年 | [ 查看 T1 WEE](https://www.dmit.io/aff.php?aff=12046) |
| TINY | 1 核 | 1GB | 20GB | 2TB／4Gbps | 100Mbps | $6.90/月 | [ 查看 T1 TINY](https://www.dmit.io/aff.php?aff=12046) |
| STARTER | 1 核 | 2GB | 40GB | 4TB／10Gbps | 100Mbps | $12.90/月 | [ 查看 T1 STARTER](https://www.dmit.io/aff.php?aff=12046) |
| MINI | 2 核 | 2GB | 60GB | 8TB／10Gbps | 100Mbps | $21.90/月 | [ 查看 T1 MINI](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 4 核 | 4GB | 80GB | 16TB／10Gbps | 200Mbps | $32.90/月 | [ 查看 T1 MICRO](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 4 核 | 8GB | 160GB | 32TB／10Gbps | 200Mbps | $49.90/月 | [ 查看 T1 MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| LARGE | 8 核 | 16GB | 320GB | 64TB／10Gbps | 500Mbps | $99.90/月 | [ 查看 T1 LARGE](https://www.dmit.io/aff.php?aff=12046) |
| GIANT | 8 核 | 24GB | 640GB | 128TB／10Gbps | 1Gbps | $199.90/月 | [ 查看 T1 GIANT](https://www.dmit.io/aff.php?aff=12046) |

T1 系列值得單獨講一句：它的超量限速值是 100Mbps 到 1Gbps，跟 Pro／EB 的 4–10Mbps 不是同一個量級。如果你網站的月流量經常超標，T1 超量後還能正常服務，Pro 超量後基本等於斷線。

### 香港 Premium 與東京 Premium（CN2 GIA）

| 機房 | 方案 | CPU | 記憶體 | 硬碟 | 月流量／端口 | 價格 | 購買 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 香港 | TINY | 1 核 | 1GB | 20GB | 500GB／1Gbps | $39.90/月 | [ 查看香港 Pro TINY](https://www.dmit.io/aff.php?aff=12046) |
| 香港 | STARTER | 1 核 | 2GB | 40GB | 1TB／1Gbps | $79.90/月 | [ 查看香港 Pro STARTER](https://www.dmit.io/aff.php?aff=12046) |
| 香港 | MINI | 2 核 | 2GB | 60GB | 1.5TB／1Gbps | $119.90/月 | [ 查看香港 Pro MINI](https://www.dmit.io/aff.php?aff=12046) |
| 香港 | MICRO | 4 核 | 4GB | 80GB | 2TB／1Gbps | $159.90/月 | [ 查看香港 Pro MICRO](https://www.dmit.io/aff.php?aff=12046) |
| 香港 | MEDIUM | 4 核 | 8GB | 160GB | 2.5TB／1Gbps | $179.90/月 | [ 查看香港 Pro MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| 香港 | LARGE | 8 核 | 16GB | 320GB | 3TB／1Gbps | $239.90/月 | [ 查看香港 Pro LARGE](https://www.dmit.io/aff.php?aff=12046) |
| 香港 | GIANT | 8 核 | 24GB | 640GB | 6TB／1Gbps | $499.90/月 | [ 查看香港 Pro GIANT](https://www.dmit.io/aff.php?aff=12046) |
| 東京 | TINY | 1 核 | 1GB | 20GB | 500GB／1Gbps | $21.90/月 | [ 查看東京 Pro TINY](https://www.dmit.io/aff.php?aff=12046) |
| 東京 | STARTER | 1 核 | 2GB | 40GB | 1TB／1Gbps | $39.90/月 | [ 查看東京 Pro STARTER](https://www.dmit.io/aff.php?aff=12046) |
| 東京 | MINI | 2 核 | 2GB | 60GB | 2TB／1Gbps | $79.90/月 | [ 查看東京 Pro MINI](https://www.dmit.io/aff.php?aff=12046) |
| 東京 | MICRO | 4 核 | 4GB | 80GB | 4TB／1Gbps | $159.90/月 | [ 查看東京 Pro MICRO](https://www.dmit.io/aff.php?aff=12046) |
| 東京 | MEDIUM | 4 核 | 8GB | 160GB | 5TB／1Gbps | $259.90/月 | [ 查看東京 Pro MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| 東京 | LARGE | 8 核 | 16GB | 320GB | 8TB／1Gbps | $429.90/月 | [ 查看東京 Pro LARGE](https://www.dmit.io/aff.php?aff=12046) |
| 東京 | GIANT | 8 核 | 24GB | 640GB | 15TB／1Gbps | $799.90/月 | [ 查看東京 Pro GIANT](https://www.dmit.io/aff.php?aff=12046) |

### 東京 Eyeball（CMI 回程）

| 方案 | CPU | 記憶體 | 硬碟 | 月流量／端口 | 價格 | 購買 |
| --- | --- | --- | --- | --- | --- | --- |
| TINY | 1 核 | 1GB | 20GB | 1TB／1Gbps | $25.90/月 | [ 查看東京 EB TINY](https://www.dmit.io/aff.php?aff=12046) |
| STARTER | 1 核 | 2GB | 40GB | 2TB／2Gbps | $55.90/月 | [ 查看東京 EB STARTER](https://www.dmit.io/aff.php?aff=12046) |
| MINI | 2 核 | 2GB | 60GB | 3TB／2Gbps | $85.90/月 | [ 查看東京 EB MINI](https://www.dmit.io/aff.php?aff=12046) |
| MICRO | 4 核 | 4GB | 80GB | 4TB／4Gbps | $119.90/月 | [ 查看東京 EB MICRO](https://www.dmit.io/aff.php?aff=12046) |
| MEDIUM | 4 核 | 8GB | 160GB | 6TB／4Gbps | $179.90/月 | [ 查看東京 EB MEDIUM](https://www.dmit.io/aff.php?aff=12046) |
| LARGE | 8 核 | 16GB | 320GB | 12TB／4Gbps | $369.90/月 | [ 查看東京 EB LARGE](https://www.dmit.io/aff.php?aff=12046) |
| GIANT | 8 核 | 24GB | 640GB | 24TB／4Gbps | $749.90/月 | [ 查看東京 EB GIANT](https://www.dmit.io/aff.php?aff=12046) |

香港還有一個大頻寬系列（原本叫 Lite，後來更名 Standard，並取消過最低價的那一款），主打大端口與大流量、走移動方向線路，規格與價格調整比較頻繁，要買的話建議直接看官網當下的標示，別照抄舊文章裡的數字。

## 優惠碼現況：循環折扣比一次性折扣值錢

DMIT 的促銷節奏不快，沒有那種「全場五折」的大促，優惠碼數量也不多。以下幾個是多方資料都提到的，但**優惠碼這種東西隨時會失效**，結帳時請務必自己按驗證確認。

| 優惠碼 | 適用範圍 | 折扣 | 類型 |
| --- | --- | --- | --- |
| `LAX-EB-LAUNCH-NON-MONTHLY-RECURRING-20OFF` | 洛杉磯 EB，非月付 | 8 折 | 循環 |
| `202510_HKG_TYO_PRO_20OFF_RECURRING` | 香港／東京 Pro，季付以上 | 8 折 | 循環 |
| `202510_HKG_TYO_T1_30OFF_RECURRING` | 香港／東京 T1（不含 WEE），季付以上 | 7 折 | 循環 |
| `2025-TYO-T1-HI-GSL-NON-MONTHLY-30OFF` | 東京 T1 TINY 以上，季付以上 | 7 折 | — |
| `2025-TYO-T1-HI-GSL-MONTHLY-10OFF` | 東京 T1 TINY 以上，月付 | 9 折 | — |
| `Lite-Annually-Recur-30OFF` | Standard 系列，年付 | 7 折 | 循環 |
| `Lite-Semi-Annually-Recur-20OFF` | Standard 系列，半年付 | 8 折 | 循環 |
| `2025-XMAS-LAX-PRO-EB-ANNUALLY-STARTER-AND-HIGHER-15OFF-RECURRING` | 洛杉磯 Pro／EB，年付 STARTER 以上 | 85 折（另有回饋） | 循環 |
| `2025-XMAS-LAX-T1-10-OFF-RECURRING` | 洛杉磯 T1（不含 WEE） | 9 折 | 循環 |

「循環折扣」的意思是不只首期打折，續約也照折。以東京 T1 STARTER 年付為例，原價 154.8 美元，打完 7 折是 108.36 美元，而且明年續約還是這個價。這種比首年五折、隔年原價的玩法實在。

也有主機測評站提到，部分最低配套餐在年付時頁面會直接顯示折扣，不用輸入優惠碼。看到結帳頁自己變便宜，不用懷疑。

## 幾個下單前該知道的限制

**庫存是真的會缺。** 這家的熱門機型經常售完，尤其洛杉磯 Pro 的中階配置與香港系列。同一款可能隔一週補貨、也可能直接下架，看到有貨但還在猶豫，就是在賭。

**換 IP 要錢。** 一般情況下更換 IP 需付費，行情約 5 美元一次；部分系列如果開到不可用的 IP，不一定能免費換。要拿來做會被針對的用途，這筆成本要先算進去。

**硬體平台換代會有價差。** AS3、AN4、AN5 是不同代次的 EPYC，同規格不同價。有人會覺得被差別待遇，實際上就是不同批機器。

**維護通知不一定及時。** 有第三方評測提到，DMIT 在升級宿主機時通常不會提前發信，可能突然發現伺服器短暫不可用。對 SLA 有硬性要求、需要書面保證的業務，這點要自己評估。

**香港 T1 不是「香港就快」。** 它走國際骨幹，對中國大陸沒有優化，回程延遲有可能高於洛杉磯。如果你的使用者主要在中國大陸，別因為「香港比較近」就買 T1。

## 不同需求對應的選擇路徑

- **個人練手、開發測試、爬蟲節點**：Tier 1 TINY，月付 6.9 美元，三個機房同價。香港或東京看你要哪個地區的 IP。
- **面向中國大陸的中小型網站**：洛杉磯 EB TINY 或 Pro TINY，月付 9.99 美元，先跑一兩個月看實際延遲再決定要不要加錢升線路。
- **中國大陸使用者為主、對延遲敏感**：香港 Pro TINY，月付 39.9 美元。貴，但 20–50ms 這個數字是美西買不到的。
- **流量吃很兇的海外業務**：Tier 1 MEDIUM 以上，或 EB 的中階配置。重點是超量後還有 100Mbps 以上可用。
- **日本人或東南亞使用者**：東京 EB，同價位流量比 Pro 大，CMI 回程對亞太方向夠用。
- **需要持續承受攻擊的站點**：DMIT 另有 Premium Secure 系列，走 CN2 GIA 加防護，價格明顯更高。一般站點不需要為這個付費。

## 常見問題

**流量用完會直接停機嗎？**
不會。超量後降速繼續跑，這是 DMIT 這幾年一直在用的做法。但降速幅度差很多：Pro 與 EB 系列只剩 4–10Mbps，等於幾乎不能用；Tier 1 是 100Mbps 到 1Gbps，還能撐住一般網站。

**月付還是年付？**
線路不確定性高的時候先月付，測完一兩個晚高峰再決定。確認沒問題就轉年付，配合循環折扣碼通常能省兩到三成。香港這種單價高的機房，年付鎖價的意義比較大。

**優惠碼可以跟其他折扣疊加嗎？**
一般不行，一筆訂單通常只接受一組優惠碼。輸入後按驗證，系統會直接告訴你能不能用。

**支援哪些付款方式？**
支付寶、PayPal、信用卡都可以，也有中文客服。

**有沒有官方測試 IP 可以先測？**
有，各機房各線路都有對應的測試位址與 Looking Glass，買之前 ping 一輪，比看任何評測都準。

**同樣的 VPS 為什麼有人說很好有人說很貴？**
因為它賣的其實是線路與不超售的資源，不是便宜的規格。你的用途如果不需要中國優化線路，它就是貴；需要的話，同價位很難找到替代。

## 最後

租 VPS 真正要做的決定只有一個：**你的使用者從哪裡連進來**。想清楚這點，線路就定了，機房跟著定，剩下規格與預算都是次要的調整。

別人的推薦清單可以當成起點，但不能當答案。先租最低配、月付、實測一輪晚高峰，再決定要不要升級或改買年付——這條路走下來，通常比一次買對三年省下的錢更多。

想直接看各機房目前的方案與庫存，可以從這裡進去：👉 [查看 DMIT 各機房方案與庫存](https://www.dmit.io/aff.php?aff=12046)
