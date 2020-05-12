---
layout: page
title: "Course Schedule"
permalink: /schedule.html
---

<style>
table.calendar {
    font-family: arial, helvetica;
    font-size: 10pt;
    empty-cells: show;
    border: 1px solid #000000;
    border-collapse: collapse;
}
table.calendar tr td {
    border: 1px solid #aaaaaa;
}
table.calendar tr {
    vertical-align: top;
    height: 5em;
    background: #ffffff;
}
table.calendar thead tr {
    text-align: center;
    background: #444444;
    color: #ffffff;
    height: auto;
    font-weight: bold;
}
/*.date {
	background: Gainsboro;
}*/
.holiday {
    background: #F0FFF0;
}
.lecture {
    background: #ffffaa;
}
.presentation {
    background: Plum;
}
.exam {
    background: DarkOrange;
}
.important {
    background: #FFEBCD;
}
.nodue {
    background: #FFFAFA;
}
.optional {
    background: Linen;
}
.reading {
    color: Black;
}
.deadline {
    background: #ffaaaa;
}
.hwdue {
    color: #ff0000;
	font-weight: bold;
}
.assignment {
    color: #0aa00a;
	font-weight: bold;
}
.date {
	background: #eeeeee;
    color: #444444;
}
</style>

The course schedule is tentative and subject to change.
<p>
<table class="calendar" cellspacing="0" cellpadding="6" width="100%">
 <thead>
  <tr>
   <td width="10%">Week</td><td width="60%">Monday</td>
   <td width="30%">Thursday</td>
  </tr>
 </thead>

<tr> <!-- week of Jan 20 -->
  <td id="2020-1-20" class="date"><b>Week 1</b></td>
  <td class="holiday">Jan 20<br/>
	<b>MLK Day</b> (NO CLASS)</td>
  <td class="nodue">Jan 23</td>
</tr>
<tr> <!-- week of Jan 27 -->
  <td id="2020-1-27" class="date"><b>Week 2</b></td>
  <td class="lecture">Jan 27<br/>
	<b>Lec 1:</b> Introduction, process abstraction [<a href="./public/lecs/lec1-intro.pdf">slides</a>]
			[<a href="./public/lecs/lec1-intro+notes.pdf">slides+notes</a>]<br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/OSTEP//intro.pdf">Intro</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/OSTEP/cpu-intro.pdf">Process</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/OSTEP/cpu-api.pdf">Process API</a><br/>
	<span class="assignment"><a href="./proj0a.html">Proj 0a</a> and 
		<a href="./proj0b.html">Proj 0b</a> out</span></td>
  <td class="nodue">Jan 30</td>
</tr>
<tr> <!-- week of Feb 3 -->
  <td id="2020-2-3" class="date"><b>Week 3</b></td>
  <td class="lecture">Feb 3<br/>
	<b>Lec 2:</b> LDE, thread abstraction [<a href="./public/lecs/lec2-lde-thread.pdf">slides</a>] 
		[<a href="./public/lecs/lec2-lde-thread+notes.pdf">slides+notes</a>]<br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/OSTEP/cpu-mechanisms.pdf">LDE</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/OSTEP/threads-api.pdf">Thread API</a>
	</td>
  <td class="deadline">Feb 6<br/>
	<span class="hwdue"><a href="./proj0a.html">Proj 0a</a> and 
		<a href="./proj0b.html">Proj 0b</a> due</span><br/>
	<span class="assignment"><a href="./proj1a.html">Proj 1a</a> out</span></td>
</tr>
<tr> <!-- week of Feb 10 -->
  <td id="2020-2-10" class="date"><b>Week 4</b></td>
  <td class="lecture">Feb 10<br/>
	<b>Lec 3:</b> Synchronization I: locks, semaphore [<a href="./public/lecs/lec3-lock-sem.pdf">slides</a>]
		[<a href="./public/lecs/lec3-lock-sem+notes.pdf">slides+notes</a>]<br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/OSTEP/threads-intro.pdf">Concurrency</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/OSTEP/threads-locks.pdf">Locks</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/OSTEP/threads-sema.pdf">Semaphores</a></td>
  <td class="nodue">Feb 13</td>
</tr>
<tr> <!-- week of Feb 17 -->
  <td id="2020-2-17" class="date"><b>Week 5</b></td>
  <td class="lecture">Feb 17<br/>
	<b>Lec 4:</b> Synchronization II: cv, classic sync problems [<a href="./public/lecs/lec4-cv-rw-5dp.pdf">slides</a>]
		[<a href="./public/lecs/lec4-cv-rw-5dp+notes.pdf">slides+notes</a>],<br/>
		Scheduling I: FIFO, SJF [<a href="./public/lecs/lec4-sched-fifo-sjf.pdf">slides</a>]
		[<a href="./public/lecs/lec4-sched-fifo-sjf+notes.pdf">slides+notes</a>]<br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/OSTEP/threads-cv.pdf">CV</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/OSTEP/threads-bugs.pdf">Deadlocks</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/cpu-sched.pdf">Scheduling (intro)</a></td>
  <td class="deadline">Feb 20<br/>
	<span class="hwdue"><a href="./proj1a.html">Proj 1a</a> due</span><br/>
	<span class="assignment"><a href="./proj1b.html">Proj 1b</a> out</span></td>
</tr>
<tr> <!-- week of Feb 24 -->
  <td id="2020-2-24" class="date"><b>Week 6</b></td>
  <td class="holiday">Feb 24
	(<b>Traveling to FAST</b> NO CLASS)<br/>
	<b>Lec 5a:</b> CPU scheduling II: RR, priority, MLFQ [<a target="_blank" href="https://youtu.be/w0VpAopq7dA">video</a>]
		[<a href="./public/lecs/lec5-sched-rr-priority-mlfq.pdf">slides</a>] 
		[<a href="./public/lecs/lec5-sched-rr-priority-mlfq+notes.pdf">slides+notes</a>], <br/>
	<b>Lec 5b:</b> Proj 1b (OS/161 sync) [<a href="./public/lecs/lec-os161-sync.pdf">slides</a>] 
		[<a target="_blank" href="https://youtu.be/gz9PUJqv1kg">video1</a>]
		[<a target="_blank" href="https://youtu.be/gU91JIUzhRU">video2</a> (src walkthru)]
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/cpu-sched-mlfq.pdf">MLFQ</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/OSTEP/cpu-sched-lottery.pdf">Lottery</a>
	</td>
  <td class="nodue">Feb 27</td>
</tr>
<tr> <!-- week of Mar 2 -->
  <td id="2020-3-2" class="date"><b>Week 7</b></td>
  <td class="lecture">Mar 2<br/>
	<b>Lec 6a:</b> Memory management I: address space, segmentation [<a href="./public/lecs/lec6-mem-addrspace-seg.pdf">slides</a>] 
		[<a href="./public/lecs/lec6-mem-addrspace+notes.pdf">slides+notes</a>],<br/>
	<b>Lec 6b:</b> Midterm review [<a href="./public/lecs/midterm-review.pdf">slides</a>]<br/>
		<!--span class="assignment"><a href="./proj2.html">Proj 2</a> out</span></td-->
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/vm-intro.pdf">Address space abstraction</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/vm-mechanism.pdf">Address translation</a></td>
  <td class="deadline">Mar 5<br/>
	<span class="hwdue"><a href="./proj1b.html">Proj 1b</a> due</span></td>
</tr>
<tr> <!-- week of Mar 9 -->
  <td id="2020-3-9" class="date"><b>Week 8</b></td>
  <td class="holiday">Mar 9<br/>
	<b>Spring Recess</b> (NO CLASS) <br/>
		<span class="assignment"><a href="./proj2.html">Proj 2</a> out</span></td>
  <td class="holiday">Mar 12<br/></td>
</tr>
<tr> <!-- week of Mar 16 -->
  <td id="2020-3-16" class="date"><b>Week 9</b></td>
  <td class="holiday">Mar 16<br/>
	<b>Extended Spring Recess</b> (NO CLASS) </td>
  <td class="holiday">Mar 19</td>
</tr>
<tr> <!-- week of Mar 23 -->
  <td id="2020-3-23" class="date"><b>Week 10</b></td>
  <td class="exam">Mar 23<br/>
	<b>Midterm exam</b></td>
  <td class="nodue">Mar 26</td>
</tr>
<tr> <!-- week of Mar 30 -->
  <td id="2020-3-30" class="date"><b>Week 11</b></td>
  <td class="lecture">Mar 30<br/>
	<b>Lec 7a:</b> Memory management II: paging [<a href="./public/lecs/lec7a-mem-paging.pdf">slides</a>]
		[<a href="./public/lecs/lec7a-mem-paging+notes.pdf">slides+notes</a>] 
		[<a href="https://youtu.be/8smufHihEa8">video7a-1</a>]
		[<a href="https://youtu.be/epdOZifNd2g">video7a-2</a>],<br/>
	<b>Lec 7b:</b> Memory management II: TLB [<a href="./public/lecs/lec7b-mem-tlb.pdf">slides</a>]
		[<a href="./public/lecs/lec7b-mem-tlb+notes.pdf">slides+notes</a>]
		[<a href="https://youtu.be/VHaPMRdV7As">video7b-1</a>]
		[<a href="https://youtu.be/YyCEdMWbF3Y">video7b-2</a>]
		[<a href="https://youtu.be/vqlO_cNHUDw">video7b-3</a>],<br/>
	<b>Lec 7c:</b> Proj 2 (OS/161 syscall+sched) [<a href="./public/lecs/lec-os161-syscall.pdf">slides</a>]
		[<a href="https://youtu.be/VDoWHNvEWEo">video</a>] <br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/vm-paging.pdf">Paging</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/vm-tlbs.pdf">TLB</a>
	</td>
  <td class="nodue">Apr 2</td>
</tr>
<tr> <!-- week of Apr 6 -->
  <td id="2020-4-6" class="date"><b>Week 12</b></td>
  <td class="lecture">Apr 6<br/>
	<b>Lec 8a:</b> Memory management III: advanced PT [<a href="./public/lecs/lec8a-mem-adv-pt.pdf">slides</a>]
		[<a href="./public/lecs/lec8a-mem-adv-pt+notes.pdf">slides+notes</a>]
		[<a href="https://youtu.be/d5CJQj-td0g">video8a-1</a>]
		[<a href="https://youtu.be/s0ZJdxff97Q">video8a-2</a>],<br/>
	<b>Lec 8b:</b> Memory management III: page faults and swapping [<a href="./public/lecs/lec8b-mem-swapping.pdf">slides</a>]
		[<a href="./public/lecs/lec8b-mem-swapping+notes.pdf">slides+notes</a>]
		[<a href="https://youtu.be/DCXDUdTd4AA">video8b-1</a>]
		[<a href="https://youtu.be/nN-KIq40Fq8">video8b-2</a>], <br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/vm-smalltables.pdf">Small tables</a> and
		<a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/vm-beyondphys.pdf">Swapping mechanisms</a>
	</td>
  <td class="nodue">Apr 9</td>
</tr>
<tr> <!-- week of Apr 13 -->
  <td id="2020-4-13" class="date"><b>Week 13</b></td>
  <td class="lecture">Apr 13<br/>
	<b>Lec 8c:</b> Memory management IV: page replacement policies 
		[<a href="./public/lecs/lec8c-mem-caching-fifo+random.pdf">fifo+random</a>]
		[<a href="./public/lecs/lec8c-mem-caching-fifo+random+notes.pdf">fifo+random+notes</a>]
		[<a href="https://youtu.be/OH2_55fkjZs">video8c-1</a>] <br/>
		[<a href="./public/lecs/lec8c-mem-caching-belady-offline.pdf">belady</a>]
		[<a href="./public/lecs/lec8c-mem-caching-belady-offline+notes.pdf">belady+notes</a>]
		[<a href="https://youtu.be/tDoflsU9htY">video8c-2</a>] <br/>
		[<a href="./public/lecs/lec8c-mem-caching-LRU+clock.pdf">lru+clock</a>]
		[<a href="./public/lecs/lec8c-mem-caching-LRU+clock+notes.pdf">lru+clock+notes</a>]
		[<a href="https://youtu.be/wfkhk345xr0">video8c-3</a>] <br/>
		[<a href="./public/lecs/lec8c-mem-caching-misc.pdf">misc.</a>]
		[<a href="./public/lecs/lec8c-mem-caching-misc+notes.pdf">misc.+notes</a>]
		[<a href="https://youtu.be/2ggDXkU9AZ4">video8c-4</a>] <br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/OSTEP/vm-beyondphys-policy.pdf">Page replacement policies</a><br/>
	<b>Lec 9a:</b> I/O I: I/O basics
		[<a href="./public/lecs/lec9a-storage-io.pdf">io</a>]
		[<a href="./public/lecs/lec9a-storage-io+notes.pdf">io+notes</a>]
		[<a href="https://youtu.be/WLH9a85x7zI">video9a</a>] <br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/file-devices.pdf">I/O devices</a>
	</td>
  <td class="nodue">Apr 16</td>
</tr>
<tr> <!-- week of Apr 20 -->
  <td id="2020-4-20" class="date"><b>Week 14</b></td>
  <td class="deadline">Apr 20<br/>
	<b>Lec 9b:</b> I/O II: HDDs [<a href="./public/lecs/lec9b-storage-hdds.pdf">slides</a>]
		[<a href="./public/lecs/lec9b-storage-hdds+notes.pdf">slides+notes</a>]
		[<a href="https://youtu.be/JjVWWboU21E">video9b</a>],  <br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/file-disks.pdf">HDDs</a><br/>	
	<b>Lec 9c:</b> I/O III: Disk scheduling [<a href="./public/lecs/lec9c-storage-disk-sched.pdf">slides</a>]
		[<a href="./public/lecs/lec9c-storage-disk-sched+notes.pdf">slides+notes</a>]
		[<a href="https://youtu.be/CXQoTZOwb4g">video9c</a>],  <br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/file-disks.pdf">Disk sched (Ch 37.5)</a><br/>	
		<span class="hwdue"><a href="./proj2.html">Proj 2</a></span> due</td>
  <td class="important">Apr 23<br/>
	<span class="assignment"><a href="./proj3.html">Proj 3</a> out</span></td>
</tr>
<tr> <!-- week of Apr 27 -->
  <td id="2020-4-27" class="date"><b>Week 15</b></td>
  <td class="lecture">Apr 27<br/>
	<b>Lec 10a:</b> I/O IV: Flash basics [<a href="./public/lecs/lec10a-storage-flash.pdf">slides</a>]
		[<a href="./public/lecs/lec10a-storage-flash+notes.pdf">slides+notes</a>]<br/>
		[<a href="https://youtu.be/HKNxxR40Txg">video10a-1</a>]
		[<a href="https://youtu.be/EAvJwdlND2Y">video10a-2</a>]
		[<a href="https://youtu.be/prgYEVpyQ2A">video10a-3</a>], <br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/file-ssd.pdf">Flash SSDs</a><br/>
	<b>Lec 10b:</b> I/O V: RAID [<a href="./public/lecs/lec10b-storage-raid.pdf">slides</a>]
		[<a href="./public/lecs/lec10b-storage-raid+notes.pdf">slides+notes</a>] <br/>
		[<a href="https://youtu.be/pmD2oW3p1Mc">video10b-1-raid-basics</a>]
		[<a href="https://youtu.be/oYbiEzHvrGw">video10b-2-raid0</a>]
		[<a href="https://youtu.be/DTNjMvgcPks">video10b-3-raid1</a>]
		[<a href="https://youtu.be/kuhSEOgx4xY">video10b-4-raid4</a>]
		[<a href="https://youtu.be/ZPashI_oznA">video10b-5-raid5</a>],<br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/file-raid.pdf">RAID</a> </td>
  <td class="nodue">Apr 30</td>
</tr>
<tr> <!-- week of May 4 -->
  <td id="2020-5-4" class="date"><b>Week 16</b></td>
  <td class="lecture">May 4<br/>
	<b>Lec 11a:</b> File system I: APIs [<a href="./public/lecs/lec11a-fs-api.pdf">slides</a>]
		[<a href="./public/lecs/lec11a-fs-api+notes.pdf">slides+notes</a>]<br/>
		[<a href="https://youtu.be/_JJrd2PJpLI">video11a-1</a>]
		[<a href="https://youtu.be/QufJoI75C-8">video11a-2</a>], <br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/file-intro.pdf">File system intro</a><br/>
	<b>Lec 11b:</b> File system II: implementation [<a href="./public/lecs/lec11b-fs-impl.pdf">slides</a>]
		[<a href="./public/lecs/lec11b-fs-impl+notes.pdf">slides+notes</a>]
		[<a href="https://youtu.be/jZ4eKevY1KA">video11b-1</a>]
		[<a href="https://youtu.be/oQI4Ja83O9Y">video11b-2</a>],<br/>
	<b>Reading:</b> <a href="http://pages.cs.wisc.edu/~remzi/Classes/537/Spring2016/Book/file-implementation.pdf">File system implementation</a> </td>
  <td class="deadline">May 7<br/>
	<span class="hwdue"><a href="./proj3.html">Proj 3</a> due</span></td>
</tr>
<tr> <!-- week of May 11 -->
  <td id="2020-5-11" class="date"><b>Week 17</b></td>
  <td class="lecture">May 11<br/>
	<b>Final review:</b> [<a href="./public/lecs/final-review.pdf">slides</a>]
		[<a href="./public/lecs/final-review+notes.pdf">slides+notes</a>]</td>
  <td class="nodue">May 14</td>
</tr>
<tr> <!-- week of May 18 -->
  <td id="2020-5-18" class="date"><b>Week 18</b></td>
  <td class="exam">May 18<br/>
	<b>Final exam:</b> 7:20 pm - 10:00 pm</td>
  <td class="nodue">May 21</td>
</tr>

</table>
