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
مكيفة مع JavaScript. هذا ليس دليل أسلوب. إنه دليل للإنتاج
برنامج [قابل للقراءة وقابل لإعادة الاستخدام وقابل لإعادة التصنيع](https://github.com/ryanmcdermott/3rs-of-software-architecture) في جافا سكريبت.

ليس كل مبدأ هنا يجب اتباعه بدقة ، وحتى أقل من ذلك سيكون
متفق عليه عالميا. هذه إرشادات وليس أكثر ، لكنها إرشادات تم تدوينها على مدى سنوات عديدة من الخبرة الجماعية من قبل مؤلفي
_ clean code _.

يزيد عمر حرفة هندسة البرمجيات عن 50 عامًا ، وكذلك
لازلنا نتعلم الكثير من الأشياء. "عندما تكون هندسة البرمجيات قديمة قدم الهندسة
في حد ذاتها" ، ربما حينئذٍ سيكون لدينا قواعد أصعب يجب اتباعها. الآن ، دع هؤلاء
المبادئ التوجيهية بمثابة محك لتقييم جودة
كود JavaScript الذي تنتجه أنت وفريقك.

شيء آخر: معرفة هذه المبادئ لن تجعلك على الفور أفضل مبرمج على الإطلاق
، والعمل معها لسنوات عديدة لا يعني أنك لن ترتكب
اخطاء.
يبدأ كل جزء من الكود كمسودة أولى ، مثل العمل على طين رطب
لن تحصل على الشكل النهائي من الوهلة الأولى فنحن دائما ما نقوم بإزالة العيوب عندما .
نراجعها مع أقراننا.إذن لا تضغط على نفسك بسبب المسودات الأولى التي تحتاج
التحسين.
تغلب على الكود بدلا من ذلك!

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

### استعمل نفس المفردات لنفس نوع المتغيرات

**سيئ:**

```javascript
getUserInfo()
getClientData()
getCustomerRecord()
```

**جيد:**

```javascript
getUser()
```

**[⬆ العودة للاعلى](#المحتوى)**

### استعمل اسماء سهلة الفهم و يمكن البحث عليها

سنقرأ كود أكثر مما سنكتبه. من المهم أن الكود الذي نكتبه قابل للقراءة والبحث. عدم تسمية المتغيرات التي ينتهي بها الأمر إلى أن تكون ذات مغزى لفهم برنامجنا ، يجعل الامر صعبا على القراء. اجعل أسماءك قابلة للبحث. يمكن أن تساعد أدوات مثل
[buddy.js](https://github.com/danielstjules/buddy.js) و
[ESLint](https://github.com/eslint/eslint/blob/660e0918933e6e7fede26bc675a0763a6b357c94/docs/rules/no-magic-numbers.md)
في تحديد الثوابت غير المسماة.

**سيئ:**

```javascript
// What the heck is 86400000 for?
setTimeout(blastOff, 86400000)
```

**جيد:**

```javascript
// Declare them as capitalized named constants.
const MILLISECONDS_PER_DAY = 60 * 60 * 24 * 1000 //86400000;

setTimeout(blastOff, MILLISECONDS_PER_DAY)
```

**[⬆ العودة للاعلى](#المحتوى)**

### Use explanatory variables

**سيئ:**

```javascript
const address = "One Infinite Loop, Cupertino 95014"
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/
saveCityZipCode(
  address.match(cityZipCodeRegex)[1],
  address.match(cityZipCodeRegex)[2]
)
```

**جيد:**

```javascript
const address = "One Infinite Loop, Cupertino 95014"
const cityZipCodeRegex = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/
const [_, city, zipCode] = address.match(cityZipCodeRegex) || []
saveCityZipCode(city, zipCode)
```

**[⬆ العودة للاعلى](#المحتوى)**

### تجنب التخطيط الذهني

الواضح دائمًا أفضل من الضمني.

**سيئ:**

```javascript
const locations = ["Austin", "New York", "San Francisco"]
locations.forEach((l) => {
  doStuff()
  doSomeOtherStuff()
  // ...
  // ...
  // ...
  // Wait, what is `l` for again?
  dispatch(l)
})
```

**جيد:**

```javascript
const locations = ["Austin", "New York", "San Francisco"]
locations.forEach((location) => {
  doStuff()
  doSomeOtherStuff()
  // ...
  // ...
  // ...
  dispatch(location)
})
```

**[⬆ العودة للاعلى](#المحتوى)**

### لا تقم بإضافة سياق غير ضروري

إذا أخبرك اسم class/object بشيء ما ، فلا تكرر ذلك في اسم المتغير الخاص بك.

**سيئ:**

```javascript
const Car = {
  carMake: "Honda",
  carModel: "Accord",
  carColor: "Blue",
}

function paintCar(car, color) {
  car.carColor = color
}
```

**جيد:**

```javascript
const Car = {
  make: "Honda",
  model: "Accord",
  color: "Blue",
}

function paintCar(car, color) {
  car.color = color
}
```

**[⬆ العودة للاعلى](#المحتوى)**

### Use default arguments instead of short circuiting or conditionals

Default arguments are often cleaner than short circuiting. Be aware that if you
use them, your function will only provide default values for `undefined`
arguments. Other "falsy" values such as `''`, `""`, `false`, `null`, `0`, and
`NaN`, will not be replaced by a default value.

**سيئ:**

```javascript
function createMicrobrewery(name) {
  const breweryName = name || "Hipster Brew Co."
  // ...
}
```

**جيد:**

```javascript
function createMicrobrewery(name = "Hipster Brew Co.") {
  // ...
}
```

**[⬆ العودة للاعلى](#المحتوى)**

## **Classes**

### تفضيل ( Classes ( ES2015 / ES6 على ( Functions ( ES5 العادية

من الصعب جدا الحصول على وراثة classes قابلة للقراءة ,للبناء والتعريفات الكلاسيكية لوراثة ES5 classes . إذا كنت بحاجة إلى الوراثة (وكن على دراية بأنك قد لا تحتاج إليه) ، فستفضل ES2015/ES6 classes. ومع ذلك ، حاول ان تفظل Functions الصغيرة على Classes, حتى تجد نفسك بحاجة إلى objects أكبر وأكثر تعقيدا .

**سيئ:**

```javascript
const Animal = function (age) {
  if (!(this instanceof Animal)) {
    throw new Error("Instantiate Animal with `new`")
  }

  this.age = age
}

Animal.prototype.move = function move() {}

const Mammal = function (age, furColor) {
  if (!(this instanceof Mammal)) {
    throw new Error("Instantiate Mammal with `new`")
  }

  Animal.call(this, age)
  this.furColor = furColor
}

Mammal.prototype = Object.create(Animal.prototype)
Mammal.prototype.constructor = Mammal
Mammal.prototype.liveBirth = function liveBirth() {}

const Human = function (age, furColor, languageSpoken) {
  if (!(this instanceof Human)) {
    throw new Error("Instantiate Human with `new`")
  }

  Mammal.call(this, age, furColor)
  this.languageSpoken = languageSpoken
}

Human.prototype = Object.create(Mammal.prototype)
Human.prototype.constructor = Human
Human.prototype.speak = function speak() {}
```

**جيد:**

```javascript
class Animal {
  constructor(age) {
    this.age = age
  }

  move() {
    /* ... */
  }
}

class Mammal extends Animal {
  constructor(age, furColor) {
    super(age)
    this.furColor = furColor
  }

  liveBirth() {
    /* ... */
  }
}

class Human extends Mammal {
  constructor(age, furColor, languageSpoken) {
    super(age, furColor)
    this.languageSpoken = languageSpoken
  }

  speak() {
    /* ... */
  }
}
```

**[⬆ العودة للاعلى](#المحتوى)**

### استخدام طريقة التسلسل (Use method chaining)

هذا النمط مفيد جدا في جافا سكريبت وتراه في العديد من المكتبات مثل jQuery و Lodash. يسمح للكود الخاص بك أن يكون معبرا ، وأقل ثرثرة. لهذا السبب ، أقترح ، استخدام طريقة التسلسل
وألق نظرة على مدى نظافة الكود الخاصة بك. في class functions الخاص بك ، ما عليك سوى إرجاع هذا في نهاية كل function، ويمكنك ربط class methods الإضافية بها.

**سيئ:**

```javascript
class Car {
  constructor(make, model, color) {
    this.make = make
    this.model = model
    this.color = color
  }

  setMake(make) {
    this.make = make
  }

  setModel(model) {
    this.model = model
  }

  setColor(color) {
    this.color = color
  }

  save() {
    console.log(this.make, this.model, this.color)
  }
}

const car = new Car("Ford", "F-150", "red")
car.setColor("pink")
car.save()
```

**جيد:**

```javascript
class Car {
  constructor(make, model, color) {
    this.make = make
    this.model = model
    this.color = color
  }

  setMake(make) {
    this.make = make
    // NOTE: Returning this for chaining
    return this
  }

  setModel(model) {
    this.model = model
    // NOTE: Returning this for chaining
    return this
  }

  setColor(color) {
    this.color = color
    // NOTE: Returning this for chaining
    return this
  }

  save() {
    console.log(this.make, this.model, this.color)
    // NOTE: Returning this for chaining
    return this
  }
}

const car = new Car("Ford", "F-150", "red").setColor("pink").save()
```

**[⬆ العودة للاعلى](#المحتوى)**

### تفضيل composition على inheritance

وكما جاء في [_Design Patterns_] (https://en.wikipedia.org/wiki/Design_Patterns) من قبل Gang of Four،
يجب أن تفضل composition على inheritance حينما يمكنك ذلك. هناك الكثير من
أسباب الوجيهية لإستخدام inheritance والكثير من الأسباب الوجيهة لإستخدام composition.
النقطة الرئيسية لهذا المبدأ هي أنه إذا كان عقلك يذهب غريزيا للinheritance ، حاول التفكير فيما إذا كان composition يمكن أن يحل مشكلتك بشكل أفضل. في بعض
الحالات التي يمكنها.

قد تتساءل بعد هذا، "متى يجب أن أستخدم inheritance؟" هذا
يعتمد على مشكلتك التي تريد حلها ، ولكن هذه قائمة لائقة عندما يكون inheritance
أكثر منطقية من composition:

1. يمثل ميراثك علاقة "هو" وليس "لديه"
   العلاقة (الإنسان->الحيوان مقابل المستخدم->تفاصيل المستخدم).
2. يمكنك إعادة استخدام االكود من classes الأساسية (يمكن للبشر التحرك مثل جميع الحيوانات).

3. تريد إجراء تغييرات عامة على derived classes عن طريق تغيير class الأساسية.
   (تغيير حرق السعرات الحرارية لجميع الحيوانات عندما تتحرك).

**سيئ:**

```javascript
class Employee {
  constructor(name, email) {
    this.name = name
    this.email = email
  }

  // ...
}

// Bad because Employees "have" tax data. EmployeeTaxData is not a type of Employee
class EmployeeTaxData extends Employee {
  constructor(ssn, salary) {
    super()
    this.ssn = ssn
    this.salary = salary
  }

  // ...
}
```

**جيد:**

```javascript
class EmployeeTaxData {
  constructor(ssn, salary) {
    this.ssn = ssn
    this.salary = salary
  }

  // ...
}

class Employee {
  constructor(name, email) {
    this.name = name
    this.email = email
  }

  setTaxData(ssn, salary) {
    this.taxData = new EmployeeTaxData(ssn, salary)
  }
  // ...
}
```

**[⬆ العودة للاعلى](#المحتوى)**
