# Write a Simple List Main
This is a simple way to write a main to test your listed list functions. Follow the commented code.

## 1. Incluir bibliotecas
São usadas as bibliotecas `stidio` e `stdlib`.
```c
#include <stdio.h>
#include <stdlib.h>  
```

## 1.2 List Struct
In the case of Project Libft, this structure is defined in the header.h. But we can also declare it in the .c file to do tests.
```c
typedef struct    s_list
{
    struct s_list *next;
    void          *data;
}   
```

## 2. Lists creation
Creation of the lists that will be linked to each other. We already allocate the memory for them
This is also done in the lstnew() function, but this form is more direct to the point for tests.

```c
	t_list *l1 = (t_list *)malloc(sizeof(t_list));
	t_list *l2 = (t_list *)malloc(sizeof(t_list));
	t_list *l3 = (t_list *)malloc(sizeof(t_list));
```
We also created a temporary variable to travel the list when it will be printed. We use a temporary pointer for the list to keep the address of the first node. If we don't do this, we lost the address of the list and could not access it anymore.
```c
	t_list *temp;
```
## 3. Declare int Values
I think the easiest way to test is using int values.
```c
	int a = 1;
	int b = 2;
	int c = 3;
```

## 4. Assign ints to lists
Now we have attributed the ints into the Void *Data lists. It is necessary to make the cast. We need to do this because date on Struct is a Void Pointer type. If it were int, we could do L1-> Data = 10;
```c
	l1->data = (void *)&a;
	l2->data = (void *)&b;
	l3->data = (void *)&c;
```
## 5. Linking Lists
List linkage. The last list should point to null.
```c
	l1->next = l2;
	l2->next = l3;
	l3->next = NULL;
```
## 6. Printing List
Now we will print the content of `Data` in each knot on the list to see if everything is right. As the list is Void Pointer type, we need to make the cast for int. Remembering that we go throught `Temp` and not` L1`, because if we go through L1, we lost the address of the list and could no longer access it.
```c
	temp = l1;
	while (temp)
	{
		printf("%d\n", *(int *)temp->data);
		temp = temp->next;
	}
```
## 7. Free Lists
In the end, we released the memory allocated to the lists
```c
	free(l1);
	free(l2);
	free(l3);
```

In this repository folder I left a example called lsts_main.c. If you want to see more lists exercises and examples, [here](https://github.com/waltergcc/42-Piscine/tree/main/C12) is a link to my C12 folder, where I did all the exercises that only work with linked lists.

It's all! :smile:
