# swift-type-casting

Type casting is a way to check the type of an instance, or to treat an instance as a diff subclass or superclass in its own class hierarchy. 
Type casting in Swift is implemented with the *is* and *as* operators.

## as vs as! vs as? vs is

### as
Used for *upcasting*, usage is quite infrequant. 
With Upcasting, a class is requested to behave like its base class. Since the derived class will already have base class properties, no error will occur.

```
class Vehicle {
    var numOfWheels: Int
    
    init(numOfWheels: Int) {
        self.numOfWheels = numOfWheels
    }
    
    func move() {
        print("Vehicle moves forword!")
    }
}

class Car: Vehicle {
    var color: String
    var make: String
    var model: String
    
    init(color: String, make: String, model: String) {
        self.color = color
        self.make = make
        self.model = model
        super.init(numOfWheels: 4)
    }
}

let volvoCar = Car(color: "Black", make: "Volvo", model: "176") as Vehicle
volvoCar.numOfWheels
volvoCar.move()
```

### as!
Used for force downcasting, might cause craches.
Attempts to both downcast and force-unwrap the result in a single action. 

```
class Airplane: Vehicle {
    var name: String
    
    init(name: String, numOfWheels: Int) {
        self.name = name
        super.init(numOfWheels: numOfWheels)
    }
}

let airP777 = Airplane(name: "777", numOfWheels: 14)
let airPA380 = Airplane(name: "A380", numOfWheels: 22)
let vehicles = [volvoCar, airP777, airPA380]
```

vehicles array is of type Vehicle, as it's the only common baseclass for the declraed instances.

```
let carObj = vehicles[0] as! Car
carObj.make
carObj.model
```
Successful force downcasting, as the instance is of type Car.

```
let anotherCarObj = vehicles[1] as! Car
```
Crash, will not be able to force downcast type Airplane to type Car.

### as?
Optional downcasting, Asks a question: “Is this object derived from this class?”. Then returns an optional value of the type we're trying to downcast to. Usually used when it's uncirtain that the downcast will succees. 

```
let anotherCarObj = vehicles[1] as? Car
```
anotherCarObj is nil in this case.

### is
Checks for the type, which class an instance it belongs to. The expression returns a value of type Bool.

```
vehicles[0] is Car
vehicles[1] is Airplane
vehicles[2] is Car
```
>output: true, true, false.


