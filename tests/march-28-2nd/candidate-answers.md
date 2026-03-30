**ANSWERS**

1.   
   class MinStack {  
     constructor() {  
       this.items=\[\];  
       this.minStack=\[\];  
     }  
     
   push(val) {

 		this.items.push(val)  
  		if (this.minStack.length \=== 0 || val \<= this.getMin()) {  
    			this.minStack.push(val);  
  }  
  }

pop() {  
  		if(this.item.isEmpty(){  
			return “overflow”;  
  		}	

  	let val=this.items.pop();  
	if(val==this.getMin(){  
	this.minStack.pop();  
}  
}  
  top() {  
    	return this.items\[this.items.length-1\];  
  }

  getMin() {  
    	return this.minStack\[this.minStack.length-1\];  
  }  
}

2.   
   class RecentCounter {  
     constructor() {  
      	this.stack\[\];  
     }  
     
     
     
     
     ping(t) {  
       	this.stack.push(t);  
   	while(this.requests\[0\] \< t \- 3000){

   let var= this.request.shift();

   	}return var;  
   	  
     }  
   }  
   since queue is FIFO. and the order of time will only increase not go less than older one queue is the right structure here

3.   
   level-order traversal is \[7,3,11,1,5,13\]

   since queue is FIFO. and the order of time will only increase not go less than older one queue is the right structure here node l if n+1 node is to be traversed there should be n node 

     
   function insertIntoBST(root, val) {  
   if(\!root){  
   	return Treenode(val);  
   }

   	if(val\<root.left)  
   {  
   	root.left=root.insertIntoBST(root.left,val);  
   }  
   else{  
   		root.right=root.insertIntoBST(root.right,val);  
     
   }  
   return root;  
   }

4. 

         8  
        / \\  
       3   10  
          /  \\  
         9    14  
   	/  
            13

   First it check on root 8 and compares it with 8 since 8\<13 it goes to right value which 10 again since 10\<13 it goes right to 14 here 14 \>13 so it goes to left node

   In balanced it is O(logn)  
   And unbalance it is O(n)”

5. nums \= \[1, 2, 5, 9\], threshold \= 6  
     
   function smallestDivisor(nums, threshold) {  
       let d=Math.max(nums),sum=0;  
       for(let i=0;i\<nums.length;i++){  
           sum=sum+nums\[i\]/d;  
            console.log(sum);  
       }  
       return sum  
   }  
   time complexity should be O(n) based on code i wrote  
   

6. 

7.   
   function topKFrequent(nums, k) {  
   	let freq={};  
   	for(let num of nums){  
   	    freq\[num\]=(freq\[num\] || 0\) \+ 1;  
   	}  
   	let arr \= Object.entries(freq);  
   	  
   	let heap=\[\];  
   	for(let \[num,count\] of arr){  
   	    heap.push(\[num, count\]);  
   	    heap.sort((a, b) \=\> a\[1\] \- b\[1\]);  
   	    if (heap.length \> k) {  
   	        heap.shift();  
   	    }  
   	}  
   	return heap.map(x \=\> Number(x\[0\]));  
   }  
     
     
   In this way u dont need to use brute force to store array u can use different for loops which will result in O(n)

   