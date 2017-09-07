# osx-commands
usefull osx commands

## set input volume for mic in osx to fixed value ( no auto adjust )
`while sleep 2; do osascript -e "set volume input volume 50"; done`

## tunnel ports from remote host to your local machine
port on remote host is 9000 local host port is 9090
ssh -L 9090:host:9000 user@host
