# BDX-R Walking Policy

Training the BDX-R droid to walk in simulation using reinforcement learning
(MuJoCo Warp).

## Final walking policy
Train: completed in 996s.
Training result: 12,000 steps in 976s on Tesla T4.

https://github.com/user-attachments/assets/4090ea06-182c-4656-a89c-fa6b21fc9a24 

I changed the walking task settings by adding a new reward to ENV_CONFIG, "walking_height": 0.26 (mean torso height). 
Enabling the walking_height_reward function "tracks the torso height above terrain using a privileged reward signal". 
Without this change, the robot lies down and waddles in the air. A fall is defined to be a tilt beyond  70° or base height below 0.12 m. However, it seems that rule did not get triggered when the robot fell because in that position the robot's torso was not tilted more than 70°, and the position of the torso is more than 0.12 m from the ground. It is possible that the policy settled for this "walking" method because lying down was leading to more reward points. 

Screenshot of fallen robots:

<img width="1972" height="726" alt="Screenshot 2026-11-15 130511" src="https://github.com/user-attachments/assets/6500f107-f735-46b2-bc1a-223636b283de" />

With the default settings, the check printed "FAIL: stayed upright; speed error > 0.05 m/s". Since the robot was laying down, its speed was 0 m/s. By adding the walking_height reward, lying on its side makes the robot lose this reward every step. 

BASELINE_CHECK:

falls=0/3, 

speed error (m/s), speedMAE=0.027, 

yaw error (rad/s), yawMAE=0.022, 

mean max drift (m), cross-track=0.096m

## Reward Variation Experiment
Original video:

https://github.com/user-attachments/assets/509cad72-bd42-4f41-a2e7-d1f5dda73e9a

Reward variation video:

Train: completed in 1032s.
Training result: 12,000 steps in 1013s on Tesla T4.

https://github.com/user-attachments/assets/0b5c3c97-aa6e-4ae4-944f-7f898876d93a

PREDICTION: The feet will stay flatter during stepping.

LEVEL_FEET_WEIGHT: 0.75

I followed the instructor example and changed only level_feet_weight from 0 to 0.75. This means having flat feet now counts as a reward and we can see the robot walk a bit faster. The measured swing-foot tilt fell from 7.8° to 6.5° while foot landings increased from 3.78 /sec to 4.56 /sec.

VARIATION_CHECK: 

falls=0/3,
speed error (m/s), speedMAE=0.015, 

yaw error (rad/s), yawMAE=0.022, 

mean max drift (m), cross-track=0.006m

Comparing the two results:
<img width="1478" height="234" alt="image" src="https://github.com/user-attachments/assets/44e5157a-08ca-43ce-8c4f-088896fe4054" />
The baseline speed was 0.273 m/s and variation speed 0.291 m/s. 

## Limitations
The walking check did not count the fall in my first few iterations, and only failed due to speed error. This means the check alone can be misleading so we need to verify with the video. 

## Final Walking Policy Using my Personal Laptop

https://github.com/user-attachments/assets/d3f7d3d9-11d3-4f90-8fb6-804223195942

Running this policy using my local GPU took less time (around 10 minutes), but produced an unexpected result since the robot shuffled instead of taking proper steps. I used the same values as the ones in Google Colab, however it still gave me a different result as can be seen in the video above. 

I then added the flat feet reward to see if it would help produce a better result and the speed error dropped from 0.086 to 0.018 m/s and the check passed. 

Here is a video of the final walking policy running on my personal laptop:

https://github.com/user-attachments/assets/c2c74991-da92-4694-bcc8-4052689c7604


