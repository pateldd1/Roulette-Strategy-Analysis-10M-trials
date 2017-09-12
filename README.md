# Roulette-Strategy-Analysis-10M-trials
Fibonacci, reverse_fibonacci, Martingale, etc. strategies debunked using heap memory allocation

## Roulette Strategy Debunking
* Many people will tell you that the game of Roulette is beatable and there are numerous strategies out there that say they can "beat the system"
* This program sets out to debunk all of those theories by running 10,000,000 trials (with the help of C Malloc and heap memory) of a gambler going to the casino
* In addition, people think that they can "pair up" with a partner and beat the system with one person playing black and the other person playing white. They're wrong.

### Strategies in existence
  [http://www.roulettestrategy.net/strategy/fibonacci/](http://www.roulettestrategy.net/strategy/fibonacci/) - Refer to this website if you want to lose your money
  
  #### Martingale Strategy - 
    * Playing one color on the wheel, If I double every time I lose, that means I have to lose > 6 or 7 times in order to lose, which can't ever happen
      - Wrong! Statistically it does happen and when it happens, you go bankrupt. 
      - Small Wins aren't enough to make up large losses
    
    * If I play with another person and I play black and he plays red we can minimize each others losses since when I lose, my partner wins and covers my losses
      - Wrong Again! The losses are too catastrophic.
  
  #### Fibonacci Strategy - 
    * Playing one color on the wheel, If I follow a pattern on the fibonacci sequence and move right one place when I lose and left 2 places when I win, I'm being more safe than Martingale
      - Wrong! this doesn't work for one or two players
      
 ### The Program
  * This Program will take user input of 
    1. How many spins do you want to take?
    2. How much money does each person start with (One person is playing red and other other is playing black)
    3. Money per unit bet (In martingale, if this is 5, you would be betting 5, 10, 20, 40, 80, etc. Fibonacci would be 5, 5, 10, 15, 25, etc.)
    4. How many times do you want to go to the casino? (10,000,000 seems to be maximum capacity)
    
    * In this program I am evaluating the fibonacci strategy with 2 players, one playing black, and the other playing red
    * TWEAKABILITY: this program can be tweaked to evaluate almost any roulette strategy. Instead of building a fibonacci bet sequence to iterate through, as in this program, build a Martingale or any other bet sequence.
    * Program will iterate through the bet sequence, figuring out if each player won or loss, and calculate the next bet for the player based on the strategy
    * Program will stop iterating if either player busts (has no money)
    * Program will find the average amount of money each player will leave the casino with after 10,000,000 trials of this strategy. 
    * Remove one player and do it for only one player by getting rid of one of the switch statements.
    * Change the betstring from a fibonacci to a reverse fib, reverse martingale, Hollandish, Oscar's Grind, whatever you want.
    * PLAYER(S) NEVER LEAVE THE CASINO WITH MORE MONEY THEY CAME IN WITH ON AVERAGE
     
