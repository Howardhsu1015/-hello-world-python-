# ai_exploration.md
- **AI 平台**：Google Gemini
- **編程環境**：Google Colab
- **選擇原因**：
  - Gemini 是 Google 推出的生成式 AI，介面直觀、回答速度快
  - Colab 是線上 Python 編輯器，免安裝且支援即時執行程式碼
### ✅ Prompt 1：請解釋什麼是 AI？

**AI 回覆：**  
人工智慧（Artificial Intelligence，簡稱 AI）是一種讓機器模仿人類智慧行為的技術。它可以讓電腦執行理解語言、辨識影像、下棋、推薦內容等任務。AI 技術包含機器學習、深度學習與自然語言處理。簡單來說，AI 讓電腦「看得懂、聽得懂、能思考」。

---

### ✅ Prompt 2：幫我寫一個 Python 程式，輸入一個整數陣列，輸出所有數字的總和，並解釋每一行的程式碼。

**AI 回覆：**

```python
# 定義一個函式來計算陣列總和
def sum_array(nums):
    total = 0  
    for num in nums:  
        total += num 
    return total 

# 測試陣列
numbers = [1, 2, 3, 4, 5]

# 印出總和
print("總和為：", sum_array(numbers

### ✅ Prompt 3：請幫我解釋「Prompt Engineering」是什麼？

**AI 回覆：**  
Prompt Engineering（提示工程）是設計給 AI 的輸入文字提示（prompt）的一種技巧。透過調整語句的方式、提供明確的上下文、加入範例等方式，我們可以讓 AI 更精準地理解我們的需求，並產生符合預期的回應。這項技巧對於與像 ChatGPT、Gemini 這類語言模型互動時特別重要。

---

### ✅ Prompt 4：請幫我列出 AI 在電機工程領域的應用

**AI 回覆：**  
AI 在電機工程領域的應用包含：
- 自動化控制系統（如智慧工廠）
- 電力系統負載預測與能源管理（智慧電網）
- 機器人路徑規劃與感測器資料處理
- 電子設計自動化（EDA）工具優化
- 故障預測與維修（Predictive Maintenance）

---

### ✅ Prompt 5：幫我解釋 LeetCode 題目 Two Sum 並用 Python 寫出解法

**AI 回覆：**  
**題目：**  
給定一個整數陣列 `nums` 和一個目標數字 `target`，請找出陣列中兩個數字，其總和等於 `target`，並回傳他們的索引。

**Python 解法：**

```python
def twoSum(nums, target):
    hashmap = {}  
    for i, num in enumerate(nums):
        complement = target - num 
        if complement in hashmap:
            return [hashmap[complement], i] 
        hashmap[num] = i
![image](https://github.com/user-attachments/assets/cc519d0f-d0ad-496e-93f4-4e05f8d90530)
