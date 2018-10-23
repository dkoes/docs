# Connecting

You should have an account on at least one workstation.  There are currently two shared workstations, `apogee.csb.pitt.edu` and `perigee.csb.pitt.edu`.
All workstations are behind the Pitt firewall, which means you cannot directly connect to them from outside the Pitt network (or even while connected to Pitt wireless).
Contact the Dept. IT staff to get VPN access.  You will need special CompBio credentials to access our network even if you already have VPN setup.

[Setup public keys](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1604)

Once you can connect to a workstation with ssh, you can port tunnel to run jupyter notebook remotely.

`ssh -L 8080:localhost:8888 apogee.csb.pitt.edu`

If you then run a jupyter notebook server on port 8888 on apogee, you will be able to access it in your web browser at port 8080 
(ie, goto `localhost:8080` in your webbrowser on the machine you ssh’ed from).  

Of course, 8888 is the default port so it probably won’t be available unless you are the first person to run jupyter, 
so you should pick a random port number (between 10000 and 65536) and launch jupyter with the specified port:  

`jupyter notebook --no-browser --port 12345`
