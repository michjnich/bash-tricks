# Useful Docker functions

Stop all containers, or all containers starting with the specified paramter value.
```
function dcstop()
{
    if [ -z "$1" ]
    then
        echo "Stopping all containers"
        docker stop $(docker ps -q)
    else
        echo "Stopping containers starting with '[$1]'"
        docker ps --format '{{.Names}}' | grep "$1" | awk '{print $1}' | xargs -I {} docker stop {}
    fi
}
```
