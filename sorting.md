# Sorting

Before walking through all the different sorting algorithms taught in this class, let's define **stability**. A sort is **stable** if objects that are viewed as equal by the sort are in the same position relative to each other before and after the sort. Let's explore stability with an example.

| Name          | Favorite Restaurant |
| ------------- | ------------------- |
| Alice         | Thai Basil          |
| Bob           | Sweetheart Cafe     |
| Carol         | Poke Parlor         |
| Dan           | Thai Basil          |
| Eve           | Kimchi Garden       |

If we sorted the table above by favorite restaurant alphabetically, the sort views (Alice, Thai Basil) and (Dan, Thai Basil) as equal since they have the same favorite restaurant. The sort is then _stable_ if Alice is still listed before Dan and unstable otherwise. 

## Comparison Sorts

Comparison sorts are the sorting algorithms that involve directly comparing the elements being sorted with each other to determine their ordering. As a result, the efficiency of comparison sorts are limited by the number of comparisons necessary to order all the elements.

### Selection Sort

Selection sort consists of selecting the 

| Prof. Hug's Walkthrough | Runtime | Stable? |
| ----------------------- | ------- | ------- |
| [Demo Link]() | 

### Insertion Sort

### Merge Sort

### Quick Sort

### Heap Sort

## Counting Sorts

### Radix Sort

#### Runtime Derivation 

### Least Significant Digit (LSD) Sort

### Most Significant Digit (MSD) Sort
