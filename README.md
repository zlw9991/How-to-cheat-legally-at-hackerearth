# How to "cheat" legally at hacker earth
Useful techniques to extract information from internal &amp; hidden test cases in hackerearth.

![Optional Text](/pictures/1.png)

# Exploiting the limited information given.

Usually, when the tester uses hidden and internal test cases, you will not be able to compare outputs to determine precisely what went wrong with your code.

However, hackerearth usually presents us with information (which is not simply binary) in the format of time taken (Time(sec)), and memory (Memory (KiB)) used.

![Optional Text](/pictures/2.PNG)

Thus, it is possible to manipulate the text output in a way which effects these two variables, in order to gain a degree of insight as to what the hidden / test case is inputting into you code.

The first method I will cover involves manipulating the time it takes for the code to run, which will in turn give us some information on what is being input.

The second method which might be plausible (manipulating memory) is something I have not tried yet.

This guide will assume the usage of the C programming language, use equivalent functions for other languages.

# Using the manipulation of the output time.

In this code example , the first input '5' is just a key item to be found in the linked list. The next line of input '8 1 5 5 7 2 5 a' produces the linked list with said numeric values (without the 'a').

![Optional Text](/pictures/3.PNG)

For hidden test cases, what can I find information on the line of input it uses to produce the linked list?

This is a list of values which can be inferred (roughly) from the time (sec) it takes to output after manipulation:
- number of inputs 
- number of items which are of the same value as the key item
- number of items greater than the key item
- number of items smaller than the key item

This method is only ineffective when there is a large amount of inputs (Time limit exceeded).

# Finding number of inputs:

```
#include <unistd.h> // add this header to be used for the rest of the code samples

void printList(ListNode *head){
	int cntr = 0;
    while(head !=NULL){
        head = head->next;
        cntr++;
    }
	usleep((cntr*1000*100)); // usleep uses microseconds, this turns it to 0.1 seconds
    printf("\n");
}
```

![Optional Text](/pictures/4.PNG)

Thus, we can infer for example, there are 7 inputs in the linked list for input 1.

# Finding number of items greater than the key item

```
void printList(ListNode *head,int pivot){ // include the key item which is to be compared to
	int cntr = 0;
    while(head !=NULL){
		if(head->item > pivot){
			cntr++;
		}
        head = head->next;
    }
	usleep((cntr*1000*100)); // usleep uses microseconds, this turns it to 0.1 seconds
    printf("\n");
}
```

![Optional Text](/pictures/5.PNG)

Thus, we can infer for example, there are 3 inputs greater than the key item in the linked list for input 1.


# Finding number of items lesser than the key item

```
void printList(ListNode *head,int pivot){ // include the key item which is to be compared to
	int cntr = 0;
    while(head !=NULL){
		if(head->item < pivot){
			cntr++;
		}
        head = head->next;
    }
	usleep((cntr*1000*100)); // usleep uses microseconds, this turns it to 0.1 seconds
    printf("\n");
}
```

![Optional Text](/pictures/6.PNG)

Thus, we can infer for example, there are 4 inputs lesser than the key item in the linked list for input 1.


# Finding number of items equal to the key item

```
void printList(ListNode *head,int pivot){ // include the key item which is to be compared to
	int cntr = 0;
    while(head !=NULL){
		if(head->item == pivot){
			cntr++;
		}
        head = head->next;
    }
	usleep((cntr*1000*100)); // usleep uses microseconds, this turns it to 0.1 seconds
    printf("\n");
}
```

![Optional Text](/pictures/7.PNG)

Thus, we can infer for example, there are 0 inputs equal to the key item in the linked list for input 1.

# Proof:

Looking at the pictures, we can see for example, for input 2:
- There are 7 inputs
- 2 are greater than the key item 
- 2 are equal to the key item
- 3 are smaller than the key item

# Using memory
WIP (Someday)
