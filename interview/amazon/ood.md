https://blog.csdn.net/chenyao1994
https://space.bilibili.com/346441475

## OOD  Viability, SD Scalability 
OOA(Analysis): analyze 
OOD(Design): design
OOP(Programming): coding

1. Can you design an elevator system? (design a complete system) little amount of coding 
2. Can you design scheduler for elevator system? (design one part of system): need implementation 

Trap of OOD: 
Try to communicate with interviewer to confirm what design client needs 
Algorithm, Ood or system design 

test case to see if design support user case 

## How to evaluate OOD interview 
S - Single responsibility principle: One class should one have one job 
O - Open close principle: open to extension, close to modification 
```aidl
public class AreaCalculator {
    pulbic float calculateArea(Shape s) {
    }
}
```
L - Liskov substitution principle: can replace parent class 
I - Interface segregation principle, not supposed to implement unused jiekou  
D - Dependency inversion principle: abstract do not supposed to rely on implement, but implement can rely on abstract 
```aidl
public interface Shape {
    public float getArea();
}
public class Triangle implements Shape{ 
    public float getArea() {
        return b*h/2;
     }
}

public class AreaCalculator { 
    private float result;
    public float getResult() {
        return this.result();
    }
    public float calculateArea(Shape s) {
        this.result = s.getArea();
    }
    
 }
 


```

## 5C method for ood
Clarify: what - find nouns
Core objects 
Cases 
Classes 
Correctness 

### Clarify 
Elevator system: 
What: 
weight of the elevator: check weight if it is overweight or not 
maintenance or not 
Building: how many entries 
How: 
same direction > stop > reverse direction , maintenance 
which key can response 
Who: 
lead by desinger vs lead by system 
Optional
passenger class including weight, elevator can sense current weight 
### Core objects 
which class,  how to 
How to define core object? 
- use one object as the basic, think linearly 
- Decide the reflection of objects 

Access modifier: 
package: no declaration, all variables and functions are package level visible, all other classes of the same package cal visit 
public: public level visible, main function has to public  + 
private: class level visible, only the class define these vairable or function can visit. - 
protected: only the class defined or subclass can visit 

Use case: close gate
An elevator
checks for overweight
close the door
then check stops corresponds to current status 
it no stops left, check the reserve direction stops 
change status to reserve direction or idle 

### Cases 
- use object, list object respond clas 
Elevator: take external request, take internal request, open gate, close gate, check weight 
Elevator button: press

### Classes 
can deliver, minimal viable product 
save time, not struggle in coding 
build up on use case, clear, communciate and modify 
if has time, convert to code 

InvalidExternalRequestException 

Use case: take external request 
an elevator takes an external request, insert in its stop list 
<<enumeration>> Direction: 
Up
Down

ExternalRequest: Direction d; int level 
ELevatorSystem: -List<Elevator> elevators; +void handleRequest(ExternalRequst r)
Elevator: -List<ElevatorButton> buttons; -List<Integerm> upStops; -List<Integer> downStops; -int currentLevel
+ void hanlleExternalRequest(ExternalRequest r); +void handleInternalRequest(InternalRequest r); -boolean isRequestValid(INternalRequest r); -Status status 
-boolean gateOpen(); -float checkWeight 

Use case; button 


### Correcteness

1. validate use cases 
2. follow good practice 
3. SOLID
4. Design pattern 

### Challenge 
How do you handle an external request? 

# Vending machine 
public class Main{ 
    public static void main(String[] args) {
        Water w1 = new Water();
        Water w2 = new Water();
        Coke c1 = new Coke();
        Coke c2 = new Coke();

        VendingMachine vm = new VendingMachine(5);
        vm.addProduct("A1", W1);
        vm.addProduct("A2", W1);
        vm.addProduct("A3", W1);
        vm.addProduct("A4", W1);

        Customer customer = new Customer(vm);
        customer.select("A1");
        customer.select("A2");
        
        Payment card = new CreditCardPayment();
        customer.checkout(card);
}

class VendingMachine {
    Map<String, Product> slots;
    int capacity;  
    int pay;

    VendingMachine(int capacity) {
        this.capacity = capacity;
    }
    
    boolean addProduct(String productId, Product product) {
        if(this.capacity >= slot.size()) return false;
        slots.put(productId, product);
    }

    boolean order(String product) {
        return map.containsKey(product) ? map.get(product) : null;  
    }

    float checkout(List<Product> cart, Payment payment) {
        int totalAmount = 0;
        for(Product p : cart) {
            totalAmount += payment.makePayment(product);
        }
        return totalAmount;
    }
}

class Customer {
    VendingMachine vendingMachine;
    List<Product> cart;

    public boolean select(String productId) {
        Product product = vendingMachine.order(productId);
        if(product != null) {
            cart.add(product);
            return true;
        }
        return false;
    }

    public float checkout(Payment payment) {
        return vendingMachine.checkout(cart, payment);
    }
}

class Product {
    float getPrice();
}

class Water implements Product{ 
    String name;
    float getPRice() return 1.0;
}

class Coke implements Product {
    String name;
    float getPrice() return 2.0;
}

class Payment {
    abstract float checkOut(Product productId);
}

class CreditCardPayment extends Payment{
    float checkout(Product productId) {
        return productId.getPrice()* (1+0.1);
    }
}

class cashPayment extends Payment{
    float checkout(Product productId) {
        return productId.getPrice() * (1+0.0);
    }
}


