The following is my program that I made using Microsoft Visual Studio 2015 with description throughout:


#include "stdafx.h"


#include<stdio.h>

#include<conio.h>

#include<stdlib.h>

#include<math.h>

#include<time.h>
#include<string.h>

int main() 
{
int l;
	int rerun;
	float c;
	int dollargain;
	int dollarloss;
	
	system("COLOR F0");
	float sd;
	time_t seconds;
	time(&seconds);
	srand((unsigned int)seconds);

	int counter;
	int zcounter;
	float zsum;
	int inner_fence_average;
	int outer_fence_average;
	int innerfencecounter;
	int outerfencecounter;
	int avsum;
	int oavsum;
	int varzum;
	int ovarzum;
	int differz;
	int odifferz;
	int inner_fence_variance;
	int outer_fence_variance;
	float inner_fence_sd;
	float outer_fence_sd;
	int quartile3, quartile1;
	int *final_gain_money;
	int variance;
	int p2counter;
	int g;
	int upper_inner_fence;
	int lower_inner_fence;
	int upper_outer_fence;
	int lower_outer_fence;
	int f;
	int m;
	int own;
	int count;
	int t;
	

	int differ;
	int varsum;
	int increment;
	int casinotimes;

	int spins;
	int money;
	
	int *p1string;
	int *p2string;
	int startmoney;

	printf("\n\nHow many spins do you want to take?\n");

	scanf_s("%d", &spins);

	printf("\nHow much money do you want to start with each?\n");

	scanf_s("%d", &startmoney);

	printf("\nMoney per unit bet\n");

	scanf_s("%d", &money);

	

//Following input is the number of trials you want to run from 1- 10,000,000.
//Larger numbers would give a better final result statistically.
	printf("\nHow many times are you going to the casino?\n");
	scanf_s("%d", &casinotimes);

	int *numstring;
	
	//Memory allocation to heap in case "casinotimes" is a large number
	final_gain_money = (int*)malloc(casinotimes * sizeof(int));
	numstring = (int*)malloc(spins * sizeof(int));
	p1string = (int*)malloc(spins * sizeof(int));
	p2string = (int*)malloc(spins * sizeof(int));
	
	/*modearray[5000];
	for (counter = 0; counter < 5000; counter++)
	{
		modearray[counter] = 0;
	}
	int *medstring;
	medstring = (int*)malloc(casinotimes * sizeof(int));*/

	int p1_tot;
	int p2_tot;
	int h;
	int bet;
	int bet2;
	int acounter;
	
//initializes the first trial
	rerun = 1;
	
	
//Creates a Fibonacci "bet dollar amount" array. money (input) variable is money per increment. To switch to Martingale System,
//geometric series with r=2 is used with money (input) as starting increment value.
	
	int fibonacci[60];
	fibonacci[0] = money;
	fibonacci[1] = money;

	for (counter = 2; counter < 60; counter++)
	{
		fibonacci[counter] = fibonacci[counter - 2] + fibonacci[counter - 1];
	}

//Label for repeating 1 - 1000000 trials
repeat:
	
// initializes money per player	
	p1_tot = startmoney;
	p2_tot = startmoney;
	
//Creates a list of random numbers from 1-38 up to # of spins
	for (counter = 0; counter < spins; counter++) 
	{

		numstring[counter] = rand() % 38 + 1;
	}
	
//Converts Numstring to an array of 1's (wins) and -1's (losses) for both players
	for (counter = 0; counter < spins; counter++) 
	{
		if (numstring[counter] % 2 == 0 && numstring[counter] != 38) {
			p1string[counter] = 1;
		}
		else {
			p1string[counter] = -1;
		}
	}

	for (counter = 0; counter < spins; counter++)
	{
		if (numstring[counter] % 2 != 0 && numstring[counter] != 37) {
			p2string[counter] = 1;
		}
		else {
			p2string[counter] = -1;
		}
	}
	
//initializes starting point on "bet dollar amount" array for both players
	g = 0;
	h = 0;

	// Reads the Win/Loss array from start to finish
	for (acounter = 0; acounter < spins; acounter++) {
	//If either player loses all their money, stop playing. Can be tweaked.
		
		if (p1_tot <= 0 || p2_tot <= 0) {
			break;
		}
//The amount that each player bets this spin based on position on "bet dollar amount" array
		bet = fibonacci[g];
		bet2 = fibonacci[h];
		
/*Currently this is fibonacci Change the +1 to -1 in the switch to get reverse fibonacci*/
		
		switch (p1string[acounter]) {
		case -1: //LOST
			g = g + 1;//The next bet will be to the right 1 place on "bet dollar amount" array
			p1_tot = p1_tot - bet;//Subtract current bet from total
			break;

		case 1: //WON
			g = g - 2;//The next bet will be to the left 2 places on "bet dollar amount" array
			
			//If the next position on bet string goes below 0, change the next position to 0
			if (g < 0) 
			{

				g = 0;
				p1_tot = p1_tot + bet;//add the current bet to the total
				break;
			}
			else 
			{
				p1_tot = p1_tot + bet;//add the current bet to the total

				break;
			}
		}

		//Do the same things for player 2
		switch (p2string[acounter]) 
		{
		case -1:
			h = h + 1;
			p2_tot = p2_tot - bet2;

			break;
		case 1:
			h = h - 2;
			if (h < 0) 
			{
				h = 0;
				p2_tot = p2_tot + bet2;
				break;
			}
			else
			{
				p2_tot = p2_tot + bet2;
				break;
			}
		}
	}

	//Once the loop is complete, where either all spins are completed or one player lost all their money, 
	//Total money between the two players is taken and added to an array of final money amount per trial.

	final_gain_money[rerun - 1] = p1_tot + p2_tot;

//Finish if the process has completed the number of trials. If not, restart the whole loop.
	if (rerun == casinotimes) 
	{

		goto end;

	}
	else 
	{
		rerun = rerun + 1;
		goto repeat;

	}


//The previous algorithm can be modified to try numerous different Roulette Strategies such as Whitaker, Hollandish, Oscar's grind, D'Alembert, Labouchere
//Remove player 2 if desired.

end: //CALCULATE average and standard deviation of trial list.

	zsum = 0;
	for (zcounter = 0; zcounter < casinotimes; zcounter++) 
	{

		zsum = zsum + (((final_gain_money[zcounter])) / 2);
	}


	c = zsum / casinotimes;
/*	for (zcounter = 0; zcounter < casinotimes; zcounter++)
	{
		printf("\n%d", final_gain_money[zcounter]);
	}
Prints the list of final money gain if desired
	*/
	
printf("\nYou both will have $%f each in the end on AVERAGE\n", c);


	varsum = 0;
	for (counter = 0; counter<casinotimes; counter++)
	{
		differ = (((final_gain_money[counter])) / 2) - c;
		varsum = varsum + pow(differ, 2);
	}

	variance = varsum / casinotimes;
	sd = sqrtf(variance);
	printf("\n\nThe standard deviation of final money per person is %6.3f", sd);
}

//The rest of the code calculates other statistical measurements such as median, quartiles, IQR, fences, etc. 
