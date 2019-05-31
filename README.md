# ft_sommelier

##Machine Learning Project


 This Dockerfile setup assumes you are going to be using the same physical
 mac for a project. In theory, it should not matter which physical mac you end
 up using, but I take no responsibility if you change where you sit, and stuff
 suddenly doesn't work >_>.

# Initial Setup Commands (should only be run once, probably!)
Run these following commands:
 1) docker-machine create --driver virtualbox sommelier

If docker-machine doesn't run, you'll need to: brew install docker-machine
 Wait for 1) to finish running completely before running 2)!!
 2) eval $(docker-machine env sommelier)

`cd` into the whichever directory contains this Dockerfile then run 3)
 If docker doesn't run, you'll need to: brew install docker
 3) docker build -t ft_sommelier .
 4) docker volume create notebooks

# Starting up a ft_sommelier container

 Remember the 8888/?token=... part that will show up when you run 5)!!
 5) docker run -it -p 8888:8888 -v notebooks:/notebooks ft_sommelier

 You can get your <docker-host-ip> with: docker-machine ip sommelier
 In your browser address:
 6) <docker-host-ip>:8888/?token=...%

# What to do if I restart or log out? 

 If you log out or restart your computer you'll need to restart the
 docker machine when you log back into your mac. Run the following:

 7) docker-machine start sommelier
 8) eval $(docker-machine env sommelier)
 Then you can proceed to re-run steps 5) and 6) again

# Finished the project and want to cleanup?

 After you are done with the project it might be a good idea to clean up all
 images and the virtual machine since they take up a LOT of space...
 (Do it for Tony!!!)

 WARNING: THE FOLLOWING COMMANDS WILL DELETE ALL NOTEBOOKS AND DATA!!

 9) docker stop $(docker ps -a -q)
 10) docker rmi $(docker images -a -q)
 11) docker volume prune
 12) docker-machine rm sommelier
