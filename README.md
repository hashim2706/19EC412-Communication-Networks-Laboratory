
GENERATION OF  NETWORK WITH TRAFFIC 
Objective: Same network, but generate traffic using TCP and FTP. 
Code: 
# Create simulator 
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
set n4 [$ns node] 
# Create links 
$ns duplex-link $n0 $n1 1Mb 10ms DropTail 
$ns duplex-link $n1 $n2 1Mb 10ms DropTail 
$ns duplex-link $n2 $n3 1Mb 10ms DropTail 
$ns duplex-link $n3 $n4 1Mb 10ms DropTail 
$ns duplex-link $n4 $n0 1Mb 10ms DropTail 
# Create TCP agent and attach to n0 
set tcp0 [new Agent/TCP] 
$ns attach-agent $n0 $tcp0 
# Create TCP sink and attach to n3 
set sink0 [new Agent/TCPSink] 
$ns attach-agent $n3 $sink0 
# Connect TCP to Sink 
$ns connect $tcp0 $sink0 
# Create FTP application and attach to TCP 
set ftp0 [new Application/FTP] 
$ftp0 attach-agent $tcp0 
# Start FTP traffic 
$ns at 1.0 "$ftp0 start" 
$ns at 4.5 "$ftp0 stop" 
# Finish procedure 
proc finish {} { 
global ns tracefile namfile 
$ns flush-trace 
close $tracefile 
24 
close $namfile 
exec nam out.nam & 
exit 0 
} 
# Schedule finish 
$ns at 5.0 "finish" 
# Run simulation 
$ns run
## output:
![piccccc 1 cn](https://github.com/user-attachments/assets/75880f3c-5814-45b5-ab96-edf26b6d42bb)
