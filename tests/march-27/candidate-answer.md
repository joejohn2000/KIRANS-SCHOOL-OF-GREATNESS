**Answers**

1. 

   class Stack {  
     constructor() {  
       this.items \= \[\];  
     }  
     
     push(item) {    
   	this.items.push(1);    
     }//O(1)  
     
     pop() {

       if (this.isEmpty()) return "Underflow";  
       return this.items.pop();

     
     }//O(n)  
     
     peek() {  
       	return this.items\[this.items.length \- 1\];  
     }//O(1)  
     
     isEmpty() {  
       	return this.items.length \=== 0;  
     }//O(1)  
     
     size() {  
       	return this.items.length;  
     }//O(1)  
   }

   This would fail in js because syntax for peek is not created

2. 

   class MyQueue {  
     constructor() {  
       this.inStack \= \[\];  
       this.outStack \= \[\];  
     }  
     
     push(x) {  
       	this.items.push(1);  
     }  
     
     pop() {  
       	this.peek();  
   	return this.pop(outStack);  
     }  
     
     peek() {  
   if (this.outStack.length \=== 0\) {

   while (this.inStack.length \> 0\) {  
               	this.outStack.push(this.inStack.pop());  
               }

   }  
   return this.outStack\[this.outStack.length \- 1\];  
     
     }  
     
     empty() {  
     	return this.s1.length \=== 0 && this.s2.length \=== 0;  
     }  
   }

   pop() is amortized O(1) and not O(n) for every operation as it just returns the array with finding last element and deleting it

3. 

   function temp(temperatures){  
         
       let results= new Array().fill(0);  
       let temps=\[\];  
         
         
       for(let i=0;i\<temperatures.length;i++){  
            
           while (temps.length \> 0 && temperatures\[i\]\>temperatures\[temps\[temps.length-1\]\])  
           {  
               //  console.log("hi")  
               const j=temps.pop;  
               results\[j\]=i-j;  
           }  
           temps.push(i);  
       }      
       return results;  
   }

   Results should be \[ 1,1,4,2,1,1,0\]  
     
   After processing the  indices 6 it checks the next value if its length\>0 and the next value which is 77 is greater than the one stored in temp array since it is the case it pops the value from temp stack and nothing is changed in results array  
     
   It stores  indices instead of temperatures to compare it with other values in array

   

     
4.   
   pre-order traversal(Root-left-right)-\[8,4,2,6,12,10,14\]  
   in-order traversal(left-root-right)-\[2,4,6,8,10,12,14\]  
   post-order traversal(left-right-root)-\[2, 6, 4, 10, 14, 12, 8\]  
   level-order traversal-\[8,4,12,2,6,10,14\]

   Because the tree is created in order that left node root and right are increasing as it goes up

5.   
   What is the time complexity of search, insert, and delete in a balanced BST?  
   Time complexity of  
   Search– O(nlogn)  
   Insert,delete — O(n)

   For every badly unbalanced BST it becomes O(n^2)  
   If insertion pattern is 

6. 

   If  \!root means there is no data in the tree so we can return 0 since the size is 0 and this is the base function telling recursion to stop. Noe we can take length from max of recursively checking length if right or left comparing which one is the biggest of them then repeat till it reach the end and the final product will be return back from function

   Time complexity is O(n)  
   Space complexity is O(n)

   function maxDepth(root) {  
     	if (\!root) return 0;  
   	return 1 \+ Math.max(maxDepth(root.left), maxDepth(root.right));  
     
   }

     		 

7. 

   To fix the code u need min and max which will dynamically check during each interaction   
   function isValidBST(root,min,max) {  
     if (\!root) return true;  
     
     if (min\!=null && node.val\<=min || max\!=null && nod.val\>=max) return false;  
     
     return isValidBST(root.left,min,max) && isValidBST(root.right,min,max);  
   }

     
   The old code Returns false as it only checks if the values just under are greater than the current  node  so in order to check if the tree is valid binary search tree u need to check all the nodes   
     
   Time complexity is O(n)

8. 