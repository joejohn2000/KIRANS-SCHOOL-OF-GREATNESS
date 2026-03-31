**Answers**

1. 

   class BrowserHistory {  
     constructor(homepage) {  
       this.tab=\[homepage\];  
       this.current \= 0;  
     }  
     
     visit(url) {  
       this.tab.push(url);  
       this.current++;  
     }// time complexity \= O(1)  
     
     back(steps) {  
         	if(this.tab.length==0){  
   			return "no tabs found";  
     		}	  
           // console.log("step",this.current,steps)  
     	    this.current \= Math.max(0, this.current \- steps);  
       //   	console.log("back step",this.current,steps,this.current,this.tab\[this.current\])  
         	return this.tab\[this.current\];  
   	  
     }// time complexity \= O(1)  
     
     forward(steps) {  
           
       // console.log(this.current)  
        
     	this.current \= Math.min(this.tab.length \- 1, this.current \+ steps);  
   //   	 console.log(this.tab,this.tab\[this.current\])  
   //   	console.log("forward step",steps,this.current,this.tab\[this.current\])  
       return this.tab\[this.current\];  
     }// time complexity \= O(1)  
   }

   stacks are a natural fit here cause they use  LIFO operation so its easy to push the tabs inside a stack easily

2. 

   function lowestCommonAncestor(root, p, q) {  
         
       if(\!root)  
       {  
           return null;  
       }  
       if(p.val\<root.val && q.val\<root.val)  
       {  
           return lowestCommonAncestor(root.left,p,q)  
       }else if(p.val\>root.val && q.val\>root.val)  
       {  
           return lowestCommonAncestor(root.right,p,q)  
       }  
       return root;  
     
   }  
     
   If condition is (p.val\<root.val && q.val\<root.val) it avoids right sub tree as the answer will be inside left tree similarly if (p.val\>root.val && q.val\>root.val) it avoids left tree so we dont need to check both trees 

   For balance tree it each step will avoid one sub tree eliminating half of the nodes so it becomes O(logn) but for unbalanced tree it would go one node at a time so complexity becomesO(n)

3.   
   function shipWithinDays(weights, days) {   
         
       let low \= 1;  
       let high \= Math.max(...weights);  
       function canFinish(k) {  
           let d \= 0;  
           for (const w of weights) {  
             d \+= Math.ceil(w / k);  
           }  
           return d \<= days;  
       }  
       while(low\<high)  
       {  
           let mid=Math.floor((low+high)/2)  
           if(canFinish(mid)){  
               low=mid;  
           }else{  
               high=mid-1;  
           }  
       }  
       return low  
     
   }  
   let weights \= \[3,2,2,4,1,4\]  
   let days \= 3  
   console.log(shipWithinDays(weights,days));

   Since it checks the values of mid it makes the problem to half if true it takes from mid to last and if false it checks from first element to mid so the problem is solved using binary search it moves to low \= mid as mid might be the answer we are looking for if we put mid+1 over there if the answer comes in mid it might ignore it and give wrong answer

   After adding all elements to the map the highest valued i will be having the most frequent numbers  
     
4.   
   const edges \= \[  
     \[0, 1\],  
     \[0, 2\],  
     \[1, 3\],  
     \[2, 4\],  
     \[3, 5\],  
     \[4, 5\]  
   \];

   O \=\> \[1,2\]  
   1  \=\> \[3\]  
   2  \=\> \[4\]  
   3  \=\> \[5\]  
   4  \=\> \[5\]  
   5  \=\> \[ \]

   Since queue uses FIFO it can be inserted from first and delete fro same side so inserting a node in graph where each node is added and removed makes more sense  
   

   Part-b

   Since the value is set without deleting current tree it would definitely change the value but does not change the location so in order to fix this we have to delete the current key using  map.delete(key) before map.set(key, value);

5. 

6. 

   function minCostClimbingStairs(cost) {  
         
       let dp \= \[new Array(cost.length ).fill(0)\];   
       a=0;  
       b=0;  
       for (let i \= 2; i \<= cost.length; i++) {  
           const c=Math.min(b \+ cost\[i-1\], a \+ cost\[i-2\]);  
     
           a=b;  
           b=c;  
           
       }  
     
       return b;  
   }  
     
   cost \= \[10,15,20\]  
     
   console.log(minCostClimbingStairs(cost));

   Time complexity is 0(n)  
   Space complexity is  0(n)

   This is DP because it dynamically change the values of a and b for each loop especially if we use  recursive functions  
     
     
7.   
   function checkInclusion(s1, s2) {  
       if (s1.length\> s2.length)  
       {  
           return false;  
       }  
       for(let i=0;i\<s1.length;i++)  
       {  
           if(s1\[i\]==s2\[j\])  
           {  
               return true;  
           }  
           {  
               else return false;  
           }  
       }  
       if(s1.includes(s2)){  
           return true  
       }  
       return false;  
   }

   time complexity \- is O(n) because there is one for loop  
   space complexity \- is O(1) since no extra data stored

8. 

   function missingNumber(nums) {  
       let xor \= 0;  
     
       for (let i \= 0; i \<= nums.length; i++) {  
           xor ^= i;  
       }  
     
       for (let i \= 0; i \< nums.length; i++) {  
           xor ^= nums\[i\];  
       }  
     
     
       return xor;  
   }

   nums=\[3,0,1\];

   In first for loop   
   i=0, xor=0  
   i=1, xor= 1  
   i=2, xor \= 3  
   i=3, xor= 0

   In second loop   
   i=0, xor=3  
   i=1, xor=2  
   i=2, xor=0  
   i=3, xor=2  
     
   Returned 2

   time complexity is O(n) since two loops are there but are called differently  
   space complexity is O(1) since no extra space was required for array or other variables that cost u space

9. 

   class Wallet {  
       constructor(owner, balance \= 0\) {  
           this.owner=owner;  
           this.balance \= balance;  
     
       }  
     
       deposit(amount) {  
           if(amout\<=0){  
               console.log("error u cant enter negative numbers");  
               return;  
           }  
           this.balance+=amount;  
       }  
     
       spend(amount) {  
           if(amout\<=0){  
               console.log("error u cant enter negative numbers");  
               return;  
           }  
           if(amount\>=this.balance){  
               console.log("error insufficient balance cant widthdraw");  
               return;  
           }  
           this.balance-=amount;  
       }  
     
       getBalance() {  
           return this.balance;  
       }  
   }  
     
   class CashbackWallet extends Wallet {  
       applyCashback(percent) {  
           this.balance \+= this.balance \* (percent / 100);  
       }  
   }  
   CashbackWallet is inherited from wallet so it contains function which can be reused from wallet so it is substituting from wallet

   Since CashbackWallet does not changed any behavior of wallet it does not LSP violation

   If we wrote

   class CashbackWallet extends Wallet {  
       getBalance() {  
           return this.balance+1;  
       }  
   }

   This is LSP violation 