---
layout: post
title:  "Yujin's Diary"
date:   2019-11-22 21:03:36 +0530
categories: 전화번호부 비디오가게 
---
I am Jeong Yu Jin majoring in media engineering at Kangwon National University. 

---나의 경험 ---
나의 경험으로는 전화번호부를 만들어 많은 사람들에게 편리함과 편의를 제공하였다. 

```javascript
#include <stdio.h> 
#include <string.h>

#define SIZE 100

typedef struct phoneBook
{
	char pName[SIZE];
	char pNumber[SIZE];
}PHONEBOOK;

void initialize(struct phoneBook PHONEBOOK[]); //변수를 초기화, 설정하겟다는 뜻 포인터로 값을 넘겨주니까 반환 값 없어도 됨.
void selectMenu(struct phoneBook PHONEBOOK[]); //포인터로 값을 넘겨주니까 반환 값 없어도 됨.
int getIndex(struct phoneBook PHONEBOOK[]); //내가 어느 배열에 넣어야 되는지 선택하게 해주는 함수.


void addAddress(struct phoneBook PHONEBOOK[]); //전화번호부 추가하기 함수.
void showAddress(struct phoneBook PHONEBOOK[]); //전체 전화번호부 보여주기.
void searchAddress(struct phoneBook PHONEBOOK[]); //전화번호부 검색하기.
void removeAddress(struct phoneBook PHONEBOOK[]); //전화번호부 삭제하기.

int search(struct phoneBook PHONEBOOK[], char pNumber[]); //검색하기 함수. 추후 삭제  때 같이 사용해야해서 따로 만듬. 


int main()
{
	struct phoneBook PHONEBOOK[SIZE];

	initialize(PHONEBOOK);

	selectMenu(PHONEBOOK);
	return 0;
}

void initialize(struct phoneBook PHONEBOOK[])
{

	for (int i = 0; i < SIZE; i++)
	{
		strcpy(PHONEBOOK[i].pName, "."); //.으로 문자를 바꾸겠다
		strcpy(PHONEBOOK[i].pNumber, ".");
	}
}

void selectMenu(struct phoneBook PHONEBOOK[]) // 
{
	int select;

	while (1)
	{
		printf("\n\n");
		printf("1. 전화번호부 추가하기\n");
		printf("2. 전화번호부 출력하기\n");
		printf("3. 전화번호부 검색하기\n");
		printf("4. 전화번호부 삭제하기\n");
		printf("5. 전화번호부 종료하기\n");
		printf("원하는 번호를 입력하세요 >>>>> ");
		scanf("%d", &select);

		switch (select)
		{
		case 1:
		{
			addAddress(PHONEBOOK);
			break;
		}
		case 2:
		{
			showAddress(PHONEBOOK);
			break;
		}
		case 3:
		{
			searchAddress(PHONEBOOK);
			break;
		}
		case 4:
		{
			removeAddress(PHONEBOOK);
			break;
		}
		case 5:
		{
			return;
			break;
		}
		default:
		{
			printf("올바르지 않은 키 입력");
			break;
		}
		}
	}
}




int getIndex(struct phoneBook PHONEBOOK[])
{
	for (int i = 0; i < SIZE; i++)
	{
		if (strcmp(PHONEBOOK[i].pName, ".") == 0)// true
		{
			return i;
			break;
		}
	}
	return -1;
}

void addAddress(struct phoneBook PHONEBOOK[])
{

	char pName[SIZE];
	char pNumber[SIZE];

	int index = getIndex(PHONEBOOK);
	int result;


	printf("\n\n====전화번호부 입력 ====\n\n");
	if (index == -1)
	{
		printf("용량이 가득 찼습니다. 죄송합니다.\n\n");
		return;
	}

	printf("이름을 입력하시오 : ");
	scanf("%s", pName);

	printf("전화번호를 입력하시오 : ");
	scanf("%s", pNumber);


	result = search(PHONEBOOK, pNumber);

	if (result == -1)
	{
		strcpy(PHONEBOOK[index].pName, pName);
		strcpy(PHONEBOOK[index].pNumber, pNumber);
		printf("추가 하였습니다.!\n");

	}
	else //-1 아닌 모두 
	{
		printf("입력한 %s는 이미 존재합니다.\n\n", pNumber);
		printf("이름 : %s\n", PHONEBOOK[result].pName);
		printf("번호 : %s\n", PHONEBOOK[result].pNumber);
		return;
	}

}


void showAddress(struct phoneBook PHONEBOOK[])
{
	printf("\n\n====전화번호부 출력 ====\n\n");
	for (int i = 0; i < SIZE; i++)
	{
		if (strcmp(PHONEBOOK[i].pName, ".") == 0) //글자가 . 인 애들은 건너 뛰어야함.
		{
			continue;
		}
		printf("이름 : %s\n", PHONEBOOK[i].pName);
		printf("번호 : %s\n", PHONEBOOK[i].pNumber);
		printf("\n\n");
	}
}

void searchAddress(struct phoneBook PHONEBOOK[])
{
	char pNumber[SIZE];
	int result;
	printf("검색하고자 하는 전화번호를 입력하시오 : ");
	scanf("%s", pNumber);

	result = search(PHONEBOOK, pNumber);

	if (result == -1)
	{
		printf("%s 로 검색한 결과를 찾을 수 없습니다.", pNumber);
		return;
	}


	printf("\n\n====전화번호부 검색 출력 ====\n\n");
	printf("이름 : %s\n", PHONEBOOK[result].pName);
	printf("번호 : %s\n", PHONEBOOK[result].pNumber);
	return;
}

void removeAddress(struct phoneBook PHONEBOOK[])
{
	char pNumber[SIZE];
	int result;
	printf("삭제하고자 하는 전화번호를 입력하시오 : ");
	scanf("%s", pNumber);

	result = search(PHONEBOOK, pNumber);

	if (result == -1)
	{
		printf("%s 로 검색한 결과를 찾을 수 없습니다.", pNumber);
		return;
	}


	printf("\n\n====전화번호부 삭제 출력 ====\n\n");
	strcpy(PHONEBOOK[result].pName, ".");
	strcpy(PHONEBOOK[result].pNumber, ".");

	printf("%s의 정보를 삭제하였습니다.", pNumber);
	return;
}

int search(struct phoneBook PHONEBOOK[], char pNumber[])
{
	for (int i = 0; i < SIZE; i++)
	{
		if (strcmp(PHONEBOOK[i].pNumber, pNumber) == 0)
		{
			return i;
			break;
		}
	}
	return -1;
}

// capture request
rzp.capture(payment_id, cost)
	.then(function (data) {
		return 2;
	})
```

이렇게 전화번호부를 만들었으며 비슷하게 파일입출력을 이용하여 비디오가게도 만든 경험이 있다. 여러번의 코드를 작성하면서 나 또한 많이 성장하였으며 취미로 코딩을 공부하는 계기가 되기도 하였다.



[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
