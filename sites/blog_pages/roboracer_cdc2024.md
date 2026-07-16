---
layout: page
permalink: /blogs/roboracer_cdc2024/index.html
title: Roboracer at CDC 2024
---
<figure style="text-align: center;">
<img src="/assets/images/blogs/roboracer_cdc2024/car_banner.jpeg" alt="" style="max-width: 100%; width: 100%; margin-top: -10px; margin-bottom: 5px">
</figure>

## Starting a Roboracer Team: From 0 to First Competition

My friends, Samir and Lukas, and I had always been big motorsport and Formula 1 fans which also lead us to be interest in the area of autonomous driving in our studies.
It all started with Lukas building the base car system as part of his Bachelor's thesis in 2024. Having the hardware setup, Lukas and Samir approached me over our shared interested in autumn 2024 and proposed to take part in the then named F1Tenth competition at the CDC 2024 in Milan, Italy.

<figure>
<img src="/assets/images/blogs/roboracer_cdc2024/team_picture.jpeg" alt="LAMARRacing team at CDC 2024: Samer Shemalleh, Lukas Kutsch, Bennett Wiegard, Luis Denninger, and Moein Eskandari with the robot car in front of the Lamarr Institute and HRL Bonn logos" class="floatpic" style="width: 50%;">
</figure>

This was a big step and ambitious plan but we were happily sponsored and supported by [Nils Dengler](https://www.hrl.uni-bonn.de/people/dengler) and [Prof. Maren Bennewitz](https://www.hrl.uni-bonn.de/people/bennewitz). Luckliy we found like-minded people, Mohamed and Benno, who shared our plan and we founded our Roboracer team *LAMARRacing* funded by the [Lamarr Institute for Machine Learning and Artificial Intelligence](https://lamarr-institute.org/). Starting from late september 2024, we only had 1.5 months until our first competition, starting from nearly zero...

---

### Getting Started
We quickly realized that F1Tenth/Roboracer is an open-source-driven and friendly community. There are great materials and lectures that can be found on their [homepage](https://roboracer.ai/). Going through their lectures starting with Roboracer can be done with minimal prior knowledge but previous experience in ROS, control theory and some hardware implementation definitely speeds up the process.

Starting a robot software stack from scratch can be a tedious and long process.
We found the best way to start is the open-source [software stack](https://github.com/ForzaETH/race_stack) of one of the leading Roboracer teams [ForzaETH](https://www.forzaeth.ch/). Due to their extensive experience the library works nearly out-of-the-box but requires fine-tuning in their parameters to work well on your car. 
<figure style="text-align: center;">
<img src="/assets/images/blogs/roboracer_cdc2024/forzaeth_stack_overview.png" alt="ForzaETH race stack overview" style="max-width: 100%; width: 80%;">
</figure>
We decided to adopt their ROS2 software stack by first getting it running on the laptop in simulation and then on the car without major tuning of the hyperparamters. This initial process took us about 1 week.

At last it drove, in a slow manner, but at least it did not crash. Thus, we continued trying to understand this system to it fullest and tuning the hyperparameters of controllers, planners and hardware drivers to the best of our knowledge.

---

### Our Modifications
{: style="margin-bottom: 5px;"}
To improve the workflow, the underlying structure and controllers on our cars we spend the next four weeks implementing the several improvements/changes to customize the software stack.
<figure style="text-align: center;">
<img src="/assets/images/blogs/roboracer_cdc2024/our_software_stack.png" alt="Overview of our software stack" style="max-width: 100%; width: 90%; margin-bottom: 20px">
</figure>

**Containerization and CLI Tool.** To start off, we wanted to always have a unified system among all team members and unify our workflows when working on the car such that we not only can help each other but also to limit the entrance barrier to new team mates.
We run all our applications in a Docker container and encapsulated the container building and deployment onto the car in a CLI tool.
It also provides shortcuts for building in the ROS2 ecosystem as well as to start specific nodes and setups.<br/><br/>
**Controller System.** We build a modular controller framework which allows the plug-n-play implementation of new controllers.
Our controller manager runs a main which controls the car and a fallback controller with minimal dependencies that is run when the main controller is failing or the behaviors dictate it. This allows our car to maintain driving when external nodes are failing or it is unsafe to run the main controller.<br/><br/>    
**Pure-Pursuit Controller.** We had troubles getting the system identification run in the short time period. Thus, decided against ForzaETH's [MAP controller](https://www.forzaeth.ch/blog/map_paper/) and used the Pure-Pursuit controller. We had couple issue especially when the car was off the raceline and implemented some dampening modifications to allow it to smoothly rejoin the raceline. Moreover, we added a custom function for the look-ahead point computation which made the car more stable on straights and prevents corner-cutting in sharp corners.<br/><br/>
**Reactive Controller.** In the short time period, we were not able to implement the perception pipeline with corresponding behaviors which made our main controller blind.
Thus, we developed a custom reactive controller for racing against other cars to safely avoid them.
This controller is based on the follow-the-gap paradigm with adaptations to stabilize it on the straights and safely avoid multiple cascaded objects. <br/><br/>
**State Machine.** In addition to the controller manager, we build a new state machine which allows to easily add and subtract new states and dynamically 
decide which to run based on a priority score. This allows quick developed of cascaded behaviors even during the competitions. <br/><br/>
**Raceline Planner.** The ForzaETH race stack provides a full implementation based on ROS2 nodes using the [Global Racetrajectory Optimization](https://github.com/TUMFTM/global_racetrajectory_optimization) software stack to compute a race trajectory for a given map and vehicle parameters. To make it more flexible outside of the ROS2 framework, we build a simple GUI using [PyQt](https://doc.qt.io/qtforpython-6/) to bundle the optimization algorithms. <br/><br/>
**Parameter Tuning.** One of the most important parts when racing on a new track is to be able to adapt the system through its hyperparameters quick and easy.
To allow quick and easy adaption of parameters while driving on track, we implemented a GUI based on [ImGui](https://github.com/ocornut/imgui) that changes parameters live on the car via the ROS2 ecosystem.

---

### Competition Preperation
<figure style="text-align: center;">
<img src="/assets/images/blogs/roboracer_cdc2024/preperation02.JPEG" alt="" style="max-width: 100%; width: 100%; margin-top: -15px; margin-bottom: 20px">
</figure>

<figure>
<img src="/assets/images/blogs/roboracer_cdc2024/preperation01.JPEG" alt="" class="floatpic" style="width: 50%;">
</figure>
One week before the competition we had our system running on an acceptable pace and it came down to further tuning the controller and planning algorithms, as well as testing the procedures at the competition. Within approximately 5 weeks we had a functional autonomous racing system, which was achieved to countless extra hours from our team and late nights at the lab.

In the last week, we had to test our system on larger racetracks than in our small lab. We fortunately got a large gym but only for the night, leading to all of us shifting our sleeping schedule to the day. We powered through this last week and fixed a great deal of issues typical when setting up new systems. Our final testing included the mapping procedure, setting up and running multiple qualifying rounds and testing the system for longevity on a different race tracks.

<figure style="text-align: center;">
<img src="/assets/images/blogs/roboracer_cdc2024/preperation03.jpg" alt="" style="max-width: 100%; width: 70%; margin-top: -15px; margin-bottom: 20px">
</figure>

---

### The Competition

Arriving at the CDC in Milan, we were greated with open arms by the organizers and other teams. 
In the initial stage, each team has 5 minutes alone on the race track to map which went smoothly for thanks to our preperation.
In the next two days, we were allowed to freely use the race track to test and setup our system.

<figure>
<img src="/assets/images/blogs/roboracer_cdc2024/racetrack02.JPEG" alt="" class="floatpic" style="width: 60%;">
</figure>
Samir and I took turnes to tune our controllers on the car. While Samir was tuning his reactive controller used for races, I tuned the pure-pursuit controller we used for qualifying and the corresponding raceline used as reference for the controller. Here we the key points of adjustment were a sector-based modification of the speed and the computation of the look-ahead point. We initially had troubles with an overloaded CPU of the [NVIDIA Jetson Orin Nano](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-orin/nano-super-developer-kit/) due to redundant marker object creation for visualization in the ROS2 framework, sending of redundant messages and wrong configuration of the particle-based localization.

<figure>
<img src="/assets/images/blogs/roboracer_cdc2024/racetrack01.JPEG" alt="" class="pull-left" style="width: 40%; margin-right: 1em">
</figure>
We also realized that our router used for communication with the car was not suitable for the high-interference environment on such competitions. Within the ROS2 framework the lossy message transfer of the DDS system resulted delayed or dropped messages. This primarily hindered the localization input to the controller and the output of it to the motor controller. With two long days of testing and evenings of implementing, we felt up for the qualifying.

The qualifying went well and we were able to achieve the fifth best time. There was a clear gap between the other top-four teams and the rest of us.
Especially, team [Scuderia Segfault](https://www.tuwien.at/inf/scuderia-segfault/) from the TU Vienna, which we had a great time meeting, showed an exceptional pace.
In the playoff round, we found ourselves against ForzaETH in the second round. Due to prior mechanical issues, they had a significant disadvantage going into the race. The robust and quick driving of our reactive controller pulled through the race while ForzaETH crashed multiple times allowing us to siege a win against one of the leading teams. Ultimately, we made the fourth place overall in our first competition which was cause to celebrate!

Overall, my team and I made a lot of new friends at the competition and had great fun participating. We are excited for upcoming competitions and meeting everybody again.
Especially, I want to thank the organizers [Rahul Mangharam](https://xlab.upenn.edu/team/rahul/) and [Ahmad Amine](https://ahmadamine998.github.io/) who we had great talks with and were very helpful in helping us with the start into the competition.

<figure style="text-align: center;">
<img src="/assets/images/blogs/roboracer_cdc2024/photo_all.png" alt="" style="max-width: 100%; width: 90%; margin-top: -15px; margin-bottom: 20px">
</figure>

