# JAVA

### Usage of arrays and hash map: 

```java 
// you can return an array as: 
int[] { elements };

// you make a hashmap as:
Map <keyType, dataType> name = new HashMap<>();

// functions of hashmap: 
hashMap.containsKey(key)                    => returns boolean
hashMap.get(key)                            => gets the value of the key
hashMap.getOrDefault(key, setDefaultValue)  => returns the value corresponding to the key, 
                                               or returns the default value that is in the 2nd parameter.
hashMap.put(key, value)                     => to put somehting in the hashmap.
<!-- hashMap.remove(key)                    => Removes a key-value mapping. -->
hashMap.size()/isEmpty()                    => Returns the maps size or check isEmpty.
hashMap.clear()                             => Removes all mappings.
```

``` java
// TWO SUM: return the indices of any two elements that add up to the target.
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer, Integer> numMap = new HashMap<>();
        int n = nums.length;

        for (int i = 0; i < n; i++) {
            int complement = target - nums[i];
            if (numMap.containsKey(complement)) {
                return new int[]{numMap.get(complement), i};
            }
            numMap.put(nums[i], i);
        }

        return new int[]{}; // No solution found
    }
}
```

### you get the length of a string as: str.length();
### you get the length of an array as: arr.length;
```java
// roman to integers. 
class Solution {
    public int romanToInt(String s) {
        Map<Character, Integer> m = new HashMap<>();
        
        m.put('I', 1);
        m.put('V', 5);
        m.put('X', 10);
        m.put('L', 50);
        m.put('C', 100);
        m.put('D', 500);
        m.put('M', 1000);
        
        int ans = 0;
        
        for (int i=0; i<s.length(); i++) {
            // if i less than the length of the string
            // and the value of the char at i is less than char at i+1 then 
            // ans = ans - value of char at i  
            // as IV => 5 - 1 = 4.
            // else ans = ans + value of char at i
            // as VI => 5 + 1 = 6.
            if (i<s.length()-1 && m.get(s.charAt(i)) < m.get(s.charAt(i+1))) {
                ans -= m.get(s.charAt(i));
            } else {
                ans += m.get(s.charAt(i));
            }
        }
        
        return ans;
    }
}
```

* for checking pallindrome, you can just reverse just half of the original number while dividing the original number, and then compare the reversed number with the original number. 
```java 
/// check pallindrome: 
class Solution {
    public boolean isPalindrome(int x) {
        if (x < 0 || (x != 0 && x % 10 == 0)) {
            return false;
        }

        int reversed = 0;
        int original = x;

        while (x > reversed) {
            reversed = reversed * 10 + x % 10;
            x /= 10;
        }

        return (x == reversed) || (x == reversed / 10);
    }
}
```

## Math functions: 
```java
Math.abs(x)      => removes the sign.
Math.max(x, y)   => max among two values
Math.min(x, y)   => min among two values
Math.round()     => rounds to the nearest integer
Math.ceil()      => rounds up
Math.floor()     => rounds down
Math.random()    => random num 0.0-1.0
Math.sqrt(x)     => sqrt of x
Math.cbrt()x     => cube root of x
Math.pow(x, y)   => x^y
Math.exp(x)      => e^x
Math.log(x)      => natural log => ln x
Math.PI          => value of pi
Math.E           => value of e
```
## KADANE'S algoritm:
```java
// Maximum sub array: find the max sum of a contiguious subarray.

// this solution uses KADANE's algorithm.
// this is a single pass approach: 
// if the sum becomes negative, you put the sum=0 and continue.
// the max continues to grow.
// this also handles -ve cases. 
class Solution {
    public int maxSubArray(int[] nums) {
        int n = nums.length;
        int max = Integer.MIN_VALUE;
        int sum = 0;
        
        for(int i=0;i<n;i++){
            sum += nums[i];
            max = Math.max(sum,max);
            
            if(sum<0) sum = 0;
        }
        
        return max;
    }
}
```

``` java
// CONTAINS DUPLICATE: if the array contains dup then return true else false: 
// create a hashmap, iterate through the array, increment the hashmap for each value. 
// do hashMap.put(key, value++) => hashMap.put(arr[i], hashMap.get(arr[i], 0) + 1)
// if for any key, the value exceeds 1 => the array contains a duplicate.

class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer, Integer> seen = new HashMap<>();
        for (int num : nums) {
            if (seen.containsKey(num) && seen.get(num) >= 1) {
                return true;
            }
            
            seen.put(num, seen.getOrDefault(num, 0) + 1);
        }
        return false;
    }
}
```

## MOORE VOTING ALGORITHM
``` java 
// return the element that occurs more than n/2 times in the array.

// normal approach: 
// the element will always occupy the middle position when the array is sorted.Therefore, we can sort the array and return the element at index n/2.

// Moores voting approach: 
// Initialize two variables: count and candidate. Set count to 0 and candidate to an arbitrary value.
// Iterate through the array nums:
    // a. If count is 0, assign the current element as the new candidate and increment count by 1.
    // b. If the current element is the same as the candidate, increment count by 1.
    // c. If the current element is different from the candidate, decrement count by 1.
// After the iteration, the candidate variable will hold the majority element.

class Solution {
    public int majorityElement(int[] nums) {
        int count = 0;
        int candidate = 0;
        
        for (int num : nums) {
            if (count == 0) {
                candidate = num;
            }
            
            if (num == candidate) {
                count++;
            } else {
                count--;
            }
        }
        
        return candidate;
    }
}
```


# Array class static methods:

```java
Arrays.sort(arr)            => sorts all the premitive types.
                                also sorts object arrays with comparator


Arrays.binarySearch(arr)    => bs on a sorted array.

Arrays.equals(arr1, arr2)   => on the basis of content and lenght.

Arrays.deepEquals(arr1, arr2) => for multidimentional arrays

Arrays.copyOf(arr)          => outputs a copy of the array.

Arrays.copyOfRange(source, 1, 4)    => 1 inclusive 4 exclusive.

Arrays.stream(arr)          => returns a Stream     

Arrays.parallelSort(arr)    => Sorts an array in parallel, which can be
                               faster for large arrays on

Arrays.mismatch(arr1, arr2) => Finds and returns the index of the 
                               first mismatch between two arrays,
```

```java
// IS ANNAGRAM => has same frequency of letters.

import java.util.Arrays;

class Solution {
    public boolean isAnagram(String s, String t) {
        char[] sChars = s.toCharArray();
        char[] tChars = t.toCharArray();
        
        Arrays.sort(sChars);
        Arrays.sort(tChars);
        
        return Arrays.equals(sChars, tChars);
    }
}
```
```java
// GROUP ANAGRAMS: 

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap<>();
        
        for (String word : strs) {
            char[] chars = word.toCharArray();
            Arrays.sort(chars);
            String sortedWord = new String(chars);
            
            if (!map.containsKey(sortedWord)) {
                map.put(sortedWord, new ArrayList<>());
            }
            
            map.get(sortedWord).add(word);
        }
        
        return new ArrayList<>(map.values());
    }
}
```

```java
// Top K Frequent Elements: output k number of elemnts who have relatively higher frequencies. 

class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        // build map<num, frequence>
        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int num: nums) map.put(num, map.getOrDefault(num, 0) + 1);
        
        // sort list from map.keyset() by map.get(num),
        List<Integer> list = new ArrayList<>(map.keySet());
        Collections.sort(list, (a, b) -> map.get(b) - map.get(a));
        
        // transfer results from list to int[];
        int[] res = new int[k];
        for (int i = 0; i < k; i++) res[i] = list.get(i);
        
        return res;
    }
}
```

### Prefix product and suffix product.
```java 
// the output array should be having the elements as the product of all other elements except self.

// solutoin using more space.
// compute the prefix product => arr[i] = arr[i-1] * arr[i-1]
//             prefix sum     => arr[i] = arr[i+1] * arr[i+1]
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int pre[] = new int[n];
        int suff[] = new int[n];
        pre[0] = 1;
        suff[n - 1] = 1;
        
       for(int i = 1; i < n; i++) {
            pre[i] = pre[i - 1] * nums[i - 1];
        }
        for(int i = n - 2; i >= 0; i--) {
            suff[i] = suff[i + 1] * nums[i + 1];
        }
        
        int ans[] = new int[n];
        for(int i = 0; i < n; i++) {
            ans[i] = pre[i] * suff[i];
        }
        return ans;
    }
}


// solution using O(1) space.
// iterate from front and update the ans array. as => ans[i] = curr, where curr holds the prefix product.
// iterate form the last and update the array. as => ans[i] = curr, where curr holds the suffix product. 
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int ans[] = new int[n];
        Arrays.fill(ans, 1);
        int curr = 1;
        for(int i = 0; i < n; i++) {
            ans[i] *= curr;
            curr *= nums[i];
        }
        curr = 1;
        for(int i = n - 1; i >= 0; i--) {
            ans[i] *= curr;
            curr *= nums[i];
        }
        return ans;
    }
}
```


# Hash Set
```java

Set<String> set = new HashSet<>();

// A HashSet automatically prevents duplicate elements.
// Elements are not stored in any particular order

set.add(x)   => adds x to the hashSet.
set.remove(x) => removes x from the hashSet.
set.contains(x) => checks if x exits in the hashSet.
set.ifEmpty() => checks if the set is empty. 
set.size() => returns the number of elements in the hashSet.
set.clear() => removes all the elements. 
set.iterator() => returns an iterator for traversal.
```

```java 
// Longest Consecutive sequence that can be created: 
// this is a O(n) solution. It does look like a O(n^2) but it is not. 

class Solution {
    public int longestConsecutive(int[] nums) {
        
        Set <Integer> set = new HashSet <Integer>();
        for(int n : nums) {
            set.add(n);
        }
        
        int streak = 0;
        
        for(int n : nums) {
            if(!set.contains(n - 1)) {             // so that we don't check for every element.
                int currStreak = 1;
                
                while(set.contains(n + 1)) {
                    set.remove(n);
                    n++;
                    currStreak++;
                }

                if(currStreak > streak) {
                    streak = currStreak; 
                }
            }
        }

        return streak;
    }
}
```

```java
// Find the intersection of two arrays. 
public class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();         // normal set.
        Set<Integer> intersect = new HashSet<>();   // intersection array
        
        for (int i = 0; i < nums1.length; i++) {
            set.add(nums1[i]);
        }
        
        for (int i = 0; i < nums2.length; i++) {
            if (set.contains(nums2[i])) {
                intersect.add(nums2[i]);
            }
        }
        
        int[] result = new int[intersect.size()];    // make result array.
        
        int i = 0;
        for (Integer num : intersect) {
            result[i++] = num;
        }
        
        return result;
    }
}
```

```java 
// Sub array sum, return the number of subarrays that have a sum of k. 

// Intuitive O(n^2) approach: 
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0;
      
        int[] sum = new int[nums.length + 1];
        sum[0] = 0;
        // make the sum array = sum uptill that array element.
        for (int i = 1; i <= nums.length; i++) {
            sum[i] = sum[i - 1] + nums[i - 1];
        }
      
        for (int start = 0; start < sum.length; start++) {
            for (int end = start + 1; end < sum.length; end++) {
                if (sum[end] - sum[start] == k) {
                    count++;
                }
            }
        }

        return count;
    }
}

// optimal O(n) approach: 
// make a map of sums and their frequency. initiate it with 0,1 where 0 is the sum, and 1 is the frequency. 
// iterate through the whoel nums array. 
// while iterating, add nums[i] to sum. 
// check if sum-k exits in the map. 
// if it exists, then count += frequency of that sum. 
// either it exits or not. put the sum into the map. 
// map.put(sum, map.getOrDefault(sum, 0) + 1)
public class Solution {
    public int subarraySum(int[] nums, int k) {
        int count = 0, sum = 0;
        Map <Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
      
        for (int i=0; i<nums.length; i++) {
            sum += nums[i];
            if (map.containsKey(sum - k)) {
                count += map.get(sum - k);
            }
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

```java 
// check Subarray Sum: return true if there exists  subarray that has a sum that is a multiple of k. 

// keep a map of previous sums. 
// if in further iterations the sum%k does exist, it means that the multiple of K can be constructed by subtracting them. 
// hence if sum%k == 0, or ps.contains(sum), then return true.
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        HashSet<Integer> ps = new HashSet<>();
        int sum = nums[0] % k;
        int previous = sum;

        for (int i = 1; i < nums.length; i++) {
            sum += nums[i];
            sum %= k; 

            if (sum == 0 || ps.contains(sum)) {
                return true;
            }

            ps.add(previous);
            previous = sum;
        }

        return false;
    }
}

```

```java
// Return the length of the longest substring without repeating characters. 

// make a set. 
// keep a right pointer, a left pointer. 
// iterate through the string using pointers. 
// if the element is not in the set, add it. 
// then calculate the maxLength till then. 

// if the character is already present in the set. (it was already found before)
// keep removing the elements from the left, until the set does not contain the right element. 
// then add back the right element, as for iterating from there onwards. 

// at last return the max length. 
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length();
        int maxLength = 0;
        Set<Character> charSet = new HashSet<>();
        int left = 0;
        
        for (int right = 0; right < n; right++) {
            if (!charSet.contains(s.charAt(right))) {
                charSet.add(s.charAt(right));
                int currLength = right - left + 1; 
                maxLength = Math.max(maxLength, currLen);
            } else {
                while (charSet.contains(s.charAt(right))) {
                    charSet.remove(s.charAt(left));
                    left++;
                }
                charSet.add(s.charAt(right));
            }
        }
        
        return maxLength;
    }
}
```


```java 
// longest repeating character replacement: 
// ex: ABABABABBBBBAAABABAAABB and k = 3 => the output should be BBBBBBBBB. where k has been used 3 times to replace A.
class Solution {
    public int characterReplacement(String s, int k) {
        int[] arr = new int[26];
        int maxFreq=0, startPtr=0, maxlen=0;

        for(int currPtr=0; currPtr<s.length(); currPtr++){

            arr[s.charAt(currPtr) - 'A']++;
            maxFreq = Math.max(maxFreq, arr[s.charAt(currPtr) - 'A']);

            // If (window size - maxFreq) > k,
            // we would need more than k replacements to make all characters equal.
            // So the window is invalid and we shrink it from the left.
            if(currPtr-startPtr+1 - maxFreq > k) {
                arr[s.charAt(startPtr) - 'A']--;
                startPtr++;
            }

            maxlen = Math.max(maxlen, currPtr-startPtr+1);
        }
        return maxlen;
    }
}
```

```java
// Minimum Window Substring
// Input: s = "ADOBECODEBANC", t = "ABC"
// Output: "BANC"
// Explanation: The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

class Solution {
    public String minWindow(String s, String t) {
        int[] count = new int[128];
        for (char ch : t.toCharArray()) count[ch]++;

        char[] sourceStr = s.toCharArray();
        String windowString = "";
        int windowLeft = 0, windowRight = 0, charsFoundInWindow = 0,
            totalCharsToFind = t.length(), minWindowLen = Integer.MAX_VALUE;

        while (windowRight < sourceStr.length) {
            int currentChar = sourceStr[windowRight];
            count[currentChar]--;

            if (count[currentChar] >= 0) {
                charsFoundInWindow++;
            }

            while (charsFoundInWindow == totalCharsToFind) {
                int currentWindowLen = windowRight - windowLeft + 1;
                if(minWindowLen > currentWindowLen) {
                    minWindowLen = currentWindowLen;
                    windowString = s.substring(windowLeft, windowRight + 1);
                }

                count[sourceStr[windowLeft]]++;

                if (count[sourceStr[windowLeft]] > 0) {
                    charsFoundInWindow--;
                }
                windowLeft++;
            }
            windowRight++;
        }
        return windowString;
    }
}
```

```java
// valid pallindome.
// Input: s = "A man, a plan, a canal: Panama"
// Output: true
// Explanation: "amanaplanacanalpanama" is a palindrome.

class Solution {
    public boolean isPalindrome(String s) {
        s = s.toLowerCase().replaceAll("[^a-z0-9]", "");
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }
        return true;        
    }
}
```

```java
// Container with most water: 
// return the area of the max possible water being stored.
class Solution {
    public int maxArea(int[] height) {
        int maxArea = 0;
        int left = 0;
        int right = height.length - 1;

        while (left < right) {
            maxArea = Math.max(maxArea, (right - left) * Math.min(height[left], height[right]));

            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }

        return maxArea;        
    }
}
```

```java
// THREE SUM
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        
        Arrays.sort(nums); // the array is sorted.

        for (int i = 0; i < nums.length; i++) {
            if (i > 0 && nums[i] == nums[i-1]) {
                continue; // skip duplicates. 
            }
            
            int j = i+1;
            int k = nums.length-1;

            while (j < k) {
                int total = nums[i] + nums[j] + nums[k];

                if (total > 0) {
                    k--;
                } else if (total < 0) {
                    j++;
                } else {
                    res.add(Arrays.asList(nums[i], nums[j], nums[k]));
                    j++;

                    while (nums[j] == nums[j-1] && j < k) {
                        j++;
                    }
                }
            }
        }
        return res;        
    }
}
```

```java
// move zeroes to the end: 
// Input: nums = [0,1,0,3,12]
// Output: [1,3,12,0,0]
class Solution {
    public void moveZeroes(int[] nums) {
        int left = 0;

        for (int right = 0; right < nums.length; right++) {
            if (nums[right] != 0) {
                int temp = nums[right];
                nums[right] = nums[left];
                nums[left] = temp;
                left++;
            }
        }        
    }
}
```

```java
// sorted squares: input => sorted array. output => sorted squares array.
// Input: nums = [-4,-1,0,3,10]
// Output: [0,1,9,16,100]

// the square would be the greatest of either leftmost or rightmost. 
// so compare them first.
// if left > right (abs value) => use the square of left. 
// else use the sqare of right as the element of the output array. 
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] res = new int[nums.length];
        int left = 0;
        int right = nums.length - 1;    

        for (int i = nums.length - 1; i >= 0; i--) {
            if (Math.abs(nums[left]) > Math.abs(nums[right])) {
                res[i] = nums[left] * nums[left];
                left++;
            } else {
                res[i] = nums[right] * nums[right];
                right--;
            }
        }
        return res;        
    }
}
```


```java

import java.util.*;

public class Demo {
    public static int solution (int n, int[] arr, int k) {
        int maxLen=0;

        for(int i=0; i<n; i++) {
            int sum=0; 
            int currLen=0; 
           for(int j=i; i<n && sum<k; j++) {
                sum += arr[j];
                currLen++;         
           }

           maxLen = Math.max(currLen, maxLen);
        }
        return maxLen; 
    }


    public static void main (String args[]) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        
        int[] arr = new int[n];
        for(int i=0; i<n; i++) {
            arr[i] = sc.nextInt();
        }

        int k = sc.nextInt(); 
        int result = solution(n, arr, k); 
        System.out.println(result);
    }
}



import java.util.*;

public class Solution {

    public static int solution(int n, int[] arr, int k) {
        int left = 0;
        int sum = 0;
        int maxLen = 0;

        for (int right=0; right<n; right++) {
            sum += arr[right];

            while (sum > k) {
                sum -= arr[left];
                left++;
            }

            maxLen = Math.max(maxLen, right-left+1);
        }

        return maxLen;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();

        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }

        int k = sc.nextInt();
        int result = solution(n, arr, k);
        System.out.println(result);

        sc.close();
    }
}
```

```java
import java.util.*; 

public class Demo {
    static int solution (String s) {
        int maxLen=0; 
        Map <Character, Integer> set = new HashMap<>();
        int left=0; 

        for(int right=0; right<s.length(); right++) {
            set.put(s[right], set.get(s[right]) + 1);
            
            if(set.get(s[right]) > 1) {
                set.put(s[right], set.get(s[right]) - 1);
                left++; 
            }

            maxLen = Math.max(maxLen, right-left+1);
        }

        return maxLen;
    }

    public static void main (String args[]) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine(); 

        int result = solution(s);

        System.out.println(result);
    }
}


import java.util.*;

public class Solution {

    public static int solution(String s) {
        Map<Character, Integer> map = new HashMap<>();

        int left=0;
        int maxLen=0;

        for (int right=0; right<s.length(); right++) {
            char ch = s.charAt(right);

            if (map.containsKey(ch)) {
                left = Math.max(left, map.get(ch) + 1);
            }

            map.put(ch, right);

            maxLen = Math.max(maxLen, right-left+1);
        }

        return maxLen;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        String s = sc.nextLine();

        int result = solution(s);

        System.out.println(result);

        sc.close();
    }
}
```

``` java
// Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();

        for(int num:nums){
            if(!set.add(num))return true;
        }
        return false;
    }
}
```

# String Builder: 

```java
// Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.

class Solution {

    public String encode(List<String> strs) {
        StringBuilder sb = new StringBuilder(); 
        for(String str : strs) {
            sb.append("©" + str); 
        }

        return sb.toString(); 
    }

    public List<String> decode(String str) {
        
        List<String> res = new ArrayList<>(); 
        StringBuilder sb = new StringBuilder();
        if (str.length() == 0) {
            return res;
        }

        char[] chr = str.toCharArray(); 
    
        for (int i=1; i<chr.length; i++) {
            char ch = chr[i];
            if(ch != '©') {
                sb.append(ch);
            } else if (ch == '©') {
                res.add(sb.toString());
                sb.setLength(0); // resets the sb. 
            }
        }

        res.add(sb.toString());
        
        return res; 
    }
}
```
