# 安裝 Gemini 套件
!pip install -q -U google-generativeai

# 匯入函式庫
import google.generativeai as genai
from google.colab import userdata
import os
import time

# 設定 API 金鑰
api_key = userdata.get('GEMINI_API_KEY')

if not api_key:
    print("❌ 無法讀取 GEMINI_API_KEY，請先在左邊 🔑 輸入你的 API 金鑰")
else:
    print(f"🔑 已讀取金鑰（部分遮蔽）：{api_key[:4]}...{api_key[-4:]}")
    genai.configure(api_key=api_key)

    # 選擇模型
    MODEL_NAME = "models/gemini-1.5-flash"
    model = genai.GenerativeModel(model_name=MODEL_NAME)

    # 讀取要摘要的原始內容（可貼入或從檔案讀）
    print("✍️ 請輸入你要摘要的內容（可貼一段文章）")
    long_text = input("👉 請輸入原始文章內容：\n")

    # 建立 prompt
    prompt = (
    f"請針對以下文章產出一段條理清晰的重點摘要，控制在適當篇幅內（不需要硬性限制字數），保持語意完整且便於理解。請使用條列式格式呈現內容：\n\n{long_text}"
)


    # 呼叫 Gemini 取得摘要
    try:
        print("\n🧠 正在生成摘要，請稍候...")
        time.sleep(2)
        response = model.generate_content(prompt)
        summary = response.text

        # 顯示結果
        print("\n✅ 摘要內容如下：\n")
        print(summary)

        # 儲存摘要
        with open("summary_output.txt", "w", encoding="utf-8") as f:
            f.write(f"原始內容：\n{long_text}\n\n摘要：\n{summary}")
        print("\n📄 已儲存為 summary_output.txt")

    except Exception as e:
        print(f"❌ 發生錯誤：{e}")
利用這個Python 腳本，可以自動將任何長文分析為簡短、易懂的條列式結論，使用者只需輸入原始文章內容，系統便會呼叫 Gemini 模型進行語意理解並輸出精簡摘要，適合用在新聞整理、學習筆記或用途。這個功能不只可以縮短閱讀時間，同時也可以讓使用者更完整的得取長文的大意。
