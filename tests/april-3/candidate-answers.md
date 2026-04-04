**ANSWERS**

1. 

   Snippet A  
     
   catalog category: Abuser  
   Smell:Switch Statements  
     
   Problem :there are too much if statements make it harder to understand.  
     
   Solution use polymorphism to solve this problem  
     
   Snippet B  
     
   Catalog Category: Coupler  
   Smell: Message Chains  
     
   Problem its difficult for user to understand whats this long chain of code also navigating through multiple levels cause fragile  
     
   Solution : delegating the work to the object so just call one object instead of chain  
     
   Snippet C   
     
   Catalog Category: Bloaters  
   Smell: Large Class  
     
   Problems :there are too much items in class making it difficult to debug  
   Solutions : convert all classes to subclass and divide all the work so its easy to understand and debug  
     
   Snippet D  
     
     
   Catalog Category: Abuser  
   Smell: Switch Statements  
     
   Problem : there function relies on type which requires to change function based on every time new shape is added   
     
   Solution use polymorphism to solve this problem  
     
     
     
     
   Snippet E  
     
   Catalog Category: Change Preventer  
   Smell: Divergent Change  
     
   Problem : single scheme requires manual  running in 17 different files  
     
   Solution: convert this to an method and call the method  
     
2. 

   function printInvoice(order) {  
     printHeader(order.customerName);  
     const total \= printItemsAndCalculateTotal(order.items);  
     printFooter(total);  
   }  
     
   function printHeader(name) {  
     console.log("=== INVOICE \===");  
     console.log(\`Customer: ${name}\`);  
     console.log(\`Date: ${new Date().toISOString()}\`);  
   }  
     
   function printItemsAndCalculateTotal(items) {  
     let total \= 0;  
     for (const item of items) {  
       console.log(\`${item.name}: $${item.price}\`);  
       total \+= item.price;  
     }  
     return total;  
   }  
     
   function printFooter(total) {  
     console.log(\`Total: $${total}\`);  
     console.log("===============");  
   }

   Catalog Category: Bloater  
   Smell: Long Method  
     
     
   Part B 

   function getDiscountedPrice(product) {  
     
     if (basePrice(product) \> 1000\) {  
       return basePrice(product)\* 0.9;  
     }  
     return basePrice(product);  
   }

   function basePrice(product) {  
     return product.quantity \* product.itemPrice;  
   }

   Catalog Category: Dispensable  
   Smell: Inline Class   
     
   Temp variable is benefited if the values are called once or minimal but the computing values complicated or changes in between   
   

   Part C   
     
   class Employee {  
     	constructor(name) { this.name \= name; }  
   }  
     
   class Engineer extends Employee {

     getBonus() { return 5000; }  
     getTitle() { return "Software Engineer"; }

}

class Manager extends Employee {  
  getBonus() { return 10000; }  
  getTitle() { return "Engineering Manager"; }  
}

Catalog Category: OO Abuser  
Smell: Switch Statements

3.   
   technical debt acts like the real debt if we don't give enough time for the code now later would create a lot problem for example if we bought a loan and had skipped some payments this would create a problem in future because the dept will increase and if we keep ignoring this would eventually be a huge problem

   Deliberate Technical Debt are dept that coders know but ignores because of certain factors like time and pressure from the management team or above inadvertent technical debt on other side are error that are made without knowledge of the coder they made it by mistake 

   Part B 

   Catalog Category: Dispensable  
   Smell: Magic Numbers  
     
   Change Preventer category makes the cost of future features or bug fixes really high  contributing to the technical dept of the problem if not fix the work would be harder since more technical dept was created which means interest has increased for the same  
     
     
4.   
   1. Singleton   
      Category: Creational  
      Problem Solved: ensures that only one instances is called for the global access  
      Example: store the instance of database

   2. Adapter   
      Category: Structural  
      Problem Solved: ensures that one instances of class can communicate with other instance of class it can be a tool of translation between the instances

   3. Observer

   4.   
      Factory Method  
      Category: Creational  
      Problem Solved: ensures instance can create an object but let them decide what all should be the features of the object  
        
      

   5. Decorator  
      Category: Structural  
      Problem solved : It allows behavior to create changes to individual objects without affecting the behavior of other instances of the same class

5.  

6.   
7. 

   class RateLimiter {  
   constructor(maxRequests, windowMs) {

   this.maxRequests=maxRequests;

   this.windowMs=windowMs;  
   this.user=\[\];  
   

     }

   

     allow(userId) {

   const now \= Date.now();  
   this.users\[userId\].push(now);

   

       }  
   Return user;  
      

     }

   }

   Time: O(N)   
   Space: O(N)   
   Since it moves to constructor and set with just user as array time and space is  O(N)   
     
   to address High Traffic increase horizontal scaling   
     
     
     
   

8.   
   PART-A

   CAP stands for Consistency,availability and partial tolerance, based on theorem only 2 of them can only increase while the other once decreases 

   Consistency: all nodes see same or consistent data  
   availability : for every node receives a result from request  
   partial tolerance: runs even after a network failures

   CP stands for Consistency and partial tolerance based on this both of them will increase but th catch is availability will decrease   
     
   AP stands for Availability and partial tolerance based on this both of them will increase but th catch is Consistency will decrease   
     
   CA stands for Availability and Consistency based on this both of them will increase but th catch is partial tolerance will decrease 

   PART-B  
     
   cache-aside pattern is a strategy in which application is responsible for managing and storing the data between cache and database

   When cache is missed It updates the cache and stores new data in cache while sending it back the result

   PART-C

   vertical scaling is increasing the performance of the current server or system for example the ram was 4 gb and storage was 1 tb it would increase to 16gb ram and 10 tb storage which would increase the performance of the system and the scenario in which the a single request cant handle in 4gb of ram is perfect example for this situation

   Horizontal scaling is increasing the number of the server or system for example there are 10 servers handling the issue add 10 more and make it 20 and the scenario to explain is if there are too much traffic for the request instead of increasing the performance its better to increase the number of systems so traffic is distributed equally to all the servers and come in control

   PART-D

   Sql is better because it follows acid properties and has Relational Data which means complex table joins can be handled

   NoSQL is better because it can Horizontal Scaled which mean it can grow along with server support flexible scheme which means support unstructured data