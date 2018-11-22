# Scala
- - - -
## INTRO
**Operators are methods**
In Scala, primitives are represented as objects. (Although after compilation they are using Java’s primitives when possible for performance).
1 + 2 is actually: (1).+(2)

**Variables**
```scala
x = 1
var x = 1
var x:Int = 1
// Declare final variable
val x = 1  
// Declare multiple variables
var x, y, z = 0  
var c, python, java = false  
// Assign multiple variables
var (x, y, z, c, python, java) = (1, 2, 3, true, false, "no!") 
```

**Printing**
```scala
println(“Hello World”)
println(s”Two times three: ${2 * 3}”)
val Tau = Pi*2
println(s”Happy $Tau Day”)
//java.lang.* is imported implicitly by default 
printf(“Now you have %.16f problems.”, Math.nextAfter(2.0, 3))  
```

**Useful operations**
Ranges
```scala
//creates a range between 1 to 10 inclusive  
val range = 1 to 10
//creates a range between 1 to 10 exclusive   
val range2 = 1 until 10
//from 2 to 10 with jumps of 3  
val range3 = 2 until 10 by 3
println(range3.toList) //List(2, 5, 8)
```
Number convenience methods
```scala
val num = -5  
val numAbs = num.abs //absolute value  
val max5or7 = numAbs.max(7)  // 7
val min5or7 = numAbs.min(7)  // 5
```
String operations   
```scala
val reverse = “Scala”.reverse //reverse a string   
println(reverse) //alacS  
val cap = “scala”.capitalize //make first char caps  
println(cap) //Scala  
val multi = “Scala!” * 7 //repeat n times   
println(multi) //Scala!Scala!Scala!Scala!Scala!Scala!Scala!
val int = “123”.toInt //parse as Int  
println(int)
```
Collections
```scala
//filter - keep only items larger than 4   
val moreThan4 = range.filter(_ > 4)  
println(moreThan4) //Vector(5, 6, 7, 8, 9, 10)  
//map - transform each item in the collection   
val doubleIt = range2.map(_ * 2)  
println(doubleIt) //Vector(2, 4, 6, 8, 10, 12, 14, 16, 18)  
```
- - - -
## FUNCTION
**Method definition**
```scala
def add(x:Int, y:Int):Int = {  
  return x + y  
}  
def add(x:Int, y:Int) = { //result type is inferred   
  x + y //"return" keyword is optional  
} 
//Curly braces are optional on single line blocks  
def add(x:Int, y:Int) = x + y 
println(add(42,13))  
```

**Anonymous Functions**
```scala
//a method that requires a function as a parameter  
//the function's type is (Int,Int) => Int  
//e.g. maps from 2 Ints to an Int  
def doWithOneAndTwo(f: (Int, Int) => Int) = {  
  f(1, 2)  
}  

//Explicit type declaration  
val call1 = doWithOneAndTwo((x: Int, y: Int) => x + y)  

//The compiler expects 2 ints so x and y types are inferred  
val call2 = doWithOneAndTwo((x, y) => x + y)  

//Even more concise syntax  
val call3 = doWithOneAndTwo(_ + _)   
```
Summary
```scala
def add1(x:Int, y:Int) = x + y //method  
val add2 = (x:Int, y:Int) => x + y //anonymous function  
val add3:(Int,Int)=>Int = _ + _ //alternate way  
val add4 = (_ + _):(Int,Int)=>Int //alternate way, rare   
```

**Return multiple variables**
```scala
def swap(x:String, y:String) = (y, x)  
val (a,b) = swap("hello","world")   
```
- - - -
## LOOP
**While**
```scala
while ( i < 10) {  
  sum += i  
  i+=1  
} 
```
**For**
```scala
for ( i <- 0 until 10) {  
  sum += i  
}
```
**Loops without loops**
`(0 until 10).sum`
- - - -
## CONDITIONS
**If else**
`val breakfast =  if (likeEggs) "scrambled eggs" else "Apple"`
**Match as a Switch**
```scala
val selection = "One"  
selection match {  
  case "One" => println("You selected option one!")  
  case "Two" => println("You selected option two!")  
  case _ => println("You selected something else")  
}  
```
- - - -
## ARRAY
- Arrays are constructed simply using Array(element1, element2, ...)
- Arrays are mutable (can’t change it’s size once created, but can modify it’s elements)
- Since they are using Java’s arrays, to print nicely an Array’s content, use .mkString(",")
- Array elements can be of any type, but the Array’s final type will be the lowest common denominator
```scala
// class Foo(val value1:Int)
// class Bar(value1:Int, val value2:Int) extends Foo(value1)
// val list:Array[Foo] = Array(new Foo(1), new Bar(2,3))
val array1 = Array("a", 2, true)  // java.lang.Object 
val array2 = Array("a", "b", "c")  // java.lang.String
// get
val itemAtIndex0 = array2(0) // a
// modify
array2(0) = "d"
// concat
val concatenated = "prepend" +: (array1 ++ array2) :+ "append"  // ("prepend","a",2,true,"a","b","c","append")
// find
array2.indexOf("b")  // 1
val personArray = Array(("Alice",1), ("Bob",2), ("Carol",3)) 
def findByName(name:String) = personArray.find(_._1 == name).getOrElse(("David",4))
val findBob = findByName("Bob")  // (Bob,2)  
val findEli = findByName("Eli")  // (David,4)  
val bobFound = findBob._2  // 2  
val eliFound = findEli._2  // 4  
// diff
val diffArray = Array(1,2,3,4).diff(Array(2,3))  // (1,4)
```

- - - -
## LIST
- The default List is implemented as a Linked list
- It is immutable (any “changes” create a new list, the original is untouched)
```scala
val list1 = List(1, 2, 3)
val list2 = List("a", 2, true)
// the "mutable version" of List  
val mlist = mutable.ArrayBuffer("a", "b", "c")
// concat using the ++ or ::: (lists only)  
val concatenated = 1 :: list1 ::: list2 ++ mlist :+ 'd'
// remove 
mlist -= "c"
mlist --= List("a", "b")
// add
mlist += "e"
mlist ++= List("f", "g")
// diff
val diffList = List(1,2,3,4) diff List(2,3) //> diffList = List(1, 4)  
// find: like array
```
- - - -
## SET
- Set implementation up to size of 4 has a specific class Set1, Set2, Set3, Set4, beyond that, it uses an immutable HashSet
- You can’t have duplicate values, adding a value that already exists, overwrites the value
- Order of iteration is not guaranteed to be consistent
```scala
val set1 = Set(1, 2, 3)
val set2 = Set("a", 2, true)
//the "mutable version" of Set  
val mset = mutable.HashSet("a", "b", "c") 
println(Set(1,2,3,2,4,3,2,1,2)) //Set(1, 2, 3, 4)  
// check if item exists
val oneExists = set1(1)  // true
// นอกนั้นทำได้เหมือน array
```
- - - -
## MAP
```scala
val map1 = Map("one" -> 1, "two" -> 2, "three" -> 3)    
val map2 = Map(1 -> "one", "2" -> 2.0, 3.0 -> false)   
// the "mutable version" of Map  
val mmap = mutable.HashMap("a" -> 1, "b" -> 2 , "c" -> 3)
//Get items using map(key)   
val one = map1("one")  
// NoSuchElementException will be thrown if key doesn't exist!   
// the get method returns an Option
val fourExistsOption = map1.get("four")  
println(fourExistsOption.isDefined) // false  
// concat
val concatenated = map1 ++ map2 ++ mmap
// remove
mmap -= "c"
// add
mmap += "e" -> 5  
mmap ++= Map("f" -> 6, "g" -> 7)  
// find  
val personMap = Map(("Alice",1), ("Bob",2), ("Carol",3))  
def findByName(name:String) = personMap.getOrElse(name, 4)  
val findBob = findByName("Bob")  // 2 
val findEli = findByName("Eli")  // 4
```
- - - -
## MUTABLE COLLECTION
- Mutable collections allow to add / remove a single / multple items while modifying the collection itself
- the methods +=, ++=, -=, --= are actually defined in the mutable collections
```scala
import scala.collection.mutable  

val arrayBuffer = mutable.ArrayBuffer(1, 2, 3)   
val listBuffer = mutable.ListBuffer("a", "b", "c")  
val hashSet = mutable.Set(0.1, 0.2, 0.3)  
val hashMap = mutable.Map("one"->1, "two"->2, "three"->3)  

arrayBuffer += 4  
listBuffer += "d"  
arrayBuffer -= 1  
listBuffer -= "a"  
hashMap += "four" -> 4  
hashMap -= "one"  

arrayBuffer ++= List(5, 6, 7)  
hashMap ++= Map("five" -> 5, "six" -> 6)  
hashMap --= Set("one", "three")  

// mutable vs immutable
var immutableSet = Set(1, 2, 3) 
immutableSet += 4   
//this is the same as:  
immutableSet = immutableSet + 4
//compare to  
val mutableSet = mutable.Set(1, 2, 3)  
mutableSet += 4   
// this is the same as:   
mutableSet.+=(4)
```
- - - -
## CLASS
- the class body, is also the default constructor’s implementation
- automatic getters are generated for the class parameters defined using val   
```Scala
class Person(val name:String) //generates a private `name` variable, and a getter with the same name
```
- automatic getters and setters are generated for class parameters defined using var
```scala
class Person(var name:String) //generates a private name variable, a getter and a setter with the same name
```
- To create explicit getters and setters - the private variable must have a different name
- everything is public by default unless explicity declared otherwise
```scala
class Person1(fname:String, lname:String){  
	// a public read only field
	val fullName = s"$fname $lname"
  def greet = s"Hi $fullName!"  
}  
val p1 = new Person1("Bob", "Marley")  
println(p1.greet)  
println(p1.fullName) 
// p2.fname / lname is not accessible  

//auto creates a getter for fname, and getter + setter to lname  
class Person2(val fname:String, var lname:String)  
val p2 = new Person2("Dave", "Matthews") {  
  //override the default string representation   
  override def toString = s"$fname $lname"   
}   
println(p2.lname)  
p2.lname = "Grohl"  
println(p2)  
```
- Scala’s getters and setters use the principle of uniform access, e.g. if you change the implentation of a field declared `var name` to a method `def name` you will not need to recompile the code
- Scala’s automatic getters and setters are following the unoform access principle, so the getter and setter name is the same as the field it encapsulates
- However if you need to have Java client code accessing your Scala class, it’s as easy as adding a `@BeanProperty` annotation to instruct the compiler to automatically add a Java bean style getter and setter.
```scala
import beans._ 
 
class SPerson(@BeanProperty var name:String)  
val sp = new SPerson("Scala Style")  
println(sp.name)  
sp.name += " rocks!"  
println(sp.getName)  
```

- - - -
## Call-by-value VS Call-by-name
- Call-by-value has the advantage that it evaluates every function argument only once.
- Call-by-name has the advantage that a function argument is not evaluated if the corresponding parameter is unused in the evaluation of the function body.
- Scala normally uses call-by-value.
- - - -
##  Nested functions
```scala
def sqrt(x: Double) = {
  def sqrtIter(guess: Double, x: Double): Double =
    if (isGoodEnough(guess, x)) guess
    else sqrtIter(improve(guess, x), x)

  def improve(guess: Double, x: Double) =
    (guess + x / guess) / 2

  def isGoodEnough(guess: Double, x: Double) =
    abs(square(guess) - x) < 0.001

  sqrtIter(1.0, x)
}
```