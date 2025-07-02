# 安裝 Gemini 套件
!pip install -q -U google-generativeai

# 匯入函式庫
import google.generativeai as genai
from google.colab import userdata
import os
import time

# 設定金鑰
api_key = userdata.get('GEMINI_API_KEY')

if not api_key:
    print("❌ 無法讀取 GEMINI_API_KEY，請先在左邊 🔑 輸入你的 API 金鑰")
else:
    print(f"🔑 已讀取金鑰（部分遮蔽）：{api_key[:4]}...{api_key[-4:]}")
    genai.configure(api_key=api_key)

    # 選擇模型
    MODEL_NAME = "models/gemini-1.5-flash"
    model = genai.GenerativeModel(model_name=MODEL_NAME)

    # Prompt 清單（原始 + 優化各 5 組）
    prompt_pairs = [
        (
            "請幫我寫一段 Python 最好的入門方法",
            "你是一位資深 Python 老師。請向從未寫過程式的高中生介紹如何入門學 Python，使用步驟教學，並搭配簡單範例。"
        ),
        (
            "請解釋什麼是人工智慧",
            "請一步步解釋什麼是人工智慧。從定義開始，接著說明運作方式，然後提供生活中的一個實例，最後說明它可能帶來的好處與挑戰。"
        ),
        (
            "請簡單介紹永續發展是什麼",
            "請為一份環境教育講義撰寫簡介，清楚介紹永續發展的意義、三大面向，並用 100 字左右的說明讓 18 歲學生理解。"
        ),
        (
            "什麼是氣候變遷？",
            "假設你正在對高中學生解釋氣候變遷，請用精確的語言和生活例子說明原因與影響。"
        ),
        (
            "人工智慧未來會取代人類嗎？",
            "請用中立語氣，探討人工智慧是否可能取代人類的部分工作，並分別列出樂觀與悲觀觀點。"
        ),
    ]

    # 發送 prompt 並儲存回應
    for idx, (original_prompt, optimized_prompt) in enumerate(prompt_pairs, 1):
        for version, prompt in zip(["original", "optimized"], [original_prompt, optimized_prompt]):
            print(f"\n🟡 正在處理第 {idx} 組（{version}）...")

            try:
                time.sleep(2)
                response = model.generate_content(prompt)
                answer = response.text

                # 顯示回應
                print(f"✅ 回應內容：\n{answer[:300]}...\n")

                # 儲存為檔案
                filename = f"response_{idx}_{version}.txt"
                with open(filename, "w", encoding="utf-8") as f:
                    f.write(f"Prompt:\n{prompt}\n\nResponse:\n{answer}")

                print(f"📄 已儲存：{filename}")

            except Exception as e:
                print(f"❌ 發生錯誤：{e}")

編號	類型	      Prompt 摘要	Gemini 回覆摘要
1	原始	         Python 入門	        簡單一句描述 + 函數說明
1	優化	        老師教高中生入門 Python	   條列式步驟 + 範例程式 + 解釋明確
2	原始	         什麼是 AI	定義 AI 的一句話
2	優化	         分步說明 AI + 舉例	明確定義 → 應用 → 影響 → 優缺點
我針對 5 組提示進行了 prompt 優化，發現原始的 prompt 較為簡單，不能完整表達prompt的意思，導致 AI 回覆內容有時候過於籠統。而在優化提示中，透過加入角色、受眾、任務說明等方式，能顯著提升 AI 輸出的結構、深度與貼近需求的程度。特別是 Chain-of-Thought 技術在概念解釋型題目中效果明顯，能讓模型逐步產生更具邏輯性的內容。整體來說，優化 prompt 大幅提升了 AI 的可用性與內容品質。
