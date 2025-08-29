GENERATION OF NETWORK WITHOUT TRAFFIC 
Objective: Create nodes and links, but no traffic/application. 
Code: 
# Create a simulator object 
set ns [new Simulator] 
# Open trace and NAM files 
set tracefile [open out.tr w] 
set namfile [open out.nam w] 
$ns trace-all $tracefile 
$ns namtrace-all $namfile 
# Create nodes 
set n0 [$ns node] 
set n1 [$ns node] 
set n2 [$ns node] 
set n3 [$ns node] 
# Create links 
$ns duplex-link $n0 $n1 1Mb 10ms DropTail 
$ns duplex-link $n1 $n2 1Mb 10ms DropTail 
$ns duplex-link $n2 $n3 1Mb 10ms DropTail 
# Finish procedure 
proc finish {} { 
global ns tracefile namfile 
$ns flush-trace 
close $tracefile 
close $namfile 
exec nam out.nam & 
exit 0 
} 
# Schedule finish 
$ns at 5.0 "finish" 
# Run simulation 
$ns run 

## Output:
![picc 2 cn](https://github.com/user-attachments/assets/8ba1f7c5-2252-4d87-8517-a446cbe95b94)

