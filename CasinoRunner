import java.util.*;
import java.util.Scanner;

public class CasinoRunner {
  private static int currentPosition;
  private static int[] deck;
  private static int coins;
  public static int bet;
  public static void main (String args[]) {
    boolean goGoGadget = true;
    while (goGoGadget) {
      Scanner in = new Scanner(System.in);
      System.out.println("////////////////////////////////////");
      System.out.println("//                                //");
      System.out.println("// WELCOME TO THE COMP SCI CASINO //");
      System.out.println("//                                //");
      System.out.println("////////////////////////////////////");
      System.out.println("");
      System.out.println("Three games are offered here. Money/Coins will be given accordingly");
      System.out.println("");
      System.out.println("1. Black Jack");
      System.out.println("2. Pokemon Roulette");
      System.out.println("3. Slot Machine");
      System.out.println("");
      System.out.print("Please select which game you would like to play: ");
      int choice = in.nextInt();
      System.out.println("");
      while (choice != 1 && choice != 2 && choice != 3) {
        System.out.println("That number is not valid.");
        System.out.print("Please select which game you would like to play: ");
        choice = in.nextInt();
        System.out.println("");
      }
      if (choice == 1)
        new CasinoRunner().blackJackRun();
      if (choice == 2)
        new CasinoRunner().rouletteRun();
      if (choice == 3)
        new CasinoRunner().slotMachineRun();
      System.out.println("Would you like to play another game? Type 1 to play another or 0 to quit");
      int hello = in.nextInt();
      while (hello != 1 && hello != 0) {
        System.out.println("That is not valid.");
        System.out.println("Would you like to play another game? Type 1 to play another or 0 to quit");
        hello = in.nextInt();
      }
      if (hello == 1)
        goGoGadget = true;
      else
        goGoGadget = false;
    }
    System.out.println("Goodbye!");
  }
  public void blackJackRun() {
  
      /*How this should work: The computer acts as the dealer. The user has a stake of $100, and makes a bet on each game.
      The user can leave at any time, or will be kicked out when he/she loses all the money.
      House rules:  The dealer always hits on a total of 16 or less and stays on a total of 17 or more.  Dealer wins ties.
      A NEW deck of cards is used for each game. If it doesn't work like this, sorry about that. */
    
    Scanner in = new Scanner(System.in);                   
    boolean didThey;   // Tells if the user won or not
    System.out.println("Welcome to the game of Blackjack.");
    System.out.println();
    coins = 100;  // User starts with $100.
    while (true) // Allows the program to execute over and over until the user quits or has 0 money {
      System.out.println("You have " + coins + " dollars.");
      do {
        System.out.println("How many dollars do you want to bet? (Enter 0 to end.)");
        bet = in.nextInt();
        if (bet < 0 || bet > coins) {
          System.out.println("Your answer must be between 0 and " + coins + '.');
        }
      } while (bet < 0 || bet > coins); // Evaluation at the end by using "do-while" allows the loop to run once no matter what, but also run again if necessary. I've actually thought this one over pretty well...
      if (bet == 0) {
        System.out.println("");
        System.out.println("Wimp.");
        break; // I know it's bad programming, but it works, right?
      }
      didThey = playBlackjack();
      if (didThey) {
        System.out.println("Your bet has been added to your total money count.");
        coins = coins + bet;
      } 
      else {
        System.out.println("Your bet has been subtracted from your total money count.");
        coins = coins - bet;
      }
      if (coins == 0) {
        System.out.println("Looks like you're out of money!");
        break;
      }
    }
    System.out.println("");
    System.out.println("You are leaving with $" + coins + '.');
  }
  private boolean playBlackjack() {
    Scanner in = new Scanner(System.in);
    Vector dealerHand = new Vector(); // A vector allows the hand to grow in size at will. It's just easier to manage than an array list or array.  
    Vector userHand = new Vector();
    Vector hand;
    deck = new int[52]; // Creates the array for the deck of cards
    int doubleCount = 0; 
    int cardCount = 0;
    for (int suit = 0; suit <= 3; suit++) {
      for (int value = 1; value <= 13; value++) {
        deck[cardCount] = value;
        cardCount++;
      }
    }
    currentPosition = 0;
    shuffle(); // Shuffle the deck
    dealerHand.addElement(giveCard());
    dealerHand.addElement(giveCard());
    userHand.addElement(giveCard());
    userHand.addElement(giveCard());
    System.out.println("");
    if (value(dealerHand) == 21) {
      System.out.println("The dealer has the " + toString(getCard(dealerHand, 0)) + " and the " + toString(getCard(dealerHand, 1)) + ".");
      System.out.println("You have the " + toString(getCard(userHand, 0)) + " and the " + toString(getCard(userHand, 1)) + ".");
      System.out.println("");
      System.out.println("Dealer has Blackjack. Dealer wins.");
      return false;
    }
    if (value(userHand) == 21) {
     System.out.println("The dealer has the " + toString(getCard(dealerHand, 0)) + " and the " + toString(getCard(dealerHand, 1)) + ".");
      System.out.println("You have the " + toString(getCard(userHand, 0)) + " and the " + toString(getCard(userHand, 1)) + ".");
      System.out.println("");
      System.out.println("You have Blackjack. You win!");
      return true;
    }
    while (true) { // Once again, it allows me to execute the program over and over until I get the result I want
      System.out.println("");
      System.out.println("Your cards are:");
      for (int i = 0; i < userHand.size(); i++) {
        System.out.println("    " + toString(getCard(userHand, i)));
      }
      System.out.println("Your total is " + value(userHand));
      System.out.println("");
      System.out.println("The dealer is showing the " + toString(getCard(dealerHand, 0)));
      System.out.println("");
      System.out.print("Hit (H), Stand (S), Surrender (X), or Double (D)?");
      char userAction = Character.toUpperCase(in.next().charAt(0));
      while (userAction != 'H' && userAction != 'S' && userAction != 'X' && userAction != 'D') {
        System.out.print("Please respond H, S, X, or D:  ");
        userAction = Character.toUpperCase(in.next().charAt(0));
      }
      if (userAction == 'S')
        break;
      if (userAction == 'X') {
        System.out.println("The dealer has the " + toString(getCard(dealerHand, 0)) + " and the " + toString(getCard(dealerHand, 1)) + ".");
        System.out.println("You have the " + toString(getCard(userHand, 0)) + " and the " + toString(getCard(userHand, 1)) + ".");
        System.out.println("");
        System.out.println("You have surrendered. You lose!");
        coins = coins + (int) (bet * .5);
        return false;
      }
      if (userAction == 'D' && doubleCount < 1 && (bet * 2) <= coins) {
        doubleCount++;
        bet = bet * 2;
        System.out.println("Your bet has been doubled.");
        int newCard = giveCard();
        userHand.addElement(newCard);
        System.out.println("");
        System.out.println("You hit...");
        System.out.println("Your card is the " + toString(newCard));
        System.out.println("Your total is now " + value(userHand));
        if (value(userHand) > 21) {
          System.out.println("");
          System.out.println("You busted by going over 21.  You lose.");
          return false;
        }
      }
      if (userAction == 'D' && (doubleCount >= 1 || (bet * 2) > coins)) {
        System.out.println("");
        System.out.println("You cannot double. Choose again.");
      }
      if (userAction == 'H') {
        int newCard = giveCard();
        userHand.addElement(newCard);
        System.out.println("");
        System.out.println("You hit...");
        System.out.println("Your card is the " + toString(newCard));
        System.out.println("Your total is now " + value(userHand));
        if (value(userHand) > 21) {
          System.out.println("");
          System.out.println("You busted by going over 21.  You lose.");
          return false;
        }
      }
    }
    System.out.println("");
    System.out.println("You stay at the value of " + value(userHand));
    System.out.println("The dealer's cards are");
    System.out.println("    " + toString(getCard(dealerHand, 0)));
    System.out.println("    " + toString(getCard(dealerHand, 1)));
    while (value(dealerHand) <= 16) {
      int newCard = giveCard();
      System.out.println("The dealer hits and gets the " + toString(newCard));
      dealerHand.addElement(newCard);
    }
    System.out.println("The dealer's total is " + value(dealerHand));
    System.out.println("");
    if (value(dealerHand) > 21) {
      System.out.println("The dealer busted by going over 21.  You win!");
      return true;
    } 
    else {
      if (value(dealerHand) == value(userHand)) {
        System.out.println("The dealer wins on a tie.  You lose.");
        return false;
      } 
      else {
        if (value(dealerHand) > value(userHand)) {
          System.out.println("The dealer wins with " + value(dealerHand) + " points against " + value(userHand) + ". You lose.");
          return false;
        } 
        else {
          System.out.println("It's your " + value(userHand) + " points to " + value(dealerHand) + ". You win!");
          return true;
        }
      }
    }
  }
  public int giveCard() {
    if (currentPosition == 52) { // If you reach the end of the deck, execute these commands
      shuffle();
    }
    currentPosition++;
    return deck[currentPosition - 1];
  }
  public void shuffle() { // Switches two random cards (Thanks to Alex for the idea)
    for (int i = 51; i > 0; i--) {
      int rand = (int) (Math.random() * (i + 1));
      int temp = deck[i];
      deck[i] = deck[rand];
      deck[rand] = temp;
    }
    currentPosition = 0; // Resets the current position
  }
  public int value(Vector hand) {
    int val = 0;
    boolean ace = false;  // Shows if the hand has an ace or not.
    int cards = hand.size();
    for (int i = 0; i < cards; i++) {
      int card;
      int cardVal;
      card = getCard(hand, i);
      cardVal = getCardValue(card);  // The normal value, 1 to 13.
      if (cardVal > 10) { // Makes it such that no matter what face card you get the value is set to 10
        cardVal = 10;
      }
      if (cardVal == 1) { // There is at least one ace
        ace = true;
      }
      val = val + cardVal;
    }
    if (ace == true && val + 10 <= 21) { // If there is an ace and if changing its value from 1 to 11 would keep the score less than 21, it is done
      val = val + 10;
    }
    return val;
  }
  public int getCard(Vector hand, int position) { // Get a card from a hand in the given position
    if (position >= 0 && position < hand.size()) {
      return (int) hand.elementAt(position); // Returns the card as its number value
    } 
    else {
      return 0;
    }
  }
  public int getCardValue(int card) {
    int result = card;
    if (card == 11 || card == 12 || card == 13)
      result =  10;
    return result;
  }
  public String toString(int card) {
    String toReturn = "";
    if (card == 1)
      toReturn = "Ace";
    if (card == 2)
      toReturn = "2";
    if (card == 3)
      toReturn = "3";
    if (card == 4)
      toReturn = "4";
    if (card == 5)
      toReturn = "5";
    if (card == 6)
      toReturn = "6";
    if (card == 7)
      toReturn = "7";
    if (card == 8)
      toReturn = "8";
    if (card == 9)
      toReturn = "9";
    if (card == 10)
      toReturn = "10";
    if (card == 11)
      toReturn = "Jack";
    if (card == 12)
      toReturn = "Queen";
    if (card == 13)
      toReturn = "King";
    return toReturn;
  }
  public void rouletteRun() {
      /*This is an attempt at Pokemon Roulette, featured in Pokemon Ruby.
      The user chooses which way he or she would like to bet (on one spot,
      one Pokemon, or one color) and then chooses hoe much they would like to bet.
      The return for the correct spot is 12x. The return for the correct Pokemon is 4x.
      The return for the correct color is 3x. After each round, the board is reset.
      This game is super easy to win. I know. It was like this in the actual game, too.*/
      
    Scanner in = new Scanner(System.in);
    int what = 0;
    boolean keepGoing = true;
    coins = 50;
    System.out.println("You have been given " + coins + " coins to start.");
    while (keepGoing) {
      System.out.println("");
      System.out.println("Welcome to Pokemon Roulette!");
      System.out.println("");
      System.out.println("This roulette wheel has twelve spaces as shown below:");
      System.out.println(" Yellow:  (1) Makuhita  (2) Azurill  (3) Skitty  (4) Wynaut");
      System.out.println(" Green:   (5) Makuhita  (6) Azurill  (7) Skitty  (8) Wynaut");
      System.out.println(" Purple:  (9) Makuhita  (10) Azurill (11) Skitty  (12) Wynaut");
      System.out.println("");
      System.out.println("You can bet one of three ways:");
      System.out.println("Type 1 to select one specific color and Pokemon for a 12X return");
      System.out.println("Type 2 to select one Pokemon for a 4X return");
      System.out.println("Type 3 to select one color for a 3X return");
      what = in.nextInt();
      while (what != 1 && what != 2 && what != 3) {
        System.out.println("That number is not valid.");
        System.out.print("Please select how you would like to wager: ");
        what = in.nextInt();
        System.out.println("");
      }
      if (what == 1){
        System.out.println("Please type the specific Pokemon you would like to bet on. Look above for the numerical choices. An example entry would be \"1\" to choose Yellow Makuhita");            
        int choice = in.nextInt();
        while (choice > 12 || choice < 1) {
          System.out.println("That entry is not valid.");
          System.out.print("Please select which color and Pokemon you would like to bet on: ");
          choice = in.nextInt();
          System.out.println("");
        }
        System.out.println("Now please select how much you would like to bet on that spot.");
        bet = in.nextInt();
        while (bet > coins || bet < 1) {
          System.out.println("That entry is not valid.");
          System.out.print("Please enter your bet.");
          bet = in.nextInt();
          System.out.println("");
        }
        int result = (int) (Math.random() * 12 + 1);
        if (choice == result) {
          System.out.println("");
          System.out.println("You won!");
          coins = coins + (bet * 12);  
          System.out.println("You now have " + coins + " coins.");     
        }
        else {
          System.out.println("You lost. The resulting Pokemon number was " + result + ", not " + choice);
          coins = coins - bet;
          System.out.println("You now have " + coins + " coins."); 
        }
      }
      if (what == 2) {
      String toPrint;
      System.out.println("Please type what Pokemon you would like to bet on. An example entry would be \"Makuhita\"");
      String decision = in.nextLine();
      decision = in.nextLine();
      while (!(decision.equalsIgnoreCase("Makuhita")) && !(decision.equalsIgnoreCase("Azurill")) && !(decision.equalsIgnoreCase("Skitty")) && !(decision.equalsIgnoreCase("Wynaut"))){
      	System.out.println("That entry is not valid.");
        System.out.print("Please select which Pokemon you would like to bet on: ");
        decision = in.nextLine();
        System.out.println("");
      }
      System.out.println("Now please select how much you would like to bet on that spot.");
      bet = in.nextInt();
      while (bet > coins || bet < 1) {
        System.out.println("That entry is not valid.");
        System.out.print("Please enter your bet.");
       	bet = in.nextInt();
        System.out.println("");
      }
      int luck = (int) (Math.random() * 4 + 1);
      if (luck == 1 && decision.equalsIgnoreCase("Makuhita")) {
        System.out.println("You won!");
        coins = coins + (bet * 4);
        System.out.println("You now have " + coins + " coins."); 
      }
      else
        if (luck == 2 && decision.equalsIgnoreCase("Azurill")) {
          System.out.println("You won!");
          coins = coins + (bet * 4);
          System.out.println("You now have " + coins + " coins."); 
        }
        else
          if (luck == 3 && decision.equalsIgnoreCase("Skitty")) {
            System.out.println("You won!");
            coins = coins + (bet * 4);
            System.out.println("You now have " + coins + " coins."); 
          }
          else
            if (luck == 4 && decision.equalsIgnoreCase("Wynaut")) {
              System.out.println("You won!");
              coins = coins + (bet * 4);
              System.out.println("You now have " + coins + " coins."); 
            }
            else {
              if (luck == 1)
                toPrint = "Makuhita";
              else
                if (luck == 2)
                  toPrint = "Azurill";
                else
                  if (luck == 3)
                    toPrint = "Skitty";
                  else
                    if (luck == 4)
                      toPrint = "Wynaut";
                  else
                    toPrint = "??";
            System.out.println("You lost. The resulting Pokemon was " + toPrint + ".");
            coins = coins - bet;
            System.out.println("You now have " + coins + " coins."); 
          }
      }
      if (what == 3) {
        String toPrint;
        System.out.println("Please type what color you would like to bet on. An example entry would be \"Yellow\"");
        String decision = in.nextLine();
        decision = in.nextLine();
        while (!(decision.equalsIgnoreCase("Yellow")) && !(decision.equalsIgnoreCase("Green")) && !(decision.equalsIgnoreCase("Purple"))) {
          System.out.println("That entry is not valid.");
          System.out.print("Please select which color you would like to bet on: ");
          decision = in.nextLine();
          System.out.println("");
        }
        System.out.println("Now please select how much you would like to bet on that spot.");
        bet = in.nextInt();
        while (bet > coins || bet < 1) {
          System.out.println("That entry is not valid.");
          System.out.print("Please enter your bet.");
          bet = in.nextInt();
          System.out.println("");
        }
        int luck = (int) (Math.random() * 3 + 1);
        if (luck == 1 && decision.equalsIgnoreCase("Yellow")) {
          System.out.println("You won!");
          coins = coins + (bet * 3);
          System.out.println("You now have " + coins + " coins."); 
        }
        else
          if (luck == 2 && decision.equalsIgnoreCase("Green")) {
            System.out.println("You won!");
            coins = coins + (bet * 3);
            System.out.println("You now have " + coins + " coins."); 
          }
          else
            if (luck == 3 && decision.equalsIgnoreCase("Purple")) {
              System.out.println("You won!");
              coins = coins + (bet * 3);
              System.out.println("You now have " + coins + " coins."); 
            }
            else {
              if (luck == 1)
                toPrint = "Yellow";
              else
                if (luck == 2)
                  toPrint = "Green";
                else
                  if (luck == 3)
                    toPrint = "Purple";
                  else
                  	toPrint = "??";
              System.out.println("You lost. The resulting color was " + toPrint + ".");
              coins = coins - bet;
              System.out.println("You now have " + coins + " coins."); 
            } 
      }
      if (coins == 0) {
        System.out.println("");
        System.out.println("You have no money left. Goodbye.");
        break; // Once again, I apologize
      }
    System.out.println("");
    System.out.println("Would you like to keep going? Type 1 to continue, or 0 to quit");
    int transfer = in.nextInt();
    System.out.println("");
    while (transfer != 0 && transfer != 1) {
      System.out.println("That entry is not valid.");
      System.out.println("Type 1 to continue, or 0 to quit");
      transfer = in.nextInt();
      System.out.println("");
    }
    if (transfer == 1)
    	keepGoing = true;
    else
      keepGoing = false;
    }
  if (keepGoing == false)
            System.out.println("Wimp");
         System.out.println("You finished with " + coins + " coins.");
      }
      public void slotMachineRun()
      {
      /*This version of a slot machine has 5 symbols.
      There are two different ways to bet.
      The user can bet on just the middle row, or triple the bet for the middle row and the two diagonals.*/
         Scanner in = new Scanner(System.in);
         boolean theDecision = true;
         boolean charles = true;
         coins = 100;
         int thisIsToCheck = 0;
         String first, second, third, firstFirst, secondFirst, thirdFirst, firstSecond, secondSecond, thirdSecond, firstThird, secondThird, thirdThird;
         System.out.println("You are starting with 100 coins.");
         while (theDecision)
         {
            thisIsToCheck = 0;
				System.out.println("You can bet 10 coins for a chance to win with the middle row.");
            System.out.println("Or you could bet 30 coins for a chance to win with the middle row and two diagonals!");
            System.out.println("Type in your bet:");
            bet = in.nextInt();
            while (bet != 10 && bet != 30)
            {
               System.out.println("");
               System.out.println("That is not a valid number. Try again:");
               bet = in.nextInt();
            }
            while (bet == 30 && coins < 30)
            {
               System.out.println("");
               System.out.println("You do not have enough coins to bet that much.");
               System.out.println("Try again:");
               bet = in.nextInt();
               while (bet != 10)
               {
                  System.out.println("");
                  System.out.println("You have to bet 10 here...");
                  System.out.println("That is not a valid number. Try again:");
                  bet = in.nextInt();
               }
            }
            if (bet == 10)
            {
               int firstDisp = (int) (Math.random() * 5 + 1);
               int secondDisp = (int) (Math.random() * 5 + 1);
               int thirdDisp = (int) (Math.random() * 5 + 1);
               if (firstDisp == 1)
                  first = "Cherry";
               else 
                  if (firstDisp == 2)
                     first = "Seven";
                  else 
                     if (firstDisp == 3)
                        first = "BAR";
                     else 
                        if (firstDisp == 4)
                           first = "Grapes";
                        else
                           first = "Bell";
               if (secondDisp == 1)
                  second = "Cherry";
               else
                  if (secondDisp == 2)
                     second = "Seven";
                  else
                     if (secondDisp == 3)
                        second = "BAR";
                     else
                        if (secondDisp == 4)
                           second = "Grapes";
                        else
                           second = "Bell";
               if (thirdDisp == 1)
                  third = "Cherry";
               else 
                  if (thirdDisp == 2)
                     third = "Seven";
                  else 
                     if (thirdDisp == 3)
                        third = "BAR";
                     else 
                        if (thirdDisp == 4)
                           third = "Grapes";
                        else
                           third = "Bell";
               System.out.println("");
               System.out.println("Here is your result...");
               System.out.println("");
               System.out.println("");
               System.out.println("| " + first + " | " + second + " | " + third + " |");
               System.out.println("");
               System.out.println("");
               if (firstDisp == 1 && secondDisp == 1 && thirdDisp == 1){
                  coins = coins + (bet * 16);
                  System.out.println("You won " + bet * 16 + " coins!");
                  System.out.println("Your total is now " + coins + " coins.");
               }
               if (firstDisp == 2 && secondDisp == 2 && thirdDisp == 2){
                  coins = coins + (bet * 8);
                  System.out.println("You won " + bet * 8 + " coins!");
                  System.out.println("Your total is now " + coins + " coins.");
               }
               if (firstDisp == 3 && secondDisp == 3 && thirdDisp == 3){
                  coins = coins + (bet *4);
                  System.out.println("You won " + bet * 4 + " coins!");
                  System.out.println("Your total is now " + coins + " coins.");
               }
               if (firstDisp == 4 && secondDisp == 4 && thirdDisp == 4){
                  coins = coins + (bet * 2);
                  System.out.println("You won " + bet * 2 + " coins!");
                  System.out.println("Your total is now " + coins + " coins.");
               }
               if (firstDisp == 5 && secondDisp == 5 && thirdDisp == 5){
                  coins = coins + bet;
                  System.out.println("You won " + bet + " coins!");
                  System.out.println("Your total is now " + coins + " coins.");
               }
               if (firstDisp != secondDisp || secondDisp != thirdDisp || thirdDisp != firstDisp){
                  coins = coins - bet;
                  System.out.println("You did not win any coins :(");
                  System.out.println("Your total is now " + coins + " coins.");
               }
            }
            if (bet == 30)
            {
            // Note: The naming scheme is columnRowDisp
               int firstFirstDisp = (int) (Math.random() * 5 + 1);
               int secondFirstDisp = (int) (Math.random() * 5 + 1);
               int thirdFirstDisp = (int) (Math.random() * 5 + 1);
               int firstSecondDisp = (int) (Math.random() * 5 + 1);
               int secondSecondDisp = (int) (Math.random() * 5 + 1);
               int thirdSecondDisp = (int) (Math.random() * 5 + 1);
               int firstThirdDisp = (int) (Math.random() * 5 + 1);
               int secondThirdDisp = (int) (Math.random() * 5 + 1);
               int thirdThirdDisp = (int) (Math.random() * 5 + 1);
               if (firstFirstDisp == 1)
                  firstFirst = "Cherry";
               else 
                  if (firstFirstDisp == 2)
                     firstFirst = "Seven";
                  else 
                     if (firstFirstDisp == 3)
                        firstFirst = "BAR";
                     else 
                        if (firstFirstDisp == 4)
                           firstFirst = "Grapes";
                        else
                           firstFirst = "Bell";
               if (secondFirstDisp == 1)
                  secondFirst = "Cherry";
               else
                  if (secondFirstDisp == 2)
                     secondFirst = "Seven";
                  else
                     if (secondFirstDisp == 3)
                        secondFirst = "BAR";
                     else
                        if (secondFirstDisp == 4)
                           secondFirst = "Grapes";
                        else
                           secondFirst = "Bell";
               if (thirdFirstDisp == 1)
                  thirdFirst = "Cherry";
               else 
                  if (thirdFirstDisp == 2)
                     thirdFirst = "Seven";
                  else 
                     if (thirdFirstDisp == 3)
                        thirdFirst = "BAR";
                     else 
                        if (thirdFirstDisp == 4)
                           thirdFirst = "Grapes";
                        else
                           thirdFirst = "Bell";
               if (firstSecondDisp == 1)
                  firstSecond = "Cherry";
               else 
                  if (firstSecondDisp == 2)
                     firstSecond = "Seven";
                  else 
                     if (firstSecondDisp == 3)
                        firstSecond = "BAR";
                     else 
                        if (firstSecondDisp == 4)
                           firstSecond = "Grapes";
                        else
                           firstSecond = "Bell";
               if (secondSecondDisp == 1)
                  secondSecond = "Cherry";
               else 
                  if (secondSecondDisp == 2)
                     secondSecond = "Seven";
                  else 
                     if (secondSecondDisp == 3)
                        secondSecond = "BAR";
                     else 
                        if (secondSecondDisp == 4)
                           secondSecond = "Grapes";
                        else
                           secondSecond = "Bell";
               if (thirdSecondDisp == 1)
                  thirdSecond = "Cherry";
               else 
                  if (thirdSecondDisp == 2)
                     thirdSecond = "Seven";
                  else 
                     if (thirdSecondDisp == 3)
                        thirdSecond = "BAR";
                     else 
                        if (thirdSecondDisp == 4)
                           thirdSecond = "Grapes";
                        else
                           thirdSecond = "Bell";
               if (firstThirdDisp == 1)
                  firstThird = "Cherry";
               else 
                  if (firstThirdDisp == 2)
                     firstThird = "Seven";
                  else 
                     if (firstThirdDisp == 3)
                        firstThird = "BAR";
                     else 
                        if (firstThirdDisp == 4)
                           firstThird = "Grapes";
                        else
                           firstThird = "Bell";
               if (secondThirdDisp == 1)
                  secondThird = "Cherry";
               else 
                  if (secondThirdDisp == 2)
                     secondThird = "Seven";
                  else 
                     if (secondThirdDisp == 3)
                        secondThird = "BAR";
                     else 
                        if (secondThirdDisp == 4)
                           secondThird = "Grapes";
                        else
                           secondThird = "Bell";
               if (thirdThirdDisp == 1)
                  thirdThird = "Cherry";
               else 
                  if (thirdThirdDisp == 2)
                     thirdThird = "Seven";
                  else 
                     if (thirdThirdDisp == 3)
                        thirdThird = "BAR";
                     else 
                        if (thirdThirdDisp == 4)
                           thirdThird = "Grapes";
                        else
                           thirdThird = "Bell";
               System.out.println("");
               System.out.println("Here is your result...");
               System.out.println("");
               System.out.println("");
               System.out.println("| " + firstFirst + " | " + secondFirst + " | " + thirdFirst + " |");
               System.out.println("| " + firstSecond + " | " + secondSecond + " | " + thirdSecond + " |");
               System.out.println("| " + firstThird + " | " + secondThird + " | " + thirdThird + " |");
               System.out.println("");
               System.out.println("");
               if (firstSecondDisp == secondSecondDisp && secondSecondDisp == thirdSecondDisp && firstSecondDisp == thirdSecondDisp)
               {
                  thisIsToCheck = 1;
                  if (firstSecondDisp == 1)
                  {
                     coins = coins + (bet * 16);
                     System.out.println("You won " + bet * 16 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstSecondDisp == 2)
                  {
                     coins = coins + (bet * 8);
                     System.out.println("You won " + bet * 8 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstSecondDisp == 3)
                  {
                     coins = coins + (bet * 4);
                     System.out.println("You won " + bet * 4 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstSecondDisp == 4)
                  {
                     coins = coins + (bet * 2);
                     System.out.println("You won " + bet * 2 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstSecondDisp == 5)
                  {
                     coins = coins + bet;
                     System.out.println("You won " + bet + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
               }
               if (firstFirstDisp == secondSecondDisp && secondSecondDisp == thirdThirdDisp && firstFirstDisp == thirdThirdDisp)
               {
                  thisIsToCheck = 1;
                  if (firstFirstDisp == 1)
                  {
                     coins = coins + (bet * 16);
                     System.out.println("You won " + bet * 16 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstFirstDisp == 2)
                  {
                     coins = coins + (bet * 8);
                     System.out.println("You won " + bet * 8 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstFirstDisp == 3)
                  {
                     coins = coins + (bet * 4);
                     System.out.println("You won " + bet * 4 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstFirstDisp == 4)
                  {
                     coins = coins + (bet * 2);
                     System.out.println("You won " + bet * 2 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstFirstDisp == 5)
                  {
                     coins = coins + bet;
                     System.out.println("You won " + bet + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
               }
               if (firstThirdDisp == secondSecondDisp && secondSecondDisp == thirdFirstDisp && firstThirdDisp == thirdFirstDisp)
               {
                  thisIsToCheck = 1;
                  if (firstThirdDisp == 1)
                  {
                     coins = coins + (bet * 16);
                     System.out.println("You won " + bet * 16 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstThirdDisp == 2)
                  {
                     coins = coins + (bet * 8);
                     System.out.println("You won " + bet * 8 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstThirdDisp == 3)
                  {
                     coins = coins + (bet * 4);
                     System.out.println("You won " + bet * 4 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstThirdDisp == 4)
                  {
                     coins = coins + (bet * 2);
                     System.out.println("You won " + bet * 2 + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
                  if (firstThirdDisp == 5)
                  {
                     coins = coins + bet;
                     System.out.println("You won " + bet + " coins!");
                     System.out.println("Your total is now " + coins + " coins.");
                  }
               }
               if (thisIsToCheck != 1)
               {
                  coins = coins - bet;
                  System.out.println("You did not win any coins :(");
                  System.out.println("Your total is now " + coins + " coins.");
               }
            }
            if (coins == 0)
            {
               System.out.println("");
               System.out.println("You have no money left. Goodbye.");
               charles = false;
               theDecision = false;         
            }
            if (charles)
            {
               System.out.println("");
               System.out.println("Would you like to keep going? Type 1 to continue, or 0 to quit");
               int transfer = in.nextInt();
               System.out.println("");
               while (transfer != 0 && transfer != 1)
               {
                  System.out.println("That entry is not valid.");
                  System.out.println("Type 1 to continue, or 0 to quit");
                  transfer = in.nextInt();
                  System.out.println("");
               }
               if (transfer == 1)
                  theDecision = true;
               else
               {
                  theDecision = false;
                  charles = false;
               }
               if (theDecision == false)
               {
                  System.out.println("Wimp");
                  System.out.println("You finished with " + coins + " coins.");
               }
            }
         }
      }
   }
