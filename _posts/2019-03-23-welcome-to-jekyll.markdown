---
layout: post
title:  "Jeong Yujin's portfolio"
date:   2019-11-22 21:03:36 +0530
categories: 전화번호부 비디오가게 
---
I am Jeong Yu Jin majoring in media engineering at Kangwon National University.
To learn more about Jeong Yu-jin, press Jeong Yu-jin's portfolio.

2)자신이 가지고 있는 능력 ---
나는 전화번호부를 만든 경험이 있다. 전화번호부란 개개인의 이름과 연락처를 기재한 문서이다. 어느새 현대인들에게 필수 기능으로 자리잡은 전화번호부는 이 시대를 살아가는 많은 사람에게 꼭 필요한 존재가 되어버렸다. 전화번호부로 인해 사람들과 소통을 하며, 관련 정보를 찾고자 할 때 용이하게 쓸 수 있다는 장점이 있다. 전화번호부를 작성함으로써 저장하고 싶은 정보를 저장하고, 연락하고자 하는 상대방의 연락처를 검색하여 연락할 수 있으며 삭제하고자 하는 기능을 통해 불필요한 정보를 삭제할 수 있다. 이렇게 전화번호부를 만들어 많은 사람들에게 편리함과 편의를 제공하였다. 

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

3)자신의 경험 : 이렇게 전화번호부를 만들었으며 비슷하게 파일입출력을 이용하여 비디오가게도 만든 경험이 있다. 여러번의 코드를 작성하면서 나 또한 많이 성장하였으며 취미로 코딩을 공부하는 계기가 되기도 하였다. 프로그램을 짜는 것을 공부하기도 하지만 혼자서는 개인적으로 시를 즐겨쓰기도 한다. 평소에도 시집이나 소설로 독서를 많이 하는 편이고 틈만 나면 글을 쓰는 것을 좋아해서 나의 블로그에 시를 담아 보겠다.

```
창문
                          
창문을 열어 젖히니
새하얀 눈 꽃 송이
보송보송 보기 좋게도 내린다

너와도 함께 맞았던 첫 눈
그저 세상이 아름답게 보였던
그 때.

하염없이 내리는 눈을 
바라보다 너가 당장이라도 
내 앞에 내릴 것 같아
차마 이 창문을 닫지 못하겠다
```

```
달
                                  ella

예쁘게 뜬 달을 보아하니
그저 넋을 잃고 바라보게 되는구나

어찌 매일 조금씩 모양이 변하는 것인지
그저 신기하기만 하다

달의 모양이 바뀌는 것처럼
나를 향한 너의 마음도
조금씩 바뀌었으면 좋겠으련만

난 오늘의 이 예쁜 달도
너가 어디선가 바라볼 것이라
생각하기에 안심이 된다.
```

```
웃음
                          ella
당신의 웃음은
세상 그 어떤 무언가에도
감히 비교할 수 없습니다

당신이 웃을 때면
푸른 하늘 아래
쑥쑥 자라는 새싹처럼
나의 마음이 자라납니다

당신이 웃고 나면 
항상 당신에게 웃을 날만 있기를
나는 항상 기도합니다
```

4) 나의 관심분야, 관심직업 : 나는 코딩에 관심이 있지만 작가를 꿈꾸는 학생이다. 글을 쓰는 것을 좋아하는데 문학적으로만 뛰어나기 보다는 여러 방면으로 다양한 재능을 얻고 싶어 지금도 열심히 다방면으로 공부하고 있는 중이다. 미디어공학을 공부하면서 미디어와 컴퓨터 쪽으로 구체적으로 알아가고 있으며 대학생활을 하면서 얻게 되는 지식을 바탕으로 방송작가를 하여 공학적으로나 문학적으로나 뛰어난 작가가 되는 것을 희망하고 있다.


[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
