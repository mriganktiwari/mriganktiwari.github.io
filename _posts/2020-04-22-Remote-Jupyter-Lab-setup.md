## Run a remote Jupyter lab setup anywhere



- Here I am assuming the remote server with Deep learning setup on Nvidia GPU is on Ubuntu.
- Install Openssh server on Ubuntu machine is not present already.
  - `sudo apt-get install openssh-server`
  - Password required of remote machine
- SSH from your local computer to remote Ubuntu machine
  - `ssh remoteuser@remoteIP`
- Setup conda virtual envs in remote system if not already resent as per requirement
  - `conda activate <env_name>`
- Fire up a **jupyter lab** session with below command
  - remoteuser**@**remotehost**:** `jupyter lab --no-browser --port=XXXX`
  - `XXXX` - any port in your remote you wish to use, by default its 8888 or 8000
  - you would get a link in this form -  `http://localhost:8888/?token=<token>`
- Forward port `XXXX` (on remote machine) to `YYYY` (on local machine) and listen to it.
  - `localuser@localhost: ssh -N -f -L localhost:YYYY:localhost:XXXX remoteuser@remotehost`
  - Password required of local machine
  - In case the `YYYY` port is busy, run below commands to kill the process
    - `lsof -n -i4TCP:YYYY` : to get the PID for this port
    - `kill <PID>`
- Open the link `localhost:YYYY` in browser in local machine.