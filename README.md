# truck-simulation-python

TRUCK MOVEMENT IN HIGH ALTITUDE AREAS

Overview
In Himalayan region logistics is carried out through trucks only. In that region very narrow roads are available where only one truck can pass at a time. For crossing there are locations/junctions at some intervals where the crossing can be done. If two trucks face one another in midway of the road then one truck has to move backward to a location where the crossing is possible

Goals
To build a model for truck movement in the Himalayan region that is single lane road with lay-by junctions
To be able to understand the issues in developing and applying simulation to real world systems


Constraints and Assumptions

Constraints:-
Only one truck can be present at one position on road
Trucks can only cross at junctions

Assumptions:-
Junction Capacity = infinite (#trucks that can stand by)
Speed of trucks to be equal and uniform throughout
Speed of truck moving forward = Speed of truck moving backward
Trucks are considered as point size entities for ease
A small precision band(𝜹 distance) is considered while calculation of positions in order to perform continuous simulation


Approach
Below are discussed the required variables and parameters for our simulation
Variables

Every Truck dictionary contains following variables :- 
x_curr- The current coordinate/position of the truck
Curr_dirn- Represents the direction in which the truck is moving. +1 indicates forward movement (along positive x-axis) while -1 indicates backward movement.
Root_dirn- The direction in which the truck needs to travel with respect to the origin to reach the destination
Speed- Represents the speed of the truck
Reverse Speed
Arr_time- The time at which truck arrives at origin
depart_time- The time at which the truck reaches its destination
For_dist- Total forward distance travelled by the truck
Back_dist- Total backward distance travelled by the truck

Parametres

Time_delta - a very small increment to run simulation
No_of_junctions - #junctions including start and end
Position_of_junct - [position of junctions on axis] (~Normal dist.)
No_of_trucks_to_sim_each_dir - no of trucks that will arrive
For_truck_arr_times = [arrival times for forward moving trucks] (~uniform dist)
Back_truck_arr_times = [arrival times for backward moving trucks] (~uniform dist)
Sim_run_totaltime - total simulation time limit decided 

Now let's jump to our approach, basically
Trucks arrive according to uniform distribution at their respective origins
Trucks keep moving in their root direction until confronts another truck
Here a decision needs to made which sets of trucks will move reverse - done on the basis of total reverse distance to be travelled by each set of trucks moving in corresponding directions, changing current directions of a set of trucks
After they reach nearby junction, they start moving back to their root direction as junction clears traffic
 This run continues until 
Total simulation time is complete (pre-defined)
All trucks reach their destination

Following functions were defined in order to simulate our process :-

I. Next_position - Updates the current position of the truck 
	x_curr= x_curr + (curr_dirn*speed*time)

II. for_truck_arr - Appends a new truck whose root direction is +1 in the list of currently active trucks


III. back_truck_arr - Appends a new truck whose root direction is -1 (whose destination is along negative x- axis) in the list of currently active trucks

IV. not_near_junction - Checks whether any of the colliding trucks are near the junction or not

V. dist_from_left_junc and dist_from_right_junc - Calculates distance of truck from nearest left and right junction

VI. Movement decision - Checks for the pair of trucks with collision and assigns them direction of movement based on cumulative dist_from_left_junc and dist_from_right_junc functions.

Observations
We had three variables namely number of backward and forward trucks, number of nodes and speed of each truck.
We used a number of forward and backward trucks as [5,5] and varied the number of nodes with time of arrival of trucks modeled by Uniform(0,25) and Normal distribution(μ=5,σ=2).
Number to nodes varied between the range of [ 8-18 ] and data were collected . Using the collected data we calculated total forward distance travelled , Backward distance travelled , Total time taken etc.
From the Graph we can see that all the metrics follow the same pattern for both the considered distributions.
Results
Dependency on distribution
We can see that the total time decreases when we increase the number of nodes from 16 in case of normal distribution whereas in uniform sixteen number of nodes is the most optimum number as it further starts increasing.
Uniform Distribution (0,25) =Optimum number of nodes = 16
Normal Distribution (5,2) =Optimum number of nodes = 18
Dependency of metrics on distribution 
For Normal distribution the values of metrics were greater than one obtained from Uniform distribution for the nodes 8,10 and 12 but when we increase the number of nodes from 12 to 18 we can see that truck arrival  time modelled Normal distribution performs better.


Conclusion and Further work

Different objectives to be fulfilled
Our distribution of junctions might be required to change when our objective varies from say minimizing distance to minimizing time
Arrival of trucks distribution might change according to times, again demanding change in junctions distribution
	All this can be done by merely changing input parameters to our model

Tolerance for backward distance travelling 
This can be one of our constraints, as harsh conditions may not support reverse movement of trucks on such high altitude areas
Arrival of trucks distribution should be kept more than anticipated so as to avoid any risk 

A lot of constraints can be added to make our simulation model more realistic or bend it according to specific requirements to be fulfilled




