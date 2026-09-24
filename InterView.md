# Intervirew_Questions
## Question1:  What is final keyword?
By the use of final keyword a class can not be inherit, a method can not be overriden, a variable value can not changed.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Question2: Why String class is immutable?
String is immutable because once a String object is created, its value cannot be changed. If we try to modify a String, Java creates a new String object instead of changing the existing one. This immutability is especially important because Strings are stored in the String Constant Pool (SCP), where the same String object can be shared by multiple references. If Strings were mutable, changing one shared String could affect other references unexpectedly. Immutability also provides security, thread-safety, and reliable use of Strings as keys in HashMap. So, SCP is not the direct reason why String is immutable; rather, the SCP benefits from String's immutability.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Question3 :  P obj = new P(); in this case what happens?
## When we write P p = new P();, Java creates a new object of class P in the heap memory using the new keyword, and the constructor of class P is called during object creation. P p declares a reference variable p of type P, and this reference variable stores the reference to the newly created object. In simple words, new P() creates the object, and p refers to that object.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
## Question3: Purpose of static block(SIT)?
## A static initialization block is used to initialize static variables or perform some setup work when the class is loaded into memory. It executes only once, before the main() method or before the class is used to create objects. It is mainly useful when the initialization requires some logic that cannot be done with a simple assignment.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
