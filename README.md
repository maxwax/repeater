repeater
========

Repeater automates continuous benchmarking.  Launch n copies, wait for completion, repeat.

### Example use

$ nohup repeater --copies 8 --name 8waytest --appcli "./mybenchapp --start 10 --end 32768" &

Summary of what this does:

* Use the 'nohup' command and '&' symbol to launch repeater as a background process and capture its output to nohup.out.
* With each iteration of repeater, launch 8 simultaneous copies of the command "mybenchapp" with parameters "--start 10 --end 32768"
* Capture the output and execution time of each instance of "mybenchapp" in a ./results-logs directory (default, not specified above)
* Log files should contain the keyword 8waytest to become app-output.8waytest.1, .2, .3, etc, and time-output.8waytest.1, .2, .3, etc.

When all 8 instances of "mybenchapp" have completed, the process will be repeated with another 8 instances.

This allows the user to run multi-threaded benchmark applications continuously for long periods of time to gather interesting data.

### Stopping repeater

The process will be stopped when the file ./results-logs/stop.repeating or ./results/stop-repeating are observed.

The check for the stop file is only performed after all launched instances are completed, so you may have to kill or stop them manually to get repeater to shutdown cleanly.

You can always just kill repeater, too.

### Options

```
--copies <n>
```
Launch n simultaneous instances of your benchmark program.  The default for this is one per logical CPU see by the OS.

```
--name <keyword>
```
Include the keyword in log filenames.  Each instance's output is logged with the format app-output.[keyword].[instance#].  Each instance's execution time is logged with the format time-output.[keyword].[instance#].  The default is 'def' if no --name parameter is provided.

```
--launchwait <seconds>
```
After launching instances, sleep for n seconds, before starting the instance monitoring process.

```
--monitorwait <seconds>
```
After checking to see if all instances have completed, sleep n seconds, before checking again.

```
--appcli <command> [parameters]
```
Execute this command to launch instances.  Place commands with parameters in one quoted element: "./mycommand --parameter one -p 2 three"

```
-- help
```
Display command line syntax

```
--debug
```
Output debugging information.

