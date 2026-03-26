**ANSWER**

1. B) O(n)  
2. A) O(1)  
3. C) O(n²)  
4. C) 30  
5.   
   B) Finding two numbers in a sorted array that add up to a target is the best problem to solve using two pointer   
     
     
   function sum(arr,target){  
     
   	let r=arr.length-1;l=0;  
     
     
   	while(l\<r){  
   	    console.log(l,r,arr\[l\],arr\[r\])  
   	let sum=arr\[l\]+arr\[r\];  
   		if(sum==target)  
   		{  
   			return \[arr\[l\],arr\[r\]\];  
   		}  
   		else if (sum\<target){  
   			l++;  
   		  
   		}else{  
   		    r--;  
   		}  
   }  
     
     
     
   };  
     
     
     
     
6. 

   function squareArray(arr) {  
     
     
   return  arr.map(x \=\> x \* 2);  
   }

7. C) 3  
8. B) When you need fast lookups by key  
9. 

   function mostFrequent(arr) {  
     
   		let map=new Map();  
   		for(let i=0;i\<arr.length;i++){  
     
       		let count,max;  
       		  
       		if(map.has(arr\[i\])){  
       			map(arr\[i\],count);  
               }  
               map.set(arr\[i\]);  
               return Math.max(map\[count\]);  
                 
     
           }  
     
     
   };

10.   
    // mostFrequent(\[1, 2, 2, 3, 3, 3\]) should return 3  
    

11. 

    D) 24

12.   
    B) To prevent infinite recursion

13. 

    function sumToN(n) {  
      if (n \=== 1\) {  
        return 1;  
      }  
      return n \+ sumToN(n \- 1);  
    }  
    

    // sumToN(5) should return 15 (1+2+3+4+5)

14.   
    C) Built-in sort methods in JS/Python are stable

15.   
    C) When you need O(n log n) guaranteed performance  
16. 

    function bubbleSort(arr) {  
       
        for (let i \= 0; i \< arr.length ; i++) {  
              
      
            for (let j \= i+1; j \< arr.length \- i \- 1; j++) {  
                  
                
                if (arr\[i\] \> arr\[j\]) {  
             
                   
                    // Swap elements  
                    let temp \= arr\[i\];  
      
                    arr\[i\] \= arr\[j\];  
      
                    arr\[j\] \= temp;  
      
                }  
            }  
           
        }   
      return arr;  
      
    }  
      
      
      
17. 

