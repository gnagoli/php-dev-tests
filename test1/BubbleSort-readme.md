# Bubble Sort
 
**1. Explain the algorithm purpose**
The purpose of this Algorithm is to sort an array of numbers by continually swapping the adjacent numbers if they are in the wrong order.

 **2. Detail each line. What is the line intended to do ?**

 ```php {.numberLines}
 
function bubbleSort($array) {
   // store the number of element in the array as $length
   $length = count($array);
 
   // Iterate over the array element by starting from the end
   for ($i = $length; $i > 0; $i--) {
       $swapped = true; // assert that every element in array has been swapped
 
       //  Iterate over the array from the beginning
       for ($j=0;$j<$i-1;$j++) {
           //  check if the next two adjacent number are in wrong order
           // (descending order in this case)
           //  then swap them.
           if ($array[$j] > $array[$j + 1]) {
               // store the value of the first number
               // in a temp variable to void losing it
               $temp = $array[$j];
               // set the first number value to the second number value.
               $array[$j] = $array[$j + 1];
               // set the second number to the temp value
               $array[$j + 1] = $temp;
               $swapped = false; //  assert that there are value that can be swapped
           }
       }
 
       // if the valued of swapped has not been update by previous block,
       // then the array has been completely sorted and  the iterations can be stopped.
       if ($swapped) break;
   }
 
   //  return the sorted array.
   return $array;
}
// That algorithm will run with a time complexity of O(n^2) and space complexity of O(1)
```
 
**3. Provide Syntax improvements or performance optimization if any**
 
 The first for loop can be replaced by a while loop with a more comprehensive syntax.
 
```php {.numberLines}
 
function bubbleSort($array) {
 $isSorted = false;
 $counter = 0;
 while(!$isSorted) {
   $isSorted = true;
   $limit =  count($array) - 1 - $counter;
   $counter++;
   for ($i = 0; $i < $limit; $i++) {
     if ($array[$i] > $array[$i + 1]) {
       $temp = $array[$i];
       $array[$i] = $array[$i + 1];
       $array[$i + 1] = $temp;
       $isSorted = false
     }
   }
 }
 return $array;
}
 
```
 
**3. Provide Test Case** (using PHPUnit)
 
```php {.numberLines}
<?php
use PHPUnit\Framework\TestCase;
class BubbleSortTest extends TestCase
{
   protected $unsortedArray = [9, 10, -50, 15, 20, -20, -15];
   protected $sortedArray   = [-50, -20, -15, 9, 10, 15, 20];
  
 
   /**
    * Test case 1 : Sort array
    *
    * @return void
    */
   public function bubbleSortTest()
   {
        $result = bubbleSort($this->unsortedArray);
        for($i=0;$i< count($result); $i++){
            $this->assertEquals($result[$i], $this->sortedArray[$i])
        }
   }
 
}
 
```