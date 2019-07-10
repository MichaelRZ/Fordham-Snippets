Exponentiation by Squaring
==========================

"Exponentiation by squaring" is a fancy way of saying "fast power operations".
For example, for 2^10, two would need to be multiplied ten times.
With this algorithm, 2^10 turns into (2*2)^5, which turns into 4(4*4)^2,
then 4(16*16), giving our answer of 1024 in only four multiplications.
As the power gets larger, it becomes clearer why this method is faster,
given that multiplication is more computationaly expensive than other
operations.

The logic goes, for a number and a power:

* If the power is less than zero, return one over the number and make the power negative.
* If the power is zero, return the number one.
* Return the number if the power is one.
* If the number is even, square the number and half the power.
* If the number is odd, multiply by the number, subtract one from the power, and do the even operation.

* Repeat until the power is one.

You don't need to memorize this, of course, but it's simple enough for practice.

.. tabs::

   .. code-tab:: c++ C++

         #include <iostream>
         using namespace std;

         long long powers(long long num, long long pow){
             cout << num << " , " << pow << endl;
             if(pow < 0){
                 return powers(1 / num, -pow);
             }else if(pow == 0){
                 return 1;
             }else if(pow == 1){
                 return num;
             }else if(pow % 2 == 0){
                 return powers(num * num, pow / 2);
             }else{
                 return num * powers(num * num, (pow - 1) / 2);
             }
         }

   .. code-tab:: c# C#

         class Program
          {
             static long powers(long num, long pow){ 
             System.Console.WriteLine(num + " , " + pow);
             if(pow < 0){
                 return powers(1 / num, -pow);
             }else if(pow == 0){
                 return 1;
             }else if(pow == 1){
                 return num;
             }else if(pow % 2 == 0){
                 return powers(num * num, pow / 2);
             }else{
                 return num * powers(num * num, (pow - 1) / 2);
             }
         }
              static void Main(string[] args)
              {
                  System.Console.WriteLine(powers(4, 25));
              }
          }

   .. code-tab:: java Java

         public class powersRecursive {
             public static long powers(long num, long pow){
                 System.out.println(num + " , " + pow);
                 if(pow < 0){
                     return powers(1 / num, -pow);
                 }else if(pow == 0){
                     return 1;
                 }else if(pow == 1){
                     return num;
                 }else if(pow % 2 == 0){
                     return powers(num * num, pow / 2);
                 }else{
                     return num * powers(num * num, (pow - 1) / 2);
                 }
               }
             public static void main(String[] args) {
                 System.out.println(powers(4, 25));
             }
         }

   .. code-tab:: javascript JavaScript

         function powers(num, pow) {
             console.log(num, pow);
             if(pow < 0){
                 return powers(1 / num, -pow);
             }else if(pow === 0){
                 return 1;
             }else if(pow === 1){
                 return num;
             }else if(pow % 2 === 0){
                 return powers(num * num, pow / 2);
             }else{
                 return num * powers(num * num, (pow - 1) / 2);
             }
         }

   .. code-tab:: python Python

         def power(num, pow):
             print(num, pow)
             if pow < 0:
                 return power(1/num, -pow)
             elif pow == 0:
                 return 1
             elif pow == 1:
                 return num
             elif pow % 2 == 0:
                 return power(num*num, pow / 2)
             else:
                 return num*power(num*num, (pow - 1) / 2)
         print(power(4,25))

   .. code-tab:: swift Swift

         func powers(_ num: Int,_ pow: Int) -> Int {
             print(num, pow)
             if pow < 0{
                 return powers(1/num, -pow)
             }else if pow == 0{
                 return 1
             }else if pow == 1{
                 return num
             }else if pow % 2 == 0{
                 return powers(num * num, pow / 2)
             }else{
                 return num * powers(num * num, (pow - 1) / 2)
             }
         }
         print(powers(4, 25))

Notes
`````

.. tabs::

   .. code-tab:: text C++

          "long long" here is a number type, just like "int", but it can store larger numbers.
          The expression "pow % 2 == 0" means there is no remainder when divided by two repeatedly,
          or the number is even.

          The only case left, of course, is that the number is odd, since the cases
          negative, zero, one, and even are accounted for.

   .. code-tab:: text C#

          In C#, the "long" type is like the C++ "long long" type, a 64 bit integer.

   .. code-tab:: text Java

          "long" here is a 64 bit integer, nothing else here of note.

   .. code-tab:: text JavaScript

          Because javascript is loosely typed (no types such as "int" are specified), be careful not
          to pass in a decimal number because this relies on equality comparisons, which those types can't do.

   .. code-tab:: text Python

          In python, "elif" is used instead of the typical "else if", because python would have you indent twice
          with that, and it would take another line.

   .. code-tab:: text Swift

          The underscore beside the parameter names make them unrequired when calling the function instead of the
          default required with swift.

          (powers(4,25) can be called instead of powers(num: 4, pow:25) which is standard in swift).
