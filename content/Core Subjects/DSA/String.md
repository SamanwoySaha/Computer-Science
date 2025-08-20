---
title: String
draft: false
tags: 
date: 19-Aug-2025
---
# Problems

- [1021. Remove Outermost Parentheses](https://leetcode.com/problems/remove-outermost-parentheses/)
    
    ```cpp
    // O(n) O(n)
    string removeOuterParentheses(string s) {
        string res;
        int opened = 0;
        for (char c : s) {
            if (c == '(' && opened++ > 0) res += c;
            if (c == ')' && opened-- > 1) res += c;
        }
        return res;
    }
    
    ```
    
- [151. Reverse Words in a String](https://leetcode.com/problems/reverse-words-in-a-string/)
    
    ![image.png](image%2024.png)
    
    ```cpp
    // O(n) O(n)
    string reverseWords(string s) {
    	vector<string> words;
        stringstream ss(s);
        string tmp;
        while (ss >> tmp)
        	words.push_back(tmp);
    
        string ans;
        for (int i = words.size() - 1; i >= 0; --i) {
        	if (i != words.size() - 1) ans += " ";
        	ans += words[i];
        }
        return ans;
    }
    
    // O(n) O(1)
    	string reverseWords(string s) {
            reverse(s.begin(), s.end());
            int n = s.size();
            int left = 0;
            int right = 0;
            int i = 0;
            while (i < n) {
                while (i < n && s[i] == ' ')
                    i++;
                if (i == n)
                    break;
                while (i < n && s[i] != ' ') {
                    s[right++] = s[i++];
                }
                reverse(s.begin() + left, s.begin() + right);
                s[right++] = ' ';
                left = right;
                i++;
            }
            s.resize(right - 1);
            return s;
        }
    
    ```
    
- [1903. Largest Odd Number in String](https://leetcode.com/problems/largest-odd-number-in-string/)
    
    ```cpp
    	// O(n) O(1)
    	string largestOddNumber(string num) {
            if (num.back() % 2 == 1) return num;
            int i = num.length() - 1;
            while (i >= 0) {
                int n = num[i];
                if (n % 2 == 1) return num.substr(0, i + 1);
                i--;
            }
            return "";
        }
    
    ```
    
- [14. Longest Common Prefix](https://leetcode.com/problems/longest-common-prefix/)
- [205. Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)
- [796. Rotate String](https://leetcode.com/problems/rotate-string/)
- [242. Valid Anagram](https://leetcode.com/problems/valid-anagram/)
- [451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/)
- [1614. Maximum Nesting Depth of the Parentheses](https://leetcode.com/problems/maximum-nesting-depth-of-the-parentheses/)
- [13. Roman to Integer](https://leetcode.com/problems/roman-to-integer/)
- [8. String to Integer (atoi)](https://leetcode.com/problems/string-to-integer-atoi/)
- [Number of substrings of a string](https://www.geeksforgeeks.org/dsa/number-substrings-string/)
- [5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/)
- [1781. Sum of Beauty of All Substrings](https://leetcode.com/problems/sum-of-beauty-of-all-substrings/)