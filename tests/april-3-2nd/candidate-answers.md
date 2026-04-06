**ANSWERS**

1. 

   1.   
      Smell: Long Method  
      Technique name: Extract Method

      validates items, calculates tax, applies discount, charges card, sends email is breakdown to separate functions

     
   2.   
      Smell: Magic Number  
      Technique name: Replace Magic Number with constant

      Replace 2592000000 with its exact day variant constant with a literal name that can be used again with the same name

   3.   
      Smell:Switch Statements (type code switching)  
      Technique name: Replace with polymorphism 

      Replace the circle and square with its own subclass to eliminate complexity 

   4.   
      Smell: Divergent Change  
      Technique name: Extract Method

      Different responsibilities are breakdown to separate functions

        
        
      

2.   
   class PaymentMethod {  
     pay(amount) { throw new Error("not implemented"); }  
   }

   Class CreditCard extends PaymentMethod  
   {  
   	pay(amount){  
   		console.log(“amount charged $${amount}\`);  
   	}  
   }  
   Class PayPal extends PaymentMethod  
   {  
   	pay(amount){  
   		console.log(“  Sent  $${amount}\`);  
   	}  
   }  
   Class BankTransfer extends PaymentMethod  
   {  
   	pay(amount){  
   		console.log(“Transferred charged $${amount}\`);  
   	}  
   }

   class PaymentMethodFactory {  
   static create(type) {

   if (type \=== "CreditCard") return new CreditCard();  
       	if (type \=== "PayPal") return new PayPal();  
      	if (type \=== "BankTransfer") return new BankTransfer();  
       	throw new Error("unknown type");  
   }

   }  
     
   let  CreditCard \= PaymentFactory.create(type);  
   let  PayPal \= PaymentFactory.create(type);  
   let  BankTransfer \= PaymentFactory.create(type);

   CreditCard.pay(50);  
     
   PayPal.pay(50);  
     
   BankTransfer.pay(50);  
   

   PaymentMethodFactory and PaymentMethod are the two participants that the client code depends on. 

   Without modifying base logic and client logic it can create crypto payments methods so it follows open/close principle

3.   
   class WeatherStation {  
     	constructor() {  
       		this.temperature \= 0;  
       		this.observer=\[\];  
     	}  
     
   setTemperature(temp) {

   	this.temperature=temp;  
   	for (let obs of this.observers) {  
         		obs.update(this.symbol, this.price);     
       	}  
     
   }

   subscribe(observer) {  
       	this.observers.push(observer);  
   }  
   unsubscribe(observer) {  
   this.observers \= this.observers.filter(o \=\> o \!== observer);  
   }

   class PhoneDisplay {  
     		update(temp) {  
       			console.log(\`\[Phone\] Temp: ${temp}°C\`);  
     		}  
   }  
     
   class WebDashboard {

     	update(temp) {  
       		console.log(\`\[Web\] Current temperature is ${temp}°C\`);

   }  
     
   }

   WeatherStation depends on a common interface allowing it to notify any observer without any specific internal logic or implementation  
   

4. 

   class TextFormatter {  
    	format(text) {  
       		return text;  
     	}  
   }  
   class TextFormatterDecorator extends TextFormatter{  
   	constructor(text){  
   		this.text=text;  
   }

   class UpperCaseFormatter extends FormatterDecorator {  
   format(text) {

   return super.format(text).toUpperCase();

   }  
   }  
     
     
     
   }  
   const f \= new ExclamationFormatter(new UpperCaseFormatter(new TextFormatter()));  
   console.log(f.format("hello"));  // expected: "HELLO\!"  
     
     
   

5. 

   class ApiRateLimiter {  
   constructor(maxCalls, windowMs) {

           	this.maxRequests \= maxRequests;  
       	this.windowMs \= windowMs;  
       	this.timestamps \= new Map(); 

     
     	}  
     
     	isAllowed(ipAddress) {  
      		    if (userTimestamps.length \< this.maxRequests) {

         userTimestamps.push(now);  
         return true;  
       }

     
     
     	}  
   }  
   