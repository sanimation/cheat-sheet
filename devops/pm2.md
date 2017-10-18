# PM2 CheatSheet
## Start
### Fork mode

```
$ pm2 start app.js --name my-api
```

### Cluster mode
Will start maximum processes with LB depending on available CPUs

```
$ pm2 start app.js -i 0

```

Same as above, but deprecated.

```
$ pm2 start app.js -i max
```

## Listing

Display all processes status

```
$ pm2 list
```

Print process list in raw JSON

```
$ pm2 jlist 
```

Print process list in beautified JSON

```
$ pm2 prettylist
```

Display all informations about a specific process

```
$ pm2 describe 0
```

Monitor all processes

```
$ pm2 monit
```

## Logs

Display all processes logs in streaming

```
$ pm2 logs [--raw]
```

Empty all log file

```
$ pm2 flush

```

Reload all logs

```
$ pm2 reloadLogs
```

## Actions

pm2 stop all           # Stop all processes
pm2 restart all        # Restart all processes

pm2 reload all         # Will 0s downtime reload (for NETWORKED apps)

pm2 stop 0             # Stop specific process id
pm2 restart 0          # Restart specific process id

pm2 delete 0           # Will remove process from pm2 list
pm2 delete all         # Will remove all processes from pm2 list

## Misc
Reset meta data (restarted time...)

`$ pm2 reset <process>`    

Update in memory pm2

```
$ pm2 updatePM2
```

Ensure pm2 daemon has been launched

```
$ pm2 ping
```

Send system signal to script

```
$ pm2 sendSignal SIGUSR2 my-app

```

```
$ pm2 start app.js --no-daemon
$ pm2 start app.js --no-vizion
$ pm2 start app.js --no-autorestart
```

# Docker
## Useful commands

Command | Description
--------|------------
```$ docker exec -it <container-id> pm2 monit``` | Monitoring CPU/Usage of each process
```$ docker exec -it <container-id> pm2 list``` | Listing managed processes
```$ docker exec -it <container-id> pm2 show``` | Get more information about a process
```$ docker exec -it <container-id> pm2 reload all``` | 0sec downtime reload all applications