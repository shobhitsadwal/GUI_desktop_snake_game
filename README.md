# GUI_desktop_snake_game
##  This is a modified version of 1997 Nokia Snake game  , created by using TKINTER  and object oriented programming .

![snake](https://media.geeksforgeeks.org/wp-content/uploads/20210611151042/Animation.gif)

# Aim and objectives 
TO build a game using the tkinter module so that the user has the capablity to play the game in their desktop . The game is slightly different from the oringal game.

# Files to refer 
the file to refer are mainly follows 
- ```main.py``` , the main file for  running the application which also has all the imports from the various modules of the whole program .
- ```scoreboard.py``` , the module that is responsible to make the scoreboeard for the game. The score class is made inside this module .
- ```snake.py``` , the module that contains the class and their methods for the snake control and its movements
- ```food.py```, this module contains the class and methods used to create the food for the snake and various shapes and sizes that we have used to design optimum food architecture
- ```data.txt``` , this module contains the score that the user has made and progressed inside the game that we have created . 

# program requirements 

this game is strictly made using python and tkinter library .

# necessary imports 
```python
from turtle import Turtle
import random
from turtle import Screen
from snake import Snake
from food import Food
from scoreboard import Scoreboard
import time
```
these are some of the necessary imports that we have used in the project in various places and in different modules altogether . We have chosen **Object Oriented Programming** as the main approach 
in this project because **OOPS** gives the code modularity and structure and also OOPS help in developing and refactoring the code in much simpler manner . The classes and objects thaat we have used in 
this program are in some ways complementing and used as a functionality to each other , thus making refactoring easier in the future.

# code-flow
The code flow that we have optimized here is based on the concepts of **Object-Oriented-Programming**. The approach is based on the modularity of the code and creating the objects based on the classes.
The primary module is main.py in which we have the necessary imports for the other classes and modules . 

the game development is divided into primarily 3 steps 
- making of the snake.py module and creating the snake class inside to make the structure of the snake
- making the food module and creating the food class inside it to make a structure of food item.
- creating a module that tests and remaps the scoreboard of the game while the user is playing the game 

## ```snake.py``` 
inside this module after importing the turtle module we first make and design the basic layout of snake .We have many times used the ```turtle.penup```,```turtle.goto```,```turtle.head``` a lot,
these are the turtle functions that are helping us to draw the snake . You can seee from the below code how we have made different segments and then combined them together to make the proper look
as compared to a snake . The length will vary for the amount of food eaten (the concept of nearest approach discussed later), this is just a basic snippet of the code and you can view the whole code in
```snake.py``` for more information regarding to the movement and direction flow .
```python

class Snake:

    def __init__(self):
        self.segments = []
        self.create_snake()
        self.head = self.segments[0]

    def create_snake(self):
        for position in STARTING_POSITIONS:
            self.add_segment(position)

    def add_segment(self, position):
        new_segment = Turtle("square")
        new_segment.color("white")
        new_segment.penup()
        new_segment.goto(position)
        self.segments.append(new_segment)
```

## ```food.py```

inside this module we have created a food class that has a method which is made by importing the random module and the main work of that function is to place the food items at the random positons inside 
the application for the snake to approach and make the high score based on the nearest proximity of the food item . We have used ```self.speed("fastest")``` to set the food item replaced and repositioned in the fastest 
mode without delaying . Below is the code snippet for the added funtionality of the module . 

```python

from turtle import Turtle
import random


class Food(Turtle):

    def __init__(self):
        super().__init__()
        self.shape("circle")
        self.penup()
        self.shapesize(stretch_len=0.5, stretch_wid=0.5)
        self.color("blue")
        self.speed("fastest")
        self.refresh()

    def refresh(self):
        random_x = random.randint(-280, 280)
        random_y = random.randint(-280, 280)
        self.goto(random_x, random_y)
```

## ```scoreboard.py``` 

the scoreboard.py is an important module because it contains the skeleton of the score that the user makes while playing the game , along with the score it also genrated the high score column that the user makes and displayes it 
periodically , the added functionlaity here is that the we also have an option to reset the high score . Below is the code snippet . 
```python
from turtle import Turtle
ALIGNMENT = "center"
FONT = ("Courier", 24, "normal")


class Scoreboard(Turtle):

    def __init__(self):
        super().__init__()
        self.score = 0
        with open("data.txt") as data:
            self.high_score = int(data.read())
        self.color("white")
        self.penup()
        self.goto(0, 270)
        self.hideturtle()
        self.update_scoreboard()

    def update_scoreboard(self):
        self.clear()
        self.write(f"Score: {self.score} High Score: {self.high_score}", align=ALIGNMENT, font=FONT)

    def reset(self):
        if self.score > self.high_score:
            self.high_score = self.score
            with open("data.txt", mode="w") as data:
                data.write(f"{self.high_score}")
        self.score = 0
        self.update_scoreboard()

    def increase_score(self):
        self.score += 1
        self.update_scoreboard()
```

importing different modules and combinining it into tbe ```main.py``` , we can program the code and run it accordingly acoording to the structure of the objects that we have initiated .

# snake game important aspects

## for **keyboard-controls** we have the following in the main.py 
```python

screen.listen()
screen.onkey(snake.up, "Up")
screen.onkey(snake.down, "Down")
screen.onkey(snake.left, "Left")
screen.onkey(snake.right, "Right")
```

screen.listen , reacts to the keyboard prompts that the user is making and onkey are objects that we have initiated to make the keyboard controls .

## the function for wall collision , tail collision  and food collision

```python
  #Detect collision with food.
    if snake.head.distance(food) < 15:
        food.refresh()
        snake.extend()
        scoreboard.increase_score()

    #Detect collision with wall.
    if snake.head.xcor() > 280 or snake.head.xcor() < -280 or snake.head.ycor() > 280 or snake.head.ycor() < -280:
        game_is_on = False
        scoreboard.game_over()

    #Detect collision with tail.
    for segment in snake.segments:
        if segment == snake.head:
            pass
        elif snake.head.distance(segment) < 10:
            game_is_on = False
            scoreboard.game_over()
```

# Conclusion

thus we can see with the help of various classes and differnet modules we have created a snake game which is skightly modified as the speed is way higher initially . We have also seen different functions for the game and also 
tested those functions. 

online snake game is available at https://snake.io/ for understanding the basics of the game and much more if you haven't played this game before . 




        





