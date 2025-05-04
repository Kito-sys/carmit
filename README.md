import streamlit as st
import openai

# הגדרת המפתח הסודי של OpenAI
openai.api_key = st.secrets["openai_api_key"]

# כותרת ראשית
st.title("👩‍⚖️ העוזר המשפטי האישי של עו\"ד כרמית יודוביץ' כהן")

# קלט טקסט מהמשתמש
user_input = st.text_area("כתבי את המשימה המשפטית שלך כאן:")

# העלאת קובץ משפטי
uploaded_file = st.file_uploader("העלאת קובץ משפטי (לא חובה)", type=["pdf", "docx", "txt"])

# כפתור שליחה
if st.button("שלח/י משימה"):
    with st.spinner("העוזר המשפטי מנתח את הבקשה..."):
        # בקשה ל־GPT
        response = openai.ChatCompletion.create(
            model="gpt-4",
            messages=[
                {"role": "system", "content": "אתה עוזר משפטי אישי. ענה כמו עו\"ד מקצועי שעובד בשלבים: 1. הבנת משימה 2. איסוף מידע 3. יצירת טיוטה."},
                {"role": "user", "content": user_input}
            ]
        )
        st.success("העוזר המשפטי הגיב:")
        st.write(response.choices[0].message["content"])
# carmit
