# File Browser Agent עם תמיכה ב-Skills 🚀

יישום שולחני מתקדם מבוסס **Electron**, המשלב דפדוף בקבצים יחד עם סוכן AI עוצמתי. הסוכן מבין את סביבת הקבצים המקומית, מסוגל לבחור קבצים ותיקיות, לקרוא ולכתוב מידע, ולהפעיל **Skills** (מיומנויות) מותאמים אישית לביצוע משימות מורכבות.

---

## ✨ תכונות עיקריות

- **Discovery & Tool Calling ל-Skills:** גילוי אוטומטי וטעינה דינמית של מיומנויות מתוך קבצי `SKILL.md`.
- **ניהול קטלוג Skills:** יצירת קטלוג מרכזי המועבר ישירות למודל ה-AI.
- **טעינה בזמן אמת:** תמיכה ב-IPC לעדכון וריענון רשימת ה-Skills בזמן הרצה.
- **כלי `activate_skill` ייעודי:** מאפשר למודל לטעון הנחיות עבודה מלאות בזמן אמת לפי סוג המשימה.

---

## 💻 דרישות מערכת

לפני התחלת העבודה, ודאו שמותקנים אצלכם הרכיבים הבאים:

| רכיב | דרישה |
| :--- | :--- |
| **סביבת הרצה** | Node.js בגירסה **18 ומעלה** |
| **מערכת הפעלה** | Windows |
| **מפתח API** | Anthropic API Key תקף (`sk-ant-...`) |

---

## 🛠️ התקנה והרצה

פתחו את המסוף (Terminal / PowerShell) בתיקיית הפרויקט והריצו את הפקודות הבאות:

```powershell
# 1. התקנת תלויות הפרויקט
npm i

# 2. התקנת Electron
node node_modules/electron/install.js

# 3. הרצת היישום בסביבת פיתוח
npm run dev
```

---

## ⚙️ הגדרת משתני סביבה (`.env`)

במידה וברצונכם להגדיר מיקום מותאם אישית לתיקיית ה-Skills או להגדיר את מפתח ה-API, צרו קובץ בשם `.env` בשורש הפרויקט והוסיפו את ההגדרות הבאות:

```env
# נתיב מותאם אישית לתיקיית ה-Skills (אופציונלי)
FILE_BROWSER_SKILLS_DIR=C:\Users\<username>\.file-browser-agent\skills

# מפתח ה-API של Anthropic (חובה לחיבור למודל)
ANTHROPIC_API_KEY=sk-ant-your-api-key-here
```

---

## 📁 ניהול ויצירת Skills

### מיקום תיקיית ברירת המחדל
ברירת המחדל של המערכת לחיפוש Skills היא:
`C:\Users\<username>\.file-browser-agent\skills`

ניתן ליצור את התיקייה במהירות באמצעות פקודת PowerShell:
```powershell
mkdir "$env:USERPROFILE\.file-browser-agent\skills"
```

---

### מבנה קובץ `SKILL.md`

כל Skill מוגדר בתוך תיקייה ייעודית המכילה קובץ בשם `SKILL.md`. הקובץ כולל חלק עליון של הגדרות (Frontmatter) ולאחריו הנחיות מפורטות למודל:

```md
---
name: summarize_folder
description: Summarize the contents of a selected folder and list important files.
---

When the user asks for a summary of a folder, inspect the directory contents,
list the main files, and provide a concise report in Hebrew.
```

---

## 🔄 איך המנגנון עובד?

1. **סריקה וטעינה:** האפליקציה סורקת את תיקיית ה-Skills ומאתרת את כל קבצי ה-`SKILL.md`.
2. **בניית קטלוג:** מופק קטלוג מרוכז המכיל את השם והתיאור של כל Skill.
3. **סנכרון מול המודל:** הקטלוג מוזן למודל דרך ה-System Prompt וכלי ה-`activate_skill`.
4. **אקטיבציה:** כאשר המשתמש מבקש משימה המתאימה ל-Skill מסוים, המודל מפעיל את כלי ה-`activate_skill`.
5. **טעינת הנחיות מלאות:** המערכת טוענת את תוכן ה-`SKILL.md` הרלוונטי ומעבירה את ההנחיות המפורטות למודל להמשך הביצוע.
