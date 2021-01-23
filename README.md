
# 三子棋.c

    #include"game.h"
    void menu()
    {
	printf("*********************\n");
	printf("****1.play 0.exit****\n");
	printf("*********************\n");
      }
    void game()
    {
    char temp = '0';
	  char board[row][line] = { 0 };//初始化棋盘
	  Fill_Arr(board, row, line);//同上
	  Border_Print(board, row, line);//打印棋盘
	  while (1)
	  {
		PlayerChoice(board, row, line);//玩家下棋
		Border_Print(board, row, line);//打印棋盘
		temp = Iswin(board, row, line);
		if (temp != 'C')
		{
			break;
		}
		ComputerChoice(board, row, line);//电脑下棋
		Border_Print(board, row, line);//打印棋盘
		temp = Iswin(board, row, line);
		if (temp != 'C')
		{
			break;
		}
	  }
	  if (temp == '*')
	  {
		 printf("玩家胜利。\n");

	  }
	  if (temp == '@')
	  {
		  printf("电脑胜利。\n");

	  }
	  if (temp == 'P') 
	  {
  		printf("平局。\n");
 
	  }

    }
    void text()
    {
	   int input = 0;
	   srand((unsigned int)time(NULL));
	   do
	  {
		menu();
		printf("请选择：");
		scanf("%d", &input);
		switch (input)
		{
		case 1:printf("三子棋\n");
			game();
			break;
		case 0:printf("退出游戏\n");
			
			break;
		default:printf("选择错误，重新选择\n");
			break;

		}
	  } while (input);

    }

    int main()
    {

	   text();

	  return 0;
    }
  
## game.h

    #pragma once
    #define row 3
    #define line 3
    #include<stdio.h>
    #include<stdlib.h>
    #include<time.h>
    void Fill_Arr(char board[row][line], int a, int b);
    void Border_Print(char board[row][line], int a, int b);
    void PlayerChoice(char board[row][line], int a, int b);
    void ComputerChoice(char board[row][line], int a, int b);
    int Iswin(char board[row][line], int a, int b);
    int IsFull(char board[row][line], int a, int b);

### game.c
    #include"game.h"
        void Fill_Arr(char board[row][line],int a,int b)
    {
    	int i;
    	int j;
    	for (i = 0; i < a; i++)
    	{
    		for (j = 0; j < b; j++)
    		{
    			board[i][j] = ' ';
		    }
    	}    
    }
    void Border_Print(char board[row][line],int a,int b )
    {
    	int i;
    	int j;
    	int o;
                	for (i = 0; i <a; i++)
        	{
    
    		for (j = 0; j < line; j++)
		{
			printf(" %c ", board[i][j]);
			if (j !=b - 1)
				printf("|"); 

		}
		printf("\n");
		if (i != a - 1)    
		{
			for (o = 0; o < a; o++)
			{
				printf("---");
				if (o != a - 1)
					printf("|");
			}
			printf("\n");
	    	}
    	}
    }
    void PlayerChoice(char board[row][line], int a, int b)
    {
    	int x;
    	int y;
    	x = 0;
    	y = 0;
    	printf("请选择你要放置棋子的位置：");
    	
    	while (1)
    	{
        scanf("%d%d", &x, &y);
    		if (x >= 1 && x <= 3 && y >= 1 && y <= 3)
    		{
    			if (board[x - 1][y - 1] == ' ')
    			{
    				board[x - 1][y - 1] = '*';
    				break;
    			}
    			else
    			{
    				printf("这个位置已经有棋子，重新选择：");
    			}
    		}
    		else
    		{
    			printf("你所选择的格子超出范围，请重新选择：");
    		}
    	}
    
    }
    void ComputerChoice(char board[row][line], int a, int b)
    {
    	int x = 0;
	    int y = 0;
    	printf("电脑选择图标为@,电脑选择如下\n");
	    while (1)
	    {
	    	x = rand() % a + 1;
	    	y = rand() % b + 1;
	        	if (board[x][y] == ' ')
	    	{
	    		board[x][y] = '@';
		    	break;
	    	}
		
        	}
    }
    int Iswin(char board[row][line], int a, int b)
    {
    	int i;
    	int t = 0;
    	        for (i = 0; i < b; i++)
    	{
    	        	if (board[i][0] == board[i][1] && board[i][1]== board[i][2] && board[i][0] != ' ')
	    {
	    		return board[i][0];
	    	}
	    }
	    for (i = 0; i < b; i++)
	    {
	    	if (board[0][i] == board[1][i] && board[1][i] == board[2][i] && board[0][i] != ' ')
	    	{
	    		return board[0][i];
	    	}
	    }
	    if (board[0][0] == board[1][1] && board[1][1] == board[2][2] && board[0][0] != ' ')
	    {
	    	return board[0][0];
	    }
	    if (board[0][2] == board[2][0] && board[2][0] == board[2][2] && board[2][2] != ' ')
	    {
	    	return board[2][2];
	    }
	    if (1 == IsFull(board, a, b))
	    {
	    	return 'P';
    	}
    	
    		return 'C';
    
    }
    int IsFull(char board[row][line], int a, int b)
    {    
    	int i, j;
    	for (i = 0; i < a; i++)
    	{
    		for (j = 0; j < b; j++)
    		{
    			if (board[i][j] == ' ')
    			{
    				return 0;
    			}
    		}
    	}
    	return 1;
    }
