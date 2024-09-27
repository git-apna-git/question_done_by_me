1.find the first repeating element in the array and return its index -- i did this in the geeks for geeks https://www.geeksforgeeks.org/problems/first-repeating-element4018/1
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


2. finding the common in the 3 sorted array done in the geeks for geeks --https://www.geeksforgeeks.org/problems/common-elements1132/1
   
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

3.Add two numbers represented by two array in gfgs  ---https://www.geeksforgeeks.org/problems/add-two-numbers-represented-by-two-arrays2408/1

class Solution {
  public:
    string calc_Sum(vector<int>& arr1, vector<int>& arr2) {
        // Complete the function
        
        int carry =0; 
        string ans; 
        int i=arr1.size()-1;
        int j=arr2.size()-1; 
        while(i>=0&& j>=0){
            int x = arr1[i]+arr2[j]+carry;
            int digit= x%10;
            ans.push_back(digit +'0');
            carry = x/10;
            i--,j--;
        }
        
         while(i>=0){
            int x = arr1[i]+ 0 +carry;
            int digit= x%10;
            ans.push_back(digit +'0');
            carry = x/10;
            i--;
        }
        
         while(j>=0){
            int x =0+arr2[j]+carry;
            int digit= x%10;
            ans.push_back(digit +'0');
            carry = x/10;
            j--;
        }
        
        if(carry){
            ans.push_back(carry + '0');
        }
        while(ans[ans.size()-1]=='0'){
            ans.pop_back();
        }
        reverse(ans.begin(), ans.end());
        return ans; 
        }
};

4.Factorial of Larger number  gfgs --https://www.geeksforgeeks.org/problems/factorials-of-large-numbers2508/1

class Solution {
public:
    vector<int> factorial(int N){
    
        // code here
        vector< int> a; 
        a.push_back(1);
        int carry =0;int x=0; 
        for(int i=2; i<=N;i++){
            
            for(int j=0;j< a.size();j++){
                x=a[j]*i+carry;
                a[j]=x%10;
                carry= x/10;
            }
            while(carry){
               
                a.push_back(carry%10);
                carry=carry/10;
            }
        }
        reverse(a.begin(),a.end());
        return a; 
    }
};


1047. Remove All Adjacent Duplicates In String---https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/submissions/1400500217/

1048. class Solution {
public:

    string removeDuplicates(string s) {
        // this approach is bad because pop back function removes elements from the last , not at the same index
        // int count=0;
        // for(int i=0;i<s.length()-1;i++){
        //     if(count>0){
        //         i=0;
        //     }
        //     if(s[i]==s[i+1]){
        //         s.pop_back();
        //         count++;
        //     }
        // }
        // return s; 
        string ans ="";
        int i=0;
        while(i<s.length()){
            if(ans.length()>0){
                if(ans[ans.length()-1]==s[i]){
                    ans.pop_back();
                }else{
                    ans.push_back(s[i]);
                }
            }else{
                ans.push_back(s[i]);
            }
            i++;
        }
        return ans;
    }
};

1047. Remove All Adjacent Duplicates In String---https://leetcode.com/problems/remove-all-occurrences-of-a-substring/
      class Solution {
public:

    string removeOccurrences(string s, string part) {

        int index = s.find(part);
       while(index!=string::npos){       
        s.erase(index,part.length());
        index = s.find(part);
       }
        return s;
    }
    
};

680. Valid Palindrome II  https://leetcode.com/problems/valid-palindrome-ii/description/

class Solution {
public:

    bool checkPalindrome(string s, int i, int j){
        while(i<=j){
            if(s[i]!=s[j]){
                return false;
            }else{
                s[i]==s[j];
                 i++;
                j--;
                           }

        }
        return true;
    }
    bool validPalindrome(string s) {
        int i=0;int n= s.length();
        int j=n-1;
        while(i<=j){
            if(s[i]==s[j]){
                // return true;// i made this mistake
                i++;
                j--;
            }else{
                return checkPalindrome(s, i+1, j)||checkPalindrome(s,i,j-1);
            }
        }
        return true;
        
    }
};
539. Minimum Time Difference----https://leetcode.com/problems/minimum-time-difference/description/
class Solution {
public:

    int findMinDifference(vector<string>& timePoints) {
        // step one is the conversion of the string to integer and storing 
        vector<int>minutes;int hour=0;int minute =0,time=0;int ans= INT_MAX;int diff=0;
        
        for(int i=0;i<timePoints.size();i++){
            // hour= stoi(timePoints.substr(1,2));// I can't do directly this 
            // min= stoi(timePoints.substr(4,2)); // first take the singal string from timePoints, then find the hour and min out of this.
            string curr = timePoints[i];
            hour= stoi(curr.substr(0,2));// "23:59" here the " double inverted isn't the character so start with the 0 index;
            minute= stoi(curr.substr(3,2));
            time = hour*60+minute;
           minutes.push_back(time);
        }
        sort(minutes.begin(), minutes.end());

       for(int i=0;i<minutes.size()-1;i++){
        diff = minutes[i+1]-minutes[i];
            ans = min(diff, ans);
       }

    // something is missing 
        diff= (minutes[0]+1440)-minutes[minutes.size()-1];
        ans = min(diff, ans);
        return ans;
    }
};
