find the first repeating element in the array and return its index -- i did this in the geeks for geeks https://www.geeksforgeeks.org/problems/first-repeating-element4018/1
// User function template in C++

class Solution {
  public:
    // Function to return the position of the first repeating element.
    int firstRepeated(vector<int> &arr) {
        // code here
        
        vector<int> hash(1000001, 0); 
        for(int i=0;i<arr.size();i++){
            hash[arr[i]]++;
        }
        for(int i=0;i<arr.size();i++){
            if(hash[arr[i]]>1){
                return i+1;
            }
        }
        return -1;
    }
};


finding the common in the 3 sorted array done in the geeks for geeks --https://www.geeksforgeeks.org/problems/common-elements1132/1
class Solution {
  public:
    // Function to find common elements in three arrays.
    vector<int> commonElements(vector<int> &arr1, vector<int> &arr2,
                               vector<int> &arr3) {
        // Code Here
        int n1=arr1.size(); int n2=arr2.size(); int n3=arr3.size();
        int i,j,k;
        vector<int>ans;int element=0, count=-1;
         i=j=k=0;// I was mistaking here for that i had done i,j,k=0 which was wrong 
        while(i<n1&&j<n2&&k<n3){
            if(arr1[i]==arr2[j]&&arr2[j]==arr3[k]){
                if(arr1[count]!=arr1[i]){// this was to handle the duplicates 
                    ans.push_back(arr1[i]);
                    count= i;
                }
             i++;j++;k++;
            }else if(arr1[i]<arr2[j]){
                i++;
            }else if(arr2[j]<arr3[k]){
                j++;
            }else{
                k++;
            }
        }
        return ans;
    }
};
