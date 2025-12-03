# 🟦 Session Persistence  
## ذخیره‌سازی موقت داده‌ها در React با استفاده از `sessionStorage`

---

## ا🔵 Session Persistence چیست؟

**اSession Persistence** یعنی حفظ داده‌ها در طول یک «جلسه» کاربر تا زمانی که تب مرورگر بسته شود.  
این کار باعث می‌شود اطلاعات بعد از رفرش یا جابه‌جایی بین صفحات از بین نرود.

---

## 🔵 چرا Session Persistence مهم است؟

- جلوگیری از از دست رفتن داده‌ها  
- بهبود تجربه کاربری  
- مناسب فرم‌های چندمرحله‌ای  
- حفظ وضعیت UI  
- مشابه اپلیکیشن‌های native

---

## 🔵 تفاوت `sessionStorage` و `localStorage`

| ویژگی | `sessionStorage` | `localStorage` |
|-------|------------------|----------------|
| مدت نگهداری | تا بستن تب | دائمی |
| سطح دسترسی | فقط همان تب | همه تب‌ها |
| کاربرد | داده موقت = فرم، فیلتر | داده پایدار = token، تنظیمات |

---

# 🟦 پیاده‌سازی Session Persistence در React

## ✔️ مثال ساده

```jsx
import { useState, useEffect } from "react";

export default function App() {
  const [name, setName] = useState(() => {
    return sessionStorage.getItem("name") || "";
  });

  useEffect(() => {
    sessionStorage.setItem("name", name);
  }, [name]);

  return (
    <input
      value={name}
      onChange={e => setName(e.target.value)}
      placeholder="Enter your name"
    />
  );
}
```
# 🟦 هوک حرفه‌ای: `useSessionState`

```jsx
import { useState, useEffect } from "react";

export function useSessionState(key, defaultValue) {
  const [value, setValue] = useState(() => {
    const saved = sessionStorage.getItem(key);
    return saved ? JSON.parse(saved) : defaultValue;
  });

  useEffect(() => {
    sessionStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
}
```

# ✔️ استفاده:

```jsx
const [formData, setFormData] = useSessionState("myForm", {
  name: "",
  email: "",
});
```
# 🟦 موارد کاربرد Session Persistence
🔸 فرم‌های چندمرحله‌ای (Multi-Step)

🔸 حفظ فیلترها و وضعیت UI

🔸 ذخیره موقت داده پروفایل

🔸 ذخیره‌سازی حالت بازی یا امتیازات

🔸 جلوگیری از گم شدن داده‌ها در رفرش

# 🟦 نکات مهم
- برای داده‌های حساس استفاده نشود

- بعد از بستن تب داده پاک می‌شود

- مناسب داده موقت و غیردائمی است

# 🟦 جمع‌بندی

ا Session Persistence یعنی نگهداری موقت داده‌ها در طول یک Session.

با sessionStorage و React Hook‌ها به‌راحتی و تمیز قابل پیاده‌سازی است.

این الگو رفتار وب‌اپ را به تجربه اپلیکیشن‌های native نزدیک می‌کند و از بین رفتن داده‌ها جلوگیری می‌کند.
