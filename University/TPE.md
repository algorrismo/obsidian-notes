---
tags:
title: How to cheat in TPE
created: 2026-08-04
---
---


# TPE Auto Submit Script

যাদের এখনো TPE দেয়া হয়নি বা অনেক কষ্ট লাগে তাদের জন্য।

---

### কিভাবে ব্যবহার করবেন

1. যে সাবজেক্টের TPE দিতে হবে, সেই পেজে যান।
2. **Chrome** হলে → Right Click → **Inspect**  
   **Firefox** হলে → Right Click → **Inspect Element**
3. উপরে থেকে **Console** ট্যাব সিলেক্ট করুন।
4. নিচের কোডটা কপি করে Console-এ পেস্ট করুন → **Enter** চাপুন।

---

### ↓ এই কোডটা কপি করুন ↓

```js
(function(){
  [].forEach.call(
    document.querySelectorAll('input[type="radio"][value="5"]'),
    function(rdo){ rdo.checked = true }
  );
  document.getElementById("Comment").value = "awesome";
  document.forms[0].submit();
})();
```

---

### Value পরিবর্তন

- `value="5"` → Strongly Agree  
- `value="4"` → Agree  
- `value="3"` → Neutral  
- `value="2"` → Disagree  
- `value="1"` → Strongly Disagree  

Comment বদলাতে চাইলে `"awesome"` এর জায়গায় যা খুশি লিখুন।

প্রতিটা TPE পেজে আলাদা করে এই কাজ করতে হবে।