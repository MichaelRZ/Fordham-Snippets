.. Fordham Snippets documentation master file, created by
   sphinx-quickstart on Fri Jul  5 19:20:09 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Bubble Sort
===========
Sorting is an important topic in computer science, and will inevitably come up at some point while you are programming.
Because of that, you should know the most common methods, starting with "Bubble sort".

"Bubble sort" is a bad sorting algorithm. However, you should know this before skipping to
the "Quick sort" section, because this one is easier to understand.

Imagine you had a hand of cards. You go through the cards, from left to right, and swap cards next to each other
whenever the left one is larger. You keep doing this until the cards are sorted. That's bubble sort.

Don't get it yet? `Here's some interpretive dance. <https://www.youtube.com/watch?v=lyZQPjUT5B4>`_

It's a bad sorting algorithm because it's slow next to everything else, but wasn't that easy to understand?
Here it is in practice:

.. tabs::

   .. code-tab:: c++ C++

          #include <iostream>
          #include <vector>
          using namespace std;

          vector<int> bubbleSort(vector<int> array) {
          bool sorted = false;
          do{
           sorted = true;
           for(int i = 0; i < array.size()-1; i++){
               if(array[i]>array[i+1]){
                   sorted = false;
                   int temp = array[i];
                   array[i] = array[i+1];
                   array[i+1] = temp;
               }
           }
          }while(!sorted);
          return array;
          }
          int main(){
          vector<int> vect{54, 3, 134, 5, 1, 98, 1531, 32};  //c++ 11
          vect = bubbleSort(vect);
          for (int i = 0; i < vect.size(); i++)
           cout << vect[i] << endl;
          return 0;
          }

   .. code-tab:: c# C#

         using System.Collections.Generic;
         class Program
          {
             static List<int> bubbleSort(List<int> array) {
             bool sorted = false;
             do{
                 sorted = true;
                 for(int i = 0; i < array.Count-1; i++){
                     if(array[i]>array[i+1]){
                         sorted = false;
                         int temp = array[i];
                         array[i] = array[i+1];
                         array[i+1] = temp;
                     }
                 }
             }while(!sorted);
             return array;
         }
              static void Main(string[] args)
              {
                  System.Console.WriteLine("Hello world!");
                  var list = new List<int> {54, 3, 134, 5, 1, 98, 1531, 32};
                  list = bubbleSort(list);
                  list.ForEach(System.Console.WriteLine);
              }
          }

   .. code-tab:: java Java

         import java.util.Arrays;

         public class bubbleSorting {
             public static int[] bubbleSort(int[] array){
                 var sorted = false;
                 do{
                     sorted = true;
                     for(var i = 0; i < array.length-1; i++){
                         if(array[i]>array[i+1]){
                             sorted = false;
                             var temp = array[i];
                             array[i] = array[i+1];
                             array[i+1] = temp;
                         }
                     }
                 }while(!sorted);
               return array;
             }
             public static void main(String[] args) {
                 var numbers = new int[] {54, 3, 134, 5, 1, 98, 1531, 32};
                 numbers = bubbleSort(numbers);
                 System.out.println(Arrays.toString(numbers));
             }
         }

   .. code-tab:: javascript JavaScript

         function bubbleSort(array) {
             var sorted = false;
             do{
                 sorted = true;
                 for(var i = 0; i < array.length-1; i++){
                     if(array[i]>array[i+1]){
                         sorted = false;
                         var temp = array[i];
                         array[i] = array[i+1];
                         array[i+1] = temp;
                     }
                 }
             }while(!sorted);
           return array;
         }
         var numbers = [1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92];
         console.log(bubbleSort(numbers));

   .. code-tab:: python Python

          def bubbleSort(array):
          sorted = False
          while not sorted:
           sorted = True
           for index in range(0,len(array)-1):
               if array[index] > array[index+1]:
                   sorted = False
                   temp = array[index]
                   array[index] = array[index+1]
                   array[index+1] = temp
          return array

          nums = [0.8, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92, 0, 19232, 193, 2, 1311, 1]
          print(nums)
          print(bubbleSort(nums))

   .. code-tab:: swift Swift

          func bubbleSort(_ input: [Int]) -> [Int] {
          var array = input
          var sorted = false
          while !sorted{
           sorted = true
           for index in 0..<array.count-1{
               if array[index] > array[index+1]{
                   sorted = false
                   let temp = array[index]
                   array[index] = array[index+1]
                   array[index+1] = temp
               }
           }
          }
          return array
          }
          print(bubbleSort([9,8,50,7,9,9012,142,90,70,6,66]))

Notes
`````

.. tabs::

   .. code-tab:: text C++

          The first thing you might notice is the weird "vector" language with the angle brackets (<likethis>).
          That's because, in C++, you should almost always prefer vectors over normal arrays. After declaring a vector,
          with vector<type>, they function the same way as arrays, but you can get the size with .size(), and they
          can be resized. Make sure to have the line "#include <vector>" at the top of the file.

          There is one line marked as C++ 11 here, so add "-std=c++11" after "g++" when compiling if it doesn't work.

          If you're stuck with an older version of C++, vectors can also be initialized like this:

          int arr[] = { 10, 20, 30 };
          int n = sizeof(arr) / sizeof(arr[0]);
          vector<int> vect(arr, arr + n);

   .. code-tab:: text C#

          Here, we are using a "List", the more useful version of an array in C#.
          Make sure to add "using System.Collections.Generic;" to the top of the file to use lists.

          The syntax for lists is similar to C++'s "vector".

          The only line which may be confusing here is "list.ForEach(System.Console.WriteLine);"
          Here, lists have a property called "ForEach", so for each item in the list it prints it to the console.

   .. code-tab:: text Java

          To use arrays in Java, have "import java.util.Arrays;" at the top of the file.
          To print the array, in the Arrays section of java, there's the syntax "Arrays.toString(array)",
          which turns the array into a string that can be given to the console.


   .. code-tab:: text JavaScript

          Here, being a loosely typed language can help because the algorithm is only comparing values.
          In fact, if you gave it a list of words, it should come back alphabetized.

          (You may be shocked to learn letters are in fact numbers, in computers at least. See an "ascii table".)

   .. code-tab:: text Python

          "not" is used instead of the typical "!" operator.
          The "range" function here is used to match Python's "for ... in ..." syntax.
          The numbers in the statement are included, and the variable after "for" iterates through these numbers.

          Here, being a loosely typed language can help because the algorithm is only comparing values.
          In fact, if you gave it a list of words, it should come back alphabetized.

          (You may be shocked to learn letters are in fact numbers, in computers at least. See an "ascii table".)

   .. code-tab:: text Swift

          The underscore before the parameter gets rid of the variable name when calling the function.
          Swift has the syntax [type] when describing an array.

          The statement "for index in 0..<array.count-1" can be read as "for each number from zero to one before this number".
          typically "..." would be used to state a range, but "..<" can be used to stop short of the second number, instead of including it.
