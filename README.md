Requirement:
software : the vesion of quartus need upon 16.
 
This project reference the scr1-sdk :
His board is de10lite bus mine is de2-115, so i need to modify something about it.
Here is Modify:
1. pin planner :
2. the assignment of the uart receive pin and uart transmit pin are just reverse with the de2-115 mannual.(I don't  know why)

Notice :

If you copy the project to your dictionary path, then you need to modify the path of the  .hex file in qysy's on-chip ram module 