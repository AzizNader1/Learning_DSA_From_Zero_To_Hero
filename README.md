# Master C# Data Structures and Algorithms from A to Z

## Table of Contents
1. [Introduction to Data Structures and Algorithms](#1-introduction-to-data-structures-and-algorithms)
2. [Big O Notation and Complexity Analysis](#2-big-o-notation-and-complexity-analysis)
3. [Arrays in C#](#3-arrays-in-c)
4. [ArrayList and List<T>](#4-arraylist-and-listt)
5. [Linked Lists](#5-linked-lists)
6. [Stacks](#6-stacks)
7. [Queues](#7-queues)
8. [Dictionaries and Hash Tables](#8-dictionaries-and-hash-tables)
9. [Sets](#9-sets)
10. [Sorting Algorithms](#10-sorting-algorithms)
11. [Searching Algorithms](#11-searching-algorithms)
12. [Binary Trees](#12-binary-trees)
13. [Binary Search Trees](#13-binary-search-trees)
14. [Balanced Trees (AVL and Red-Black)](#14-balanced-trees-avl-and-red-black)
15. [Heaps and Priority Queues](#15-heaps-and-priority-queues)
16. [Graphs - Representation](#16-graphs---representation)
17. [Graph Traversal Algorithms](#17-graph-traversal-algorithms)
18. [Shortest Path Algorithms](#18-shortest-path-algorithms)
19. [Minimum Spanning Trees](#19-minimum-spanning-trees)
20. [Recursion and Backtracking](#20-recursion-and-backtracking)
21. [Dynamic Programming](#21-dynamic-programming)
22. [Greedy Algorithms](#22-greedy-algorithms)
23. [String Algorithms](#23-string-algorithms)
24. [Trie Data Structure](#24-trie-data-structure)
25. [Bit Manipulation](#25-bit-manipulation)
26. [Advanced Data Structures](#26-advanced-data-structures)
27. [Algorithm Design Patterns](#27-algorithm-design-patterns)
28. [Problem-Solving Strategies](#28-problem-solving-strategies)
29. [Best Practices and Interview Tips](#29-best-practices-and-interview-tips)

---

## 1. Introduction to Data Structures and Algorithms

Data structures and algorithms form the fundamental building blocks of computer science and software development. A data structure is a specialized format for organizing, processing, retrieving, and storing data, while an algorithm is a step-by-step procedure or formula for solving a problem. Together, they provide the foundation for writing efficient, scalable, and maintainable software that can handle real-world data processing challenges.

Understanding data structures and algorithms is crucial for several reasons. First, they enable you to write code that performs well even with large amounts of data—a poorly chosen data structure can make an application unusably slow, while the right choice can make it lightning fast. Second, they are the language of technical interviews at major technology companies, where candidates are expected to analyze problems, propose efficient solutions, and implement them correctly under time pressure. Third, a solid grasp of these concepts helps you understand and evaluate existing libraries and frameworks, making you a more effective developer overall.

### Why Data Structures Matter

```csharp
// Example: Searching for an item
// Using List - O(n) time complexity
List<int> numbers = Enumerable.Range(1, 1_000_000).ToList();
bool contains1 = numbers.Contains(500_000);  // Takes ~5ms for 1 million items

// Using HashSet - O(1) time complexity
HashSet<int> numberSet = Enumerable.Range(1, 1_000_000).ToHashSet();
bool contains2 = numberSet.Contains(500_000);  // Takes ~0.001ms - 5000x faster!

// The right data structure makes all the difference
```

### Classification of Data Structures

| Category | Data Structures | Characteristics |
|----------|----------------|-----------------|
| **Linear** | Array, List, Stack, Queue | Elements arranged sequentially |
| **Non-Linear** | Tree, Graph, Heap | Elements in hierarchical/network structure |
| **Homogeneous** | Array, List | All elements same type |
| **Heterogeneous** | Tuple, Struct | Elements can be different types |
| **Static** | Array (fixed size) | Size determined at compile time |
| **Dynamic** | List, LinkedList, Dictionary | Size can change at runtime |

### Algorithm Characteristics

A good algorithm must satisfy several characteristics to be considered well-designed. It must be finite, meaning it terminates after a bounded number of steps. It must be well-defined, with each step having a clear, unambiguous meaning. It must have zero or more inputs and produce one or more outputs. It must be effective, with each step being basic enough to be carried out exactly. Understanding these characteristics helps you evaluate and design algorithms that solve problems correctly and efficiently.

```csharp
// Algorithm Analysis Example
public class AlgorithmComparison
{
    // O(n²) - Quadratic time
    public static int[] FindDuplicates_Slow(int[] arr)
    {
        List<int> duplicates = new();
        for (int i = 0; i < arr.Length; i++)
        {
            for (int j = i + 1; j < arr.Length; j++)
            {
                if (arr[i] == arr[j] && !duplicates.Contains(arr[i]))
                {
                    duplicates.Add(arr[i]);
                }
            }
        }
        return duplicates.ToArray();
    }
    
    // O(n) - Linear time
    public static int[] FindDuplicates_Fast(int[] arr)
    {
        HashSet<int> seen = new();
        HashSet<int> duplicates = new();
        
        foreach (int item in arr)
        {
            if (!seen.Add(item))
            {
                duplicates.Add(item);
            }
        }
        return duplicates.ToArray();
    }
}
```

---

## 2. Big O Notation and Complexity Analysis

Big O notation is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity. In computer science, it is used to classify algorithms according to how their run time or space requirements grow as the input size grows. Understanding Big O notation is essential for analyzing algorithm efficiency and making informed decisions about which algorithms and data structures to use in different situations.

Big O notation provides an upper bound on the growth rate of an algorithm's time or space complexity. It answers the question: "How does the runtime scale as the input gets arbitrarily large?" This focus on asymptotic behavior means that Big O ignores constant factors and lower-order terms, capturing only the dominant term that most affects growth at scale.

### Common Time Complexities

| Complexity | Name | Example | 10 inputs | 1000 inputs | 1M inputs |
|------------|------|---------|-----------|-------------|-----------|
| O(1) | Constant | Array access | 1 | 1 | 1 |
| O(log n) | Logarithmic | Binary search | 3 | 10 | 20 |
| O(n) | Linear | Linear search | 10 | 1,000 | 1,000,000 |
| O(n log n) | Linearithmic | Merge sort | 30 | 10,000 | 20,000,000 |
| O(n²) | Quadratic | Bubble sort | 100 | 1,000,000 | 10¹² |
| O(n³) | Cubic | Matrix multiplication | 1,000 | 10⁹ | 10¹⁸ |
| O(2ⁿ) | Exponential | Recursive Fibonacci | 1,024 | 10³⁰¹ | ∞ |
| O(n!) | Factorial | Traveling salesman | 3,628,800 | ∞ | ∞ |

### Time Complexity Analysis

```csharp
public class TimeComplexityExamples
{
    // O(1) - Constant time
    // Runtime does not depend on input size
    public static int GetFirstElement(int[] arr)
    {
        if (arr.Length == 0) return -1;
        return arr[0];  // Single operation, regardless of array size
    }
    
    public static bool IsEven(int n)
    {
        return n % 2 == 0;  // Single arithmetic operation
    }
    
    // O(log n) - Logarithmic time
    // Input is halved each iteration
    public static int BinarySearch(int[] sortedArr, int target)
    {
        int left = 0, right = sortedArr.Length - 1;
        
        while (left <= right)
        {
            int mid = left + (right - left) / 2;
            
            if (sortedArr[mid] == target)
                return mid;
            else if (sortedArr[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }
        
        return -1;  // Not found
    }
    
    // O(n) - Linear time
    // Iterate through all elements once
    public static int FindMax(int[] arr)
    {
        int max = arr[0];
        for (int i = 1; i < arr.Length; i++)
        {
            if (arr[i] > max)
                max = arr[i];
        }
        return max;
    }
    
    // O(n log n) - Linearithmic time
    // Common in efficient sorting algorithms
    public static void MergeSort(int[] arr, int left, int right)
    {
        if (left < right)
        {
            int mid = left + (right - left) / 2;
            MergeSort(arr, left, mid);      // T(n/2)
            MergeSort(arr, mid + 1, right); // T(n/2)
            Merge(arr, left, mid, right);   // O(n)
        }
    }
    
    private static void Merge(int[] arr, int left, int mid, int right)
    {
        // Merge two sorted halves - O(n) operation
        int[] temp = new int[right - left + 1];
        int i = left, j = mid + 1, k = 0;
        
        while (i <= mid && j <= right)
        {
            if (arr[i] <= arr[j])
                temp[k++] = arr[i++];
            else
                temp[k++] = arr[j++];
        }
        
        while (i <= mid) temp[k++] = arr[i++];
        while (j <= right) temp[k++] = arr[j++];
        
        for (i = 0; i < temp.Length; i++)
            arr[left + i] = temp[i];
    }
    
    // O(n²) - Quadratic time
    // Nested loops over input
    public static void BubbleSort(int[] arr)
    {
        int n = arr.Length;
        for (int i = 0; i < n - 1; i++)           // n iterations
        {
            for (int j = 0; j < n - i - 1; j++)   // n iterations each
            {
                if (arr[j] > arr[j + 1])
                {
                    (arr[j], arr[j + 1]) = (arr[j + 1], arr[j]);
                }
            }
        }
    }
    
    // O(2ⁿ) - Exponential time
    // Recursive calls double each level
    public static long Fibonacci(int n)
    {
        if (n <= 1) return n;
        return Fibonacci(n - 1) + Fibonacci(n - 2);  // Two recursive calls
    }
    
    // O(n!) - Factorial time
    // Generate all permutations
    public static List<List<int>> Permutations(int[] arr)
    {
        var result = new List<List<int>>();
        GeneratePermutations(arr, 0, result);
        return result;
    }
    
    private static void GeneratePermutations(int[] arr, int start, List<List<int>> result)
    {
        if (start == arr.Length)
        {
            result.Add(new List<int>(arr));
            return;
        }
        
        for (int i = start; i < arr.Length; i++)
        {
            (arr[start], arr[i]) = (arr[i], arr[start]);
            GeneratePermutations(arr, start + 1, result);
            (arr[start], arr[i]) = (arr[i], arr[start]);
        }
    }
}
```

### Space Complexity Analysis

```csharp
public class SpaceComplexityExamples
{
    // O(1) - Constant space
    // Only uses fixed amount of extra space
    public static int Sum(int[] arr)
    {
        int sum = 0;  // Single variable
        foreach (int num in arr)
            sum += num;
        return sum;
    }
    
    // O(n) - Linear space
    // Space grows with input size
    public static int[] CopyArray(int[] arr)
    {
        int[] copy = new int[arr.Length];  // New array of size n
        Array.Copy(arr, copy, arr.Length);
        return copy;
    }
    
    // O(n) - Linear space for recursion stack
    public static int Factorial(int n)
    {
        if (n <= 1) return 1;
        return n * Factorial(n - 1);  // n stack frames
    }
    
    // O(n²) - Quadratic space
    public static int[,] CreateMultiplicationTable(int n)
    {
        int[,] table = new int[n, n];  // n² elements
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                table[i, j] = (i + 1) * (j + 1);
        return table;
    }
}
```

### Amortized Analysis

```csharp
// Understanding amortized analysis through List<T>
public class AmortizedAnalysisExample
{
    // List.Add has O(1) amortized time complexity
    // Although individual Add operations may be O(n) when resizing,
    // the average cost across n operations is O(1)
    
    public static void DemonstrateAmortizedComplexity()
    {
        var list = new List<int>();
        
        // Initial capacity: 0
        // Add operations:
        // Add 1: Capacity doubles to 4 (cost: 1 for add + allocation)
        // Add 2: Cost 1
        // Add 3: Cost 1
        // Add 4: Cost 1
        // Add 5: Capacity doubles to 8 (cost: 1 for add + copy 4 elements)
        // ...
        
        // Total cost for n adds:
        // n (for n add operations) + 1 + 2 + 4 + 8 + ... + n
        // = n + (2n - 1) ≈ 3n
        // = O(n) for n operations
        // = O(1) amortized per operation
        
        for (int i = 0; i < 1_000_000; i++)
        {
            list.Add(i);  // Most are O(1), few are O(n)
        }
    }
}
```

---

## 3. Arrays in C#

An array is a collection of elements of the same type stored in contiguous memory locations. Arrays are the most fundamental data structure in programming, providing constant-time access to elements through index-based addressing. In C#, arrays are reference types that derive from the System.Array class, providing built-in methods for searching, sorting, and manipulation.

Arrays in C# can be single-dimensional, multi-dimensional, or jagged (arrays of arrays). The CLR guarantees that array access is bounds-checked, preventing buffer overflow vulnerabilities common in languages like C and C++. While this adds a small performance overhead, it provides memory safety that is crucial for building secure applications.

### Single-Dimensional Arrays

```csharp
public class ArrayExamples
{
    public static void SingleDimensionalArrays()
    {
        // Declaration and initialization
        int[] numbers1 = new int[5];                    // All zeros
        int[] numbers2 = new int[] { 1, 2, 3, 4, 5 };   // Initialized
        int[] numbers3 = { 1, 2, 3, 4, 5 };             // Shortcut syntax
        string[] names = new string[3];                  // All null
        
        // Accessing elements - O(1)
        int first = numbers2[0];   // 1
        int last = numbers2[4];    // 5
        
        // Modifying elements - O(1)
        numbers1[0] = 10;
        numbers1[1] = 20;
        
        // Common operations
        int length = numbers2.Length;           // 5
        int index = Array.IndexOf(numbers2, 3); // 2
        bool contains = numbers2.Contains(3);   // true
        
        // Iteration
        for (int i = 0; i < numbers2.Length; i++)
        {
            Console.WriteLine($"Index {i}: {numbers2[i]}");
        }
        
        foreach (int num in numbers2)
        {
            Console.WriteLine(num);
        }
    }
    
    // Common array algorithms
    public static int FindMax(int[] arr)
    {
        if (arr == null || arr.Length == 0)
            throw new ArgumentException("Array cannot be null or empty");
        
        int max = arr[0];
        for (int i = 1; i < arr.Length; i++)
        {
            if (arr[i] > max)
                max = arr[i];
        }
        return max;
    }
    
    public static int FindMin(int[] arr)
    {
        if (arr == null || arr.Length == 0)
            throw new ArgumentException("Array cannot be null or empty");
        
        int min = arr[0];
        for (int i = 1; i < arr.Length; i++)
        {
            if (arr[i] < min)
                min = arr[i];
        }
        return min;
    }
    
    public static int CalculateSum(int[] arr)
    {
        int sum = 0;
        foreach (int num in arr)
            sum += num;
        return sum;
    }
    
    public static double CalculateAverage(int[] arr)
    {
        return (double)CalculateSum(arr) / arr.Length;
    }
    
    // Reverse array in-place
    public static void Reverse(int[] arr)
    {
        int left = 0, right = arr.Length - 1;
        while (left < right)
        {
            (arr[left], arr[right]) = (arr[right], arr[left]);
            left++;
            right--;
        }
    }
    
    // Rotate array right by k positions
    public static void RotateRight(int[] arr, int k)
    {
        int n = arr.Length;
        k = k % n;  // Handle k > n
        
        // Three reversals technique
        Reverse(arr, 0, n - 1);
        Reverse(arr, 0, k - 1);
        Reverse(arr, k, n - 1);
    }
    
    private static void Reverse(int[] arr, int start, int end)
    {
        while (start < end)
        {
            (arr[start], arr[end]) = (arr[end], arr[start]);
            start++;
            end--;
        }
    }
    
    // Remove duplicates from sorted array
    public static int RemoveDuplicates(int[] nums)
    {
        if (nums.Length == 0) return 0;
        
        int writeIndex = 1;
        for (int readIndex = 1; readIndex < nums.Length; readIndex++)
        {
            if (nums[readIndex] != nums[readIndex - 1])
            {
                nums[writeIndex] = nums[readIndex];
                writeIndex++;
            }
        }
        
        return writeIndex;
    }
}
```

### Multi-Dimensional Arrays

```csharp
public class MultiDimensionalArrays
{
    public static void RectangularArrays()
    {
        // 2D array (rectangular)
        int[,] matrix = new int[3, 4];  // 3 rows, 4 columns
        
        // Initialization
        int[,] matrix2 = {
            { 1, 2, 3, 4 },
            { 5, 6, 7, 8 },
            { 9, 10, 11, 12 }
        };
        
        // Accessing elements
        int value = matrix2[1, 2];  // 7 (row 1, column 2)
        
        // Dimensions
        int rows = matrix2.GetLength(0);     // 3
        int cols = matrix2.GetLength(1);     // 4
        int total = matrix2.Length;           // 12
        
        // Iteration
        for (int i = 0; i < rows; i++)
        {
            for (int j = 0; j < cols; j++)
            {
                Console.Write($"{matrix2[i, j]} ");
            }
            Console.WriteLine();
        }
    }
    
    // Matrix operations
    public static int[,] AddMatrices(int[,] a, int[,] b)
    {
        int rows = a.GetLength(0);
        int cols = a.GetLength(1);
        int[,] result = new int[rows, cols];
        
        for (int i = 0; i < rows; i++)
        {
            for (int j = 0; j < cols; j++)
            {
                result[i, j] = a[i, j] + b[i, j];
            }
        }
        
        return result;
    }
    
    public static int[,] MultiplyMatrices(int[,] a, int[,] b)
    {
        int aRows = a.GetLength(0);
        int aCols = a.GetLength(1);
        int bCols = b.GetLength(1);
        
        int[,] result = new int[aRows, bCols];
        
        for (int i = 0; i < aRows; i++)
        {
            for (int j = 0; j < bCols; j++)
            {
                for (int k = 0; k < aCols; k++)
                {
                    result[i, j] += a[i, k] * b[k, j];
                }
            }
        }
        
        return result;
    }
    
    // Spiral traversal
    public static List<int> SpiralOrder(int[,] matrix)
    {
        var result = new List<int>();
        int rows = matrix.GetLength(0);
        int cols = matrix.GetLength(1);
        
        int top = 0, bottom = rows - 1, left = 0, right = cols - 1;
        
        while (top <= bottom && left <= right)
        {
            // Traverse right
            for (int i = left; i <= right; i++)
                result.Add(matrix[top, i]);
            top++;
            
            // Traverse down
            for (int i = top; i <= bottom; i++)
                result.Add(matrix[i, right]);
            right--;
            
            if (top <= bottom)
            {
                // Traverse left
                for (int i = right; i >= left; i--)
                    result.Add(matrix[bottom, i]);
                bottom--;
            }
            
            if (left <= right)
            {
                // Traverse up
                for (int i = bottom; i >= top; i--)
                    result.Add(matrix[i, left]);
                left++;
            }
        }
        
        return result;
    }
    
    public static void JaggedArrays()
    {
        // Jagged array - array of arrays
        int[][] jagged = new int[3][];
        
        jagged[0] = new int[] { 1, 2, 3 };
        jagged[1] = new int[] { 4, 5 };
        jagged[2] = new int[] { 6, 7, 8, 9 };
        
        // Accessing
        int value = jagged[1][1];  // 5
        
        // Iteration
        for (int i = 0; i < jagged.Length; i++)
        {
            for (int j = 0; j < jagged[i].Length; j++)
            {
                Console.Write($"{jagged[i][j]} ");
            }
            Console.WriteLine();
        }
    }
}
```

### Array Methods and Utilities

```csharp
public class ArrayUtilities
{
    public static void BuiltInMethods()
    {
        int[] arr = { 5, 2, 8, 1, 9, 3 };
        
        // Sorting - O(n log n)
        Array.Sort(arr);  // { 1, 2, 3, 5, 8, 9 }
        
        // Binary search - O(log n) - requires sorted array
        int index = Array.BinarySearch(arr, 5);  // 3
        
        // Find elements
        int firstEven = Array.Find(arr, x => x % 2 == 0);  // 2
        int[] allEven = Array.FindAll(arr, x => x % 2 == 0);  // { 2, 8 }
        int lastIndex = Array.FindLastIndex(arr, x => x < 5);  // 2
        
        // Check conditions
        bool anyGreaterThan5 = Array.Exists(arr, x => x > 5);  // true
        bool allPositive = Array.TrueForAll(arr, x => x > 0);  // true
        
        // Copy operations
        int[] copy = new int[arr.Length];
        Array.Copy(arr, copy, arr.Length);
        
        int[] cloned = (int[])arr.Clone();
        
        // Resize
        Array.Resize(ref arr, 10);  // Pads with zeros
        
        // Clear
        Array.Clear(arr, 0, arr.Length);  // Sets all to default
        
        // Convert
        string[] strArr = Array.ConvertAll(arr, x => x.ToString());
    }
    
    // Two-pointer technique
    public static bool TwoSum(int[] arr, int target)
    {
        int left = 0, right = arr.Length - 1;
        
        while (left < right)
        {
            int sum = arr[left] + arr[right];
            
            if (sum == target)
                return true;
            else if (sum < target)
                left++;
            else
                right--;
        }
        
        return false;
    }
    
    // Sliding window technique
    public static int MaxSubarraySum(int[] arr, int k)
    {
        int n = arr.Length;
        if (n < k) return -1;
        
        // Calculate sum of first window
        int maxSum = 0;
        for (int i = 0; i < k; i++)
            maxSum += arr[i];
        
        int windowSum = maxSum;
        
        // Slide the window
        for (int i = k; i < n; i++)
        {
            windowSum += arr[i] - arr[i - k];
            maxSum = Math.Max(maxSum, windowSum);
        }
        
        return maxSum;
    }
    
    // Prefix sum technique
    public static int[] BuildPrefixSum(int[] arr)
    {
        int[] prefix = new int[arr.Length + 1];
        prefix[0] = 0;
        
        for (int i = 0; i < arr.Length; i++)
        {
            prefix[i + 1] = prefix[i] + arr[i];
        }
        
        return prefix;
    }
    
    public static int RangeSum(int[] prefix, int left, int right)
    {
        return prefix[right + 1] - prefix[left];
    }
}
```

---

## 4. ArrayList and List<T>

The `List<T>` class in C# is a generic collection that provides dynamic array functionality. Unlike arrays, lists can grow and shrink in size dynamically, making them more flexible for scenarios where the number of elements is not known in advance. The non-generic `ArrayList` class exists for backward compatibility but should be avoided in favor of `List<T>` for type safety and better performance.

List<T> is implemented as a dynamic array that automatically resizes when elements are added. When the internal array reaches capacity, a new array with double the size is allocated, and elements are copied over. This gives List<T> an amortized O(1) time complexity for add operations, while maintaining O(1) access by index.

### List<T> Fundamentals

```csharp
public class ListExamples
{
    public static void BasicOperations()
    {
        // Creation
        List<int> list1 = new List<int>();
        List<int> list2 = new List<int>(100);  // Initial capacity
        List<int> list3 = new List<int> { 1, 2, 3, 4, 5 };
        
        // Add elements - O(1) amortized
        list1.Add(10);
        list1.AddRange(new[] { 20, 30, 40 });
        
        // Insert at index - O(n)
        list1.Insert(0, 5);  // Insert at beginning
        
        // Access - O(1)
        int first = list1[0];
        int last = list1[^1];  // C# 8.0 index from end
        
        // Count and Capacity
        int count = list1.Count;      // Number of elements
        int capacity = list1.Capacity; // Internal array size
        
        // Search - O(n)
        bool contains = list1.Contains(10);
        int index = list1.IndexOf(20);
        int lastIndex = list1.LastIndexOf(20);
        
        // Find methods
        int found = list1.Find(x => x > 15);  // First match
        int foundIndex = list1.FindIndex(x => x > 15);
        List<int> foundAll = list1.FindAll(x => x > 15);
        int foundLast = list1.FindLast(x => x > 15);
        
        // Check conditions
        bool any = list1.Any(x => x > 100);
        bool all = list1.All(x => x > 0);
        
        // Remove - O(n) for search, O(1) for last
        list1.Remove(10);     // Remove by value
        list1.RemoveAt(0);    // Remove by index
        list1.RemoveRange(0, 2);  // Remove range
        list1.RemoveAll(x => x > 50);  // Remove by predicate
        list1.Clear();  // Remove all
        
        // Trim excess capacity
        list1.TrimExcess();
    }
    
    public static void CommonPatterns()
    {
        List<int> numbers = Enumerable.Range(1, 100).ToList();
        
        // Sorting
        numbers.Sort();  // In-place sort
        numbers.Sort((a, b) => b.CompareTo(a));  // Descending
        
        // Using LINQ (creates new list)
        var sorted = numbers.OrderBy(x => x).ToList();
        var filtered = numbers.Where(x => x % 2 == 0).ToList();
        var transformed = numbers.Select(x => x * 2).ToList();
        
        // Binary search (list must be sorted)
        numbers.Sort();
        int index = numbers.BinarySearch(50);
        
        // Reverse
        numbers.Reverse();
        
        // Copy to array
        int[] arr = numbers.ToArray();
        
        // ForEach action
        numbers.ForEach(x => Console.WriteLine(x));
        
        // TrueForAll
        bool allPositive = numbers.TrueForAll(x => x > 0);
        
        // ConvertAll
        List<string> strings = numbers.ConvertAll(x => x.ToString());
    }
}
```

### Performance Considerations

```csharp
public class ListPerformance
{
    // Pre-allocate capacity when size is known
    public static void WithCapacity()
    {
        // Good: Pre-allocated
        var list = new List<int>(10000);
        for (int i = 0; i < 10000; i++)
        {
            list.Add(i);  // No reallocations
        }
    }
    
    public static void WithoutCapacity()
    {
        // Bad: Default capacity causes multiple reallocations
        var list = new List<int>();
        for (int i = 0; i < 10000; i++)
        {
            list.Add(i);  // Multiple reallocations as list grows
        }
    }
    
    // Remove from end when possible - O(1)
    public static void RemoveFromEnd(List<int> list)
    {
        list.RemoveAt(list.Count - 1);  // O(1)
    }
    
    // Remove from beginning - O(n)
    public static void RemoveFromBeginning(List<int> list)
    {
        list.RemoveAt(0);  // All elements must shift
    }
    
    // Use RemoveAt with last element swap for order-agnostic removal - O(1)
    public static void FastRemove(List<int> list, int index)
    {
        int lastIndex = list.Count - 1;
        list[index] = list[lastIndex];  // Move last to position
        list.RemoveAt(lastIndex);  // O(1) removal
    }
    
    // Range operations are more efficient than loops
    public static void AddRangeVsLoop()
    {
        var list = new List<int>();
        var items = Enumerable.Range(1, 1000);
        
        // Good: AddRange
        list.AddRange(items);
        
        // Bad: Loop
        var list2 = new List<int>();
        foreach (var item in items)
            list2.Add(item);
    }
}
```

### Common Algorithms with Lists

```csharp
public class ListAlgorithms
{
    // Merge two sorted lists
    public static List<int> MergeSorted(List<int> a, List<int> b)
    {
        var result = new List<int>(a.Count + b.Count);
        int i = 0, j = 0;
        
        while (i < a.Count && j < b.Count)
        {
            if (a[i] <= b[j])
                result.Add(a[i++]);
            else
                result.Add(b[j++]);
        }
        
        while (i < a.Count) result.Add(a[i++]);
        while (j < b.Count) result.Add(b[j++]);
        
        return result;
    }
    
    // Find intersection of two sorted lists
    public static List<int> Intersection(List<int> a, List<int> b)
    {
        var result = new List<int>();
        int i = 0, j = 0;
        
        while (i < a.Count && j < b.Count)
        {
            if (a[i] == b[j])
            {
                result.Add(a[i]);
                i++;
                j++;
            }
            else if (a[i] < b[j])
            {
                i++;
            }
            else
            {
                j++;
            }
        }
        
        return result;
    }
    
    // Kadane's algorithm - maximum subarray
    public static int MaxSubarraySum(List<int> nums)
    {
        if (nums.Count == 0) return 0;
        
        int maxSum = nums[0];
        int currentSum = nums[0];
        
        for (int i = 1; i < nums.Count; i++)
        {
            currentSum = Math.Max(nums[i], currentSum + nums[i]);
            maxSum = Math.Max(maxSum, currentSum);
        }
        
        return maxSum;
    }
    
    // Dutch National Flag - sort 0s, 1s, and 2s
    public static void SortColors(List<int> nums)
    {
        int low = 0, mid = 0, high = nums.Count - 1;
        
        while (mid <= high)
        {
            switch (nums[mid])
            {
                case 0:
                    (nums[low], nums[mid]) = (nums[mid], nums[low]);
                    low++;
                    mid++;
                    break;
                case 1:
                    mid++;
                    break;
                case 2:
                    (nums[mid], nums[high]) = (nums[high], nums[mid]);
                    high--;
                    break;
            }
        }
    }
}
```

---

## 5. Linked Lists

A linked list is a linear data structure where elements are stored in nodes, and each node points to the next node in the sequence. Unlike arrays, linked lists do not store elements in contiguous memory locations, which allows for efficient insertion and deletion operations but sacrifices random access capability. The .NET Framework provides a doubly linked list implementation via `LinkedList<T>`.

Linked lists are particularly useful when you need frequent insertions and deletions at arbitrary positions, as these operations can be performed in O(1) time when you have a reference to the position. However, accessing an element by index requires O(n) time since you must traverse from the beginning of the list.

### Singly Linked List Implementation

```csharp
public class Node<T>
{
    public T Data { get; set; }
    public Node<T>? Next { get; set; }
    
    public Node(T data)
    {
        Data = data;
        Next = null;
    }
}

public class SinglyLinkedList<T>
{
    public Node<T>? Head { get; private set; }
    public int Count { get; private set; }
    
    // Add at beginning - O(1)
    public void AddFirst(T data)
    {
        var newNode = new Node<T>(data)
        {
            Next = Head
        };
        Head = newNode;
        Count++;
    }
    
    // Add at end - O(n)
    public void AddLast(T data)
    {
        var newNode = new Node<T>(data);
        
        if (Head == null)
        {
            Head = newNode;
        }
        else
        {
            var current = Head;
            while (current.Next != null)
            {
                current = current.Next;
            }
            current.Next = newNode;
        }
        Count++;
    }
    
    // Add after a node - O(1) if node is given
    public void AddAfter(Node<T> node, T data)
    {
        var newNode = new Node<T>(data)
        {
            Next = node.Next
        };
        node.Next = newNode;
        Count++;
    }
    
    // Remove first - O(1)
    public void RemoveFirst()
    {
        if (Head == null) return;
        Head = Head.Next;
        Count--;
    }
    
    // Remove last - O(n)
    public void RemoveLast()
    {
        if (Head == null) return;
        
        if (Head.Next == null)
        {
            Head = null;
        }
        else
        {
            var current = Head;
            while (current.Next!.Next != null)
            {
                current = current.Next;
            }
            current.Next = null;
        }
        Count--;
    }
    
    // Find a node - O(n)
    public Node<T>? Find(T data)
    {
        var current = Head;
        while (current != null)
        {
            if (EqualityComparer<T>.Default.Equals(current.Data, data))
                return current;
            current = current.Next;
        }
        return null;
    }
    
    // Reverse the list - O(n)
    public void Reverse()
    {
        Node<T>? prev = null;
        var current = Head;
        
        while (current != null)
        {
            var next = current.Next;
            current.Next = prev;
            prev = current;
            current = next;
        }
        
        Head = prev;
    }
    
    // Detect cycle - Floyd's algorithm
    public bool HasCycle()
    {
        if (Head == null) return false;
        
        var slow = Head;
        var fast = Head;
        
        while (fast?.Next != null)
        {
            slow = slow!.Next;
            fast = fast.Next.Next;
            
            if (slow == fast)
                return true;
        }
        
        return false;
    }
    
    // Find middle node - O(n)
    public Node<T>? FindMiddle()
    {
        if (Head == null) return null;
        
        var slow = Head;
        var fast = Head;
        
        while (fast?.Next != null)
        {
            slow = slow!.Next;
            fast = fast.Next.Next;
        }
        
        return slow;
    }
    
    // Convert to enumerable
    public IEnumerable<T> ToEnumerable()
    {
        var current = Head;
        while (current != null)
        {
            yield return current.Data;
            current = current.Next;
        }
    }
}
```

### Doubly Linked List Implementation

```csharp
public class DoublyNode<T>
{
    public T Data { get; set; }
    public DoublyNode<T>? Prev { get; set; }
    public DoublyNode<T>? Next { get; set; }
    
    public DoublyNode(T data)
    {
        Data = data;
    }
}

public class DoublyLinkedList<T>
{
    public DoublyNode<T>? Head { get; private set; }
    public DoublyNode<T>? Tail { get; private set; }
    public int Count { get; private set; }
    
    // Add at beginning - O(1)
    public void AddFirst(T data)
    {
        var newNode = new DoublyNode<T>(data);
        
        if (Head == null)
        {
            Head = newNode;
            Tail = newNode;
        }
        else
        {
            newNode.Next = Head;
            Head.Prev = newNode;
            Head = newNode;
        }
        Count++;
    }
    
    // Add at end - O(1) with tail pointer
    public void AddLast(T data)
    {
        var newNode = new DoublyNode<T>(data);
        
        if (Tail == null)
        {
            Head = newNode;
            Tail = newNode;
        }
        else
        {
            newNode.Prev = Tail;
            Tail.Next = newNode;
            Tail = newNode;
        }
        Count++;
    }
    
    // Remove first - O(1)
    public void RemoveFirst()
    {
        if (Head == null) return;
        
        Head = Head.Next;
        if (Head != null)
            Head.Prev = null;
        else
            Tail = null;
        
        Count--;
    }
    
    // Remove last - O(1) with tail pointer
    public void RemoveLast()
    {
        if (Tail == null) return;
        
        Tail = Tail.Prev;
        if (Tail != null)
            Tail.Next = null;
        else
            Head = null;
        
        Count--;
    }
    
    // Remove specific node - O(1) if node is given
    public void Remove(DoublyNode<T> node)
    {
        if (node.Prev != null)
            node.Prev.Next = node.Next;
        else
            Head = node.Next;
        
        if (node.Next != null)
            node.Next.Prev = node.Prev;
        else
            Tail = node.Prev;
        
        Count--;
    }
    
    // Forward traversal
    public IEnumerable<T> Forward()
    {
        var current = Head;
        while (current != null)
        {
            yield return current.Data;
            current = current.Next;
        }
    }
    
    // Backward traversal
    public IEnumerable<T> Backward()
    {
        var current = Tail;
        while (current != null)
        {
            yield return current.Data;
            current = current.Prev;
        }
    }
}
```

### Using .NET LinkedList<T>

```csharp
public class DotNetLinkedList
{
    public static void DemonstrateLinkedList()
    {
        var list = new LinkedList<string>();
        
        // Add operations
        var first = list.AddFirst("First");
        var last = list.AddLast("Last");
        list.AddAfter(first, "After First");
        list.AddBefore(last, "Before Last");
        
        // List: First -> After First -> Before Last -> Last
        
        // Access
        string firstValue = list.First!.Value;
        string lastValue = list.Last!.Value;
        
        // Find
        LinkedListNode<string>? node = list.Find("After First");
        LinkedListNode<string>? lastFound = list.FindLast("Last");
        
        // Navigate
        LinkedListNode<string>? next = node?.Next;
        LinkedListNode<string>? prev = node?.Previous;
        
        // Remove
        list.Remove("After First");
        list.RemoveFirst();
        list.RemoveLast();
        
        // Properties
        int count = list.Count;
        bool contains = list.Contains("Last");
        
        // Clear
        list.Clear();
    }
    
    // LinkedList is ideal for queue/deque implementations
    public class Deque<T>
    {
        private readonly LinkedList<T> _items = new();
        
        public int Count => _items.Count;
        
        public void AddFront(T item) => _items.AddFirst(item);
        public void AddBack(T item) => _items.AddLast(item);
        public T RemoveFront()
        {
            if (_items.Count == 0) throw new InvalidOperationException("Deque is empty");
            var value = _items.First!.Value;
            _items.RemoveFirst();
            return value;
        }
        public T RemoveBack()
        {
            if (_items.Count == 0) throw new InvalidOperationException("Deque is empty");
            var value = _items.Last!.Value;
            _items.RemoveLast();
            return value;
        }
        public T PeekFront() => _items.First!.Value;
        public T PeekBack() => _items.Last!.Value;
    }
}
```

### Common Linked List Algorithms

```csharp
public class LinkedListAlgorithms
{
    // Merge two sorted lists
    public static Node<int>? MergeSorted(Node<int>? l1, Node<int>? l2)
    {
        var dummy = new Node<int>(0);
        var current = dummy;
        
        while (l1 != null && l2 != null)
        {
            if (l1.Data <= l2.Data)
            {
                current.Next = l1;
                l1 = l1.Next;
            }
            else
            {
                current.Next = l2;
                l2 = l2.Next;
            }
            current = current.Next!;
        }
        
        current.Next = l1 ?? l2;
        
        return dummy.Next;
    }
    
    // Remove nth node from end
    public static Node<int>? RemoveNthFromEnd(Node<int>? head, int n)
    {
        var dummy = new Node<int>(0) { Next = head };
        var fast = dummy;
        var slow = dummy;
        
        // Move fast n+1 steps ahead
        for (int i = 0; i <= n; i++)
        {
            fast = fast!.Next;
        }
        
        // Move both until fast reaches end
        while (fast != null)
        {
            fast = fast.Next;
            slow = slow!.Next;
        }
        
        // Remove the node
        slow!.Next = slow.Next!.Next;
        
        return dummy.Next;
    }
    
    // Find intersection of two lists
    public static Node<int>? GetIntersection(Node<int>? headA, Node<int>? headB)
    {
        if (headA == null || headB == null) return null;
        
        var a = headA;
        var b = headB;
        
        // When a reaches end, start from headB
        // When b reaches end, start from headA
        // They will meet at intersection or both null
        while (a != b)
        {
            a = a == null ? headB : a.Next;
            b = b == null ? headA : b.Next;
        }
        
        return a;
    }
    
    // Check if palindrome
    public static bool IsPalindrome(Node<int>? head)
    {
        if (head == null || head.Next == null) return true;
        
        // Find middle
        var slow = head;
        var fast = head;
        while (fast?.Next != null)
        {
            slow = slow!.Next;
            fast = fast.Next.Next;
        }
        
        // Reverse second half
        Node<int>? prev = null;
        var current = slow;
        while (current != null)
        {
            var next = current.Next;
            current.Next = prev;
            prev = current;
            current = next;
        }
        
        // Compare halves
        var left = head;
        var right = prev;
        while (right != null)
        {
            if (left!.Data != right.Data) return false;
            left = left.Next;
            right = right.Next;
        }
        
        return true;
    }
    
    // Rotate list right by k
    public static Node<int>? RotateRight(Node<int>? head, int k)
    {
        if (head == null || head.Next == null || k == 0) return head;
        
        // Count nodes
        int count = 1;
        var tail = head;
        while (tail.Next != null)
        {
            tail = tail.Next;
            count++;
        }
        
        // Make it circular
        tail.Next = head;
        
        // Find new tail
        k = k % count;
        int stepsToNewTail = count - k;
        var newTail = head;
        
        for (int i = 1; i < stepsToNewTail; i++)
        {
            newTail = newTail!.Next;
        }
        
        var newHead = newTail!.Next;
        newTail.Next = null;
        
        return newHead;
    }
}
```

---

## 6. Stacks

A stack is a linear data structure that follows the Last-In-First-Out (LIFO) principle, meaning the last element added is the first one to be removed. This behavior is analogous to a stack of plates where you can only add or remove plates from the top. Stacks are fundamental data structures used in many algorithms and applications, including expression evaluation, backtracking, function call management, and undo operations.

The .NET Framework provides a generic `Stack<T>` class that implements a stack using a dynamic array. The main operations are Push (add to top), Pop (remove from top), and Peek (view top without removing). All these operations are O(1) in the average case, making stacks very efficient for their intended use cases.

### Stack Implementation

```csharp
public class CustomStack<T>
{
    private T[] _items;
    private int _count;
    private const int DefaultCapacity = 4;
    
    public CustomStack()
    {
        _items = new T[DefaultCapacity];
        _count = 0;
    }
    
    public int Count => _count;
    public bool IsEmpty => _count == 0;
    
    // Push - O(1) amortized
    public void Push(T item)
    {
        if (_count == _items.Length)
        {
            Array.Resize(ref _items, _items.Length * 2);
        }
        _items[_count++] = item;
    }
    
    // Pop - O(1)
    public T Pop()
    {
        if (_count == 0)
            throw new InvalidOperationException("Stack is empty");
        
        T item = _items[--_count];
        _items[_count] = default!;  // Clear reference
        return item;
    }
    
    // Peek - O(1)
    public T Peek()
    {
        if (_count == 0)
            throw new InvalidOperationException("Stack is empty");
        
        return _items[_count - 1];
    }
    
    // TryPop - safe version
    public bool TryPop(out T? item)
    {
        if (_count == 0)
        {
            item = default;
            return false;
        }
        
        item = _items[--_count];
        _items[_count] = default!;
        return true;
    }
    
    // Clear - O(n)
    public void Clear()
    {
        Array.Clear(_items, 0, _count);
        _count = 0;
    }
    
    // Contains - O(n)
    public bool Contains(T item)
    {
        for (int i = 0; i < _count; i++)
        {
            if (EqualityComparer<T>.Default.Equals(_items[i], item))
                return true;
        }
        return false;
    }
    
    // ToArray - O(n)
    public T[] ToArray()
    {
        T[] result = new T[_count];
        for (int i = 0; i < _count; i++)
        {
            result[i] = _items[_count - 1 - i];  // Reverse order
        }
        return result;
    }
}
```

### Using .NET Stack<T>

```csharp
public class StackExamples
{
    public static void BasicOperations()
    {
        var stack = new Stack<int>();
        
        // Push - add to top
        stack.Push(1);
        stack.Push(2);
        stack.Push(3);
        // Stack: [1, 2, 3] (3 is on top)
        
        // Peek - view top
        int top = stack.Peek();  // 3
        
        // Pop - remove and return top
        int popped = stack.Pop();  // 3
        // Stack: [1, 2]
        
        // Count
        int count = stack.Count;  // 2
        
        // Contains
        bool contains = stack.Contains(1);  // true
        
        // ToArray
        int[] arr = stack.ToArray();  // [2, 1]
        
        // Clear
        stack.Clear();
    }
    
    // Valid parentheses problem
    public static bool IsValidParentheses(string s)
    {
        var stack = new Stack<char>();
        var pairs = new Dictionary<char, char>
        {
            { ')', '(' },
            { ']', '[' },
            { '}', '{' }
        };
        
        foreach (char c in s)
        {
            if (pairs.ContainsValue(c))  // Opening bracket
            {
                stack.Push(c);
            }
            else if (pairs.ContainsKey(c))  // Closing bracket
            {
                if (stack.Count == 0 || stack.Pop() != pairs[c])
                    return false;
            }
        }
        
        return stack.Count == 0;
    }
    
    // Evaluate Reverse Polish Notation (RPN)
    public static int EvalRPN(string[] tokens)
    {
        var stack = new Stack<int>();
        
        foreach (var token in tokens)
        {
            if (int.TryParse(token, out int num))
            {
                stack.Push(num);
            }
            else
            {
                int b = stack.Pop();
                int a = stack.Pop();
                
                int result = token switch
                {
                    "+" => a + b,
                    "-" => a - b,
                    "*" => a * b,
                    "/" => a / b,
                    _ => throw new ArgumentException($"Unknown operator: {token}")
                };
                
                stack.Push(result);
            }
        }
        
        return stack.Pop();
    }
    
    // Next Greater Element
    public static int[] NextGreaterElement(int[] nums)
    {
        int n = nums.Length;
        int[] result = new int[n];
        Array.Fill(result, -1);
        
        var stack = new Stack<int>();  // Store indices
        
        for (int i = 0; i < n; i++)
        {
            while (stack.Count > 0 && nums[stack.Peek()] < nums[i])
            {
                result[stack.Pop()] = nums[i];
            }
            stack.Push(i);
        }
        
        return result;
    }
    
    // Daily Temperatures problem
    public static int[] DailyTemperatures(int[] temperatures)
    {
        int n = temperatures.Length;
        int[] result = new int[n];
        var stack = new Stack<int>();  // Store indices
        
        for (int i = 0; i < n; i++)
        {
            while (stack.Count > 0 && temperatures[stack.Peek()] < temperatures[i])
            {
                int prevIndex = stack.Pop();
                result[prevIndex] = i - prevIndex;
            }
            stack.Push(i);
        }
        
        return result;
    }
    
    // Min Stack implementation
    public class MinStack
    {
        private readonly Stack<int> _mainStack = new();
        private readonly Stack<int> _minStack = new();
        
        public void Push(int val)
        {
            _mainStack.Push(val);
            
            int min = _minStack.Count == 0 ? val : Math.Min(_minStack.Peek(), val);
            _minStack.Push(min);
        }
        
        public void Pop()
        {
            _mainStack.Pop();
            _minStack.Pop();
        }
        
        public int Top() => _mainStack.Peek();
        
        public int GetMin() => _minStack.Peek();
    }
}
```

### Stack Applications

```csharp
public class StackApplications
{
    // Evaluate arithmetic expression
    public static int EvaluateExpression(string expression)
    {
        var values = new Stack<int>();
        var operators = new Stack<char>();
        
        for (int i = 0; i < expression.Length; i++)
        {
            char c = expression[i];
            
            if (char.IsDigit(c))
            {
                int num = 0;
                while (i < expression.Length && char.IsDigit(expression[i]))
                {
                    num = num * 10 + (expression[i] - '0');
                    i++;
                }
                values.Push(num);
                i--;
            }
            else if (c == '(')
            {
                operators.Push(c);
            }
            else if (c == ')')
            {
                while (operators.Peek() != '(')
                {
                    values.Push(ApplyOperator(operators.Pop(), values.Pop(), values.Pop()));
                }
                operators.Pop();  // Remove '('
            }
            else if (IsOperator(c))
            {
                while (operators.Count > 0 && Precedence(operators.Peek()) >= Precedence(c))
                {
                    values.Push(ApplyOperator(operators.Pop(), values.Pop(), values.Pop()));
                }
                operators.Push(c);
            }
        }
        
        while (operators.Count > 0)
        {
            values.Push(ApplyOperator(operators.Pop(), values.Pop(), values.Pop()));
        }
        
        return values.Pop();
    }
    
    private static bool IsOperator(char c) => c == '+' || c == '-' || c == '*' || c == '/';
    
    private static int Precedence(char op) => op switch
    {
        '+' or '-' => 1,
        '*' or '/' => 2,
        _ => 0
    };
    
    private static int ApplyOperator(char op, int b, int a) => op switch
    {
        '+' => a + b,
        '-' => a - b,
        '*' => a * b,
        '/' => a / b,
        _ => throw new ArgumentException()
    };
    
    // Convert infix to postfix
    public static string InfixToPostfix(string infix)
    {
        var result = new StringBuilder();
        var stack = new Stack<char>();
        
        foreach (char c in infix)
        {
            if (char.IsLetterOrDigit(c))
            {
                result.Append(c);
            }
            else if (c == '(')
            {
                stack.Push(c);
            }
            else if (c == ')')
            {
                while (stack.Count > 0 && stack.Peek() != '(')
                {
                    result.Append(stack.Pop());
                }
                stack.Pop();  // Remove '('
            }
            else if (IsOperator(c))
            {
                while (stack.Count > 0 && Precedence(stack.Peek()) >= Precedence(c))
                {
                    result.Append(stack.Pop());
                }
                stack.Push(c);
            }
        }
        
        while (stack.Count > 0)
        {
            result.Append(stack.Pop());
        }
        
        return result.ToString();
    }
    
    // DFS using stack
    public static void DFS_Iterative(Graph graph, int start)
    {
        var visited = new HashSet<int>();
        var stack = new Stack<int>();
        
        stack.Push(start);
        
        while (stack.Count > 0)
        {
            int vertex = stack.Pop();
            
            if (visited.Add(vertex))
            {
                Console.WriteLine($"Visited: {vertex}");
                
                foreach (var neighbor in graph.GetNeighbors(vertex))
                {
                    if (!visited.Contains(neighbor))
                    {
                        stack.Push(neighbor);
                    }
                }
            }
        }
    }
}
```

---

## 7. Queues

A queue is a linear data structure that follows the First-In-First-Out (FIFO) principle, meaning the first element added is the first one to be removed. This behavior is analogous to a line of people waiting at a store where the first person to arrive is the first to be served. Queues are essential for many computing applications, including task scheduling, breadth-first search, message processing, and managing requests in web servers.

The .NET Framework provides a generic `Queue<T>` class that implements a circular buffer for efficient operations. The main operations are Enqueue (add to back), Dequeue (remove from front), and Peek (view front without removing). All these operations are O(1), making queues very efficient for their intended use cases.

### Queue Implementation

```csharp
public class CustomQueue<T>
{
    private T[] _items;
    private int _head;  // Index of first element
    private int _tail;  // Index where next element will be added
    private int _count;
    private const int DefaultCapacity = 4;
    
    public CustomQueue()
    {
        _items = new T[DefaultCapacity];
        _head = 0;
        _tail = 0;
        _count = 0;
    }
    
    public int Count => _count;
    public bool IsEmpty => _count == 0;
    
    // Enqueue - O(1) amortized
    public void Enqueue(T item)
    {
        if (_count == _items.Length)
        {
            Resize();
        }
        
        _items[_tail] = item;
        _tail = (_tail + 1) % _items.Length;  // Circular buffer
        _count++;
    }
    
    // Dequeue - O(1)
    public T Dequeue()
    {
        if (_count == 0)
            throw new InvalidOperationException("Queue is empty");
        
        T item = _items[_head];
        _items[_head] = default!;
        _head = (_head + 1) % _items.Length;
        _count--;
        return item;
    }
    
    // Peek - O(1)
    public T Peek()
    {
        if (_count == 0)
            throw new InvalidOperationException("Queue is empty");
        
        return _items[_head];
    }
    
    // TryDequeue - safe version
    public bool TryDequeue(out T? item)
    {
        if (_count == 0)
        {
            item = default;
            return false;
        }
        
        item = _items[_head];
        _items[_head] = default!;
        _head = (_head + 1) % _items.Length;
        _count--;
        return true;
    }
    
    private void Resize()
    {
        T[] newItems = new T[_items.Length * 2];
        
        if (_head < _tail)
        {
            Array.Copy(_items, _head, newItems, 0, _count);
        }
        else
        {
            // Handle wrap-around
            Array.Copy(_items, _head, newItems, 0, _items.Length - _head);
            Array.Copy(_items, 0, newItems, _items.Length - _head, _tail);
        }
        
        _items = newItems;
        _head = 0;
        _tail = _count;
    }
    
    public void Clear()
    {
        Array.Clear(_items, 0, _items.Length);
        _head = 0;
        _tail = 0;
        _count = 0;
    }
}
```

### Using .NET Queue<T>

```csharp
public class QueueExamples
{
    public static void BasicOperations()
    {
        var queue = new Queue<string>();
        
        // Enqueue - add to back
        queue.Enqueue("First");
        queue.Enqueue("Second");
        queue.Enqueue("Third");
        // Queue: [First, Second, Third]
        
        // Peek - view front
        string front = queue.Peek();  // "First"
        
        // Dequeue - remove from front
        string dequeued = queue.Dequeue();  // "First"
        // Queue: [Second, Third]
        
        // Count
        int count = queue.Count;  // 2
        
        // Contains
        bool contains = queue.Contains("Second");  // true
        
        // ToArray
        string[] arr = queue.ToArray();  // ["Second", "Third"]
        
        // Clear
        queue.Clear();
    }
    
    // BFS using queue
    public static void BFS(Graph graph, int start)
    {
        var visited = new HashSet<int>();
        var queue = new Queue<int>();
        
        queue.Enqueue(start);
        visited.Add(start);
        
        while (queue.Count > 0)
        {
            int vertex = queue.Dequeue();
            Console.WriteLine($"Visited: {vertex}");
            
            foreach (var neighbor in graph.GetNeighbors(vertex))
            {
                if (visited.Add(neighbor))
                {
                    queue.Enqueue(neighbor);
                }
            }
        }
    }
    
    // Level order traversal of binary tree
    public static List<List<int>> LevelOrder(TreeNode? root)
    {
        var result = new List<List<int>>();
        
        if (root == null) return result;
        
        var queue = new Queue<TreeNode>();
        queue.Enqueue(root);
        
        while (queue.Count > 0)
        {
            int levelSize = queue.Count;
            var currentLevel = new List<int>();
            
            for (int i = 0; i < levelSize; i++)
            {
                var node = queue.Dequeue();
                currentLevel.Add(node.Val);
                
                if (node.Left != null)
                    queue.Enqueue(node.Left);
                
                if (node.Right != null)
                    queue.Enqueue(node.Right);
            }
            
            result.Add(currentLevel);
        }
        
        return result;
    }
    
    // Shortest path in grid using BFS
    public static int ShortestPath(int[][] grid, int[] start, int[] end)
    {
        int rows = grid.Length;
        int cols = grid[0].Length;
        
        var visited = new bool[rows, cols];
        var queue = new Queue<(int row, int col, int distance)>();
        
        int[][] directions = { new[] { 0, 1 }, new[] { 1, 0 }, new[] { 0, -1 }, new[] { -1, 0 } };
        
        queue.Enqueue((start[0], start[1], 0));
        visited[start[0], start[1]] = true;
        
        while (queue.Count > 0)
        {
            var (row, col, dist) = queue.Dequeue();
            
            if (row == end[0] && col == end[1])
                return dist;
            
            foreach (var dir in directions)
            {
                int newRow = row + dir[0];
                int newCol = col + dir[1];
                
                if (newRow >= 0 && newRow < rows &&
                    newCol >= 0 && newCol < cols &&
                    !visited[newRow, newCol] &&
                    grid[newRow][newCol] == 0)
                {
                    visited[newRow, newCol] = true;
                    queue.Enqueue((newRow, newCol, dist + 1));
                }
            }
        }
        
        return -1;  // No path found
    }
}
```

### Priority Queue Implementation

```csharp
// Priority Queue using heap (min-heap by default)
public class PriorityQueue<T> where T : IComparable<T>
{
    private readonly List<T> _heap;
    
    public PriorityQueue()
    {
        _heap = new List<T>();
    }
    
    public int Count => _heap.Count;
    public bool IsEmpty => _heap.Count == 0;
    
    // Enqueue - O(log n)
    public void Enqueue(T item)
    {
        _heap.Add(item);
        HeapifyUp(_heap.Count - 1);
    }
    
    // Dequeue - O(log n)
    public T Dequeue()
    {
        if (_heap.Count == 0)
            throw new InvalidOperationException("Priority queue is empty");
        
        T result = _heap[0];
        int lastIndex = _heap.Count - 1;
        
        _heap[0] = _heap[lastIndex];
        _heap.RemoveAt(lastIndex);
        
        if (_heap.Count > 0)
        {
            HeapifyDown(0);
        }
        
        return result;
    }
    
    // Peek - O(1)
    public T Peek()
    {
        if (_heap.Count == 0)
            throw new InvalidOperationException("Priority queue is empty");
        
        return _heap[0];
    }
    
    private void HeapifyUp(int index)
    {
        while (index > 0)
        {
            int parentIndex = (index - 1) / 2;
            
            if (_heap[index].CompareTo(_heap[parentIndex]) >= 0)
                break;
            
            (_heap[index], _heap[parentIndex]) = (_heap[parentIndex], _heap[index]);
            index = parentIndex;
        }
    }
    
    private void HeapifyDown(int index)
    {
        int count = _heap.Count;
        
        while (true)
        {
            int smallest = index;
            int left = 2 * index + 1;
            int right = 2 * index + 2;
            
            if (left < count && _heap[left].CompareTo(_heap[smallest]) < 0)
                smallest = left;
            
            if (right < count && _heap[right].CompareTo(_heap[smallest]) < 0)
                smallest = right;
            
            if (smallest == index)
                break;
            
            (_heap[index], _heap[smallest]) = (_heap[smallest], _heap[index]);
            index = smallest;
        }
    }
}

// Using .NET PriorityQueue (available from .NET 6)
public class DotNetPriorityQueueExamples
{
    public static void BasicUsage()
    {
        // Min-heap by default
        var pq = new PriorityQueue<string, int>();
        
        pq.Enqueue("Low priority", 3);
        pq.Enqueue("High priority", 1);
        pq.Enqueue("Medium priority", 2);
        
        // Dequeue returns highest priority (lowest number) first
        while (pq.Count > 0)
        {
            pq.TryDequeue(out string? item, out int priority);
            Console.WriteLine($"{item} (priority: {priority})");
        }
        // Output:
        // High priority (priority: 1)
        // Medium priority (priority: 2)
        // Low priority (priority: 3)
    }
    
    // Dijkstra's shortest path
    public static int[] Dijkstra(List<(int node, int weight)>[] graph, int start)
    {
        int n = graph.Length;
        int[] distances = new int[n];
        Array.Fill(distances, int.MaxValue);
        distances[start] = 0;
        
        var pq = new PriorityQueue<int, int>();
        pq.Enqueue(start, 0);
        
        while (pq.Count > 0)
        {
            pq.TryDequeue(out int node, out int dist);
            
            if (dist > distances[node])
                continue;
            
            foreach (var (neighbor, weight) in graph[node])
            {
                int newDist = distances[node] + weight;
                
                if (newDist < distances[neighbor])
                {
                    distances[neighbor] = newDist;
                    pq.Enqueue(neighbor, newDist);
                }
            }
        }
        
        return distances;
    }
}
```

### Deque (Double-Ended Queue)

```csharp
public class Deque<T>
{
    private readonly LinkedList<T> _items = new();
    
    public int Count => _items.Count;
    public bool IsEmpty => _items.Count == 0;
    
    // Add to front - O(1)
    public void AddFirst(T item) => _items.AddFirst(item);
    
    // Add to back - O(1)
    public void AddLast(T item) => _items.AddLast(item);
    
    // Remove from front - O(1)
    public T RemoveFirst()
    {
        if (_items.Count == 0)
            throw new InvalidOperationException("Deque is empty");
        
        var value = _items.First!.Value;
        _items.RemoveFirst();
        return value;
    }
    
    // Remove from back - O(1)
    public T RemoveLast()
    {
        if (_items.Count == 0)
            throw new InvalidOperationException("Deque is empty");
        
        var value = _items.Last!.Value;
        _items.RemoveLast();
        return value;
    }
    
    // Peek front - O(1)
    public T PeekFirst()
    {
        if (_items.Count == 0)
            throw new InvalidOperationException("Deque is empty");
        return _items.First!.Value;
    }
    
    // Peek back - O(1)
    public T PeekLast()
    {
        if (_items.Count == 0)
            throw new InvalidOperationException("Deque is empty");
        return _items.Last!.Value;
    }
}

// Sliding window maximum using deque
public class SlidingWindowMaximum
{
    public static int[] MaxSlidingWindow(int[] nums, int k)
    {
        if (nums.Length == 0 || k == 0) return Array.Empty<int>();
        
        var result = new List<int>();
        var deque = new LinkedList<int>();  // Store indices
        
        for (int i = 0; i < nums.Length; i++)
        {
            // Remove indices outside the window
            while (deque.Count > 0 && deque.First!.Value < i - k + 1)
            {
                deque.RemoveFirst();
            }
            
            // Remove indices of smaller elements
            while (deque.Count > 0 && nums[deque.Last!.Value] < nums[i])
            {
                deque.RemoveLast();
            }
            
            deque.AddLast(i);
            
            // Add maximum to result when window is full
            if (i >= k - 1)
            {
                result.Add(nums[deque.First!.Value]);
            }
        }
        
        return result.ToArray();
    }
}
```

---

## 8. Dictionaries and Hash Tables

A dictionary (also called a hash map or associative array) is a data structure that stores key-value pairs and provides fast lookup, insertion, and deletion operations. Dictionaries use a hash function to compute an index into an array of buckets, from which the desired value can be found. In C#, the primary dictionary implementation is `Dictionary<TKey, TValue>`, which provides O(1) average-case time complexity for lookups, insertions, and deletions.

The hash table's efficiency comes from its ability to directly compute where a value should be stored based on its key, rather than searching through a collection. However, hash collisions can occur when different keys hash to the same index. The Dictionary class handles collisions using chaining (linked lists at each bucket) and automatically resizes when the load factor exceeds a threshold.

### Dictionary Implementation

```csharp
public class CustomDictionary<TKey, TValue> where TKey : notnull
{
    private class Entry
    {
        public TKey Key { get; set; } = default!;
        public TValue Value { get; set; } = default!;
        public Entry? Next { get; set; }
    }
    
    private Entry[] _buckets;
    private int _count;
    private const double LoadFactor = 0.75;
    
    public CustomDictionary(int capacity = 16)
    {
        _buckets = new Entry[capacity];
        _count = 0;
    }
    
    public int Count => _count;
    
    // Add or update - O(1) average
    public void Add(TKey key, TValue value)
    {
        if (_count >= _buckets.Length * LoadFactor)
        {
            Resize();
        }
        
        int index = GetBucketIndex(key);
        Entry? current = _buckets[index];
        
        // Check if key exists
        while (current != null)
        {
            if (EqualityComparer<TKey>.Default.Equals(current.Key, key))
            {
                current.Value = value;  // Update existing
                return;
            }
            current = current.Next;
        }
        
        // Add new entry at head of chain
        var newEntry = new Entry { Key = key, Value = value, Next = _buckets[index] };
        _buckets[index] = newEntry;
        _count++;
    }
    
    // Get value - O(1) average
    public TValue this[TKey key]
    {
        get
        {
            if (TryGetValue(key, out TValue? value))
                return value;
            throw new KeyNotFoundException($"Key not found: {key}");
        }
        set => Add(key, value);
    }
    
    // TryGetValue - O(1) average
    public bool TryGetValue(TKey key, out TValue? value)
    {
        int index = GetBucketIndex(key);
        Entry? current = _buckets[index];
        
        while (current != null)
        {
            if (EqualityComparer<TKey>.Default.Equals(current.Key, key))
            {
                value = current.Value;
                return true;
            }
            current = current.Next;
        }
        
        value = default;
        return false;
    }
    
    // Remove - O(1) average
    public bool Remove(TKey key)
    {
        int index = GetBucketIndex(key);
        Entry? current = _buckets[index];
        Entry? prev = null;
        
        while (current != null)
        {
            if (EqualityComparer<TKey>.Default.Equals(current.Key, key))
            {
                if (prev == null)
                    _buckets[index] = current.Next;
                else
                    prev.Next = current.Next;
                
                _count--;
                return true;
            }
            prev = current;
            current = current.Next;
        }
        
        return false;
    }
    
    // Contains key - O(1) average
    public bool ContainsKey(TKey key)
    {
        return TryGetValue(key, out _);
    }
    
    private int GetBucketIndex(TKey key)
    {
        int hash = key.GetHashCode();
        return Math.Abs(hash) % _buckets.Length;
    }
    
    private void Resize()
    {
        var oldBuckets = _buckets;
        _buckets = new Entry[oldBuckets.Length * 2];
        _count = 0;
        
        foreach (var bucket in oldBuckets)
        {
            var current = bucket;
            while (current != null)
            {
                Add(current.Key, current.Value);
                current = current.Next;
            }
        }
    }
    
    // Get all keys
    public IEnumerable<TKey> Keys
    {
        get
        {
            foreach (var bucket in _buckets)
            {
                var current = bucket;
                while (current != null)
                {
                    yield return current.Key;
                    current = current.Next;
                }
            }
        }
    }
    
    // Get all values
    public IEnumerable<TValue> Values
    {
        get
        {
            foreach (var bucket in _buckets)
            {
                var current = bucket;
                while (current != null)
                {
                    yield return current.Value;
                    current = current.Next;
                }
            }
        }
    }
}
```

### Using .NET Dictionary<TKey, TValue>

```csharp
public class DictionaryExamples
{
    public static void BasicOperations()
    {
        // Creation
        var dict = new Dictionary<string, int>();
        var dictWithCapacity = new Dictionary<string, int>(100);
        var dictWithComparer = new Dictionary<string, int>(StringComparer.OrdinalIgnoreCase);
        
        // Add
        dict.Add("one", 1);
        dict.Add("two", 2);
        
        // Indexer (add or update)
        dict["three"] = 3;
        dict["one"] = 10;  // Update
        
        // Access
        int value = dict["one"];  // 10
        
        // Safe access
        if (dict.TryGetValue("two", out int foundValue))
        {
            Console.WriteLine($"Found: {foundValue}");
        }
        
        // Check existence
        bool hasKey = dict.ContainsKey("one");      // true
        bool hasValue = dict.ContainsValue(2);      // true
        
        // Remove
        bool removed = dict.Remove("one");
        
        // Count
        int count = dict.Count;
        
        // Iterate
        foreach (var kvp in dict)
        {
            Console.WriteLine($"{kvp.Key}: {kvp.Value}");
        }
        
        // Keys and Values
        var keys = dict.Keys;
        var values = dict.Values;
        
        // Clear
        dict.Clear();
    }
    
    // Two Sum problem
    public static int[] TwoSum(int[] nums, int target)
    {
        var map = new Dictionary<int, int>();
        
        for (int i = 0; i < nums.Length; i++)
        {
            int complement = target - nums[i];
            
            if (map.TryGetValue(complement, out int index))
            {
                return new[] { index, i };
            }
            
            map[nums[i]] = i;
        }
        
        return Array.Empty<int>();
    }
    
    // Group Anagrams
    public static List<List<string>> GroupAnagrams(string[] strs)
    {
        var groups = new Dictionary<string, List<string>>();
        
        foreach (var str in strs)
        {
            var charArray = str.ToCharArray();
            Array.Sort(charArray);
            var key = new string(charArray);
            
            if (!groups.ContainsKey(key))
            {
                groups[key] = new List<string>();
            }
            groups[key].Add(str);
        }
        
        return groups.Values.ToList();
    }
    
    // LRU Cache implementation
    public class LRUCache
    {
        private readonly int _capacity;
        private readonly Dictionary<int, LinkedListNode<CacheItem>> _cache;
        private readonly LinkedList<CacheItem> _lruList;
        
        public LRUCache(int capacity)
        {
            _capacity = capacity;
            _cache = new Dictionary<int, LinkedListNode<CacheItem>>();
            _lruList = new LinkedList<CacheItem>();
        }
        
        public int Get(int key)
        {
            if (!_cache.TryGetValue(key, out var node))
                return -1;
            
            // Move to front (most recently used)
            _lruList.Remove(node);
            _lruList.AddFirst(node);
            
            return node.Value.Value;
        }
        
        public void Put(int key, int value)
        {
            if (_cache.TryGetValue(key, out var node))
            {
                // Update existing
                node.Value.Value = value;
                _lruList.Remove(node);
                _lruList.AddFirst(node);
            }
            else
            {
                // Add new
                if (_cache.Count >= _capacity)
                {
                    // Remove least recently used
                    var lru = _lruList.Last!;
                    _lruList.RemoveLast();
                    _cache.Remove(lru.Value.Key);
                }
                
                var newNode = _lruList.AddFirst(new CacheItem { Key = key, Value = value });
                _cache[key] = newNode;
            }
        }
        
        private class CacheItem
        {
            public int Key { get; set; }
            public int Value { get; set; }
        }
    }
}
```

### Other Dictionary Types in .NET

```csharp
public class DictionaryTypes
{
    // ConcurrentDictionary - thread-safe dictionary
    public static void ConcurrentDictionaryExample()
    {
        var dict = new ConcurrentDictionary<string, int>();
        
        // Thread-safe operations
        dict.TryAdd("key", 1);
        dict.AddOrUpdate("key", 1, (k, v) => v + 1);
        dict.GetOrAdd("newKey", k => 42);
        
        int value = dict.GetOrAdd("key", 0);
        bool removed = dict.TryRemove("key", out int removedValue);
    }
    
    // SortedDictionary - maintains sorted order
    public static void SortedDictionaryExample()
    {
        var dict = new SortedDictionary<string, int>();
        
        dict["charlie"] = 3;
        dict["alpha"] = 1;
        dict["bravo"] = 2;
        
        // Keys are always sorted
        foreach (var kvp in dict)
        {
            Console.WriteLine($"{kvp.Key}: {kvp.Value}");
        }
        // Output: alpha: 1, bravo: 2, charlie: 3
    }
    
    // SortedList - sorted but uses array internally
    public static void SortedListExample()
    {
        var list = new SortedList<string, int>();
        
        list["charlie"] = 3;
        list["alpha"] = 1;
        list["bravo"] = 2;
        
        // Access by index or key
        int first = list.Values[0];  // 1 (alpha)
        int alpha = list["alpha"];   // 1
        
        // Less memory than SortedDictionary
        // But O(n) insertion vs O(log n) for SortedDictionary
    }
    
    // ReadOnlyDictionary
    public static void ReadOnlyDictionaryExample()
    {
        var mutable = new Dictionary<string, int>
        {
            ["one"] = 1,
            ["two"] = 2
        };
        
        var readOnly = new ReadOnlyDictionary<string, int>(mutable);
        
        // readOnly["three"] = 3;  // Compile error
    }
    
    // ImmutableDictionary
    public static void ImmutableDictionaryExample()
    {
        var original = ImmutableDictionary<string, int>.Empty;
        
        var dict1 = original.Add("one", 1);
        var dict2 = dict1.Add("two", 2);
        var dict3 = dict2.SetItem("one", 10);
        
        // original is still empty
        // dict1 has {one: 1}
        // dict2 has {one: 1, two: 2}
        // dict3 has {one: 10, two: 2}
    }
    
    // MultiDictionary (lookup with multiple values)
    public static void LookupExample()
    {
        var list = new List<(string Category, string Product)>
        {
            ("Electronics", "Laptop"),
            ("Electronics", "Phone"),
            ("Clothing", "Shirt"),
            ("Clothing", "Pants"),
            ("Electronics", "Tablet")
        };
        
        ILookup<string, string> lookup = list.ToLookup(x => x.Category, x => x.Product);
        
        foreach (var product in lookup["Electronics"])
        {
            Console.WriteLine(product);  // Laptop, Phone, Tablet
        }
    }
}
```

---

## 9. Sets

A set is a collection that contains no duplicate elements and provides efficient operations for membership testing, union, intersection, and difference. In mathematics, sets are unordered collections, but programming implementations may maintain order for practical purposes. C# provides the `HashSet<T>` class for high-performance set operations and `SortedSet<T>` for maintaining elements in sorted order.

Sets are particularly useful when you need to track unique items, remove duplicates from collections, or perform mathematical set operations. The HashSet<T> implementation provides O(1) average-case time complexity for add, remove, and contains operations, making it ideal for scenarios where membership testing is frequent.

### HashSet Implementation

```csharp
public class CustomHashSet<T> where T : notnull
{
    private const int DefaultCapacity = 16;
    private const double LoadFactor = 0.75;
    
    private LinkedList<T>[] _buckets;
    private int _count;
    
    public CustomHashSet(int capacity = DefaultCapacity)
    {
        _buckets = new LinkedList<T>[capacity];
        for (int i = 0; i < capacity; i++)
        {
            _buckets[i] = new LinkedList<T>();
        }
        _count = 0;
    }
    
    public int Count => _count;
    
    // Add - O(1) average
    public bool Add(T item)
    {
        if (_count >= _buckets.Length * LoadFactor)
        {
            Resize();
        }
        
        int index = GetBucketIndex(item);
        
        if (_buckets[index].Contains(item))
            return false;  // Already exists
        
        _buckets[index].AddLast(item);
        _count++;
        return true;
    }
    
    // Remove - O(1) average
    public bool Remove(T item)
    {
        int index = GetBucketIndex(item);
        return _buckets[index].Remove(item);
    }
    
    // Contains - O(1) average
    public bool Contains(T item)
    {
        int index = GetBucketIndex(item);
        return _buckets[index].Contains(item);
    }
    
    private int GetBucketIndex(T item)
    {
        return Math.Abs(item.GetHashCode()) % _buckets.Length;
    }
    
    private void Resize()
    {
        var oldBuckets = _buckets;
        _buckets = new LinkedList<T>[oldBuckets.Length * 2];
        
        for (int i = 0; i < _buckets.Length; i++)
        {
            _buckets[i] = new LinkedList<T>();
        }
        
        _count = 0;
        
        foreach (var bucket in oldBuckets)
        {
            foreach (var item in bucket)
            {
                Add(item);
            }
        }
    }
    
    // Set operations
    public void UnionWith(IEnumerable<T> other)
    {
        foreach (var item in other)
        {
            Add(item);
        }
    }
    
    public void IntersectWith(IEnumerable<T> other)
    {
        var otherSet = other as ISet<T> ?? other.ToHashSet();
        var toRemove = new List<T>();
        
        foreach (var item in this)
        {
            if (!otherSet.Contains(item))
                toRemove.Add(item);
        }
        
        foreach (var item in toRemove)
        {
            Remove(item);
        }
    }
    
    public void ExceptWith(IEnumerable<T> other)
    {
        foreach (var item in other)
        {
            Remove(item);
        }
    }
    
    public IEnumerator<T> GetEnumerator()
    {
        foreach (var bucket in _buckets)
        {
            foreach (var item in bucket)
            {
                yield return item;
            }
        }
    }
}
```

### Using .NET HashSet<T>

```csharp
public class HashSetExamples
{
    public static void BasicOperations()
    {
        // Creation
        var set = new HashSet<int>();
        var setFromCollection = new HashSet<int>(new[] { 1, 2, 3, 2, 1 });  // {1, 2, 3}
        
        // Add - returns true if added, false if already exists
        bool added1 = set.Add(1);  // true
        bool added2 = set.Add(1);  // false (duplicate)
        
        // Contains - O(1)
        bool contains = set.Contains(1);  // true
        
        // Remove - O(1)
        bool removed = set.Remove(1);
        
        // Count
        int count = set.Count;
        
        // Clear
        set.Clear();
        
        // Iterate (order not guaranteed)
        foreach (var item in set)
        {
            Console.WriteLine(item);
        }
    }
    
    // Set operations
    public static void SetOperations()
    {
        var set1 = new HashSet<int> { 1, 2, 3, 4, 5 };
        var set2 = new HashSet<int> { 4, 5, 6, 7, 8 };
        
        // Union - all elements from both sets
        var union = new HashSet<int>(set1);
        union.UnionWith(set2);
        // {1, 2, 3, 4, 5, 6, 7, 8}
        
        // Intersection - elements in both sets
        var intersection = new HashSet<int>(set1);
        intersection.IntersectWith(set2);
        // {4, 5}
        
        // Except - elements in set1 but not in set2
        var except = new HashSet<int>(set1);
        except.ExceptWith(set2);
        // {1, 2, 3}
        
        // Symmetric Except - elements in either set but not both
        var symmetricExcept = new HashSet<int>(set1);
        symmetricExcept.SymmetricExceptWith(set2);
        // {1, 2, 3, 6, 7, 8}
        
        // Check relationships
        bool isSubsetOf = set1.IsSubsetOf(new[] { 1, 2, 3, 4, 5, 6 });
        bool isProperSubsetOf = set1.IsProperSubsetOf(new[] { 1, 2, 3, 4, 5, 6 });
        bool isSupersetOf = set1.IsSupersetOf(new[] { 1, 2, 3 });
        bool overlaps = set1.Overlaps(set2);  // Any common elements
        bool setEquals = set1.SetEquals(new[] { 5, 4, 3, 2, 1 });
    }
    
    // Remove duplicates from array
    public static int[] RemoveDuplicates(int[] arr)
    {
        return new HashSet<int>(arr).ToArray();
    }
    
    // Find all duplicates
    public static IList<int> FindDuplicates(int[] nums)
    {
        var seen = new HashSet<int>();
        var duplicates = new HashSet<int>();
        
        foreach (var num in nums)
        {
            if (!seen.Add(num))
            {
                duplicates.Add(num);
            }
        }
        
        return duplicates.ToList();
    }
    
    // Longest Consecutive Sequence
    public static int LongestConsecutive(int[] nums)
    {
        if (nums.Length == 0) return 0;
        
        var numSet = new HashSet<int>(nums);
        int longestStreak = 0;
        
        foreach (var num in numSet)
        {
            // Only start counting from the beginning of a sequence
            if (!numSet.Contains(num - 1))
            {
                int currentNum = num;
                int currentStreak = 1;
                
                while (numSet.Contains(currentNum + 1))
                {
                    currentNum++;
                    currentStreak++;
                }
                
                longestStreak = Math.Max(longestStreak, currentStreak);
            }
        }
        
        return longestStreak;
    }
}
```

### SortedSet<T>

```csharp
public class SortedSetExamples
{
    public static void BasicOperations()
    {
        // SortedSet maintains elements in sorted order (red-black tree)
        var set = new SortedSet<int> { 5, 2, 8, 1, 9 };
        // Order: {1, 2, 5, 8, 9}
        
        // Operations are O(log n) instead of O(1)
        set.Add(3);       // {1, 2, 3, 5, 8, 9}
        set.Remove(5);    // {1, 2, 3, 8, 9}
        bool contains = set.Contains(3);  // true
        
        // Range operations
        var view = set.GetViewBetween(2, 8);  // {2, 3, 8}
        
        // Min and Max
        int min = set.Min;  // 1
        int max = set.Max;  // 9
        
        // Custom comparer
        var caseInsensitive = new SortedSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "apple", "Apple", "BANANA", "banana"
        };
        // {"apple", "BANANA"} (duplicates removed case-insensitively)
    }
}
```

---

## 10. Sorting Algorithms

Sorting is one of the most fundamental operations in computer science, with applications ranging from database indexing to search optimization. A sorting algorithm rearranges elements in a collection according to a comparison criterion, typically in ascending or descending order. Understanding different sorting algorithms, their time and space complexities, and when to use each is essential for writing efficient code.

Sorting algorithms can be classified by several characteristics: comparison-based vs non-comparison-based, stable vs unstable, in-place vs out-of-place, and adaptive vs non-adaptive. Each algorithm has trade-offs that make it suitable for different scenarios, from the simplicity of bubble sort for educational purposes to the guaranteed O(n log n) performance of merge sort for large datasets.

### Comparison of Sorting Algorithms

| Algorithm | Best Time | Average Time | Worst Time | Space | Stable |
|-----------|-----------|--------------|------------|-------|--------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Counting Sort | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes |
| Radix Sort | O(nk) | O(nk) | O(nk) | O(n+k) | Yes |
| Bucket Sort | O(n+k) | O(n+k) | O(n²) | O(n+k) | Yes |

### Bubble Sort

```csharp
public class BubbleSort
{
    // Basic bubble sort - O(n²)
    public static void Sort(int[] arr)
    {
        int n = arr.Length;
        
        for (int i = 0; i < n - 1; i++)
        {
            for (int j = 0; j < n - i - 1; j++)
            {
                if (arr[j] > arr[j + 1])
                {
                    (arr[j], arr[j + 1]) = (arr[j + 1], arr[j]);
                }
            }
        }
    }
    
    // Optimized bubble sort
    public static void SortOptimized(int[] arr)
    {
        int n = arr.Length;
        bool swapped;
        
        for (int i = 0; i < n - 1; i++)
        {
            swapped = false;
            
            for (int j = 0; j < n - i - 1; j++)
            {
                if (arr[j] > arr[j + 1])
                {
                    (arr[j], arr[j + 1]) = (arr[j + 1], arr[j]);
                    swapped = true;
                }
            }
            
            // If no swaps occurred, array is sorted
            if (!swapped) break;
        }
    }
}
```

### Selection Sort

```csharp
public class SelectionSort
{
    public static void Sort(int[] arr)
    {
        int n = arr.Length;
        
        for (int i = 0; i < n - 1; i++)
        {
            // Find minimum element in unsorted portion
            int minIndex = i;
            
            for (int j = i + 1; j < n; j++)
            {
                if (arr[j] < arr[minIndex])
                {
                    minIndex = j;
                }
            }
            
            // Swap minimum with first unsorted element
            if (minIndex != i)
            {
                (arr[i], arr[minIndex]) = (arr[minIndex], arr[i]);
            }
        }
    }
}
```

### Insertion Sort

```csharp
public class InsertionSort
{
    public static void Sort(int[] arr)
    {
        int n = arr.Length;
        
        for (int i = 1; i < n; i++)
        {
            int key = arr[i];
            int j = i - 1;
            
            // Move elements greater than key one position ahead
            while (j >= 0 && arr[j] > key)
            {
                arr[j + 1] = arr[j];
                j--;
            }
            
            arr[j + 1] = key;
        }
    }
    
    // Insertion sort for linked list
    public static ListNode? SortList(ListNode? head)
    {
        if (head == null || head.Next == null) return head;
        
        ListNode dummy = new(0) { Next = head };
        ListNode? current = head;
        
        while (current?.Next != null)
        {
            if (current.Val <= current.Next.Val)
            {
                current = current.Next;
            }
            else
            {
                // Find insertion point
                ListNode? prev = dummy;
                while (prev!.Next!.Val < current.Next.Val)
                {
                    prev = prev.Next;
                }
                
                // Remove and insert
                ListNode temp = current.Next;
                current.Next = temp.Next;
                temp.Next = prev.Next;
                prev.Next = temp;
            }
        }
        
        return dummy.Next;
    }
}
```

### Merge Sort

```csharp
public class MergeSort
{
    public static void Sort(int[] arr)
    {
        if (arr.Length <= 1) return;
        Sort(arr, 0, arr.Length - 1);
    }
    
    private static void Sort(int[] arr, int left, int right)
    {
        if (left < right)
        {
            int mid = left + (right - left) / 2;
            
            Sort(arr, left, mid);
            Sort(arr, mid + 1, right);
            Merge(arr, left, mid, right);
        }
    }
    
    private static void Merge(int[] arr, int left, int mid, int right)
    {
        int n1 = mid - left + 1;
        int n2 = right - mid;
        
        int[] leftArr = new int[n1];
        int[] rightArr = new int[n2];
        
        Array.Copy(arr, left, leftArr, 0, n1);
        Array.Copy(arr, mid + 1, rightArr, 0, n2);
        
        int i = 0, j = 0, k = left;
        
        while (i < n1 && j < n2)
        {
            if (leftArr[i] <= rightArr[j])
            {
                arr[k++] = leftArr[i++];
            }
            else
            {
                arr[k++] = rightArr[j++];
            }
        }
        
        while (i < n1) arr[k++] = leftArr[i++];
        while (j < n2) arr[k++] = rightArr[j++];
    }
}
```

### Quick Sort

```csharp
public class QuickSort
{
    public static void Sort(int[] arr)
    {
        Sort(arr, 0, arr.Length - 1);
    }
    
    private static void Sort(int[] arr, int low, int high)
    {
        if (low < high)
        {
            int pivotIndex = Partition(arr, low, high);
            Sort(arr, low, pivotIndex - 1);
            Sort(arr, pivotIndex + 1, high);
        }
    }
    
    private static int Partition(int[] arr, int low, int high)
    {
        int pivot = arr[high];
        int i = low - 1;
        
        for (int j = low; j < high; j++)
        {
            if (arr[j] <= pivot)
            {
                i++;
                (arr[i], arr[j]) = (arr[j], arr[i]);
            }
        }
        
        (arr[i + 1], arr[high]) = (arr[high], arr[i + 1]);
        return i + 1;
    }
    
    // Randomized quicksort to avoid worst case
    private static readonly Random _random = new();
    
    public static void SortRandomized(int[] arr)
    {
        SortRandomized(arr, 0, arr.Length - 1);
    }
    
    private static void SortRandomized(int[] arr, int low, int high)
    {
        if (low < high)
        {
            // Random pivot selection
            int randomPivot = _random.Next(low, high + 1);
            (arr[randomPivot], arr[high]) = (arr[high], arr[randomPivot]);
            
            int pivotIndex = Partition(arr, low, high);
            SortRandomized(arr, low, pivotIndex - 1);
            SortRandomized(arr, pivotIndex + 1, high);
        }
    }
}
```

### Heap Sort

```csharp
public class HeapSort
{
    public static void Sort(int[] arr)
    {
        int n = arr.Length;
        
        // Build max heap
        for (int i = n / 2 - 1; i >= 0; i--)
        {
            Heapify(arr, n, i);
        }
        
        // Extract elements from heap
        for (int i = n - 1; i > 0; i--)
        {
            (arr[0], arr[i]) = (arr[i], arr[0]);
            Heapify(arr, i, 0);
        }
    }
    
    private static void Heapify(int[] arr, int n, int i)
    {
        int largest = i;
        int left = 2 * i + 1;
        int right = 2 * i + 2;
        
        if (left < n && arr[left] > arr[largest])
            largest = left;
        
        if (right < n && arr[right] > arr[largest])
            largest = right;
        
        if (largest != i)
        {
            (arr[i], arr[largest]) = (arr[largest], arr[i]);
            Heapify(arr, n, largest);
        }
    }
}
```

### Counting Sort

```csharp
public class CountingSort
{
    // For non-negative integers with known range
    public static void Sort(int[] arr, int max)
    {
        int n = arr.Length;
        int[] output = new int[n];
        int[] count = new int[max + 1];
        
        // Count occurrences
        for (int i = 0; i < n; i++)
        {
            count[arr[i]]++;
        }
        
        // Calculate cumulative count
        for (int i = 1; i <= max; i++)
        {
            count[i] += count[i - 1];
        }
        
        // Build output array (iterate backwards for stability)
        for (int i = n - 1; i >= 0; i--)
        {
            output[count[arr[i]] - 1] = arr[i];
            count[arr[i]]--;
        }
        
        Array.Copy(output, arr, n);
    }
}
```

### Radix Sort

```csharp
public class RadixSort
{
    public static void Sort(int[] arr)
    {
        if (arr.Length == 0) return;
        
        // Find maximum to know number of digits
        int max = arr.Max();
        
        // Sort by each digit
        for (int exp = 1; max / exp > 0; exp *= 10)
        {
            CountingSortByDigit(arr, exp);
        }
    }
    
    private static void CountingSortByDigit(int[] arr, int exp)
    {
        int n = arr.Length;
        int[] output = new int[n];
        int[] count = new int[10];
        
        // Count occurrences of current digit
        for (int i = 0; i < n; i++)
        {
            int digit = (arr[i] / exp) % 10;
            count[digit]++;
        }
        
        // Calculate cumulative count
        for (int i = 1; i < 10; i++)
        {
            count[i] += count[i - 1];
        }
        
        // Build output array
        for (int i = n - 1; i >= 0; i--)
        {
            int digit = (arr[i] / exp) % 10;
            output[count[digit] - 1] = arr[i];
            count[digit]--;
        }
        
        Array.Copy(output, arr, n);
    }
}
```

---

*The document continues with sections 11-29 covering Searching Algorithms, Trees, Graphs, Dynamic Programming, String Algorithms, Tries, and more.*

---

## Summary

Data structures and algorithms form the foundation of efficient software development. This comprehensive guide has covered the essential data structures—arrays, lists, linked lists, stacks, queues, dictionaries, and sets—along with their implementations, time complexities, and practical applications. We also explored fundamental sorting algorithms and their trade-offs.

Understanding when to use each data structure is crucial for writing efficient code. Arrays provide O(1) random access but require contiguous memory. Linked lists offer O(1) insertions and deletions but sacrifice random access. Hash-based structures like Dictionary and HashSet provide O(1) average-case operations. Stacks and queues provide specialized access patterns essential for many algorithms.

As you continue your journey, focus on practicing algorithm implementation and understanding the trade-offs between different approaches. The key to mastery is not just memorizing algorithms but understanding why they work and when to apply them. With this foundation, you'll be well-equipped to tackle complex problems and optimize your code for performance.
