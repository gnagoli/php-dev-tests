# Bubble Sort
 
**1. Explain the algorithm purpose**
The purpose of this Algorithm is to sort an array of numbers by progressively inserting values in a sorted array. The array is  divided in two part a sorted and an unsorted part. Values from the unsorted part are picked and inserted at the correct position in the sorted part.

**2. Detail each line. What is the line intended to do ?**
 
 ```php {.numberLines}
 
function insertionSort(array $array)
{
 //  Iterate over the array starting from
 //  the second element in the array.
   for ($i = 1; $i < count($array); $i++)
   {
     //  stort the current element in a variable.
       $currentVal = $array[$i];
 
       // loop through the element with index less than the current value index,
       // and check if the element is greater than the current value.
       for ($j = $i - 1; $j >= 0 && $array[$j] > $currentVal; $j--)
       {
         //  if found then insert the element right after the current value.
         $array[$j + 1] = $array[$j];
       }
       // update the index of current value.
       $array[$j + 1] = $currentVal;
   }
 //  return the sorted array.
   return $array;
}
 
// That algorithm will run with a time complexity of O(n^2) and space complexity of O(1)
```
 
**3. Provide Test Case** (using PHPUnit)
 
```php {.numberLines}
<?php
use PHPUnit\Framework\TestCase;
class InsertionSortTest extends TestCase
{
   protected $unsortedArray = [9, 10, -50, 15, 20, -20, -15];
   protected $sortedArray   = [-50, -20, -15, 9, 10, 15, 20];
  
 
   /**
    * Test case 1 : Sort array
    *
    * @return void
    */
   public function insertionSortTest()
   {
        $result = insertionSort($this->unsortedArray);
        for($i=0;$i< count($result); $i++){
            $this->assertEquals($result[$i], $this->sortedArray[$i])
        }
   }
 
}
 
```