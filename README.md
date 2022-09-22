MENU = {
    "espresso": {
        "ingredients": {
            "water": 50,
            "coffee": 18,
        },
        "cost": 1.5,
    },
    "latte": {
        "ingredients": {
            "water": 200,
            "milk": 150,
            "coffee": 24,
        },
        "cost": 2.5,
    },
    "cappuccino": {
        "ingredients": {
            "water": 250,
            "milk": 100,
            "coffee": 24,
        },
        "cost": 3.0,
    }
}



def coins_sum():
    print("please insert coins")
    quarters=int(input("How many quarters? "))
    value_per_quarter=0.25
    dimes = int(input("How many dimes? "))
    value_per_dime = 0.10
    nickel=int(input("How many nickel? "))
    value_per_nickel = 0.05
    pennies = int(input("How many pennies? "))
    value_per_penny = 0.01
    coin_sum=(quarters*value_per_quarter)+(dimes*value_per_dime)+(nickel*value_per_nickel)+(pennies*value_per_penny)
    return coin_sum


def is_resource_suffice(choice):
    for item in choice:
       if choice[item]>=resource[item]:
           print(f"Sorry there is not enough{item}")
           return False
    return True

def make_coffee(choice,order_ingredients):
    for item in order_ingredients:
        resource[item]-=order_ingredients[item]
        print(f"Here is your {choice}")

def report():

    water = 300
    milk = 200
    coffee = 100
    Money = 0
    print(f"Water: {water}ml \nMilk:{milk}ml \nCoffee:{coffee}mg")

resource={ "water":300,"milk":200, "coffee":100,
"Money":0,}


choice=input("What would you like to have? latte or Cappuccino or espresso? :" ).lower()


print(MENU["latte"]["ingredients"]["water"])
total_price=0
order_ingredients={}
if choice=="report":
    report_data=report()
    print(report_data)

if choice=="latte":
    total_price=round(coins_sum(),2)
    print(f"total:{total_price}")
    latte_price=MENU["latte"]["cost"]
    exchange =0
    order_ingredients = MENU["latte"]["ingredients"]
    if  is_resource_suffice(order_ingredients)==True:

      if latte_price>total_price:
        print("sorry,insufficient amount,amount refunded")

      elif latte_price<total_price:
        exchange=total_price-latte_price
        print(f"Take your exchange{exchange}")

        resource["Money"]+=latte_price
        make_coffee(choice,order_ingredients)
    else:
       print("No resource is not suffice")
elif choice == "cappuccino":

    total_price = round(coins_sum(),2)

    print(f"total:{total_price}")
    cappuccino_price = MENU["cappuccino"]["cost"]
    exchange = 0
    order_ingredients = MENU["cappuccino"]["ingredients"]
    if is_resource_suffice(order_ingredients)==True:
     if cappuccino_price > total_price:
        print("sorry,insufficient amount,amount refunded")
     elif cappuccino_price < total_price:
        exchange = total_price - cappuccino_price
        print(f"Take your exchange{exchange}")
        resource["Money"] += cappuccino_price
        make_coffee(choice, order_ingredients)

    print(total_price)


elif choice == "espresso":
    total_price=round(coins_sum(),2)
    print(f"total:{total_price}")

    espresso_price = MENU["espresso"]["cost"]
    exchange = 0
    order_ingredients = MENU["espresso"]["ingredients"]
    if is_resource_suffice(order_ingredients)==True:

     if espresso_price > total_price:
        print("sorry,insufficient amount,amount refunded")
     elif espresso_price < total_price:
        exchange = total_price - espresso_price
        print(f"Take your exchange{exchange}")

        resource["Money"] += espresso_price
        make_coffee(choice, order_ingredients)


print(f"Available resource{resource}")
