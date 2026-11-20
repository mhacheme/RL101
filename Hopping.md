# Hopping policy 

## Video of final hopping policy
ran on NVIDIA GeForce RTX 5070 Laptop GPU

https://github.com/user-attachments/assets/048db5a2-fe3f-419a-9944-d55eee4e5dd2

Results:

Jump 1 | clearance 4.8 cm | flight 0.18 s | fell: False | passed: True

Jump 2 | clearance 4.7 cm | flight 0.18 s | fell: False | passed: True

Jump 3 | clearance 4.7 cm | flight 0.18 s | fell: False | passed: True


## Click Jump

https://github.com/user-attachments/assets/649f4417-c6b0-49d5-a113-926f4d4281df


## Other Tests

I attempted to make it jump higher by changing hop_height  from 0.05 to 0.1. Unfortunately it seems like that was too large of a jump and a target the robot couldn't reach. 

https://github.com/user-attachments/assets/1233e298-bb39-4c6e-a537-83d370acfc1a

Jump 1 | clearance 0.2 cm | flight 0.04 s | fell: False | passed: False

Jump 2 | clearance 0.0 cm | flight 0.04 s | fell: False | passed: False

Jump 3 | clearance 0.0 cm | flight 0.04 s | fell: False | passed: False


I then tried to change it to 0.07 instead to see if it would work then and obtained the following results:


https://github.com/user-attachments/assets/e9550506-6ed0-4def-89e1-b976a34579d2


Jump 1 | clearance 7.6 cm | flight 0.20 s | fell: False | passed: True

Jump 2 | clearance 7.7 cm | flight 0.20 s | fell: False | passed: True

Jump 3 | clearance 7.6 cm | flight 0.20 s | fell: False | passed: True

It seems to also be moving forward slightly. It also seems to be leaning forward a lot, which could be due to the reward points associated with staying upright and landing, which are much lower than hop height. Also, maybe adding more steps (currently at 6000) could give the droid more time to learn how to hop. 







