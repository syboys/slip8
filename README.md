# slip8


Q. 1 Write a Java Program to implement State Pattern for Gumball Machine.
Create instance variable that holds current state from there, we just need to handle all
actions, behaviors and state transition that can happen 
Q.2. Write a python program to implement Decision Tree whether or not to play Tennis.
Q. 3 Create a Node.js file that demonstrates create database and table in MySQL. 



Q. 1 Write a Java Program to implement State Pattern for Gumball Machine.
Create instance variable that holds current state from there, we just need to handle all
actions, behaviors and state transition that can happen.

:
interface State {

 public void insertQuarter();
 public void ejectQuarter();
 public void turnCrank();
 public void dispense();

 public void refill();
}
 class NoQuarterState implements State {
 GumballMachine gumballMachine;

 public NoQuarterState(GumballMachine gumballMachine) {
 this.gumballMachine = gumballMachine;
 }

 public void insertQuarter() {
 System.out.println("You inserted a quarter");
 gumballMachine.setState(gumballMachine.getHasQuarterState());
 }

 public void ejectQuarter() {
 System.out.println("You haven't inserted a quarter");
 }

 public void turnCrank() {
 System.out.println("You turned, but there's no quarter");
 }

 public void dispense() {
 System.out.println("You need to pay first");
 }

 public void refill() { }

 public String toString() {
 return "waiting for quarter";
 }
}
 class GumballMachine {

 State soldOutState;
 State noQuarterState;
State hasQuarterState;
 State soldState;

 State state;
 int count = 0;

 public GumballMachine(int numberGumballs) {
 soldOutState = new SoldOutState(this);
 noQuarterState = new NoQuarterState(this);
 hasQuarterState = new HasQuarterState(this);
 soldState = new SoldState(this);
 this.count = numberGumballs;
 if (numberGumballs > 0) {
 state = noQuarterState;
 } else {
 state = soldOutState;
 }
 }

 public void insertQuarter() {
 state.insertQuarter();
 }

 public void ejectQuarter() {
 state.ejectQuarter();
 }

 public void turnCrank() {
 state.turnCrank();
 state.dispense();
 }

 void releaseBall() {
 System.out.println("A gumball comes rolling out the slot...");
 if (count != 0) {
 count = count - 1;
 }
 }

 int getCount() {
 return count;
 }

 void refill(int count) {
 this.count += count;
 System.out.println("The gumball machine was just refilled; it's new count
is: " + this.count);
 state.refill();
 } 
void setState(State state) {
 this.state = state;
 }
 public State getState() {
 return state;
 }
 public State getSoldOutState() {
 return soldOutState;
 }
 public State getNoQuarterState() {
 return noQuarterState;
 }
 public State getHasQuarterState() {
 return hasQuarterState;
 }
 public State getSoldState() {
 return soldState;
 }

 public String toString() {
 StringBuffer result = new StringBuffer();
 result.append("\nMighty Gumball, Inc.");
 result.append("\nJava-enabled Standing Gumball Model #2004");
 result.append("\nInventory: " + count + " gumball");
 if (count != 1) {
 result.append("s");
 }
 result.append("\n");
 result.append("Machine is " + state + "\n");
 return result.toString();
 }
}
 class HasQuarterState implements State {
 GumballMachine gumballMachine;

 public HasQuarterState(GumballMachine gumballMachine) {
 this.gumballMachine = gumballMachine;
 }

 public void insertQuarter() {
 System.out.println("You can't insert another quarter");
 } 
public void ejectQuarter() {
 System.out.println("Quarter returned");
 gumballMachine.setState(gumballMachine.getNoQuarterState());
 }

 public void turnCrank() {
 System.out.println("You turned...");
 gumballMachine.setState(gumballMachine.getSoldState());
 }
 public void dispense() {
 System.out.println("No gumball dispensed");
 }

 public void refill() { }

 public String toString() {
 return "waiting for turn of crank";
 }
}
 class SoldState implements State {

 GumballMachine gumballMachine;

 public SoldState(GumballMachine gumballMachine) {
 this.gumballMachine = gumballMachine;
 }

 public void insertQuarter() {
 System.out.println("Please wait, we're already giving you a gumball");
 }

 public void ejectQuarter() {
 System.out.println("Sorry, you already turned the crank");
 }

 public void turnCrank() {
 System.out.println("Turning twice doesn't get you another gumball!");
 }

 public void dispense() {
 gumballMachine.releaseBall();
 if (gumballMachine.getCount() > 0) {
 gumballMachine.setState(gumballMachine.getNoQuarterState());
 } else {
 System.out.println("Oops, out of gumballs!");
 gumballMachine.setState(gumballMachine.getSoldOutState());
 }
 } 
public void refill() { }

 public String toString() {
 return "dispensing a gumball";
 }
}
 class SoldOutState implements State {
 GumballMachine gumballMachine;

 public SoldOutState(GumballMachine gumballMachine) {
 this.gumballMachine = gumballMachine;
 }

 public void insertQuarter() {
 System.out.println("You can't insert a quarter, the machine is sold out");
 }

 public void ejectQuarter() {
 System.out.println("You can't eject, you haven't inserted a quarter yet");
 }

 public void turnCrank() {
 System.out.println("You turned, but there are no gumballs");
 }
 public void dispense() {
 System.out.println("No gumball dispensed");
 }

 public void refill() {
 gumballMachine.setState(gumballMachine.getNoQuarterState());
 }

 public String toString() {
 return "sold out";
 }

}
public class Main {
 public static void main(String[] args) {
 GumballMachine gumballMachine = new GumballMachine(2);
 System.out.println(gumballMachine);
 gumballMachine.insertQuarter();
 gumballMachine.turnCrank();
 System.out.println(gumballMachine); 
gumballMachine.insertQuarter();
 gumballMachine.turnCrank();
 gumballMachine.insertQuarter();
 gumballMachine.turnCrank();

 gumballMachine.refill(5);
 gumballMachine.insertQuarter();
 gumballMachine.turnCrank();
 System.out.println(gumballMachine);
 }
} 



Q.2. Write a python program to implement Decision Tree whether or not to play Tennis.

:		//My current code in python: 
from sklearn.cross_validation import train_test_split 
from sklearn.tree import DecisionTreeClassifier 
from sklearn.metrics import accuracy_score 
from sklearn import tree 
from sklearn.preprocessing import LabelEncoder

import pandas as pd 
import numpy as np 

df = pd.read_csv('playTennis.csv') 

lb = LabelEncoder() 
df['outlook_'] = lb.fit_transform(df['outlook']) 
df['temp_'] = lb.fit_transform(df['temp'] ) 
df['humidity_'] = lb.fit_transform(df['humidity'] ) 
df['windy_'] = lb.fit_transform(df['windy'] )   
df['play_'] = lb.fit_transform(df['play'] ) 
X = df.iloc[:,5:9] 
Y = df.iloc[:,9]

X_train, X_test , y_train,y_test = train_test_split(X, Y, test_size = 0.3, random_state = 100) 

clf_entropy = DecisionTreeClassifier(criterion='entropy')
clf_entropy.fit(X_train.astype(int),y_train.astype(int)) 
y_pred_en = clf_entropy.predict(X_test)

print("Accuracy is :{0}".format(accuracy_score(y_test.astype(int),y_pred_en) * 100))


//If you would skip this line:
X_train, X_test , y_train,y_test = train_test_split(X, Y, test_size = 0.3, random_state = 100)


//and change the method parameters to train your model like this:
clf_entropy.fit(X, Y)


Q. 3 Create a Node.js file that demonstrates create database and table in MySQL.
:

var mysql = require('mysql');
var con = mysql.createConnection({
host: "localhost",
user: "yourusername",
password: "yourpassword"
});
con.connect(function(err) {
if (err) throw err;
console.log("Connected!");
con.query("CREATE DATABASE mydb", function (err, result) {
 if (err) throw err;
 console.log("Database created");
});
});
TABLE
var mysql = require('mysql');
var con = mysql.createConnection({
 host: "localhost",
 user: "myusername",
 password: "mypassword",
 database: "mydb"
});
con.connect(function(err) {
if (err) throw err;
 console.log("Connected!");
/*Create a table named "customers":*/
var sql = "CREATE TABLE customers (name VARCHAR(255), address
VARCHAR(255))";
 con.query(sql, function (err, result) {
 if (err) throw err;
 console.log("Table created");
});
});
