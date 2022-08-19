# Deploy Caldera Sandcat agent plug-in as a Windows Service

Addition to the Sandcat plug-in on MITRE Caldera. Adds a GUI option to deploy the agent as a randomly-named agent executable & Windows Service.

## What it does
- Deploys Sandcat as a Windows Service
- Runs commands as 'system'
- Downloads the agent as a randomly-named .exe
- Creates a randomly-named Windows Service & starts it
- Adds the option to the agent deployment menu in the Caldera GUI
- Maintains persistence on target hosts
- If the agent dies, the service will automatically reconnect to the C2

## Usefulness
- The Caldera Sandcat plug-in only supports installation as a background process for Linux/Darwin
- Persistence of the agent on target hosts (in case of connection issues or reboot)
- Testing detections for commands run from background processes

## Adding the plug-in to Caldera
- Gracefully stop the Caldera server from the terminal running it: 
  [Ctrl+C]
- Backup, then overwrite the .yml in caldera/plugins/sandcat/data/abilities/command-and-control/ with the custom .yml.
    - sudo git clone https://github.com/Ce1s/caldera-sandcat-plugin-deploy-as-windows-service.git --recursive
- Start the Caldera server with the fresh flag (note that this will remove user data, read Caldera docs regarding backups: https://caldera.readthedocs.io/en/latest/Server-Configuration.html?highlight=--fresh#startup-parameters):  
  [sudo python3 server.py --fresh]
- Deploy a new Windows agent in the GUI; you will find this option under Windows variations
- Script must be executed as administrator 

## Cleaning up
Steps to perform when you no longer need the agent on the target host.
### Stop this:
- Randomly-named Windows Service [nssm stop <service_name>]
### Remove these:
- NSSM directory
- NSSM path entry
- Randomly-named Sandcat agent executable
- Randomly-named Windows Service [nssm remove <service_name>]

## Maintainer
I made this as a proof-of-concept for Caldera extensibility, as part of a study project. I'm not a Powershell expert - please let me know of any issues or suggestions for improvement.
  
