import random
import tkinter as tk
import tkinter.messagebox as tkMessBox

root = tk.Tk()
root.geometry("500x500")

class Card:
    """Represents a standard playing card."""
    def __init__(self, suit = 0, rank = 2, value = 2):
            self.suit = suit
            self.rank = rank
            self.value = value

    suit_names = [None,'Clubs','Diamonds','Hearts','Spades']
    rank_names = [None,'Ace','2','3','4','5','6','7','8','9','10','Jack','Queen','King']
    card_value = [None,1,2,3,4,5,6,7,8,9,10,11,12,13]    

    def __str__(self):
        return '{} of {}'.format(Card.rank_names[self.rank],Card.suit_names[self.suit])

class Desk:
    def __init__(self):
        self.cards = []
        for suit in range(1,5):                     # / range(len(self.suit_name)) / (Card.suit_names)(nhưng cách Card.suit ko làm đc, kiểu ko kế thừa đc phần print)
            for rank in range(1,14):
                card = Card(suit,rank,rank)
                self.cards.append(card)

    def print_desk(self):
        for card in self.cards:
            print(card)

    def pop_card(self):
        return self.cards.pop()

    def add_card(self,card):
        return self.cards.append(card)

    def shuffle(self):
        random.shuffle(self.cards)
  
class Hand(Desk):
    def __init__(self, value = 0):
        self.cards = []
        self.value = value
       
    def checking(self,other,root2):
        if(self.value > 21 and other.value <= 21):
            tkMessBox.showinfo("KQ","You bust out with {} point and lose,dealer have {} point".format(self.value,other.value))
            root2.destroy()
        elif(self.value > 21 and other.value > 21):
            tkMessBox.showinfo("KQ","You guys all bust out")
            root2.destroy()
        elif(self.value <= 21 and other.value > 21):
            tkMessBox.showinfo("KQ","You win with {} point, dealer have {} point".format(self.value,other.value))
            root2.destroy()

    def checking_end(self,other,root2):
        if(self.value > other.value):
            tkMessBox.showinfo("KQ","You win with {} point, dealer have {} point".format(self.value,other.value))
            root2.destroy()
        elif(self.value < other.value):
            tkMessBox.showinfo("KQ","You lose with {} point, dealer have {} point".format(self.value,other.value))
            root2.destroy()
        elif(self.value == other.value):
            tkMessBox.showinfo("KQ","Draw with {} point".format(self.value))
            root2.destroy()
       
    def first_roll(self,other,desk,root2):
        self.draw_a_card(desk,root2)
        self.draw_a_card(desk,root2)

    def first_roll_bot(self,desk,root2):
        self.draw_a_card(desk,root2)
        self.bot_draw(desk)
        tk.Label(root2,text = "?").pack()
    
    def draw_a_card(self,other,root2):
        card = other.pop_card()
        self.add_card(card)
        #if(card.value == 1):                                            #Làm cái A = 11 và 1 này hơi khó => bỏ qua (về sau làm)
            #if(self.value >= 11): self.value += 1
            #else: self.value += 11
        #else:
            #self.value += card.value
        self.value += card.value
        tk.Label(root2,text = card).pack()
        tk.Label(root2,text = "Tong = {}".format(self.value)).pack()
 
    def bot_draw(self,other):
        card = other.pop_card() 
        self.add_card(card)
        self.value += card.value

    def code_for_bot(self,other,desk):
        while(other.value > self.value and self.value <= 17): 
            self.bot_draw(desk)   

def start_button():
        player = Hand()
        bot = Hand()
        desk = Desk()

        def button():            
            player.draw_a_card(desk,root2)         
            bot.code_for_bot(player,desk)
            player.checking(bot,root2)
            print("\nBot's hand:")
            bot.print_desk()
            print("\nPlayer's hand")
            player.print_desk()

        def button_end():
            player.checking_end(bot,root2)

        def button_for_lesor():
            tkMessBox.showinfo("Sad for you","Okay sure, see you next time")
            root2.destroy()

        desk.shuffle()
        root2 = tk.Tk()
        root2.geometry("500x500")
        tk.Button(root2,text="Fight",command = button).pack()
        tk.Button(root2,text="Hold",command= button_end).pack()
        tk.Button(root2,text="Give up",command=button_for_lesor).pack()

        tk.Label(root2,text = "Dealer's Hand",bg = "green").pack()
        bot.first_roll_bot(desk,root2)
        tk.Label(root2,text = "Player's Hand",bg  = "black",fg = "white").pack()
        player.first_roll(bot,desk,root2)
        bot.code_for_bot(player,desk)
        player.checking(bot,root2)

        print("\nBot's hand:")
        bot.print_desk()
        print("\nPlayer's hand:")
        player.print_desk()

tk.Label(root,text="Welcome to Black Jack game",font = "Times 25 bold italic").pack()        
tk.Button(root,text="Press here to start",font="Times 15",command = start_button).pack()  
tk.Button(root,text="Exit",font="Times 15",command=root.destroy).pack()

root.mainloop()
