import random

#PAUSES PROGRAM UNTIL USER PRESSES ENTER
def wait_for_player():
    '''()->None
    Pauses the program until the user presses enter
    '''
    try:
         input("\nPress enter to continue. ")
         print()
    except SyntaxError:
         pass

#CREATES LIST REPRESENTING DECK OF CARDS & REMOVING ONE QUEEN
def make_deck():
    '''()->list of str
        Returns a list of strings representing the playing deck,
        with one queen missing.
    '''
    deck=[]
    suits = ['\u2660', '\u2661', '\u2662', '\u2663']
    ranks = ['2','3','4','5','6','7','8','9','10','J','Q','K','A']
    for suit in suits:
        for rank in ranks:
            deck.append(rank+suit)
    deck.remove('Q\u2663') # remove a queen as the game requires
    return deck

#SHUFFLES DECK OF CARDS
def shuffle_deck(deck):
    '''(list of str)->None
       Shuffles the given list of strings representing the playing deck    
    '''
    random.shuffle(deck)

############################################################

#DISTRIBUTE SHUFFLED DECK BETWEEN ROBOT AND HUMAN
def deal_cards(deck):
     '''(list of str)-> tuple of (list of str,list of str)

     Returns two lists representing two decks that are obtained
     after the dealer deals the cards from the given deck.
     The first list represents dealer's i.e. computer's deck
     and the second represents the other player's i.e user's list.
     '''
     dealer=[]
     other=[]

     split_deck= len(deck)//2 
    
     dealer = deck[:split_deck] #give first half to robot
     other = deck[split_deck:] #second half to player

     return (dealer, other)

#REMOVES PAIRS FROM PLAYERS DECK
def remove_pairs(l):
    '''
     (list of str)->list of str

     Returns a copy of list l where all the pairs from l are removed AND
     the elements of the new list shuffled

     Precondition: elements of l are cards represented as strings described above

     Testing:
     Note that for the individual calls below, the function should
     return the displayed list but not necessarily in the order given in the examples.

     >>> remove_pairs(['9♠', '5♠', 'K♢', 'A♣', 'K♣', 'K♡', '2♠', 'Q♠', 'K♠', 'Q♢', 'J♠', 'A♡', '4♣', '5♣', '7♡', 'A♠', '10♣', 'Q♡', '8♡', '9♢', '10♢', 'J♡', '10♡', 'J♣', '3♡'])
     ['10♣', '2♠', '3♡', '4♣', '7♡', '8♡', 'A♣', 'J♣', 'Q♢']
     >>> remove_pairs(['10♣', '2♣', '5♢', '6♣', '9♣', 'A♢', '10♢'])
     ['2♣', '5♢', '6♣', '9♣', 'A♢']
    '''

    no_pairs=[]

    # seperate ranks from the symbols since we're removing pairs based on the ranks 
    just_ranks = []
    
    for card in l:
        rank = card[:-1]  # Extract rank (all characters except the last symbol)
        just_ranks.append(rank)

    '''
    rank=card[:-1]
    for rank in just_ranks:
        if just_ranks.count(rank) %2 != 0:
            no_pairs.append(card)
            just_ranks.remove(rank)
    '''       
    for card in l:
        rank = card[:-1]
        if just_ranks.count(rank) % 2 != 0:  # If there is an odd number of this rank, add ONE to no_pairs since its the remaining (eg: if 3 we take out 2, if we 5 take out 4..)
            no_pairs.append(card)
            just_ranks.remove(rank)  # remove that rank so that we don't add the same card again if we come across it 
    
    random.shuffle(no_pairs)
    return no_pairs

#DISPLAYS PLAYER'S DECK TO USER
def print_deck(deck):
    '''
    (list)->None
    Prints elements of a given list deck separated by a space
    '''
    
    print(" ")

    for card in deck: #aka for every element in the list
        print(card, end=" ")
    print('\n')

#GETS INPUT FROM PLAYER ABOUT WHICH FACE-DOWN CARD THEY WANT FROM ROBOT
def get_valid_input(n):
     '''
     (int)->int
     Returns an integer given by the user that is at least 1 and at most n.
     Keeps on asking for valid input as long as the user gives integer outside of the range [1,n]
     
     Precondition: n>=1
     '''
     
     #function continues to loop until a valid integer within the specified range is obtained, and it returns this valid integer to the caller

     print("I have " + str(n) + " cards. If 1 stands for my first card and " + str(n)+" for my last card, which of my cards would you like?")

     while True: #will keep running until a valid integer is given
         user_input = int(input("Give me an integer between 1 and " + str(n) + ": "))
         
         if user_input >= 1 and user_input <= n:
            return user_input #exit loop and return valid input
         else:
             print("Invalid number. Please enter an integer between 1 and " + str(n) + ".")
     
def card_suffix(num):
    if num==1:
        suffix='st'

    elif num==2:
        suffix='nd'
    elif num==3:
        suffix='rd'
    else:
        suffix='th'

    return str(num) + suffix

#PUT EVERYTHING TOGEHER
def play_game():
     '''()->None
     This function plays the game'''
    
     deck=make_deck() #deck is created
     shuffle_deck(deck) #deck is shuffled
     tmp=deal_cards(deck) #deck is divided into equal parts

     dealer=tmp[0]
     human=tmp[1]
     
    #introductory messages

     print("Hello. My name is Robot and I am the dealer.")
     print("Welcome to my card game!")
     print("Your current deck of cards is:")
     print_deck(human)
     print("Do not worry. I cannot see the order of your cards")

     print("Now discard all the pairs from your deck. I will do the same.")
     wait_for_player()

     #remove_pairs function is called for both the dealer and the player
     dealer=remove_pairs(dealer)
     human=remove_pairs(human)

     #loop that continues until someone runs out of cards:
     
     while dealer and human: #while TRUE and TRUE, aka while they both arent empty lists
        
        print("Your turn:")

        #PLAYERS SIDE
        
        #display current player deck at the start of their turn
        print("Your current deck of cards is:")
        print_deck(human)
        
        #calls input function to promt player to give an integer between 1 and the number of dealer's cards
        #we do -1 for the input because python starts at 0. eg if i choose 2 its card 3 (0,1,2) so we -1 for it to be card 2  

        card_input = get_valid_input(len(dealer)) - 1

        #chosen card is retrieved from dealer's deck using pop() which removes the card from dealers deck and assigns it to chosen_card
        chosen_card = dealer.pop(card_input)

        #chosen_card that was taken out of the dealer's deck is ADDED to the player's deck with .append() 
        human.append(chosen_card)

        #tells player which card they asked for with a SUFFIX. we do +1 because if i choose 2 for ex its card number 3
        print("You asked for my " + card_suffix(card_input + 1) + " card.")

        print("Here it is. It is " + chosen_card + "\n")

        #display the updated player's deck after taking robot's card
        print("With " + chosen_card + " added, your current deck of cards is:")
        print_deck(human)

        #remove pairs if any & print new deck
        human = remove_pairs(human)
        shuffle_deck(human)
        
        print("After discarding pairs and shuffling, your deck is:")
        print_deck(human)
        
        wait_for_player()

        if not dealer: #check if dealer's list is empty after the player takes a card
            print("I do not have any more cards.")
            print("You lost! I win. Goodbye!")

        else: #if dealer still has cards, proceed to dealer's turn

            print("My turn:")
            card_input = random.randint(0, len(human) - 1)
            chosen_card = human.pop(card_input)
            dealer.append(chosen_card)
            dealer = remove_pairs(dealer)
            print("I took your " + card_suffix(card_input + 1) + " card.")

        #loop back to player's turn
    
    #when the while loop isnt respected anymore, ie human list is empty, we exit the loop
     if not human:
         wait_for_player()
         print("You do not have any more cards.")
         print("Congratulations! You won! Play again soon!")

# main
play_game()
