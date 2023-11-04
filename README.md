# Recursively-Remove-all-Adjacent-Duplicate-Characters-in-CPP  

Remove all Adjacent Duplicate Characters Recursively in C++
Here, in this page we will discuss the program to remove all adjacent duplicate characters recursively in C++ programming language. We are given with an string and need to return the string after removing all its adjacent duplicate characters.

Example :

Input : str = “aabaabccded”
Output : e
Remove all Adjacent Duplicate Characters recursively in C++
Method 1 :
In this algorithm we will discuss the recursive way to remove all  duplicate character from the given input string s.

First we check whether the String remStr has the repeated character that matches the last char of the parent String.
If that is so then we have to keep removing that character before concatenating string s and string remStr.
Remove all adjacent duplicates
Code to Recursively Remove all Adjacent Duplicate in C++
Run
#include <bits/stdc++.h>
using namespace std;

string removeDuplicates(string s, char ch)
{

   // Base condition
   if (s.length() <= 1) {
       return s;
   }

   int i = 0;
   while (i < s.length()) {
      if (i + 1 < s.length() && s[i] == s[i + 1]) {
         int j = i;
         while (j + 1 < s.length() && s[j] == s[j + 1]) { 
             j++; 
             
         } 
         char lastChar = i > 0 ? s[i - 1] : ch;

         string remStr = removeDuplicates(
         s.substr(j + 1, s.length()), lastChar);

         s = s.substr(0, i);
         int k = s.length(), l = 0;

         while (remStr.length() > 0 && s.length() > 0 && remStr[0] == s[s.length() - 1]) 
         {

             while (remStr.length() > 0 && remStr[0] != ch && remStr[0] == s[s.length() - 1]) {
                   remStr = remStr.substr(1, remStr.length());
             }
             s = s.substr(0, s.length() - 1);
         }
         s = s + remStr;
         i = j;
    }
    else {
         i++;
    }
  }
  return s;
}

// Driver Code
int main()
{

   string str1 = "aabbaaacdffd";
   cout << removeDuplicates(str1, ' ') << endl;
}
Output :

c
Method 2 (Using Stack) :
In this method we will use Stack as it follows last in first out (LIFO) mechanism.

Declare a stack of char type say stck.
Now, iterate the string str and for every i-th character,
Check if stck.empty() == true and stck.top() != str[i]. Then, push str[i] into stack.
Otherwise pop() the element from the stack.
Now, check if stck.empty() == true then print(“Empty String”)
Otherwise, declare a string say result=””
Run a loop till stck.empty()==false,
And set, result = stck.top()+ result.
At last print(result)
Code in C++
Run
#include<bits/stdc++.h>
using namespace std;

//Function to remove Duplicates
string removeDuplicates(string str){

   stack<char>stck;

   for(int i=0; i< str.length(); i++){

      if(stck.empty() or stck.top()!= str[i])
        stck.push(str[i]);

      else stck.pop();
   }

   if(stck.empty())
     return "Empty String";

    string result = "";

    while(!stck.empty()){
         result = stck.top()+result;
         stck.pop();
    }

    return result;
}


//Driver Code
int main(){
    string str="aacbbcaaded";
    cout<< removeDuplicates(str);
}
Output :

ded
