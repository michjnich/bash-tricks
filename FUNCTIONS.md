# Useful functions

# To display a process tree
Usage : pt <partial process name>
```
function pt() {
   pids="$(ps -ef|grep "$1"|grep -v grep|sed -e "s/^[[:space:]]*//"|cut -f2 -d" ")"
   for pid in ${pids}; do
      pstree -lpuGh ${pid}
   done
}
```

# To repeatedly scan for a process every 30 secs & output with timestamp
```
function pscan() {
   s="[${1::1}]${1:1}"
   while ps auxw | grep "$s"; do
      sleep 30;
   done | stdbuf -o0 uniq | awk '{ print strftime("[%Y-%m-%d %H:%M:%S]"), $0 }'
}
```
