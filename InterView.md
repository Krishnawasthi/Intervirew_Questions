# Intervirew_Questions
### Question1:  What is final keyword?
By the use of final keyword a class can not be inherit, a method can not be overriden, a variable value can not changed.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Question1: Why String class is immutable?
String is immutable because once a String object is created, its value cannot be changed. If we try to modify a String, Java creates a new String object instead of changing the existing one. This immutability is especially important because Strings are stored in the String Constant Pool (SCP), where the same String object can be shared by multiple references. If Strings were mutable, changing one shared String could affect other references unexpectedly. Immutability also provides security, thread-safety, and reliable use of Strings as keys in HashMap. So, SCP is not the direct reason why String is immutable; rather, the SCP benefits from String's immutability.
--------------------------------------------------------------------------------------------------------------------------------------------------------------------
