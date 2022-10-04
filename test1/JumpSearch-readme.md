# Jump search
 
**1. Explain the algorithm purpose**
The purpose of this Algorithm is to optimally find an element in a sorted array of numbers. It performs the search by jumping ahead by fixed steps or skipping some elements in place of searching all elements.
 
**2. Detail each line. What is the line intended to do ?**
 ```php {.numberLines}
 
function jumpSearch($list,$key)
{
   /*number of elements in the sorted array*/
   $num = count($list);
  /*block size to be jumped*/
  // define the step to jump by. By default sqr of the list size.
   $step = (int)sqrt($num);
   // define a variable to hold the previous step
   $prev = 0;
  
   // Find the block containing the target element
   //  At each iteration , it (jump and) excludes all elements lower than the target number. 
   // if the element at index min($step, $num)-1 is lower than it jump the next step
   while ($list[min($step, $num)-1] < $key)
   {
       // set the current step to the previous.
       $prev = $step;
       // update the value of step to the next.
       $step += (int)sqrt($num);
       // if the end of array is reached then the block is empty
       //  and the target value index is -1
       if ($prev >= $num)
           return -1;
   }
 
   /*Performing linear search for $key in block*/
   while ($list[$prev] < $key)
   {
       $prev++;
       // if the end of block is reached then
       // the target number is not in the block and it index is -1
       if ($prev == min($step, $num))
           return -1;
   }
   // If the final value at prev index matches the target value
   // then return $prev as the index of the target value
   // else return -1.
   
   // if ($list[$prev] === $key)
   //     return $prev;
   // return -1;
 
    return $list[$prev] === $key ? $prev : -1;
}
// That algorithm will run with a time complexity of O(√n) and space complexity of O(1)
```
 
 
**3. Provide Test Case** (using PHPUnit)
 
 
```php {.numberLines}
<?php
use PHPUnit\Framework\TestCase;
class JumpSearchTest extends TestCase
{
   protected $arry1 = [-50, -20, -15, 9, 10, 15, 20];
   protected $existingTarget =  9;
   protected $nonexistingTarget =  19;
 
   /**
    * Test case 1 : Find existing target
    *
    * @return void
    */
   public function jumpSearchShouldFindExistingTargetTest()
   {
        $result = binarySearchIterative($this->arry1,$this->existingTarget);
        $this->assertEquals($result, 3)
  
   }
 
 
   /**
    * Test case 2 : Find nonexisting target
    *
    * @return void
    */
   public function jumpSearchShouldNotFindUnexistingTargetTest()
   {
        $result = binarySearchIterative($this->arry1,$this->nonexistingTarget);
        $this->assertEquals(-1, $this->nonexistingTarget)
   }
 
 
}
 
```