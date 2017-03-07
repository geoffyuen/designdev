# MacOS Things

- [Clone drive to smaller drive using only MacOS tools](http://apple.stackexchange.com/questions/48798/cloning-a-half-full-500-gb-drive-to-a-256-gb-ssd-drive)

# Macbook close lid to sleep with external display (not working on Sierra)

`sudo nvram boot-args=iog=0x0`

Restore it to "dumbass-leave-it-on" setting: `sudo nvram -d boot-args` or reset pram.
