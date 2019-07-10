.. Fordham Snippets documentation master file, created by
   sphinx-quickstart on Fri Jul  5 19:20:09 2019.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Quicksort
==========
Quicksort is a sorting algorithm you should probably memorize. Besides being only 10 - 15 lines,
quicksort is typically the fastest sort by itself, in an average case. It doesn't do so well with
reversing an array, and that is the worst case (which is why we have hybrid sorts, but that's going to be
a later section).

So it's short and fast. Basically, if you had a hand of cards, you would pick a card (the "pivot"), and
seperate the rest of the cards into cards with values less than that and cards valued greater than that.
Then you pick a "pivot" in those groups of cards and repeat, until everything is sorted.

As you can imagine, you eventually get to a group with just one value, and you just return that value
(this would be called the "base case" here, because it stops the "recursion", but I'll stop using long words now).

It can be hard to understand, so `here's some Hungarian people dancing through it. <https://www.youtube.com/watch?v=ywWBy6J5gz8>`_

This example uses the first value as the "pivot", because it's easier to understand, but there are versions with a
middle-pivot, mean pivot, or even two pivots.

This example is also "stable", meaning equal values have the same relative order after sorting. See `this page <https://www.geeksforgeeks.org/stability-in-sorting-algorithms/>`_
for an explanation of that.

.. tabs::

   .. code-tab:: c++ C++

         #include <iostream>
         #include <vector>
         using namespace std;

         vector<int> quickSort(vector<int> array) {
             if (array.size() <= 1)
                 return array;
             vector<int> left;
             vector<int> right;
             int pivot = array[0];
             for(int i = 1; i < array.size(); i++)
                 array[i] < pivot ? left.push_back(array[i]) : right.push_back(array[i]);
             left = quickSort(left);
             left.push_back(pivot);
             right = quickSort(right);
             left.insert(left.end(), right.begin(), right.end());
             return left;
         }
         int main(){
             vector<int> vect{54, 3, 134, 5, 1, 98, 1531, 32};  //c++ 11
             vect = quickSort(vect);
             for (int i = 0; i < vect.size(); i++)
                 cout << vect[i] << endl;
             return 0;
         }

   .. code-tab:: c# C#

         using System.Collections.Generic;
         class Program
          {
             static List<int> quickSort(List<int> array) {
                 if(array.Count <= 1)
                     return array;
                 var left = new List<int>();
                 var right = new List<int>();
                 var pivot = array[0];
                 for(int i = 1; i < array.Count; i++){
                     if (array[i] < pivot)
                         left.Add(array[i]);
                     else
                         right.Add(array[i]);
                 }
                 left = quickSort(left);
                 left.Add(pivot);
                 left.AddRange(quickSort(right));
                 return left;
             }
              static void Main(string[] args)
              {
                  var list = new List<int> {54, 3, 134, 5, 1, 98, 1531, 32};
                  list = quickSort(list);
                  list.ForEach(System.Console.WriteLine);
              }
          }

   .. code-tab:: java Java

         import java.util.*;

         public class quickSorting {
             public static List<Integer> quickSort(List<Integer> numbers){
                 if(numbers.size() <= 1)
                     return numbers;
                 List<Integer> left = new ArrayList<>();
                 List<Integer> right = new ArrayList<>();
                 Integer pivot = numbers.get(0);
                 for(int i = 1; i < numbers.size(); i++){
                     if (numbers.get(i) < pivot)
                         left.add(numbers.get(i));
                     else
                         right.add(numbers.get(i));
                 }
                 left = quickSort(left);
                 left.add(pivot);
                 left.addAll(quickSort(right));
                 return left;
             }
             public static void main(String[] args) {
                 List<Integer> numbers = new ArrayList<>(Arrays.asList(54, 3, 134, 5, 1, 98, 1531, 32));
                 numbers = quickSort(numbers);
                 System.out.println(numbers);
             }
         }

   .. code-tab:: javascript JavaScript

         function quickSort(array) {
             if(array.length <= 1)
               return array;
             var pivot = array[0];
             var left = [];
             var right = [];
             for(var i = 1; i < array.length; i++)
                 array[i] < pivot ? left.push(array[i]) : right.push(array[i]);
             return quickSort(left).concat(pivot, quickSort(right));
           }
         console.log(quickSort([1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92, 0, 19232, 193, 2, 1311, 1]))


   .. code-tab:: python Python

         def quickSort(arr):
             if not len(arr) > 1:
                 return arr
             left = []
             right = []
             pivot = arr[0]
             for num in range(1,len(arr)):
                 left.append(arr[num]) if arr[num] < pivot else right.append(arr[num])
             return quickSort(left)+[pivot]+quickSort(right)

         names = ["Michael", "Luke", "Billy", "Tom", "McShane"]
         print(names)
         print(quickSort(names))

   .. code-tab:: swift Swift

         func quicksort<type: Comparable>(_ array: [type]) -> [type] {
           guard array.count > 1 else {return array}
           let pivot = array[0]
           var less: [type] = []
           var more: [type] = []
           for i in 1..<array.count{
             array[i] < pivot ? less.append(array[i]) : more.append(array[i])
           }
           return quicksort(less) + [pivot] + quicksort(more)
         }

         var arr = [9,8,5,7,9,8,8.8,90,70,6,66]
         print(quicksort(arr))

   .. code-tab:: swift Swift Alt.

         func quicksort<type: Comparable>(_ array: [type]) -> [type] {
           guard array.count > 1 else {return array}

           let pivot = array[0]
           let less = array.filter { $0 < pivot }
           let equal = array.filter { $0 == pivot }
           let greater = array.filter { $0 > pivot }

           return quicksort(less) + equal + quicksort(greater)
         }

         var arr = [9,8,5,7,9,8,8.8,90,70,6,66]
         print(quicksort(arr))


Notes
`````

.. tabs::

   .. code-tab:: text C++

          You'll notice the "base case" mentioned is the first part of the quicksort method, and that
          is for when we'll call the method repeatedly later. All you need to know is that this "base case"
          comes first.

          After making the left and right groups (lesser and greater values than the pivot), we need a way to
          determine which values are lesser or greater, so we iterate through them with the "for" loop. You'll
          notice inside this loop there are unfamiliar symbols here; this is the ternary conditional (?) operator.
          All it means is that there's a condition, the question mark, the true outcome, and the false outcome, all
          in that order (condition ? true_action : false_action), with that syntax.

          It's equivalent to:

          if(condition)
            true_action;
          else
            false_action;

          The more you know. Next, we want to sort the left side (left = quickSort(left)), add the pivot
          (left.push_back(pivot)), sort the right side, and add the two sides.

          In c++, concatenation (adding multiple things together) of vectors is done with the insert() method,
          with the syntax first.insert(first.end(), second.begin(), second.end()), with first and second
          being vectors. So that's what is being done there.

          Then you return your sorted array.

   .. code-tab:: text C#

          This is largely the same as the C++ operation, except with C#'s "List" instead of C++'s "vector".
          For the number of items in the list, the "count" property is used (list.count). To add something to
          the list, "list.Add(thing)" is used. To add a list to another list, "list.AddRange(secondList)" is
          used.

          Notice that instead of directly using the left and right lists, quicksort is called again when
          adding the lists together, making sure they are sorted and saving lines that would be used to assign
          them to sorted versions.

   .. code-tab:: text Java

          Here, we're using the "ArrayList" class, because it's relatively easy to use, can be expanded, and can
          be converted to other data structures such as a "linked list" through the "list" interface. In other words,
          you should prefer to use ArrayLists in Java when you can.

          To use an arraylist, you can use the line "import java.util.*;", getting the "array", "arraylist", and "list"
          dependencies all at the same time with the star ("*") operator.

          Because generic type arguments (the list<stuff> parts) can't use primitive types (like int) in Java,
          wrapper types are used instead. Here, instead of "int", the wrapper type is "Integer", which automatically
          casts (converts itself) between the two when necessary, so it works just like an int.

          With ArrayList, items are accessed with the syntax "list.get(index)", and can be set with the syntax
          "list.set(index, value)" . Because we are making a new list to return, only the "get()" method is needed.

          Adding items to the end of the list is done with the syntax list.add(item), and adding lists together is done
          with the syntax "listOne.addAll(listTwo)".

   .. code-tab:: text JavaScript

          You'll notice this is simpler than the solutions of the verbose (more articulated) languages, and that's a good thing.
          The syntax should be self explanatory up until the last few lines of the sort.

          In the line "array[i] < pivot ? left.push(array[i]) : right.push(array[i]);", JavaScript's ternary operator
          has the common syntax "condition ? true_action : false_action" . This is equivalent to:

          if(condition)
            true_action;
          else
            false_action;

          So the line reads "if the number is less than the pivot, put it in the left array,
          else put it in the right array".

          Next, when returning the array, the line "return quickSort(left).concat(pivot, quickSort(right));" is used
          to sort the left side and add the pivot and right arrays with the "concat()" method. The right array is also
          sorted in this line.

   .. code-tab:: text Python

          The syntax here should be self explanatory, for the most part. The range starts at one because the pivot is at index 0,
          and we want to compare everything else. There is a ternary operation here; the line
          "left.append(arr[num]) if arr[num] < pivot else right.append(arr[num])" has the syntax
          "true_action if condition else false_action", which is a little different than typical ternary
          operators.

          In the line returning the array, you'll notice the pivot is in square brackets ("[ ]"), and that's because
          the addition ("+") operator takes two arrays, so it's being put in its own little array.

          You'll also notice that there are words instead of numbers, and they get sorted alphabetically.
          This is taking advantage of the fact that quicksort is a comparative sort, and strings can be compared
          in python.

   .. code-tab:: text Swift

          Here, we are using a "type alias" (having a word that counts as many types) to make the function accept not only
          numbers, but any type that can be compared. The syntax for this is "<aliasName: type_describing_things>",
          and it's put right next to "func" to give that information to the function (the alias can be used in the parameters
          as well as the body of the function itself when placed there).

          Swift has what is known as "protocols" which define properties or requirements for different things. Here,
          we are using the "Comparable" protocol, requiring whatever type the alias is to be comparable (functional with less than,
          greater than, and similar operators). This is better than Javascript and Python because it will tell you if you are
          passing types that can't be compared before compiling, whereas other languages would just give you a runtime error.

          In the first line, instead of having a statement like "if (!condition)", we can have a "guard" statement with the syntax
          "guard condition else{false_action}" , which is neater than usual.

          There is the ternary operator here ("?"), with the syntax "condition ? true_action : false_action", equivalent to

          if condition{
            true_action
          }else{
            false_action
          }

          The pivot is placed in square brackets ("[ ]") to behave like an array when adding the left, pivot, and right together.

   .. code-tab:: text Swift Alt.

          See the other Swift tab for other syntax details.

          This implementation can also be done with swift using the "filter" method of the array class.
          "filter" has the syntax "array.filter {some_condition_with_$0}", where $0 is any given item.
          It returns the array where the condition is true for all the items. So "$0 < pivot" returns the array
          that has all the items less than the pivot. Similar conditions are used for the other arrays.

          Obviously, the "equal" array doesn't need to be sorted because all the items are equivalent.
