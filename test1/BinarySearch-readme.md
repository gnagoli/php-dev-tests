# Binary search
 
**1. Explain the algorithm purpose**
The purpose of this Algorithm is to optimally find an element in a sorted array of numbers. It progressively reduces the size of the list by dividing it by two until it finds the target number.

**2. Detail each line. What is the line intended to do ?**
 
- *binarySearchIterative*
 ```php {.numberLines}
 
function binarySearchIterative($list, $target)
{
   // create a variable to hold the starting index of
   // the sub-array that contains the target number.
   // default value : first index of the $list
   $first = 0;
 
   //  create a variable to hold the last index of
   //  the sub-array that contains the $target number.
   //  default value : last index of the $list
   $last = count($list)-1;
 
   // create a while loop to iterate over
   // the sub-array containing the $target number
   // while the  starting index is lower than the ending index
   while ($first <= $last) {
 
       // find the index of the element in the middle of the sub-array
       // take the lowest integer closest to the middle of $first and $last
       // $mid = floor(($first + $last)/2);
       $mid = ($first + $last) >> 1;
 
       // compare the target number to the number in the middle
       if ($list[$mid] == $target) {
           // if found then return the value and break the while loop
           return $mid;
       } elseif ($list[$mid] > $target) {
           // if target lower than the number in middle
           // then update the $last index,
           // set it value the integer right before $mid
           $last = $mid - 1;
       } elseif ($list[$mid] < $target) {
           // if target greater than the number in middle
           // then update the $first index,
           // set it value the integer right after $mid
           $first = $mid + 1;
       }
   }
 
   // This line is reached when the target number is not found. The returning value is null.
   return null;
}
// That algorithm will run with a time complexity of O(log(n)) and space complexity of O(1)
```
 
- *binarySearchByRecursion*
 ```php {.numberLines}
function binarySearchByRecursion($list, $target, $start, $end)
{
// ========= start:  Optimize the algorithm by handling edge cases ======= //
   if (count($list) == 0) {
       return null;
   }
 
   if (count($list) < 2) {
       return $list[0] == $target ? 0 : null;
   }
 
   if ($start > $end)
       return null;
 // ========= end: Optimize the algorithm by handling edge cases ======= //
 
 // find the index of the element in the middle of the list
 // take the lowest integer closest to the middle of $start and $end
 // $mid = floor(($start + $end)/2);
 $mid = ($start + $end) >> 1;
 
   // compare the target number to the number in the middle of the list
   if ($list[$mid] == $target) {
       // if found then return the value and end the recursion
       return $mid;
   } elseif ($list[$mid] > $target) {
       // if target lower than the number in middle
       // then recursively call the search function
       // by passing  the integer right before $mid as the value of $end variable
       return binarySearchByRecursion($list, $target, $start, $mid-1);
   } elseif ($list[$mid] < $target) {
       // if target greater than the number in middle
       // then recursively call the search function
       // by passing  the integer right after $mid as the value of $start variable
       return binarySearchByRecursion($list, $target, $mid+1, $end);
   }
 
   // This line is reached when the target number is not found. The returning value is null.
   return null;
}
// That algorithm will run with a time complexity of O(log(n)) and space complexity of O(log(n))
```
 
**3. Provide Test Case** (using PHPUnit)
 
 
```php {.numberLines}
<?php
 
use PHPUnit\Framework\TestCase;
class BinarySearchTest extends TestCase
{
   protected $arry1 = [-50, -20, -15, 9, 10, 15, 20];
   protected $existingTarget =  9;
   protected $nonexistingTarget =  19;
 
   /**
    * Test case 1 : Find existing target
    *
    * @return void
    */
   public function binarySearchIterativeShouldFindExistingTargetTest()
   {
        $result = binarySearchIterative($this->arry1,$this->existingTarget);
        $this->assertEquals($result, $this->existingTarget)
  
   }
 
 
   /**
    * Test case 2 : Find nonexisting target
    *
    * @return void
    */
   public function binarySearchIterativeShouldNotFindUnexistingTargetTest()
   {
        $result = binarySearchIterative($this->arry1,$this->nonexistingTarget);
        $this->assertEquals(null, $this->nonexistingTarget)
   }
 
 
 
   /**
    * Test case 3 : Find existing target
    *
    * @return void
    */
   public function binarySearchByRecursionShouldFindExistingTargetTest()
   {
       $result =  binarySearchByRecursion($this->arry1,$this->existingTarget, 0, 6);
       $this->assertEquals($result, $this->existingTarget)
     
   }
 
 
   /**
    * Test case 4 : Find nonexisting target
    *
    * @return void
    */
   public function binarySearchByRecursionShouldNotFindUnexistingTargetTest()
   {
       $result =  binarySearchByRecursion($this->arry1,$this->nonexistingTarget, 0, 6);
       $this->assertEquals(null, $this->nonexistingTarget)
   }
}
 
```