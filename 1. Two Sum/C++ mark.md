# Approach 1: Linear Search
## Time Complexity : O(n^2)
## Space Complexity: O(1)
<code>
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int sum = 0, size = nums.size();
        vector<int> vec(2,0);
        for(int i = 0; i < size-1; i++) {
            for(int j = i+1; j < size; j++) {
                if(nums[i] + nums[j] == target) {
                    vec[0] = i;
                    vec[1] = j;
                    return vec;
                }
            }
        }
        return vec;
    }
};
</code>


# Approach 2: Sort the array and then use binary search
## Time Complexity : (O(NlogN)) 
## Space Complexity: O(N)
<code>
class Solution {
public:
    int findInd(vector<int>& nums, int target, int ind, int size) {
        int mid;
        while(ind <= size) {
            mid = (ind + size) >> 1;   // incase of overflow use (unsigned_ind(ind) + unsigned_ind(size)) >> 1
            if(nums[mid] == target) return mid;
            else if(nums[mid] > target) size = mid - 1;
            else ind = mid + 1;
        }
        return -1;
    }
    vector<int> twoSum(vector<int>& nums, int target) {
        int size = nums.size(), ind;
        vector<int> dummy = nums; 
        sort(dummy.begin(),dummy.end()); // sort the array so that binary search can be performed
        int n1,n2; //will store the position of elements in sorted array
        vector<int> vec(2,0);
        for(int i = 0; i < size-1; i++) {
            ind = findInd(dummy, target - dummy[i], i + 1, size - 1);
            if (ind >= 0) {
                n1 = dummy[i];
                n2 = dummy[ind];
                break;
            }
        }
        for(int i = 0; i < size; i++) {
            if ( n1 == nums[i]) {
                vec[0] = i;
                break;
            }
        }
        for(int i = 0; i < size; i++) {
            if ( n2 == nums[i] && i != vec[0]) {
                vec[1] = i;
                break;
            }
        }
        return vec;
    }
};
</code>


# Approach 3: Sort the array and then use binary search
## Time Complexity : O(N)  
## Space Complexity: O(N)
<code>
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int,int> umap;
        umap[nums[0]]=0;
        for(int i=1;i < nums.size();i++) {
            if(umap.find(target-nums[i]) != umap.end()) return {i,umap[ target - nums[i]]};
            umap[nums[i]] = i;
        }
        return {-1,-1};
    }
};
</code>