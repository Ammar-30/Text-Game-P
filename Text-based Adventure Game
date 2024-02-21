# Importing libraries 
import random
import tkinter


# Player's Credential
Players_name = input("Please enter Your name >> ")
Players_money = random.randint(200,500)
Players_health = 100 # health is 100 intially
Players_points = 0
Players_inventory= {'Weapon': [],'Keys': [],'Armour': []} # Use of complex data structure to show players inventory, will be appended later in the code


# Creating a new window of this size
window = tkinter.Tk() 
window.geometry("500x800")

# Giving it a title and a back ground colour
window.title("Text_based adventure game")
window.config(background ='red')

# defining a function Shop
def shop():
    # Global, so it can fetch data from outside the funtion
    global Players_health 
    global Players_money

    with open("Shop.txt",'r') as Shop_file:
        whole_text = Shop_file.read()
        print(whole_text)
        
    while True:
        item_type = input("What item do you want to buy? (Weapon/Armour/key) or Healing >> ")
        if item_type.lower() not in ["weapon", "armour", "key", "healing"]:
            print("Invalid selection!")
        else:
            break
  
  # Error checking      
    try:
        if item_type.lower() == "weapon":
             name = input("Which Weapon do you want to buy? >> ")
             with open("Shop.txt", "r") as Shop_file:
                 whole_text = Shop_file.readlines() # reads the file as in list of strings
                 for line in whole_text:
                  if name in line:
                    temp = line
                 temp = temp.strip().split(":")[-1].split(",") # Getting the desired position in the line
                 if int(temp[2]) <= Players_money:
                     print ("Item bought successfully!\n",temp)
                     Players_money -= int(temp[2])
                     Players_inventory["Weapon"].append({"name": temp[0],"damage" :temp[1],"price": temp[2]})
                 else:
                     print("Not enough money! ")
    except:
        print('Invalid Input!')
    
       
    try:
        if item_type.lower() == "armour":
            name = input("Which armour do you want to buy? >> ")
            with open("Shop.txt", "r") as Shop_file:
                whole_text = Shop_file.readlines() # reads the file as in list of strings
                for line in whole_text:
                    if name in line:
                        temp = line
                    temp = temp.strip().split(":")[-1].split(",") # Getting the desired position in the line
                    if int(temp[1]) < Players_money:
                        print ("Item bought successfully!\n",temp)
                        Players_money -= int(temp[1])
                        Players_inventory["Armour"].append({"durability": temp[0],"price" :temp[1]})
                    else:
                        print("Not enough Money!")
    except:
     print("Invalid input!")
        
        
   
    try:     
        if item_type.lower() == "key":
            name = input("Which     key do you want to buy? >> ")
            with open("Shop.txt", "r") as Shop_file:
             whole_text = Shop_file.readlines() # reads the file as in list of strings
             for line in whole_text:
                if name in line:
                    temp = line
                temp = temp.strip().split(":")[-1].split(",") # Getting the desired position in the line
                if temp[1] < Players_money:
                    print ("Item bought successfully!\n",temp)
                    Players_money -= int(temp[1])
                    Players_inventory["Keys"].append({"code": temp[0],"price" :temp[1]})
                else:
                    print ("Not enough money!")
    except:
     print("Invalid input!")

    try:     
        if item_type.lower() == "healing":
            if Players_money <= 100:
                print("not enough money! ")   
            else: 
                Players_health += 50 
                Players_money -= 100
                print("Health increased by 50 points! ")
    except:
        print("Invalid Input!")
        
    update_all()


# Defined a function to configure GUI
def update_all():
    global Players_health 
    global Players_money
    global Players_points
    
    Money.config(text = "Total Money: " + str(Players_money))
    Health.config(text = "Health: " + str(Players_health))
    Points.config(text = "Points: " + str(Players_points))
    

# Defined a function to display room information and ask user for the fight
def scan_room(file_name):
    global Players_health
    global Players_money
    global Players_points
    
    with open(file_name + ".txt", "r") as room_file:
        whole_text = room_file.readlines()
        print(whole_text[0])
        print(whole_text[1])
    
    for idx,line in enumerate(whole_text):
        if "points" in line.lower():
            att = whole_text[idx+1]
            break
        
    Points_gained  = att[0]
     
    for idx, line in enumerate(whole_text):
        if "enemy" in line.lower():
            temp = whole_text[idx+1]
            break
    
    temp = temp.strip().split(",")
    enemy = {"name": temp[0], "damage": temp[1], "health": temp[2]}
    enemies_damage =  int(temp[1])
    fight_enemy = input("Would you like to fight with the enemy? (yes/no) >> ")
    if fight_enemy.lower() == "no":
        print("Hahaha you are afraid!")
    if fight_enemy.lower() == "yes":
        if Players_health >= enemies_damage:
            battle_weapon = input("Which of the weapon would you like to choose for the battle >> " )
            if battle_weapon not in Players_inventory['Weapon']: 
                print ("No such weapon found in inventory!")
            else:
                Players_health -= enemies_damage
                Players_points += int(Points_gained)
                print ("You've defeated the enemy")
        else:
            print("you could not beat the enemy. You lost!")     
    else:
        print("please enter yes or no! ")

    update_all()


# Defined a function to show players inventory
def Show_inventory():
    for item in Players_inventory:
        print(item, Players_inventory[item])
        

greet= tkinter.Label(window, text = "Text Based Adventure Game", font = ("Athelas 25"))
greet.pack(padx=20,pady= 40)

Player = tkinter.Label(window, text ="Player's Name: " + Players_name ,padx=2, pady=0, bg="red", fg="black" ,font= ('Abadi',15))
Player.pack(padx= 10, pady=5)

Health = tkinter.Label(window, text ="Player's Health: " + str(Players_health), padx=1, pady=0, bg="red" , fg="black",font= ('Abadi',15))
Health.pack(padx= 10, pady=5)

Money = tkinter.Label(window, text ="Total Money: " + str(Players_money), padx=1, pady=0,bg="red", fg="black",font= ('Abadi',15))
Money.pack(padx= 10, pady=5)

Points = tkinter.Label(window, text ="Points: " + str(Players_points),padx=1, pady=0,bg="red", fg="black",font= ('Abadi',15))
Points.pack(padx= 10, pady=5)

Inventory_button = tkinter.Button(window, command = Show_inventory, text = "My-Inventory", fg= "Blue" ,font = ('Academy Engraved LET',18))
Inventory_button.pack(pady=20)

Shop_button = tkinter.Button(window,command= shop, text = "Shop", fg= "Blue" ,padx=11 ,font = ('Academy Engraved LET',18))
Shop_button.pack(pady= 20)

Room1_button = tkinter.Button(window,command = lambda: scan_room("Room1"), text = "Room-1",fg= "Blue" , font = ('Academy Engraved LET',18))
Room1_button.pack(pady= 20)

Room2_button = tkinter.Button(window,command = lambda: scan_room("Room2"), text = "Room-2",fg= "Blue" , font = ('Academy Engraved LET',18))
Room2_button.pack(pady= 20)

Room3_button = tkinter.Button(window,command = lambda: scan_room("Room3"), text = "Room-3",fg= "Blue" ,font = ('Academy Engraved LET',18))
Room3_button.pack(pady= 20)

Room4_button = tkinter.Button(window,command= lambda: scan_room("Room4"), text =  "Room-4",fg= "Blue" , font = ('Academy Engraved LET',18))
Room4_button.pack(pady= 20)


window.mainloop()


