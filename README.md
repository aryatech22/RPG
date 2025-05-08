import random

mageRange = 1


class Character:
    def __init__(self, strength, health, constitution, mana, dexterity):

        self.strength = strength
        self.health = health
        self.constitution = constitution
        self.mana = mana
        self.dexterity = dexterity


    def dodge(self):
        miss = random.randint(1, 23) < 17
        if miss == True:
            damage_taken = 0
            print("(Successful Dodge)")
            return damage_taken


    def take_damage(self, damage):
        if self.dexterity > 16:
            miss = random.randint(1, 25) < 17
            if miss == True:
                damage_taken = 0
                print("(Successful Dodge)")
                return damage_taken
        damage_taken = damage - self.constitution
        self.health -= int(damage_taken)
        return damage_taken


    def attack(self, target):
        if role == Mage:
            damage = self.mana
            damage_dealt = target.take_damage(damage)
            return damage_dealt
        else:
            damage = self.strength
            damage_dealt = target.take_damage(damage)
            return damage_dealt

    def is_alive(self):
        return self.health > 0
    def is_dead(self):
        return self.health < 1


#class Rogue(Character):
    # attack() Method
    #def attack(self, target):
        #dexterity = 16
        #critical_hit = random.randint(0, 60) < dexterity
        #damage = self.dexterity * 2
        #if critical_hit:
            #damage *= 3
            #print("*** Critical Hit ***")
        #damage_dealt = target.take_damage(damage)
        #return damage_dealt


class Mage(Character):
    # attack() Method
    def attack(self, target):
        mana = 70
        critical_hit = random.randint(0, 200) < mana
        damage = self.mana * 2
        if critical_hit:
            damage *= 2
            print("*** Critical Hit ***")
        damage_dealt = target.take_damage(damage)
        return damage_dealt


class Demon(Character):
    def attack(self, target):
        strength = 201
        critical_hit = random.randint(1, 200) < strength
        damage = self.strength * 100
        if critical_hit:
            damage *= 100
            print("*** Critical Hit ***")
        damage_dealt = target.take_damage(damage)
        return damage_dealt


BladeDemon = Demon(150, 1000, 0, 0, 0)


class Enemy(Character):
    def attack(self, target):
        strength = 14
        critical_hit = random.randint(1, 300) < strength
        damage = self.strength * 2
        if critical_hit:
            damage *= 2
            print("*** Critical Hit ***")
        damage_dealt = target.take_damage(damage)
        return damage_dealt


BloodWing = Enemy(35, 300, 0, 17, 14)
Troll = Enemy(25, 70, 0, 0, 2)
goblin = Enemy(20, 50, 0, 0, 10)
Owlbear = Enemy(22, 60, 0, 0, 5)


class Fighter(Character):
    # attack() Method
    def attack(self, target):
        strength = 17
        critical_hit = random.randint(0, 100) < strength
        damage = self.strength * 2
        if critical_hit:
            damage *= 4
            print("*** Critical Hit ***")
        damage_dealt = target.take_damage(damage)
        return damage_dealt


role = input("Please pick the class your character: \n"
             "  Rogue: Close range attacker that deals low amounts of damage with a moderate health bar"
             "      Relies on dodging and critical hits, \n"
             "      Health: 60, Dex: 17, Str: 13, Mana: 10, Con: 11, \n"
             "  \nFighter: Close range tank that deals average amounts of damage with a large health bar,\n"
             "      Relies on high constitution and health \n"
             "      Health: 150, Dex: 10, Str: 17, Mana: 10, Con: 14,  \n"
             "  \nMage: Long range caster that deals mass amounts of damage with an incredibly small health bar,\n"
             "      Relies on high damage AOEs and distance from enemies,"
             "      Health: 30, Dex: 10, Str: 10, Mana: 70, Con: 10, Int: 15, \n"
             "      Spells: Fireball (4->6) * int dmg 10mana, Force Shield +30 health 20mana,\n"
             "\n  Please write choice: ")
if role == "Rogue" or role == "rogue":
    player = Rogue(13, 60, 11, 10, 17)


if role == "Mage" or role == "mage":
    player = Mage(10, 30, 10, 70, 10)

if role == "Fighter" or role == "fighter":
    player = Fighter(17, 150, 14, 10, 10)

    def attack(self, target):
        strength = 17
        critical_hit = random.randint(0, 200) < strength
        damage = self.strength * 2
        if critical_hit:
            damage *= 2
        damage_dealt = target.take_damage(damage)
        return damage_dealt

print("\n(You walk into an inn by the side of the road)\n")
questPath = input(
    'Innkeeper: Welcome weary traveler, to my inn. I see that you are a strong adventurer, would you be \n'
    '           so kind to go on a quest for me? I know a danger that needs to be vanquished, I hear that a red \n'
    '           mighty dragon known as Vortairn the Vicious lives in the mountains to the east terrorizing the \n'
    '           surrounding towns. Will you defeat him for me? y/n ')

if questPath == "Y" or questPath == "y" or questPath == "Yes" or questPath == "yes":
    print("\nInnkeeper: Let the quest begin! But first, sleep\n"
          "\n*** The Next Day ***\n"
          "\n* You set off on the dusty path towards the eastern mountains *\n")
    investigate = input("(You hear noises off the path, do you investigate? y/n) ")

    if investigate == "Y" or investigate == "y" or investigate == "yes" or investigate == "Yes":
        print("\n(As you crest the hill you see a massive goblin camp near the road, but the ambush sentries aren't "
              "watching)\n")
        action = input("(Do you attack? y/n) ")
        if action == "Y" or action == "y" or action == "Yes" or action == "yes":
            print("(You sneak towards the guards at the road)\n")
            print("Player vs. Goblin")

            while player.is_alive() and goblin.is_alive():
                print("Player health: " + str(player.health))
                print("Goblin: " + str(goblin.health))

                damage = player.attack(goblin)
                print("Player hits goblin for " + str(damage))
                if goblin.is_alive():
                    damage = goblin.attack(player)
                    print("Goblin hits player for " + str(damage))

            # Declaring the winner
            if player.is_alive():
                print("\nYou win!\n")
                if role == "Mage" or role == "mage":
                    player.health = 30
                elif role == "Rogue" or role == "rogue":
                    player.health = 60
                else:
                    player.health = 150
            elif goblin.is_alive() or player.is_dead():
                print("*** GAME OVER ***")
                exit()

        elif action == "N" or action == "n" or action == "No" or action == "no":
            print("(You chose not to attack and set back along the path)\n")
        print("You continue along the path and soon arrive at a bridge, there is a troll who states: \n"
              "This Thing all things devours; \n"
              "Birds, beasts, trees, flower; \n"
              "Gnaws iron, bites steel; \n"
              "Grinds hard stones to meal; \n"
              "Slays king, ruins town, \n"
              "And beats mountain down. \n")
        answer = input("What is it? ")

        if answer == "time" or answer == "Time":
            print("Troll: Correct! you may pass")
        else:
            print("Troll: WRONG! you will DIE!")
            print("Player vs. Troll")

            while player.is_alive() and Troll.is_alive():
                print("Player health: " + str(player.health))
                print("Troll health: " + str(Troll.health))

                damage = player.attack(Troll)
                print("Player hits Troll for " + str(damage))

                if Troll.is_alive():
                    damage = Troll.attack(player)
                    print("Troll hits Player for " + str(damage))

            # Declaring the winner
            if player.is_alive():
                print("Player wins!")
                if role == "Mage" or role == "mage":
                    player.health = 30
                elif role == "Rogue" or role == "rogue":
                    player.health = 60
                else:
                    player.health = 150
            elif Troll.is_alive() or player.is_dead():
                print("*** GAME OVER ***")
                exit()

    else:
        print("(You continue along the path)")
        print("Farther along the path and soon arrive at a bridge, there is a troll who states: \n"
              "This Thing all things devours; \n"
              "Birds, beasts, trees, flower; \n"
              "Gnaws iron, bites steel; \n"
              "Grinds hard stones to meal; \n"
              "Slays king, ruins town, \n"
              "And beats mountain down. \n")
        answer = input("What is it? ")

        if answer == "time" or answer == "Time":
            print("Troll: Correct! you may pass")
        else:
            print("Troll: WRONG! you will DIE!")
            print("Player vs. Troll")

            while player.is_alive() and Troll.is_alive():
                print("Player health: " + str(player.health))
                print("Troll health: " + str(Troll.health))

                damage = player.attack(Troll)
                print("Player hits Troll for " + str(damage))

                if Troll.is_alive():
                    damage = Troll.attack(player)
                    print("Troll hits Player for " + str(damage))

            # Declaring the winner
            if player.is_alive():
                print("Player wins!")
                if role == "Mage" or role == "mage":
                    player.health = 30
                elif role == "Rogue" or role == "rogue":
                    player.health = 60
                else:
                    player.health = 150
            elif Troll.is_alive() or player.is_dead():
                print("*** GAME OVER ***")
                exit()

    print("(You continue along the path in the fading sunlight)\n"
          "\n*** Dusk ***\n"
          "\n(As the night falls you climb into a tree to sleep, safe from the predators below)"
          "\n\n*** Snap ***\n")
    print("Player vs. Owlbear")

    while player.is_alive() and Owlbear.is_alive():
        print("Player health: " + str(player.health))
        print("Owlbear health: " + str(Owlbear.health))

        damage = player.attack(Owlbear)
        print("Player hits Owlbear for " + str(damage))

        if Owlbear.is_alive():
            damage = Owlbear.attack(player)
            print("Owlbear hits player for " + str(damage))

    # Declaring the winner
    if player.is_alive():
        print("Player wins!")
        if role == "Mage" or role == "mage":
            player.health = 30
        elif role == "Rogue" or role == "rogue":
            player.health = 60
        else:
            player.health = 150
    elif Owlbear.is_alive() or player.is_dead():
        print("*** GAME OVER ***")
        exit()

    print("(You step over the destroyed remains of the killed owlbear before running to the mountain between the "
          "trees)\n"
          "\n*** Noon ***\n"
          "\n(You arrive at the entrance of a cave cut into the side of the mountain)\n")
    bladeDemonFight = input("Unknown: Whoooo goooeeeesss theeerrreee, another challenger? No one can defeat me, "
                            "fight me and DIE! Do YOU wish to battle? y/n ")
    if bladeDemonFight == "Y" or bladeDemonFight == "y" or bladeDemonFight == "Yes" or bladeDemonFight == "yes":
        print(" *** Slice ***\n"
              "*** GAME OVER ***")
        exit()
    else:
        print("*sigh* Very well, you may pass\n")
    print("(You go into the cave and see that the dragon is asleep, you immediately attack)\n")
    print("Player vs. Bloodwing\n")

    while player.is_alive() and BloodWing.is_alive():
        print("Player health: " + str(player.health))
        print("Bloodwing health: " + str(BloodWing.health))

        damage = player.attack(BloodWing)
        print("Player hits Bloodwing for " + str(damage))

        if mageRange == 1:
            damage = player.attack(BloodWing)
            print("(Player gets extra attack due to element of surprise)")
            print("Player hits Bloodwing for " + str(damage))

        if BloodWing.is_alive():
            damage = BloodWing.attack(player)
            print("Bloodwing hits Player for " + str(damage))
        mageRange += 1

    # Declaring the winner
    if player.is_alive():
        print("Congratulations! You win!")
        if role == "Mage" or role == "mage":
            player.health = 30
        elif role == "Rogue" or role == "rogue":
            player.health = 60
        else:
            player.health = 150
    elif BloodWing.is_alive() or player.is_dead():
        print("*** GAME OVER ***")
        exit()

elif questPath == "N" or questPath == "n" or questPath == "No" or questPath == "no":
    print("Innkeeper: Very well tra- \n"
          "\n *** Crash ***\n"
          "  GAME OVER\n"
          "Bandits came and killed you")
    exit()
else:
    print("Sorry, I couldn't hear you")

print("This game was created by:\n"
      "\nDavid Parsons,"
      "\n&"
      "\nArya Chellappah,")

# if questPath == "fame" or questPath =="Fame":
#    print("")
# if questPath == "fortune" or questPath == "Fortune":
#    print("")
# if questPath == "power" or questPath == "Power":
#    print("")

#    "           Welcome weary traveler, to my inn. I see great deal of potential in you, would you \n"
#    "           be so kind to go on a quest for me? I know of three separate dangers that need to be \n"
#    "           vanquished, first I hear of a red mighty dragon known as Vortairn the Vicious, or \n"
#    "           perhaps you like to delve into human affairs. I also hear of a tyrant king named \n"
#    "           Acheron who rules with an iron fist. Perhaps you only want to line your pockets with \n"
#    "           gold, if so I have some information for you. Caligula's vault lies in the mountains to \n"
#    "           the east, it is said to contain the crown of Caligula which can grant untold power to \n"
#    "           the wearer, but be wary it is the most dangerous path of all. Caligula was a madman \n"
#    "           commanding the masses, known for his horrific tickling. Be warned, with great power \n"
#    "           comes great sacrifice. Which path will you take? Fame? Power? or fortune? "
