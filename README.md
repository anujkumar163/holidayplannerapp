# holidayplannerapp
#holiday travel destination app
import pymysql
print("--!--Welcome to Holiday Planner Agency--!--")
import pickle
f1 = open("userdetail", "wb")
i = []
mydb = pymysql.connect(host="localhost",port=3306,user="root",passwd="",database="abhay")
mycursor = mydb.cursor()

def admin_session():
    print("Login success welcome admin")
    while 1:
        print("")
        print("1. Register new customer")
        print("2. Delete Existing customer")
        print("3. Logout")
        user_option = input(str("option: "))
        if user_option == "1":
            j = 1
            print("Register New customer")
            username = input(str("customer username:"))
            password = input(str("customer password:"))
            query_vals = (username, password)
            mycursor.execute("INSERT INTO ONE1(username, password,type) VALUE (%s,%s,'customer')",query_vals)
            mydb.commit()
            print(username  +  "has been registered as a custo. member")
            while(j<=3):
                num = int(input("enter no user you want to add"))
                name= input("enter your name")
                gender = input("enter your gender, male/female")
                address = input("enter your city name")
                contno = int(input("enter your phone no."))
                mycursor.execute("insert into two2(name,gender,address,contno) values ('{}','{}','{}','{}')".format(name,gender,address,contno))
                mydb.commit()
                print(username + "has been registered as a custo. member")
                i.append(name)
                i.append(gender)
                i.append(address)
                i.append(contno)
                print(i)
                j=j+1
                if j>num:
                    break
         
        elif user_option =="2":
            print("")
            print("Delete Existing customer Account")
            username = input(str("customer  username:"))
            query_vals = (username,"customer")
            mycursor.execute("DELETE FROM ONE1 WHERE username = %s AND type = %s",query_vals)
            mydb.commit()
            if mycursor.rowcount < 1:
                print("customer not found")
            else:
                print(username + "has been delected")

        elif user_option == "3":
            break 

        
def auth_admin():
    print("")
    print("Admin Login")
    print("")
    username =input(str("username: "))
    password = input(str("password:"))
    if username == "admin":
        if password == "password":
            admin_session()
        else:
            print("Incorrect password:")
    else:
        print("Login details not recognied")

def main():
    #while 1:
    print("1. Login as costumer")
    print("2. Login as admin")
    user_option = input(str("option: "))
    if user_option == "1":
        print("costumer login")
    elif user_option == "2":
        auth_admin()
    else:
        print("No valid option was selected")
main()


def city_option():
    print("city options")
    print("1. satna")
    print("2. mahiar")
    print("3. panna")
    print("4. rewa")
    place = input("select city")
    i.append(place)
    print("City Added!")
def city_select(nm):
    nm = int(input("city options")) 
    if nm==1:
        print("satna is famous for heritage places")    
    elif nm==2:
        print("mahiar is famous for temples")          
    elif nm==3:
        print("panna is famous for diamond mines")            
    elif nm==4:
        print("rewa is famous for white tiger")
    print( "Great choice, Nice place to visit")        
print(city_option(),city_select(0))



def hotel_cost(days):
    print("hotel options")
    print("1. ram hotel")
    print("2. jain hotel")
    print("3. sai hotel")
    print("4. patel hotel")
    hotel = input("select hotel")
    print("you have select a good hotel")
    days = int(input("enter no. of days you want to stay"))
    i.append(hotel)
    mycursor.execute("insert into three3(hotel,days)values('{}','{}')".format(hotel,days))
    mydb.commit()
    print("hotel Added!")   
    return 140*days
    

def plane_ride_cost(city):
    if city=="satna":
        return 183
    elif city=="mahiar":
        return 120
    elif city=="panna":
        return 222
    elif city=="rewa":
        return 100
def rental_car_cost(days):
    if days<3:
        return days*40
    elif days>=3<7:
        return days*20
    elif days>=7:
        return days*70
def trip_cost(city, days, sp):
    city = str(input("enter city name"))
    days = int(input("enter no. of days to stay in hotel"))
    sp = int(input("enter spending momeny"))
    i.append(sp)
    print("tripcost Added!")
    return hotel_cost(days) + rental_car_cost(days) + plane_ride_cost(city) + sp

cost = print(trip_cost('rewa',5,500))

pickle.dump(i, f1)
f1.close()



print("tripcost Added!")
print(cost)

f2=open("userdetail", "rb")
data = pickle.load(f2)
print(data)
print("Updated user detail.")
f2.close()
print("!--Thank for your support--!")
print("!---mauj karoo sir--!")
print("!:-)==!Enjoy the trip!==(-:!")











