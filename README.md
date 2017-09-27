# sitemailer
From a performance perspective, it is possible to increase the performance of your DC by
moving the database and transaction log fi les to different drives. For optimal disk performance
of Active Directory, you may use a confi guration similar to this:
◆ C:\ drive: Operating system
◆ D:\ drive: Active Directory database fi le and SYSVOL
◆ E:\ drive: Transaction log fi le
In this confi guration, each of the drives needs to be a separate spindle (a separate physical
disk). A single drive with three partitions wouldn’t provide any performance gain. Additionally,
if your disk drives have different speeds, you should put the operating system on the fastest
disk, the transaction log on the next fastest, and the Active Directory database fi le and
SYSVOL on the slowest disk. The operating system and the transaction log fi le will receive the
heaviest usage.
To optimize your domain controller just a bit more, you can distinguish between heavy
read and heavy write operations. If you have heavy read operations, you should add suffi cient
memory to the domain controller so that it can cache the database in memory. For heavy write
operations, you can improve performance by adding the following:
◆ Hardware RAID controllers
◆ High RPM disks
◆ Battery backend write-caching (BBWC) on the RAID controller
This sounds good and makes sense, but what will happen if you virtualize your domain
controller? In this case it’s a good idea to add suffi cient memory for your domain controller
so that it can cache the database. If you are going to place the transaction log, database, and
SYSVOL on different virtual disks, the performance improvement will probably be minimal.
The problem is that all the virtual disks are on the same LUN, and this LUN is spread over an
array of disks. That means that all virtual disks share the same physical disks in the storage.
From a theoretical standpoint, it would be best to place each fi le on a separate array or LUN. In
any case, you should use the fastest storage you have.
For a good starting point to fi gure out if you have a disk performance problem, you can use
these performance counters. Each of these counters should have a low value:
◆ Avg. Disk Queue Length
◆ Avg. Disk Read Queue Length
◆ Avg. Disk Write Queue Length
Let’s look at an example. If your domain includes 100 users, you can store the database and
log fi les on the C drive with the operating system and not notice any performance problems.
On the other hand, if you are supporting 50,000 users, you may want to squeeze every ounce of
performance out of the server, so you will locate the database and log fi les on different drives. If
you are building a test system, there is nothing wrong with leaving everything on C.
