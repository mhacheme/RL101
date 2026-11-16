# BDX-R Walking Policy

Training the BDX-R droid to walk in simulation using reinforcement learning
(MuJoCo Warp).

# Final walking policy
https://github.com/user-attachments/assets/4090ea06-182c-4656-a89c-fa6b21fc9a24 

I changed the walking task settings by adding a new reward to ENV_CONFIG, "walking_height": 0.26 (mean torso height). 
Implementing the walking_height_reward function "tracks the torso height above terrain using a privileged reward signal". 
Without this change, the robot lies down and waddles in the air. A fall is defined to be a tilt beyond  70° or base height below 0.12 m. However, it seems that rule did not get triggered when the robot fell because in that position the robot's torso was not tilted more than 70°, and the center of mass of the torso is more than 0.12 m from the ground. It is possible that the policy settled for this "walking" method because lying down leads to more reward points. 
<img width="1972" height="726" alt="Screenshot 2026-11-15 130511" src="https://github.com/user-attachments/assets/6500f107-f735-46b2-bc1a-223636b283de" />

