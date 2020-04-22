# Useful functions

#### To display a process tree
Usage : `pt <partial process name>`
```
function pt() {
   pids="$(ps -ef|grep "$1"|grep -v grep|sed -e "s/^[[:space:]]*//"|cut -f2 -d" ")"
   for pid in ${pids}; do
      pstree -lpuGh ${pid}
   done
}
```
#### To repeatedly scan for new processes every 30 secs & output with timestamp
Usage : `pscan <partial process name>`
```
function pscan() {
   s="[${1::1}]${1:1}"
   while ps auxw | grep "$s"; do
      sleep 30
   done | stdbuf -o0 uniq | awk '{ print strftime("[%Y-%m-%d %H:%M:%S]"), $0 }'
}
```
#### To repeatedly scan the matching process every 30 secs for an ongoing status
Usage : `pscano <partial process name>`
```
function pscano() {
   s="[${1::1}]${1:1}"
   while ps auxw | grep "$s"; do
      sleep 30
   done | stdbuf -o0 awk '{ print strftime("[%Y-%m-%d %H:%M:%S]"), $0 }'
}
```
#### To run a command with x seconds interval and previx the output with a timestamp
Usage : `ftime <interval> <cmd>`
```
function ftime() {
   while (( 1==1 )); do
      eval "${@:2}" | sed "s/^/\[`date +"%Y-%m-%d %H:%M:%S"`]/"
      sleep $1
   done
}
```
