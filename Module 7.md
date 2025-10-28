EXP NO:1 C PROGRAM FOR ARRAY OF STRUCTURE TO CHECK ELIGIBILITY FOR THE VACCINE.

Aim:
To write a C program for array of structure to check eligibility for the vaccine person age above 6 years of age.

Algorithm:
1.	Declare structure eligible with age (integer) and n (character array)
2.	Declare variable e of type eligible
3.	Input age and name using scanf, store in e
4.	If e.age <= 6
-	Print "Vaccine Eligibility: No"
Else
-	Print "Vaccine Eligibility: Yes"
5.	Print details (e.age, e.n)
6.	Return 0
 
Program:
```
#include <stdio.h>

struct Person {
    char name[50];
    int age;
};

int main() {
    int n, i;

    printf("Enter the number of people: ");
    scanf("%d", &n);

    struct Person people[n]; 
    for(i = 0; i < n; i++) {
        printf("\nEnter details for person %d:\n", i + 1);
        printf("Name: ");
        scanf(" %[^\n]s", people[i].name);
        printf("Age: ");
        scanf("%d", &people[i].age);
    }

    printf("\nVaccine Eligibility:\n");
    for(i = 0; i < n; i++) {
        if(people[i].age > 6) {
            printf("%s (Age %d) is eligible for the vaccine.\n", people[i].name, people[i].age);
        } else {
            printf("%s (Age %d) is NOT eligible for the vaccine.\n", people[i].name, people[i].age);
        }
    }

    return 0;
}
```


Output:


<img width="637" height="694" alt="image" src="https://github.com/user-attachments/assets/0477aecd-8d32-4572-85c3-3cfebfe3c259" />


Result:
Thus, the program is verified successfully. 



EXP NO:2 C PROGRAM FOR PASSING STRUCTURES AS FUNCTION ARGUMENTS AND RETURNING A STRUCTURE FROM A FUNCTION
Aim:
To write a C program for passing structure as function and returning a structure from a function

Algorithm:
1.	Define structure numbers with members a and b.
2.	Declare variable n of type numbers.
3.	Prompt the user to enter values for a and b.
4.	Input values for a and b into n using scanf.
5.	Call the add function with n as an argument.
6.	Print the result returned by the add function.
7.	Return 0
 
Program:
```
#include <stdio.h>
#include <string.h>

struct Person {
    char name[50];
    int age;
    int eligible;
};

struct Person checkEligibility(struct Person p) {
    if (p.age > 6) {
        p.eligible = 1; 
    } else {
        p.eligible = 0;
    }
    return p; 
}

int main() {
    struct Person p;

    printf("Enter name: ");
    scanf(" %[^\n]s", p.name); 
    printf("Enter age: ");
    scanf("%d", &p.age);

    p = checkEligibility(p);

    if(p.eligible) {
        printf("%s (Age %d) is eligible for the vaccine.\n", p.name, p.age);
    } else {
        printf("%s (Age %d) is NOT eligible for the vaccine.\n", p.name, p.age);
    }

    return 0;
}

```





Output:


<img width="621" height="302" alt="image" src="https://github.com/user-attachments/assets/b957cef9-9bf7-424d-82b3-d038d27d2bbc" />





Result:
Thus, the program is verified successfully


 
EXP.NO:3 C PROGRAM TO READ A FILE NAME FROM USER AND WRITE THAT FILE USING FOPEN()

Aim:
To write a C program to read a file name from user

Algorithm:
1.	Include the necessary header file stdio.h.
2.	Begin the main function.
3.	Declare a file pointer p.
Declare a character array name to store the file name.
4.	Prompt the user to enter a file name.
Use scanf to input the file name into the name array.
5.	Print a message indicating that the file with the specified name has been created successfully.
6.	Use fopen to open a file with the name provided by the user in write mode ("w").
-	If successful, continue to the next step.
-	If unsuccessful, print an error message and exit the program with a non-zero status.
1.	Print a message indicating that the file has been opened successfully.
2.	Use fclose to close the file.
3.	Print a message indicating that the file has been closed.
4.	End the main function.
5.	Return 0 to indicate successful program execution.
 
Program:

 ```
#include <stdio.h>

int main() {
    char filename[100];
    FILE *file;

    printf("Enter the file name to open: ");
    scanf("%s", filename);

    file = fopen(filename, "r");
    if (file == NULL) {
        printf("Error: Could not open file %s\n", filename);
        return 1;
    }

    printf("File %s opened successfully.\n", filename);

    // Close the file
    fclose(file);
    return 0;
}


```




Output:


<img width="587" height="296" alt="image" src="https://github.com/user-attachments/assets/8d7e16e0-a529-4b75-b72d-72c5cdce59b0" />












Result:
Thus, the program is verified successfully
 


EXP NO:4   PROGRAM TO READ A FILE NAME FROM USER, WRITE THAT FILE AND INSERT TEXT IN TO THAT FILE
Aim:
To write a C program to read, a file and insert text in that file
Algorithm:
1.	Include the necessary header file stdio.h.
2.	Begin the main function.
3.	Declare a file pointer p.
Declare character arrays name and text. Declare an integer variable num.
4.	Prompt the user to enter a file name and the number of strings.
Use scanf to input the file name into the name array and the number of strings into the num variable.
5.	Use fopen to open a file with the name provided by the user in write mode ("w").
-	If successful, continue to the next step.
-	If unsuccessful, print an error message and exit the program with a non-zero status.
6.	Print a message indicating that the file has been opened successfully.
1.	Use a loop to input strings from the user and write them to the file using fputs.
2.	Use fclose to close the file.
3.	Print a message indicating that data has been added successfully.
4.	End the main function.
5.	Return 0 to indicate successful program execution.
 
Program:
```
#include <stdio.h>

int main() {
    char filename[100];
    char text[500];
    FILE *file;

    printf("Enter the file name: ");
    scanf("%s", filename);

    file = fopen(filename, "r");
    if (file == NULL) {
        printf("File does not exist. A new file will be created.\n");
    } else {
        printf("\nCurrent contents of %s:\n", filename);
        char ch;
        while ((ch = fgetc(file)) != EOF) {
            putchar(ch);
        }
        fclose(file);
        printf("\n");
    }
    file = fopen(filename, "a");
    if (file == NULL) {
        printf("Error opening file for writing.\n");
        return 1;
    }

    printf("Enter text to insert into the file (end with a newline):\n");
    getchar(); // To consume leftover newline from previous input
    fgets(text, sizeof(text), stdin); 
    fprintf(file, "%s", text); 
    fclose(file);

    printf("Text successfully inserted into %s.\n", filename);
    return 0;
}



```


Output:
<img width="604" height="310" alt="image" src="https://github.com/user-attachments/assets/50e42332-796b-4f5e-8861-3c2457f0d5ac" />









Result:
Thus, the program is verified successfully



Ex No 5 : C PROGRAM TO DISPLAY STUDENT DETAILS USING STRUCTURE

Aim:
The aim of this program is to dynamically allocate memory to store information about multiple subjects (name and marks), input the details for each subject, and then display the stored information. Finally, it frees the allocated memory to prevent memory leaks.

Algorithm:
1.Input the number of subjects.

2.Read the integer value n from the user, which represents the number of subjects.

3.Dynamically allocate memory:

4.Use malloc to allocate memory for n subjects. Each subject has a name (array of characters) and marks (integer).

5.If memory allocation fails (i.e., the pointer s is NULL), display an error message and exit the program.

6.Input the details of each subject

7.Use a for loop to read the name and marks of each subject using scanf. For each subject, store the name as a string and marks as an integer in the dynamically allocated memory.

8.Display the details of each subject

9.Use another for loop to print the name and marks of each subject.

10.Free the allocated memory

11.After all operations are done, call free(s) to release the dynamically allocated memory.

12.Return from the main function

13.End the program by returning 0.

Program:
```
#include <stdio.h>

struct Student {
    char name[50];
    int rollNo;
    float marks;
};

int main() {
    int n, i;

    printf("Enter the number of students: ");
    scanf("%d", &n);

    struct Student students[n]; 

    for(i = 0; i < n; i++) {
        printf("\nEnter details for student %d:\n", i + 1);

        printf("Name: ");
        scanf(" %[^\n]s", students[i].name); 

        printf("Roll Number: ");
        scanf("%d", &students[i].rollNo);

        printf("Marks: ");
        scanf("%f", &students[i].marks);
    }

    printf("\nStudent Details:\n");
    printf("S.No\tName\t\tRoll No\tMarks\n");
    printf("-------------------------------------------\n");
    for(i = 0; i < n; i++) {
        printf("%d\t%s\t\t%d\t%.2f\n", i + 1, students[i].name, students[i].rollNo, students[i].marks);
    }

    return 0;
}
```





Output:







<img width="613" height="805" alt="image" src="https://github.com/user-attachments/assets/52e99cfd-f876-47c8-99d4-99126e7e3b6a" />


Result:
Thus, the program is verified successfully
