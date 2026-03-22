**ANSWER-1**

1.    
     
     
   Undefined  
   Error  
   Error  
     
   Because of hoisting all the initialisation is on top and for const and let its in tmz so it returns error  
      
     
2.


   Undefined

   Undefined

   10 

   Undefined

   

   Since var is function scope it goes to the top because of hoisting but for let its block scope and the scope end in if statement

3.    
   5  
   Error since function is passed to variable and function variable is not hoisted  
     
     
4.    
   1: Start  
   7: End  
   3: Promise  
   4: Microtask  
   5: Promise Chain  
   2: Timeout  
   6: Timeout in Promise  
     
     
     
   It follows an order in which first sync code runs first then comes microtask then only the macro tasks runs   
     
     
5.    
   A: Start  
   F: End  
   B: First then  
   C: Second then  
   D: Nested Promise  
   E: Third then  
     
   E prints after d because after then only it prints  
     
     
6.    
   **Output** \- 4 4 4

   **Fix using let**   
     
   for (let i \= 0; i \< 3; i++) {  
     setTimeout(() \=\> console.log(i), 0);  
   }  
     
   **Fix using let IIFE**  
     
   for (var i \= 1; i \<= 3; i++) {  
     (function(x){  
       setTimeout(() \=\> {  
         console.log(x);  
       }, 0);  
     })(i);  
   }  
     
     
     
     
     
     
     
     
     
     
     
   

 

7.      
   function createBankAccount(initialBalance) {  
   	let balance=initialBalance;  
     
   	return{  
   

   		deposit(amount){  
   			return balance=balance+amount;  
   		},

   		

   		withdraw(amount){  
   			If(amount \>= 0){  
   				return “error insufficient fund”;

   }else  
   {

   				return balance=balance-amount;  
   			}

   },

   		getBalance(){  
   			return balance;  
   		},

   		

   	

   		

   }

     
     
     
     
     
     
   }  
     
   // Tests:  
   const account \= createBankAccount(100);  
   console.log(account.deposit(50));      // 150  
   console.log(account.withdraw(30));      // 120  
   console.log(account.getBalance());      // 120  
   console.log(account.balance);           // undefined  
   console.log(account.withdraw(200));     // error insufficient fund  
   

    

8.   
     
     
   function curry(fn) {  
   

   function curriedAdd(...args){  
   	if( args.length\>=fn.length)  
   	{  
   		fn.apply(this,args)  
   	}  
   	   
   return function(...next){

         return curried.apply(this,args.concat(next));

   }  
     
   }

     
     
     
   }  
     
   // MUST work for ANY number of arguments:  
   const add \= (a, b, c, d) \=\> a \+ b \+ c \+ d;  
   const curriedAdd \= curry(add);  
     
   console.log(curriedAdd(1)(2)(3)(4));     // 10  
   console.log(curriedAdd(1, 2)(3)(4));     // 10  
   console.log(curriedAdd(1, 2, 3)(4));    // 10  
   console.log(curriedAdd(1)(2, 3, 4));    // 10  
     
     
   **PARTB**  
     
     
   function curry(fn) {  
   

   function curriedmultiply(...args){  
   	if( args.length\>=fn.length)  
   	{  
   		fn.apply(this,args)  
   	}  
   	   
   return function(...next){

         return curried.apply(this,args.concat(next));

   }  
     
   }

     
     
     
   }  
   const multiply \= (a, b, c) \=\> a \* b \* c;  
   const curriedMultiply \= curry(multiply);  
     
   const multiplyBy2 \= curriedMultiply(2);  // function that multiplies by 2  
   console.log(multiplyBy2(3)(4));          // 24  
     
     
     
     
     
      
9.  

   

10.    
    function createStack() {  
      // Implement using closures (NOT classes)  
      // Requirements:  
      // \- push(item) \- add to stack  
      // \- pop() \- remove and return last item  
      // \- peek() \- see last item without removing  
      // \- isEmpty() \- boolean  
      // \- size \- read-only property (how?)  
      
    let stk=\[\];  
      
      
      return {  
        // Your code  
    	 push(item) {  
    		return stk.push(item);  
    	},  
    	pop() {  
    		return stk.pop();  
    	},  
    	peek() {  
    		return stk.peek();  
    	},  
    	size() {  
    		return stk.length;  
    	},  
    	isEmpty() {  
    		If (stk.length \==0)  
    		{  
    			return true;  
    		}  
    		else {

    return false;  
    }

    	  
    }  
      
    	  
      
      
      };  
    }  
      
    // Tests:  
    const stack \= createStack();  
    stack.push(1);  
    stack.push(2);  
    stack.push(3);  
    console.log(stack.pop());     // \[1,2\]  
    console.log(stack.peek());    // \[1,2\]  
    console.log(stack.size);      // 2  
    console.log(stack.pop());     // \[1\]  
    console.log(stack.pop());     // \[\]  
    console.log(stack.isEmpty()); // true  
      
      
11.    
      
      
      
      
    True  
    False  
    False  
    0.3  
    “\[object Object\]”

     

12.   
      
    var x \= 1;  
      
    function outer() {  
      var x \= 2;  
        
      function middle() {  
        var x \= 3;  
          
        function inner() {  
          console.log(x);  // 3  
        }  
          
        inner();  
        console.log(x);   // 3  
      }  
        
      middle();  
      console.log(x);     // 2  
    }  
      
    outer();  
    console.log(x);       // 1  
      
    