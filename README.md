import os
import time
import random
from pygame import mixer
os.system('color b5')
inventory = ["wood sword", " ", "", "", "", ""]
PlayerHealth = 100
mixer.init()
mixer.music.load('C:/Users/770857/Downloads/CSEDYB5-coin.mp3')
mixer.music.play()

#monster battle loop-----------------------------------------------------------
def BossBattle(PlayerHealth):
    MonsterHealth = 50
    while MonsterHealth >0 and PlayerHealth>0:
        for i in range(len(inventory)):
            if inventory[i] == "Hero's Armor":
                damage = random.randrange(10, 15)
            else:
                damage = random.randrange(20, 25)
        print("The monster attacks you for", damage)
        PlayerHealth -= damage
        print("You now have", PlayerHealth, "health left.")
        if inventory[0] == "Hero's Sword":
            damage = random.randrange(10, 15)
        else:
            damage = random.randrange(1, 5)
        print("You hit the monster for", damage)
        MonsterHealth -= damage
        print("The monster now has", MonsterHealth, "health left.")
        choice = input("press (p) to use potion or (s) to use sword")
        if choice == "p" and inventory[1] == "potion":
            PlayerHealth += 5
            print("you drank the potion! +5 hp!")
            inventory[1] = "empty"
        else:
            print("you don't have a potion")
    if MonsterHealth <=0:
        print("You defeated the monster!")
    elif PlayerHealth <0:
        dead = True
        
    return PlayerHealth
        
#Floor falling loop----------------------------------------------------------
def FloorFall():
    num = random.randrange(0, 100)
    if num < 5:
        print("you fell through the floor and died")
        return 1
    elif num < 10:
        print("you found the magic door that lets you out!")
        return 2
    else:
        print("the floor creaks ominously")
        return 3

start = time.time()
room = 1
TimeLeft = 2000

dead = False
win = False

while dead != True and win != True:#GAME LOOP
    print()
    newTime = time.time()
    timeElapsed = start - newTime
    print(int(timeElapsed*-1), "seconds have passed.")
    TimeLeft += timeElapsed
    print("you have", int(TimeLeft), "seconds left to complete the game!")
    if TimeLeft <= 0:
        dead = True
    #room 1----------------
    print("your inventory:", end = "")
    print(inventory)
    if room == 1:
        print("you awake in a unown and mysterious room. as you get up you see a sign that says 'THE DUNGEON' you see a yellow rusted door to the (N)orth side, a open corridor to the (S)outh side and a lcoked door to the (E)ast")
        choice = input()
        print("you got a potion")
        inventory[1] = "potion"
        mixer.music.load('C:/Users/770857/Downloads/CSEDYB5-coin.mp3')
        mixer.music.play()
        if choice == 's' or choice == 'S':
            room = 2
        elif choice == 'e' or choice == 'E':
            redKey = False
            if inventory[4] == "Red key":
                redKey = True
            if redKey == True:
                print("You open the door with the red key")
                room = 9
            else:
                print("The door is locked")
        elif choice == 'n' or choice == 'N':
            room = 14
    #room 2----------------
    if room == 2:
        print("you enter the second room, theres a door towards the (s)outh. There is a (r)ug on the floor, you cane go back (n)orth.")
        choice = input()
        if choice == "r" or choice =="R":
            print("you lift up the rug and find a key underneath. 'key' has been added to you're inventory!")
            inventory[2] = "key"
            mixer.music.load('C:/Users/770857/Downloads/CSEDYB5-coin.mp3')
            mixer.music.play()
        if choice == 's' or choice == 'S':
            room = 3
        elif choice == 'n' or choice == 'N':
            room =1
    #room 3----------------
    if room == 3:
        print("you enter the third room, there doesn't seem to be anything of interest here, you can go (w)est or back (n)orth")
        choice = input()
        if choice == 'w' or choice == 'W':
            room = 4
        elif choice == 'n' or choice == 'N':
            room =2
            
    #room 4----------------
    if room == 4:
        print("you pass through the fourth room, as you notice the floors aren't in the best condition, you realise it's a better idea to just get the heck out of there")
        result = FloorFall()
        if result == 1:
            dead = True
        elif result == 2:
            win == True    
        else:
            if choice == 'w' or choice == 'W':
            
                room = 5
            elif choice == 'e' or choice == 'E':
                room = 3
    #room 5----------------
    if room == 5:
        print("you enter the fifth room, there's a bunch of spiders you can either (s)lay the spiders and go or run back to the (e)ast")
        choice = input()
        if choice == 's' or choice == 'S':
            spider = random.randrange(1, 3)
            if spider == 1:
                print("The spiders bit you")
                PlayerHealth -= 10
            else:
                print("you slayed the spiders!")
                PlayerHealth += 5
                room = 6
        elif choice == 'e' or choice == 'E':
            room = 4
    #room 6----------------
    if room == 6:
        print("you enter the sixth room, you notice a wierd looking (c)oin on the floor it has the number 10 you can go back (s)outh or (n)orth")
        choice = input()
        if choice == 'n' or choice == 'N':
            room = 7
        elif choice == 'c' or choice == 'C':
            inventory[3] = "10 coins"
            mixer.music.load('C:/Users/770857/Downloads/CSEDYB5-coin.mp3')
            mixer.music.play()
            print("You got 10 coins!")
        elif choice == 's' or choice == 'S':
            room = 5
    #room 7----------------
    if room == 7:
        print("you enter the seventh room, there doesn't seem to be anything interesting here, you can go back (s)outh or east")
        choice = input()
        if choice == 'e' or choice == 'E':
            room = 8
        elif choice == 's' or choice == 'S':
            room = 6
    #room 8----------------
    if room == 8:
        print("you enter the eighth room, you see a rusted old (b)ox, you also see a laundry chute towards the (e)ast, you can go back (w)est")
        choice = input()
        if choice == "b" or choice =="B":
            print("you found a red key!")
            inventory[4] = "Red key"
            mixer.music.load('C:/Users/770857/Downloads/CSEDYB5-coin.mp3')
            mixer.music.play()
        elif choice == 'e' or choice == 'E':
            room = 1
        elif choice == 'w' or choice == 'W':
            room = 7
    #room 9----------------
    if room == 9:
        print("you enter the ninth room, you see yet another (c)oin on the ground, this one has the number twenty on it, you can go back (w)est or (e)ast")
        choice = input()
        if choice == 'e' or choice == 'E':
            room = 10
        elif choice == 'c' or choice == 'C':
            inventory[5] = "20 coins"
            mixer.music.load('C:/Users/770857/Downloads/CSEDYB5-coin.mp3')
            mixer.music.play()
            print("You got 20 coins!")
        elif choice == 'w' or choice == 'W':
            room = 1
    #room 10----------------
    if room == 10:
        print("you enter the tenth room, ther's a bunch of zombies you can either (s)lay them or you can go back (w)est")
        choice = input()
        if choice == 's' or choice == 'S':
            Zombie = random.randrange(1, 3)
            if Zombie == 1:
                print("The zombies attack you!")
                PlayerHealth -= 15
            else:
                print("you slayed the zombies!")
                PlayerHealth += 10
                room = 11
        elif choice == 'w' or choice == 'W':
            room = 9
    #room 11----------------
    if room == 11:
        print("you enter the eleventh room, you see a locked door towards the (s)outh with a sign on the top that says 'Shop', you can go back (n)orth")
        choice = input()
        if choice == 's' or choice == 'S':
            Key = False
            if inventory[2] == "key":
                Key = True
                if Key == True:
                    print("You open the door with the key")
                    room = 12
        elif choice == 'n' or choice == 'N':
            room = 10
    #room 12----------------
    if room == 12:
        print("you enter the shop and are greeted by an old man. 'Why, hello there adventurer, i've been waiting for you for quite some time, thru that door to my right is you're final challenge. if you think you're ready you may enter by pressing (W) or you could buy items from me such as the Hero's (A)rmor for 20 coins or the Hero's (S)word for 10 coins. what would you like to do?")
        choice = input()
        if choice == 'w' or choice == 'W':
            room = 13
        elif choice == 'A' or choice == 'a':
            if inventory[5] == "20 coins":
                inventory[5] = "Hero's Armor"
            else:
                print("Sorry but you don't have 20 coins")
        elif choice == 's' or choice == 'S':
            if inventory[3] == "10 coins":
                inventory[0] = "Hero's Sword"
                print(("""
         />_________________________________
[########[]_________________________________>
         \>
         
                                             """))
                inventory[3] = "Empty"
            else:
                print("Sorry but you don't have 10 coins")
        elif choice == 'n' or choice == 'N':
            room = 11
    #room 13----------------
    if room == 13:
        print("As you open the door you suddenly see the mastermind behind the entire situation, you're arch-nemesis, Dark Claw. 'HAHAHA, this is you're final test Jason Chavez, defeat my all mighty minion and I'll let you leave! But if you lose, you shall die!")
        PlayerHealth = BossBattle(PlayerHealth)
        if PlayerHealth > 0:
            print("You escaped")
            win = True
        else:
            dead = True
        
    #room 14----------------
    if room == 14:
        print("you open the door and see a bright yellow wallpaper, as you turn back to go thru the door, it's gone. You hear something coming towards you. This is it. The End.")
        choice = input()
#end of game loop!
if dead == True:
    print("game over, you lose")
if win == True:
    print("You won! good job!")
