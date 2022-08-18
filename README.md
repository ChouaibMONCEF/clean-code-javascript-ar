# clean-code-javascript

## المحتوى

1. [مقدمة](#مقدمة)
2. [المتغيرات](#المتغيرات)
3. [الدوال](#الدوال)
4. [Objects و Data Structures](#objects-و-data-structures)
5. [Classes](#classes)
6. [SOLID](#solid)
7. [التجريب](#التجريب)
8. [التنسيق (Concurrency)](<#التنسيق(Concurrency)>)
9. [معالجة الاخطاء (Error Handling)](<#معالجة-الاخطاء(error-handling)>)
10. [التشكيل](#التشكيل)
11. [الملاحظات](#الملاحظات)
12. [ترجمة](#ترجمة)

## مقدمة

![Humorous image of software quality estimation as a count of how many expletives
you shout when reading code](https://www.osnews.com/images/comics/wtfm.jpg)

مبادئ هندسة البرمجيات ، من كتاب روبرت سي مارتن
[_Clean Code_](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882) ،
تتكيف مع JavaScript. هذا ليس دليل أسلوب. إنه دليل للإنتاج
برنامج [قابل للقراءة وقابل لإعادة الاستخدام وقابل لإعادة التصنيع](https://github.com/ryanmcdermott/3rs-of-software-architecture) في جافا سكريبت.

ليس كل مبدأ هنا يجب اتباعه بدقة ، وحتى أقل من ذلك سيكون
متفق عليه عالميا. هذه إرشادات وليس أكثر ، لكنها كذلك
تلك التي تم تدوينها على مدى سنوات عديدة من الخبرة الجماعية من قبل مؤلفي
_ كود نظيف_.

يزيد عمر حرفة هندسة البرمجيات لدينا عن 50 عامًا ، ونحن كذلك
لازلنا نتعلم الكثير. عندما تكون هندسة البرمجيات قديمة قدم الهندسة
في حد ذاته ، ربما حينئذٍ سيكون لدينا قواعد أصعب يجب اتباعها. الآن ، دع هؤلاء
المبادئ التوجيهية بمثابة محك لتقييم جودة
كود JavaScript الذي تنتجه أنت وفريقك.

شيء آخر: معرفة هذه لن تجعلك على الفور برنامجًا أفضل
المطور ، والعمل معهم لسنوات عديدة لا يعني أنك لن ترتكب
اخطاء. يبدأ كل جزء من الكود كمسودة أولى ، مثل الحصول على الطين الرطب
تتشكل في شكلها النهائي. أخيرًا ، نقوم بإزالة العيوب عندما
نراجعها مع أقراننا. لا تضغط على نفسك بسبب المسودات الأولى التي تحتاج
التحسين. تغلب على الكود بدلا من ذلك!

## **المتغيرات**

### استعمل اسماء متغيرات دات معنى

**سيئ:**

```javascript
const yyyymmdstr = moment().format("YYYY/MM/DD")
```

**جيد:**

```javascript
const currentDate = moment().format("YYYY/MM/DD")
```

**[⬆ العودة للاعلى](#المحتوى)**
