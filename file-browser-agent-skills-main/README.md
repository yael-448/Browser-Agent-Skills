File Browser Agent עם תמיכה ב-Skills 🚀יישום שולחני מתקדם מבוסס Electron, המשלב דפדוף בקבצים יחד עם סוכן AI עוצמתי. הסוכן מבין את סביבת הקבצים המקומית, מסוגל לבחור קבצים ותיקיות, לקרוא ולכתוב מידע, ולהפעיל Skills (מיומנויות) מותאמים אישית לביצוע משימות מורכבות.✨ תכונות עיקריותDiscovery & Tool Calling ל-Skills: גילוי אוטומטי וטעינה דינמית של מיומנויות מתוך קבצי SKILL.md.ניהול קטלוג Skills: יצירת קטלוג מרכזי המועבר ישירות למודל ה-AI.טעינה בזמן אמת: תמיכה ב-IPC לעדכון וריענון רשימת ה-Skills בזמן הרצה.כלי activate_skill ייעודי: מאפשר למודל לטעון הנחיות עבודה מלאות בזמן אמת לפי סוג המשימה.💻 דרישות מערכתלפני להתחלת העבודה, ודאו שמותקנים אצלכם הרכיבים הבאים:רכיבדרישהסביבת הרצהNode.js בגירסה 18 ומעלהמערכת הפעלהWindowsמפתח APIAnthropic API Key תקף (sk-ant-...)🛠️ התקנה והרצהפתחו את המסוף (Terminal / PowerShell) בתיקיית הפרויקט והריצו את הפקודות הבאות:PowerShell# 1. התקנת תלויות הפרויקט
npm i

# 2. התקנת Electron
node node_modules/electron/install.js

# 3. הרצת היישום בסביבת פיתוח
npm run dev
⚙️ הגדרת משתני סביבה (.env)במידה וברצונכם להגדיר מיקום מותאם אישית לתיקיית ה-Skills או להגדיר את מפתח ה-API, צרו קובץ בשם .env בשורש הפרויקט והוסיפו את ההגדרות הבאות:קטע קוד# נתיב מותאם אישית לתיקיית ה-Skills (אופציונלי)
FILE_BROWSER_SKILLS_DIR=C:\Users\<username>\.file-browser-agent\skills

# מפתח ה-API של Anthropic (חובה לחיבור למודל)
ANTHROPIC_API_KEY=sk-ant-your-api-key-here
📁 ניהול ויצירת Skillsמיקום תיקיית ברירת המחדלברירת המחדל של המערכת לחיפוש Skills היא:PlaintextC:\Users\<username>\.file-browser-agent\skills
ניתן ליצור את התיקייה במהירות באמצעות פקודת PowerShell:PowerShellmkdir "$env:USERPROFILE\.file-browser-agent\skills"
מבנה קובץ SKILL.mdכל Skill מוגדר בתוך תיקייה ייעודית המכילה קובץ בשם SKILL.md. הקובץ כולל חלק עליון של הגדרות (Frontmatter) ולאחריו הנחיות מפורטות למודל:Markdown---
name: summarize_folder
description: Summarize the contents of a selected folder and list important files.
---

When the user asks for a summary of a folder, inspect the directory contents,
list the main files, and provide a concise report in Hebrew.
🔄 איך המנגנון עובד?Plaintext┌────────────────────────┐      ┌────────────────────────┐      ┌────────────────────────┐
│  1. סריקת ה-Skills     │ ───> │  2. יצירת הקטלוג      │ ───> │  3. העברת הנתונים      │
│  טעינת קבצי SKILL.md   │      │  איגוד שמות ותיאורים   │      │  ל-System Prompt ולכלי │
└────────────────────────┘      └────────────────────────┘      └────────────────────────┘
                                                                            │
                                                                            ▼
┌────────────────────────┐      ┌────────────────────────┐      ┌────────────────────────┐
│  6. ביצוע המשימה       │ <─── │  5. קבלת ההנחיות       │ <─── │  4. הפעלת Skill        │
│  בהתאם להנחיות המלאות  │      │  טעינת קובץ SKILL.md   │      │  שימוש ב-activate_skill│
└────────────────────────┘      └────────────────────────┘      └────────────────────────┘
סריקה וטעינה: האפליקציה סורקת את תיקיית ה-Skills ומאתרת את כל קבצי ה-SKILL.md.בניית קטלוג: מופק קטלוג מרוכז המכיל את השם והתיאור של כל Skill.סנכרון מול המודל: הקטלוג מוזן למודל דרך ה-System Prompt וכלי ה-activate_skill.אקטיבציה: כאשר המשתמש מבקש משימה המתאימה ל-Skill מסוים, המודל מפעיל את כלי ה-activate_skill.טעינת הנחיות מלאות: המערכת טוענת את תוכן ה-SKILL.md הרלוונטי ומעבירה את ההנחיות המפורטות למודל להמשך ביצוע הביצוע.
