[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/6wGdpkN5)

# Longest Nice Substring
class Solution {
public:
    string longestNiceSubstring(string s) 
    {
        int n = s.size();
        if (n < 2) return "";  

        unordered_set<char> charSet(s.begin(), s.end());

        
        for (int i = 0; i < n; ++i) 
        {
            if (charSet.count(tolower(s[i])) && charSet.count(toupper(s[i]))) continue;
            
             
            string left = longestNiceSubstring(s.substr(0, i));
            string right = longestNiceSubstring(s.substr(i + 1));

            return left.size() >= right.size() ? left : right;
        }

        return s; 
    }
};

# Reverse Bits
class Solution
{
public:
    uint32_t reverseBits(uint32_t n) 
    {
        uint32_t result = 0;
        
        for (int i = 0; i < 32; i++) 
        {
            result = (result << 1) | (n & 1);   
            n >>= 1;  
        }
        
        return result;
    }
};

# .Number of 1 Bits
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int count = 0;
        
        while (n) {
            count += (n & 1);  
            n >>= 1;            
        }
        
        return count;
    }
};
 # .Maximum Subarray



#include <vector>
#include <queue>
#include <set>
#include <algorithm>

using namespace std;

class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        vector<pair<int, int>> events;
        for (const auto& b : buildings) {
            events.emplace_back(b[0], -b[2]);  
            events.emplace_back(b[1], b[2]);  
        }
        
        sort(events.begin(), events.end());
        
        multiset<int> heights = {0};  
        vector<vector<int>> result;
        int prevHeight = 0;
        
        for (const auto& [x, h] : events) {
            if (h < 0) {
                heights.insert(-h); 
            } else {
                heights.erase(heights.find(h));  
            }
            
            int currHeight = *heights.rbegin(); 
            if (currHeight != prevHeight) {
                result.push_back({x, currHeight});
                prevHeight = currHeight;
            }
        }
        
        return result;
    }
    
    int maxSubArray(vector<int>& nums) {
        int maxSum = nums[0], currentSum = nums[0];
        for (size_t i = 1; i < nums.size(); ++i) {
            currentSum = max(nums[i], currentSum + nums[i]);
            maxSum = max(maxSum, currentSum);
        }
        return maxSum;
    }
};


# .Search a 2D Matrix II

class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        vector<pair<int, int>> events;
        for (const auto& b : buildings) {
            events.emplace_back(b[0], -b[2]); 
            events.emplace_back(b[1], b[2]);  
        }
        
        sort(events.begin(), events.end());
        
        multiset<int> heights = {0}; 
        vector<vector<int>> result;
        int prevHeight = 0;
        
        for (const auto& [x, h] : events) {
            if (h < 0) {
                heights.insert(-h); 
            } else {
                heights.erase(heights.find(h));  
            }
            
            int currHeight = *heights.rbegin();  
            if (currHeight != prevHeight) {
                result.push_back({x, currHeight});
                prevHeight = currHeight;
            }
        }
        
        return result;
    }
    
    int maxSubArray(vector<int>& nums) {
        int maxSum = nums[0], currentSum = nums[0];
        for (size_t i = 1; i < nums.size(); ++i) {
            currentSum = max(nums[i], currentSum + nums[i]);
            maxSum = max(maxSum, currentSum);
        }
        return maxSum;
    }
    
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.empty() || matrix[0].empty()) return false;
        int row = 0, col = matrix[0].size() - 1;
        while (row < matrix.size() && col >= 0) {
            if (matrix[row][col] == target) return true;
            else if (matrix[row][col] > target) --col;
            else ++row;
        }
        return false;
    }
};

# . Super Pow
class Solution {
public:
    const int MOD = 1337;
    
    int modPow(int x, int n) {
        int result = 1;
        x %= MOD;
        while (n > 0) {
            if (n % 2 == 1) result = (result * x) % MOD;
            x = (x * x) % MOD;
            n /= 2;
        }
        return result;
    }
    
    int superPow(int a, vector<int>& b) {
        a %= MOD;
        int result = 1;
        for (int digit : b) {
            result = modPow(result, 10) * modPow(a, digit) % MOD;
        }
        return result;
    }
};

# . Beautiful Array

class Solution {
public:
    vector<int> beautifulArray(int n) {
        vector<int> result = {1};  // Base case
        
        while (result.size() < n) {
            vector<int> temp;
            
            // Construct the odd part
            for (int x : result) {
                if (2 * x - 1 <= n) temp.push_back(2 * x - 1);
            }
            
            // Construct the even part
            for (int x : result) {
                if (2 * x <= n) temp.push_back(2 * x);
            }
            
            result = temp;  // Update with the newly constructed sequence
        }
        
        return result;
    }
};

# . The Skyline Problem

class Solution {
public:
    vector<vector<int>> getSkyline(vector<vector<int>>& buildings) {
        vector<pair<int, int>> events;
        for (const auto& b : buildings)
        {
            events.emplace_back(b[0], -b[2]);  
            events.emplace_back(b[1], b[2]); 
            
        }

        sort(events.begin(), events.end());
        multiset<int> heights = {0}; 

        vector<vector<int>> result;
        int prevHeight = 0;
        
        for (const auto& [x, h] : events) 
        {
            if (h < 0) 
            {
                heights.insert(-h);  
            } else {
                heights.erase(heights.find(h)); 
                
            }
            
            int currHeight = *heights.rbegin();  
            if (currHeight != prevHeight) {
                result.push_back({x, currHeight});
                prevHeight = currHeight;
            }
        }
        
        return result;
    }
};

# . Reverse Pairs

class Solution {
public:
    int mergeAndCount(vector<int>& nums, int left, int mid, int right) {
        int count = 0, j = mid + 1;
        
        // Count reverse pairs
        for (int i = left; i <= mid; i++) {
            while (j <= right && nums[i] > 2LL * nums[j]) {
                j++;
            }
            count += (j - (mid + 1));
        }
        
        // Merge two sorted halves
        vector<int> temp;
        int i = left, k = mid + 1;
        while (i <= mid && k <= right) {
            if (nums[i] <= nums[k]) temp.push_back(nums[i++]);
            else temp.push_back(nums[k++]);
        }
        while (i <= mid) temp.push_back(nums[i++]);
        while (k <= right) temp.push_back(nums[k++]);
        
        
        for (int i = left; i <= right; i++) {
            nums[i] = temp[i - left];
        }
        
        return count;
    }

    int mergeSort(vector<int>& nums, int left, int right) {
        if (left >= right) return 0;
        
        int mid = left + (right - left) / 2;
        int count = mergeSort(nums, left, mid) + mergeSort(nums, mid + 1, right);
        count += mergeAndCount(nums, left, mid, right);
        
        return count;
    }

    int reversePairs(vector<int>& nums) {
        return mergeSort(nums, 0, nums.size() - 1);
    }
};

# . Longest Increasing Subsequence II

class Solution {
public:
    int lengthOfLIS(vector<int>& nums, int k) {
        int maxValue = *max_element(nums.begin(), nums.end());  
        
        vector<int> segTree(maxValue + 1, 0); 
        
        
        auto query = [&](int left, int right) {
            int maxVal = 0;
            for (int i = right; i >= left; --i) {
                maxVal = max(maxVal, segTree[i]);
            }
            return maxVal;
        };

        auto update = [&](int index, int value) {
            segTree[index] = max(segTree[index], value);
        };

        int maxLen = 1;
        for (int num : nums) {
            int bestPrev = query(max(1, num - k), num - 1); 
            
            int newLength = bestPrev + 1;
            update(num, newLength);
            maxLen = max(maxLen, newLength);
        }
        return maxLen;
    }
};
