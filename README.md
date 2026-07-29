# 12. Integer to Roman

![Difficulty](https://img.shields.io/badge/Difficulty-Medium-yellow.svg)
![Language](https://img.shields.io/badge/Language-Java-orange.svg)
![Approach](https://img.shields.io/badge/Approach-Greedy%20%2F%20Lookup-brightgreen.svg)
![Time Complexity](https://img.shields.io/badge/Time-O(1)-orange.svg)
![Space Complexity](https://img.shields.io/badge/Space-O(1)-green.svg)

---

## 📌 Problem Overview

Seven different symbols represent Roman numerals with the following values:

| Symbol | Value |
| :---: | :---: |
| **I** | 1 |
| **V** | 5 |
| **X** | 10 |
| **L** | 50 |
| **C** | 100 |
| **D** | 500 |
| **M** | 1000 |

Roman numerals are formed by appending the conversions of decimal place values from highest to lowest. Converting a decimal place value into a Roman numeral has the following rules:

- If the value does not start with 4 or 9, select the symbol of the maximal value that can be subtracted from the input, append that symbol to the result, subtract its value, and convert the remainder to a Roman numeral.
- If the value starts with 4 or 9, use the **subtractive form** representing one symbol subtracted from the following symbol. For example:
  - `4` is `IV` (1 less than 5)
  - `9` is `IX` (1 less than 10)
  - `40` is `XL`
  - `90` is `XC`
  - `400` is `CD`
  - `900` is `CM`

Only powers of 10 (`I`, `X`, `C`, `M`) can be appended consecutively at most 3 times. You cannot append `V`, `L`, or `D` multiple times.

Given an integer `num`, convert it to a Roman numeral.

---

## 💡 Examples

### Example 1:
- **Input:** `num = 3749`
- **Output:** `"MMMDCCXLIX"`
- **Explanation:**
  - $3000 = \text{MMM}$ ($1000 + 1000 + 1000$)
  - $700 = \text{DCC}$ ($500 + 100 + 100$)
  - $40 = \text{XL}$ (10 less than 50)
  - $9 = \text{IX}$ (1 less than 10)

### Example 2:
- **Input:** `num = 58`
- **Output:** `"LVIII"`
- **Explanation:**
  - $50 = \text{L}$
  - $8 = \text{VIII}$ ($5 + 1 + 1 + 1$)

### Example 3:
- **Input:** `num = 1994`
- **Output:** `"MCMXCIV"`
- **Explanation:**
  - $1000 = \text{M}$
  - $900 = \text{CM}$
  - $90 = \text{XC}$
  - $4 = \text{IV}$

---

## ⚡ Technical Constraints

- $1 \le \text{num} \le 3999$

---

## 🧠 Intuition & Strategy

### Greedy Approach

Since $1 \le \text{num} \le 3999$, we can solve this problem greedily by matching the largest possible values first using predefined lookup arrays in descending order.

Including subtractive forms (`900`, `400`, `90`, `40`, `9`, `4`) directly in our lookup arrays simplifies the logic completely. Using a `StringBuilder` in Java ensures maximum runtime efficiency.

---

## 💻 Java Solution

```java
class Solution {
    public String intToRoman(int num) {
        int[] values = {1000, 900, 500, 400, 100, 90, 50, 40, 10, 9, 5, 4, 1};
        String[] symbols = {"M", "CM", "D", "CD", "C", "XC", "L", "XL", "X", "IX", "V", "IV", "I"};

        StringBuilder sb = new StringBuilder();

        for (int i = 0; i < values.length; i++) {
            while (num >= values[i]) {
                sb.append(symbols[i]);
                num -= values[i];
            }
        }

        return sb.toString();
    }
}
