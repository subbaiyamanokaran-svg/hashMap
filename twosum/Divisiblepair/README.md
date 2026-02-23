# 📌 Divisible Pair Checker (Java)

## 🧠 Problem Statement
Given an integer array `arr[]` and an integer `k`, determine whether the array can be divided into pairs such that the sum of every pair is divisible by `k`.

---

## ⚙️ Approach

The solution uses a **HashMap** to store frequencies of remainders when elements are divided by `k`.

### Key Steps:

1. If array length is odd → return `false`
2. Compute remainder:
   ```
   rem = ((arr[i] % k) + k) % k
   ```
3. Store frequency of each remainder
4. Validate pairing conditions:

- If `rem == 0` → frequency must be even  
- If `2 * rem == k` → frequency must be even  
- Otherwise →  
  ```
  freq[rem] == freq[k - rem]
  ```

---

## 🚀 Example

### Input:
```
arr = [92, 75, 65, 48, 45, 35]
k = 10
```

### Output:
```
True
```

### Explanation:
Valid pairs:
- (92, 48)
- (75, 65)
- (45, 35)

All sums are divisible by 10.

---

## 🏗️ Code

```java
import java.util.HashMap;

public class Divisiblepair {

    static boolean canPairs(int ar[], int k) {
        if (ar.length % 2 == 1)
            return false;

        HashMap<Integer, Integer> hm = new HashMap<>();

        for (int i = 0; i < ar.length; i++) {
            int rem = ((ar[i] % k) + k) % k;
            hm.put(rem, hm.getOrDefault(rem, 0) + 1);
        }

        for (int i = 0; i < ar.length; i++) {
            int rem = ((ar[i] % k) + k) % k;

            if (rem == 0) {
                if (hm.get(rem) % 2 == 1)
                    return false;
            }
            else if (2 * rem == k) {
                if (hm.get(rem) % 2 == 1)
                    return false;
            }
            else {
                if (hm.get(rem) != hm.getOrDefault(k - rem, 0))
                    return false;
            }
        }

        return true;
    }

    public static void main(String[] args) {
        int arr[] = {92, 75, 65, 48, 45, 35};
        int k = 10;

        System.out.println(canPairs(arr, k));
    }
}
```

---

## ⏱️ Complexity

- **Time Complexity:** O(n)  
- **Space Complexity:** O(k)

---

## 💡 Key Insight

Instead of checking all pairs (O(n²)), we use **remainder frequency matching**:

```
rem + (k - rem) = k
```

---

## 🧪 Use Cases

- Competitive programming  
- Modular arithmetic problems  
- Efficient pair validation  

---