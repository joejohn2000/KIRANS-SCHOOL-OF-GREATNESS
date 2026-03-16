**Answer sheet:**

1. number  
2. True  
3. “ ”  
4. "\[object Object\]"  
5. "\[object Object\]"

1. 

   

   In console it runs Running module: Module-4

   In console it runs Running module: Module-4

   In console it runs Running module: Module-4

   Var is function scope so it cannot store the variable in a block like for. Name is shared by call by reference

   

   We can fix this by using let instead of var

   

2. Middle it has given output middle because of the legb rule which means first it takes local variable after that enclosing variables if not there then global variables if nothing among this is there then only it takes built in function  
     
3. This returns error because var is function scoped and not block scope so the scope of var value \= "I am never executed"; stays in the block only  
     
4.   
      
   // TODO: Implement this  
   function createPreferencesManager() {  
     // Your code here  
   Return {  
     
     
   }  
     
   // Expected usage:  
   const prefs \= createPreferencesManager();  
   prefs.set('theme', 'dark');  
   prefs.set('language', 'en');  
   console.log(prefs.get('theme')); // 'dark'  
     
   prefs.reset(); // Admin function  
   console.log(prefs.get('theme')); // Should be reset  
     
   // This should NOT work:  
   console.log(prefs.\_internalStore); // undefined or error  
     
     
   Internal store does not work because of lack of permission   
     
     
5.   
   4  
   4  
   4  
     
     
     
   var functions \= \[\];  
     
   for (let i \= 1; i \<= 3; i++) {  
     functions.push(function() {  
       console.log(i);  
     });  
   }  
     
     
    for (var i \= 1; i \<= 3; i++) {  
     functions.push(function(k) {  
       console.log(k);  
     });  
   }  
     
    for (var i \= 1; i \<= 3; i++) {  
   Let j=i  
     functions.push(function() {  
       console.log(j);  
     });  
   }  
     
     
6.    
   Part-A  
   function curry(fn) {  
     // Your implementation  
   function curried(a) {  
     return function(b) {  
       return function(c) {  
         return a \+ b \+ c;  
       };  
     };  
     
   // Example:  
   function add(a, b, c) {  
     return a \+ b \+ c;  
   }  
     
   const curriedAdd \= curry(add);  
   console.log(curriedAdd(1)(2)(3)); // 6  
   console.log(curriedAdd(1, 2)(3)); // 6  
   console.log(curriedAdd(1)(2, 3)); // 6  
     
   Part-B  
     
     
   function multiplyBy(n) {  
     
     return n\*3;  
   }  
     
   const multiplyBy3 \= multiplyBy(3);  
   console.log(multiplyBy3(10)); // 30  
   console.log(multiplyBy3(5));  // 15

7.   
   1: Start     //started in begin as its in the top of the code  
   2: Timeout  //started second as its in the second of the code and timer shows 0 secs so it shows at that moment

   5: Timeout 2  // it ignores promise to end

   6: Promise 1 // this comes because timer should close after this and microtask queue

   7: End // same reason as above

   3: Promise 1  //comes the first promise macrotask queue

   4: Promise 1 // then comes this promise

   

   

8. 

   function createCounter() {

     let currentValue \= 0;

     return {

       increment: function() {

         currentValue \+= 1;    },

       decrement: function() {

         currentValue \-= 1;    },

       getValue: function() {

         return currentValue;

       }

     reset: function() {

         return 0;

       }

     };

   }

   

   // Tests:

   const counter \= createCounter();

   console.log(counter.increment()); // 1

   console.log(counter.increment()); // 2

   console.log(counter.getValue()); // 2

   console.log(counter.decrement()); // 1

   console.log(counter.reset());    // 0

   console.log(counter.getValue()); // 0

   Closure acts as a backpack. It remembers the values stored in data in the scope only 

   So it is more secure

   

    

9. 

   var x \= 10;  
     
   function foo() {  
     console.log(x);  
   }  
     
   function bar(fn) {  
     var x \= 20;  
     fn();  // error  
   }  
     
   bar(foo);  // 10  
   It got 10 because its enclosing variable is 10   
10.   
      
      
  


    