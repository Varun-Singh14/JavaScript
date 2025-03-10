# JavaScript

## Closures:
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

