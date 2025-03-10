# JavaScript

# Closures:
Closures ka matlab yeh hota hai ki ek function apne outer scope ke variables aur functions ko yaad rakh sakta hai, chahe woh function execute hone ke baad bhi use kare. Matlab, function apne surrounding environment ka reference hold karke rakhta hai.

Agar hum example dekhein:

```js
var Person = function(pName){
  var name = pName;
  this.getName = function(){
      return name;
  }
}

var person = new Person("Neelesh");
console.log(person.getName()); // Output: Neelesh
```

Yahan `name` variable `Person` function ke andar declare hua hai, jo normally function ke bahar access nahi ho sakta. Lekin `getName()` function us variable ko access kar sakta hai, kyunki closure ke wajah se `name` ka reference bana rehta hai.

### One More Example:

```js
function randomFunc(){
  var obj1 = {name:"Vivian", age:45};
  return function(){
      console.log(obj1.name + " is awesome");
  }
}

var initialiseClosure = randomFunc(); // Yeh ek function return karega
initialiseClosure(); // Output: Vivian is awesome
```

#### Is code ko samajhte hain:
1. Jab `randomFunc()` call hota hai, yeh ek function return karta hai jo `obj1` ka use kar raha hai.
   ```js
   var initialiseClosure = randomFunc();
   ```
2. Ab jab hum `initialiseClosure()` ko call karte hain:
   ```js
   initialiseClosure(); 
   ```

   Toh output aata hai:
   ```
   Vivian is awesome
   ```

### Yeh kaise possible hua?
- Jab `randomFunc()` execute hota hai, toh normally uska `obj1` variable memory se hat jana chahiye.
- **Lekin**, jo function return hua hai (`return function() { console.log(obj1.name + " is awesome"); }`), woh `obj1` ko use kar raha hai.
- JavaScript ka closure mechanism ensure karta hai ki `obj1` ka reference memory me bana rahe, taki return hua function usko access kar sake.

### Conclusion:
Closure ki wajah se ek function apne outer scope ke variables ko yaad rakh sakta hai, chahe parent function execute ho chuka ho. Yeh concept tab useful hota hai jab hume **data encapsulation**, **callback functions**, aur **event handling** jaise scenarios me variables ko preserve karna ho.

This ability of a function to store a variable for further reference even after it is executed is called **Closure**.



# Object Prototypes
JavaScript me har object kisi na kisi **prototype** se properties aur methods inherit karta hai. Matlab, objects apne prototype se features lete hain aur unhe use karte hain.

### Kuch Examples:
- **Date objects** → `Date.prototype` se properties inherit karte hain.
- **Math objects** → `Math.prototype` se properties inherit karte hain.
- **Array objects** → `Array.prototype` se properties inherit karte hain.
- **Sabse upar** `Object.prototype` hota hai, jisse har prototype properties aur methods inherit karta hai.

### Prototype Kya Kaam Karta Hai?
Prototype ek object ka **blueprint** hota hai. Yeh allow karta hai ki ek object par woh properties aur methods use ho sakein jo usme directly exist nahi karte.

### Example:
```js
var arr = [];
arr.push(2);
console.log(arr); // Output: [2]
```

#### Yeh Kaise Work Karta Hai?
- Yahan `arr` ek empty array hai.
- Humne `arr.push(2)` use kiya, lekin `push` method humne khud define nahi ki.
- JavaScript engine sabse pehle check karega ki `push` method `arr` object ke andar hai ya nahi.
- Jab `push` method `arr` me nahi mila, toh engine `Array.prototype` me check karega.
- `Array.prototype` me `push` method mil gaya, toh woh execute ho jayega.

### Prototype Chain:
Agar ek property ya method **current object** me nahi milti, toh JavaScript engine **uske prototype** me check karega. Agar wahan bhi nahi mili, toh **us prototype ke prototype** me check karega. Yeh process tab tak chalega jab tak `Object.prototype` tak nahi pahunch jata.

### Conclusion:
Prototype system ki wajah se hum JavaScript objects ko **reusable** bana sakte hain aur **inheritance** implement kar sakte hain. Agar koi method ya property directly object me na ho, toh JavaScript uske prototype me automatically check karti hai.


# Callbacks
JavaScript me **callback ek function hota hai jo tab execute hota hai jab dusra function execute ho chuka ho**. JavaScript me functions **first-class citizens** hote hain, iska matlab:
- Functions ko ek argument ki tarah pass kiya ja sakta hai.
- Functions ko return bhi kiya ja sakta hai.
- Functions ko ek object ki property ke roop me bhi use kiya ja sakta hai.

Jab ek function ko dusre function ke argument ki tarah diya jata hai, usse **callback function** kehte hain.

### Example:
```js
function divideByHalf(sum){
    console.log(Math.floor(sum / 2));
}
function multiplyBy2(sum){
    console.log(sum * 2);
}
function operationOnSum(num1, num2, operation){
    var sum = num1 + num2;
    operation(sum);
}

operationOnSum(3, 3, divideByHalf); // Output: 3
operationOnSum(5, 5, multiplyBy2); // Output: 20
```

#### Is Code Ka Explanation:
- `operationOnSum` function **3 arguments** leta hai → `num1`, `num2`, aur ek **operation (callback function)**
- `num1` aur `num2` ka sum nikalta hai.
- Fir callback function (`operation`) ko call karta hai jo `sum` par operation apply karta hai.
- `divideByHalf` aur `multiplyBy2` dono **callback functions** hain.

#### Callback Function Kaise Kaam Karta Hai?
1. Jab `operationOnSum(3, 3, divideByHalf);` call hota hai:
   - `sum = 3 + 3 = 6`
   - `divideByHalf(6)` call hota hai → Output: `3`

2. Jab `operationOnSum(5, 5, multiplyBy2);` call hota hai:
   - `sum = 5 + 5 = 10`
   - `multiplyBy2(10)` call hota hai → Output: `20`

### Conclusion:
Callback function ek **important concept** hai jo asynchronous programming me kaafi useful hota hai, jaise ki:
- Event handling
- API calls
- Timers (`setTimeout`, `setInterval`)

Yeh mechanism ensure karta hai ki ek function dusre function ke execute hone ke baad hi chale, jo JavaScript me **non-blocking execution** ke liye kaafi important hai!


# Errors in JavaScript
JavaScript me errors **do tarike ke hote hain:**

### 1. Syntax Error
- Jab hum code likhte waqt **galat syntax** use karte hain ya koi **spelling mistake** hoti hai, tab **syntax error** aata hai.
- Is wajah se program **execute nahi hota** ya beech me **ruk jata hai**.
- JavaScript ek **error message** bhi deta hai jo batata hai ki problem kaha hai.

#### Example:
```js
console.log('Hello World) // Missing closing quote
```
**Error:** `Uncaught SyntaxError: missing ) after argument list`

---

### 2. Logical Error
- Jab **code ka syntax sahi hota hai** lekin **logic galat hota hai**, toh **logical error** aata hai.
- Is type ke errors me **koi error message nahi milta**, lekin output **galat aata hai**.
- Yeh **debug karna mushkil hota hai** kyunki program bina error ke chal jata hai, par sahi result nahi deta.

#### Example:
```js
function add(a, b) {
    return a - b; // Galti se '-' use kar diya '+' ki jagah
}
console.log(add(5, 3)); // Output: 2 (Jo ki galat hai, expected 8 tha)
```

### Conclusion
- **Syntax Errors** ko JavaScript **detect aur report** karta hai, isliye inhe fix karna **asan** hota hai.
- **Logical Errors** me koi warning nahi milti, isliye debugging **mushkil** hoti hai.
- Logical errors ko fix karne ke liye **console.log()** aur **debugging tools** ka use karna zaroori hota hai.

Agar aapko JavaScript me coding karte waqt error aaye toh error message ko **dhyan se padho** aur debugging tools ka use karo!

