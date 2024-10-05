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


5-  1047. Remove All Adjacent Duplicates In String---https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/submissions/1400500217/

 class Solution {
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

6   1047. Remove All Adjacent Duplicates In String---https://leetcode.com/problems/remove-all-occurrences-of-a-substring/
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

7    680. Valid Palindrome II  https://leetcode.com/problems/valid-palindrome-ii/description/

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
8   539. Minimum Time Difference----https://leetcode.com/problems/minimum-time-difference/description/
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

9    242. Valid Anagram---https://leetcode.com/problems/valid-anagram/description/

class Solution {
public:

    bool isAnagram(string s, string t) {
    //     // done by me in one attempt
    //     sort(s.begin(), s.end());
    //     sort(t.begin(), t.end());
    // //  for(int i=0;i<s.length();i++){
        
    // //  }   
    // if(s.compare(t)==0){
    //     return true;
    // }
    //  return false;
    
    //second method
    int hashTable[256]={0};
    for(int i=0;i<s.size();i++){
        hashTable[s[i]]++;
    }
    for(int i=0;i<t.size();i++){
        hashTable[t[i]]--;
    }
    for(int i=0;i<256;i++){
        if(hashTable[i]!=0){
            return false;// you can't return the true here and should not use the concept of the ==0 but should use !=0 and then return the false becuase we are storing the value and if the two string are not equal then it is not going to be 0 so in that casee we have to return the false,  case1 
        }
    }
    return true;
    }
};
10   917. Reverse Only Letters---https://leetcode.com/problems/reverse-only-letters/description/
class Solution {
public:

    string reverseOnlyLetters(string s) {
        int ch= '!';//97 122 65 90
        cout<<ch;
        int i=0;int j=s.size()-1;
        while(i<j){// you can check the alphabet is or not by isalpha stl function 
            if((s[i]>=65&&s[i]<=90||s[i]>=97&&s[i]<=122)&&(s[j]>=65&&s[j]<=90||s[j]>=97&&s[j]<=122)){
                swap(s[i],s[j]);
                i++;j--;
            }else if(!(s[i]>=65&&s[i]<=90||s[i]>=97&&s[i]<=122)){
                i++;
            }else if(!(s[j]>=65&&s[j]<=90||s[j]>=97&&s[j]<=122)){
                j--;
            }
        }
       
        return s; 
    }
};
11  14. Longest Common Prefix---https://leetcode.com/problems/longest-common-prefix/description/
class Solution {
public:

    string longestCommonPrefix(vector<string>& strs) {
        int i=0;
        string ans="";
        
        while(true){
            cout<<"ram";
            char char_str='\0';
           for(auto str : strs){
             if(i>=str.size()){
                char_str= '\0';
                break;
                }
                if(char_str=='\0'){
                    char_str=str[i];
                }else if(char_str!= str[i]){
                    char_str=0;
                    break; 
                }
           }
            
            if(char_str=='\0'){
                break;
            }
            ans.push_back(char_str);
            i++;
        }
        return ans;
    }
};
12-345. Reverse Vowels of a String---https://leetcode.com/problems/reverse-vowels-of-a-string/description/
class Solution {
public:

    bool isVowel(char ch){
     if(ch=='a'||ch=='e'||ch=='i'||ch=='o'||ch=='u'||ch=='A'||ch=='E'||ch=='I'||ch=='O'||ch=='U'){
    return true;
    }
    return false;
    }
    string reverseVowels(string s) {
       int i=0, j=s.size()-1;
        while(i<=j){
            if(isVowel(s[i])&&isVowel(s[j])){
                swap(s[i],s[j]);
                i++;j--;
            }else if(!(isVowel(s[i]))){
                i++;
            }else{
                j--;
            }
        }
        return s;
    }
};
13   https://leetcode.com/problems/isomorphic-strings/submissions/    ---205. Isomorphic Strings
class Solution {
public:

    bool isIsomorphic(string s, string t) {
        int hash[256]= {0};// mapping of each char of language 's' to language 't'
        bool istCharsMapped[256]= {0};// stores if t[i] char already mapped with s[i].
        for(int i=0;i<s.size();i++){
            if(hash[s[i]] == 0 && istCharsMapped[t[i]]==0){
                hash[s[i]]= t[i];
                istCharsMapped[t[i]]=true;
            }
        }
        for(int i=0;i<s.size();i++){
            if(hash[s[i]] !=t[i]){
              return false;
            }
        }
        return true;
    }
};
14  767. Reorganize String  --https://leetcode.com/problems/reorganize-string/description/
class Solution {
public:

    string reorganizeString(string s) {
        int hash[26]={0};char curr_char=0;
        for(int i=0;i<s.size();i++){
            hash[s[i]-'a']++;
        }
        int max =INT_MIN;
        for(int i=0; i<26;i++){
            if(hash[i]>max){
                max=hash[i];
            curr_char = i+'a';
            // cout<<curr_char;
            }
        }
        int index =0;
        while(max>0&&index<s.length()){// max>=0 i have done this and also i have done the index<=s.size()
            
            s[index]=curr_char;
            index=index+2;
            max--;
        }
        if(max!=0){
            return "";
        }
        hash[curr_char-'a']=0;
        // putting in the rest of the char into the string ;
        
        for(int i=0;i<26;i++){
           while(hash[i]>0){
                index=index>=s.size()?1:index;
                s[index]=i+'a';
                hash[i]--;
                index=index+2;

            }
        }
        return s;
    }
};
15   5 Longest Palindromic Substring    https://leetcode.com/problems/longest-palindromic-substring/
class Solution {
public:  // later doing it with the dynamic programming I have done this now by the brute force

        bool isPalindrome(string&s, int i, int j){
            while(i<j){
                if(s[i]!=s[j]){
                    return false;
                }
                i++;j--;
            }
            return true;
        }
    string longestPalindrome(string s) {
        string ans= "";
        for(int i=0; i<s.size();i++){
            for(int j=i;j<s.size();j++){
                if(isPalindrome(s,i,j)){
                    string t= s.substr(i,j-i+1);
                    ans= t.size()>ans.size()?t:ans; 
                }
            }
        }
        return ans;
    }
};
16  49. Group Anagrams   https://leetcode.com/problems/group-anagrams/description/
class Solution {
public:

    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>>ans;
        map<string,vector<string>>mp;// i had made the mistake her that why though i was calling the right way , but it was not getting matching with what i was passing .
        for(auto str: strs){
            string st= str;
            cout<<st;
            sort(st.begin(),st.end());
            mp[st].push_back(str);
        }

            for(auto i=mp.begin();i!=mp.end();i++){
                ans.push_back(i->second);
            }

        return ans; 
    }
};
17  . Find the Index of the First Occurrence in a String(28)    https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/
class Solution {
public:

    int strStr(string haystack, string needle) {
        // done by me method 1
        // int ans= haystack.find(needle);
        // method 2 done by the me 
        for(int i=0;i<haystack.size();i++){ // you can also do here the haystack.size()-needle.size() because we are not needed  to traverse to the last element in the sliding window.
                    for(int j=0;j<needle.size();j++){
                if(needle[j]!=haystack[i+j]){
                    break;
                }
                if(j+1==needle.size()){
                    return i;
                }

            }
        }
        return -1;
    }
};
18  204. Count Primes    https://leetcode.com/problems/count-primes/
class Solution {
public:

    int countPrimes(int n) {
        // vector<long long int>v(n,1);
        // long long int count=0;
        // if(n==1||n==0){
        //     return false;
        // }
        // for(long long int i=2;i<n;i++){
        //     if(v[i]==1){
        //         for(long long int j=i*i;j<n;j+=i){
        //             v[j]=0;// you are mistaking here why are you doing v[i]you should v[j]
        //     }
        //     }
        // }
        // for(int i=2;i<n;i++){
        //     if(v[i]==1){
        //         count++;
        //     }
        // }
        // return count;

         vector< int>v(n,1);
         int count=0;
        if(n==1||n==0){
            return false;
        }
        for(int i=2;i<n;i++){

            if(v[i]==1){
                int j=2*i;// here i am not doing the long long int and it is alternative to avoid the long long
                for( ;j<n;j=j+=i){
                    v[j]=0;// you are mistaking here why are you doing v[i]you should v[j]
            }
            }
            
        }
        for(int i=2;i<n;i++){
            if(v[i]==1){
                count++;
            }
        }
        return count;
        
    }
};
19   GCD of two number (gfgs)   https://www.geeksforgeeks.org/problems/gcd-of-two-numbers3459/1
class Solution {
  public:
  
    int gcd(int a, int b) {
        // code here
        while(a>0&&b>0){
            if(a>b){
                a=a-b;
            }else
            b=b-a;
        }
        return a==0?b:a;
    }
};

20    8. String to Integer (atoi)   https://leetcode.com/problems/string-to-integer-atoi/
class Solution {
public:

    int myAtoi(string s) {
        int ans=0; int i=0; int sign=1;
        while(s[i]==' '){
            i++;
        }
        while(i<s.size()&&(s[i]=='+'||s[i]=='-')){
            sign=s[i]=='+'?1:(-1);
            i++;
            break;
        }
        while(i<s.size()&&isdigit(s[i])){
            if(ans>INT_MAX/10||ans==INT_MAX/10&&s[i]>'7'){// this is used to go till the extent our number is near to the greatest limit.
                return sign ==-1?INT_MIN: INT_MAX;
            }
                ans= ans*10 + (s[i]-'0');
            i++;
        }
        return ans*sign;
    }
};

21    443. String Compression  https://leetcode.com/problems/string-compression/
class Solution {
public:
// this is done by me but not as efficient solution so i am sharing below the more efficient.

    int compress(vector<char>& chars) {
        if(chars.size()==0){
            return 0;
        }
        int prev =chars[0];int count=1;
        int index=0;
        for(int i=1;i<chars.size();i++){
            if(chars[i]==prev){
                count++;
            }else{
                chars[index]=prev;index++;
                int start= index;
                if(count>1){
                    while(count){  chars[index++]=count%10+'0'; 
                     count= count/10;}
                       }
                       reverse(chars.begin()+start, chars.begin()+index);
            count=1;   
            }
              prev=chars[i];
        }
       
        chars[index++]= prev;
         int start= index;
       while(count>1){
            while(count){  chars[index++]=count%10+'0'; 
            count= count/10;}
                       }
                        reverse(chars.begin()+start, chars.begin()+index);
        return index;
        
    }
};

// this is the another solution 
class Solution {
public:
    int compress(vector<char>& chars) {
        int ans = 0;

        // iterate through input vector using i pointer
        for (int i = 0; i < chars.size();) {
            const char letter = chars[i]; // current character being compressed
            int count = 0; // count of consecutive occurrences of letter

            // count consecutive occurrences of letter in input vector
            while (i < chars.size() && chars[i] == letter) {
                ++count;
                ++i;
            }

            // write letter to compressed vector
            chars[ans++] = letter;

            // if count is greater than 1, write count as string to compressed vector
            if (count > 1) {
                // convert count to string and iterate over each character in string
                for (const char c : to_string(count)) {
                    chars[ans++] = c;
                }
            }
        }

        // return length of compressed vector
        return ans;
    }
};
22  12. Integer to Roman  https://leetcode.com/problems/integer-to-roman/
class Solution {
public:

    string intToRoman(int num) {
        string ans="";
        string  roman[] = {"M", "CM", "D" , "CD","C", "XC", "L","XL","X","IX","V","IV","I" };
        int value[]={1000,900,500,400,100,90,50,40,10,9,5,4,1};
        int n =sizeof(value) / sizeof(int);
        for(int i=0;i<n;i++){
            while(num>=value[i]){
                ans=ans+roman[i];
                num=num-value[i];
            }
        }
        return ans;
    }
};
23  658. Find K Closest Elements    https://leetcode.com/problems/find-k-closest-elements/
class Solution {
public:

    vector<int>twoPointer(vector<int>& arr, int k, int x){
        int l=0,z=arr.size()-1;
        // for(int i=0;i<arr.size();i++){

        // }
        while(z-l>=k){
            if(x-arr[l]>arr[z]-x){
                l++;
            }else{
                z--;
            }
          cout<<"ram";
        }
        //  vector<int>ans;
        //  for(int i=l;i<=z;i++){
        //     ans.push_back(arr[i]);

        //  }
        //  return ans; another way of returning the ouput without using the extra space.

        return vector<int>(arr.begin()+l, arr.begin()+z+1);
    }
    vector<int> findClosestElements(vector<int>& arr, int k, int x) {
        // return vector<int>twoPointer(vector<int> arr, int k, int x); the mistake i was doing 
        return twoPointer(arr,k, x); //the mistake i was doing 

    }
};
