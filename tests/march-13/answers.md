**Answer sheet:**

1. A) "object"  
2. A) var is block-scoped  
3. C) 3, 3, 3  
4. A) \[1, 2, 3\]  
5. C) Assignment creates a copy of the object  
6. C) \[1, 2, 3\]  
7. C) 2, 1  
8. D) All of the above  
9. A) () \=\> { return {a: 1}; }  
10. C) Create new local variables  
      
11. For ‘==’ if the value is same even after the datatype is different it will return true  
    For example  
    5==’5’   will return true  
    For ‘===’ if the value is same and the datatype is also same then only  it will return true  
    For example

    5===’5’   will return false  
      
12. Function can access the inner function  
    Var is block scoped so the value cannot be re-declared  
    By using let we can re-declare the variable again

13. Mutable objects in Python are the objects that can be changed  for example array, list ,set

    In array   
    ar\[2,3\].append(2)

    Gives   
    ar\[2,3,2\];

    immutable objects in Python are the objects that cannot be changed  for example tuple,string  
    In string  
    a=‘data’  
    a\[0\]=’b’ cannot be done   
    

14. 

15.   
      
       
16.   2 the reason is because it takes the second variable since var is function scope and closure means it can access of inner function

17. 1    
    2  
    1  
    It prints in new line because its using syntax print and for the increment first 2 will call since its in same function but the last one is calling separately so it starts differently

18. True as value is same data type is different but its ‘==’  
    True as value is same data type is different but its ‘==’  
    false as value is different data type is different but its ‘==’  
    True as value is same data type is same but its ‘==’  
    True as value is same data type is different but its ‘==’  
    false as value is different data type is different and  its ‘===’  
19.  \[\[1, 2\], \[3, 4\]\]  
     \[\[1, 2\], \[3, 4\]\] 

    Since its mentioned in first line this is value and in second line its mentioned copy of a is assigned to b  
    The third line is different data so it does not support or has anything to do with print  
20. a returns error because its block scoped and wont move above   
    But b is fine since b use let and it results in moving above the block scope

21. 

def createCounter(count):

def increment():

   		count \+= 1

        		return count

   	def decriment():

        		count \-= 1

        		return count

	def getcount():

		return count

22.   
    

fibonacci\_memoized(n):

	if(n==0)

		Return 0

	Else if (n==1)

		Return 1

	Else

	for( i in n):

		j+=i

i++

	Return j

