---
layout: page
permalink: /blogs/nimbro_robocup2024/index.html
title: NimbRo at RoboCup 2024
---
{: style="margin-bottom: 5px;"}
<figure style="text-align: center;">
<img src="/assets/images/blogs/nimbro_robocup2024/title_image.jpg" alt="" style="max-width: 100%; width: 100%; margin-top: -10px; margin-bottom: 0px;">
</figure>

## NimbRo at RoboCup 2024 in Bourdeaux

This year was my second time taking part in the RoboCup Humanoid AdultSize Soccer league as part of team [NimbRo](https://www.nimbro.net/). Over the last year, I have taken over the perception system from Angel, and continued understanding the complete software stack.
<figure>
<img src="/assets/images/blogs/nimbro_robocup2024/team_photo.jpg" alt="" class="floatpic" style="width: 55%;">
</figure>
This year two new team members, some fellow Master students, Vitalii and Nick joined. In the same position as I was a year ago, they started understanding our extensive software stack and helped out in the perception and behavior system of the robot. Throughout our extensive preperation period prior to this year's RoboCup, we all grew closely together and improved the speed of our robot, making it kicks more dynamic and its perception system.

<figure>
<img src="/assets/images/blogs/nimbro_robocup2024/working_extra_hard.JPEG" alt="" class="pull-left" style="width:35%; margin-right: 1em;">
</figure>
After last year's RoboCup, I started implementing a new industrial camera capable of capturing the game on 4K resolution. To support the processing of such large images I have refactored the complete vision pipeline to implement CUDA-based processing, mitigate any bottlenecks and enable real-time processing of 4K imagery.
The pipeline is based on a novel [FasterNet-based](https://arxiv.org/abs/2303.03667) U-Net, TensorRT optimized operations and a custom GPU-scheduler to mitigate any memory transfer bottlenecks.
This allowed us to detect and track balls from anywhere on the field but was instable in variable lighting conditions as observed at the competition. Moreover, the highly different competition conditions revealed more bugs and required many modifications made during the competition. 
<figure>
<img src="/assets/images/blogs/nimbro_robocup2024/nimbro_romela_finals.jpg" alt="" class="floatpic" style="width: 55%;">
</figure>
The initial round robin stage went losing a couple of games but we were available to fix our problems for the playoff stage. In a good run, we were able to make the finals where we faced the [RoMeLa team](https://www.romela.org/). Since last year, they made significant improvements having an agile, fast-walking system which was able to out-pace us in every means. With a 1:6 defeat against RoMeLa, we made second in this years RoboCup Humanoid AdultSize soccer competition. After a great run at the technical competitions showing of some of our improvments, we still managed to win this year's *Best Humanoid* award.

<figure>
<img src="/assets/images/blogs/nimbro_robocup2024/after_competition.JPEG" alt="" class="pull-left" style="width:35%; margin-right: 1em;">
</figure>
This year's competition definitely improved significantly. We have seen many impressive new humanoid robots such as the [Unitree G1](https://www.unitree.com/g1), the [Booster T1](https://www.booster.tech/booster-t1/) or the [Fourier GR-1](https://www.fftai.com/products-gr1). We had a great time, eventhough stressful at times, and really enjoyed our time at this year's RoboCup. We rounded up the competition with a nice *Bierchen*, meeting up with the RoMeLa team and a trip through Eindhoven.