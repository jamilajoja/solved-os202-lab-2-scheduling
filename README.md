Download Link: https://assignmentchef.com/product/solved-os202-lab-2-scheduling
<br>
<em>                                                                                     </em>

In this lab you will simulate scheduling in order to see how the time required depends on the scheduling algorithm and the request patterns.

A process is characterized by just four non-negative integers <em>A</em>, <em>B</em>, <em>C</em>, and <em>IO</em>. <em>A </em>is the arrival time of the process and <em>C </em>is the total CPU time needed. A process execution consists of computation alternating with I/O. I refer to these as CPU bursts and I/O bursts.

To calculate CPU burst times we make the simplifying assumption that, for each process, the CPU burst times are uniformly distributed random integers (or UDRIs for short) in the interval (0<em>,B</em>]. To obtain a UDRI <em>t </em>in some interval (0<em>,U</em>] use the function randomOS(U) described below. So the next CPU burst is randomOS(B). If the value returned by randomOS(B), is larger than the total CPU time remaining, set the next CPU burst to the remaining time.

Similarly, we assume the I/O times are UDRIs in the interval (0,<em>IO</em>] and hence the next I/O burst is randomOS(IO).

You are to read a file describing <em>n </em>processes (i.e., <em>n </em>quadruples of numbers) and then simulate the <em>n </em>processes until they all terminate. The way to do this is to keep track of the state of each process (e.g., ready, running, blocked) and advance time, making any state transitions needed. At the end of the run you first print an identification of the run including the scheduling algorithm used, any parameters (e.g. the quantum for RR), and the number of processes simulated.

You then print for each process

<ul>

 <li><em>A</em>, <em>B</em>, <em>C</em>, and <em>IO</em></li>

 <li>Finishing time.</li>

 <li>Turnaround time (i.e., finishing time – <em>A</em>).</li>

 <li>I/O time (i.e., time in Blocked state).</li>

 <li>Waiting time (i.e., time in Ready state).</li>

</ul>

You then print the following summary data.

<ul>

 <li>Finishing time (i.e., when all the processes have finished).</li>

 <li>CPU Utilization (i.e., percentage of time some job is running).</li>

 <li>I/O Utilization (i.e., percentage of time some job is blocked).</li>

 <li>Throughput, expressed in processes completed per hundred time units.</li>

 <li>Average turnaround time.</li>

 <li>Average waiting time.</li>

</ul>

You must simulate each of the following scheduling algorithms, assuming, for simplicity, that a context switch takes zero time. You need only do calculations every time unit (e.g., you may assume nothing happens at time 2.5).

<ul>

 <li>FCFS</li>

 <li>RR with quantum 2.</li>

 <li>Just one process active. When it is blocked, the system waits.</li>

 <li>SJF (This is <strong>not </strong>preemptive, but is <strong>not </strong>uniprogrammed, i.e., we do switch on I/O bursts). Recall that SJF is shortest job first, not shortest burst first. So the time you use to determine priority is the total time remaining (i.e., the input value C minus the number of cycles this process has run).</li>

</ul>

For each scheduling algorithm there are several runs with different process mixes. A mix is a value of <em>n </em>followed by <em>n A,B,C,IO </em>quadruples.

Here are the first two input sets. The comments are <strong>not </strong>part of the input.

<ul>

 <li>0 1 5 1 about as easy as possible</li>

 <li>0 1 5 1 0 1 5 1 should alternate with FCFS</li>

</ul>

All the input sets, with their corresponding outputs are on the NYU Classes.

The simple function randomOS(U), which you are to write, reads a random non-negative integer <em>X </em>from a file named random-numbers (in the current directory) and returns the value 1+(<em>X </em>mod <em>U</em>). I will supply a file with a large number of random non-negative integers. The purpose of standardizing the random numbers is so that all correct programs will produce the same answers.

<strong>Breaking ties</strong>

There are three places where the above specification is not deterministic and different choices can lead to different answers. To standardize the answers, you must do the following.

<ol>

 <li>A running process can have up to three events occur during the same cycle.

  <ol>

   <li>It can terminate (remaining CPU time goes to zero). ii. It can block (remaining CPU burst time goes to zero).</li>

  </ol></li>

</ol>

iii.         It can be preempted (e.g., the RR quantum goes to zero).

They must be considered in the above order. For example if all three occur at one cycle, the process terminates.

<ol start="2">

 <li>Many jobs can have the same “priority”. For example, in RR several jobs can become ready at thesame cycle and thus have the same priority. You must decide in what order they will subsequently be run. These ties are broken by favoring the process with the earliest arrival time <em>A</em>. If the arrival times are the same for two processes with the same priority, then favor the process that is listed earliest in the input. We break ties to standardize answers. We use this particular rule for two reason. First, it does break all ties. Second, it is very simple to implement. It is not especially wonderful and is not used in practice. I refer to this method as the “lab 2 tie-breaking rule” and often use it on exams for the same two reasons.</li>

 <li>A random number is chosen at two points.

  <ol>

   <li>When a running process is blocked (to determine the I/O-burst).</li>

   <li>When a ready process is run (to determine the cpu-burst).</li>

  </ol></li>

</ol>

If both events occur during the same cycle, process them in the above order.

<strong>Running your program</strong>

Your program must read its input from a file, whose name is given as a command line argument. The preceding sentence is a <em>requirement</em>. The format of the input is shown above (but the “comments” are not necessary); sample inputs are on the NYU Classes. Be sure you can process the sample inputs. Do <em>not </em>assume you can change the input by adding or removing whitespace or commas, etc.

Your program must send its output to the screen (printf() in C; System.out in Java).

In addition your program must accept an optional “–verbose” flag, which if present precedes the file name. When –verbose is given, your program is to produce detailed output that you will find useful in debugging (indeed, you will thank me for requiring this option). See the sample outputs on the NYU Classes for the format of debugging output. So the two possible invocations of your program are

&lt;program-name&gt; &lt;input-filename&gt;

&lt;program-name&gt; –verbose &lt;input-filename&gt;

My program also supports an even more verbose mode (show-random) that prints the random number chosen each time. This is useful, but your program is <strong>not </strong>required to support it.