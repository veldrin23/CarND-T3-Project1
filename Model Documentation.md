### CarND-Path-Planning-Project 
André Marais
2018-01-26
---

#####Reflections
The project walkthrough and Q&A really helped a lot to get things up and going. My main worry was how will I get the car to transition from one lane to the other in a smooth fashion. The spline function really helped a LOT with this. 

The challenge I faced was how to get the car to switch lanes in a logical fashion. I spent a few days on the project, and every time I was driving on the highway myself, I paid attention to what I would do under certain situations. For one, I'd keep on the highway and avoid oncoming traffic :) After that, what lane do you choose when you want to overtake someone? Even though it's better to go over to the faster lane (more to the centre) if you want to overtake, in this simulator there didn't seem to be a rule of 'faster lanes are more to the centre '. Considering this, I use a simple cost function which takes into account how much open space there is in the adjacent lanes.

When my car gets too close to a car in the same lane, it firstly checks if it’s safe to move into the adjacent lanes. It checks for cars 20m ahead and 5m behind it. After this, it will check if the lane if viable, and then calculate the cost of each option and then go for the lowest cost action. 

The functions I wrote to help me with this are as follows:

* possible_lanes
Takes in an integer and returns a vector of integers. Vector contains all the viable lanes

* super_simple_cost_function
Takes a double, returns a double. Function calculates a cost based on a given distance. The cost functions is as follows: (1 - exp(-1/dist))

* lane_changer
Takes an integer (current lane), vector of boolean values (safe lanes) and a vector of doubles (open spaces in lanes). This function uses the above functions to return a single target lane which is safe and has the lowest cost. 

##### Challenges faced
One challenge I faced was to keep the car in the designated lane if there was a car in front of it, right after the change. Originally my lane changing function would hop between the old and new lane which would keep the car between the lanes. This was solved by using the cost function with the valid lane boolean values. 

One approach I think that would be interesting, is to have a ‘best lane’ function, and a function to plan the router to that lane. If it means that the car needs to skip a lane to get to the other side, it would match the speed of the adjacent cars and switch lanes until it gets to the target lane. In a scenario with more than 3 lanes it might be a much better solution than my current program. 
