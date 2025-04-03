# monitoring
Repo for some PostgreSQL monitoring experiments


There are some code for checking availability of monitoring PostgreSQL at the start of recovery, until the DBMS has reached a state of consistency. 

How to use use it

- clone PostgreSQL (version 17) to your pc
- add sujested code (in [bgcheckpointer](bgcheckpointer_stats.txt), [bgwrites](bgwriter_stats.txt), [pg_stat_activity(kinda)](dynamic_activity.txt)) to src/backend/access/transam/xlogrecovery.c - to ApplyWalRecord(...)

like
#include's (and #define's, if needed) written in the files

// declare functions
void someBGWriterInfo(void);
void someCheckpointerInfo(void);
void someActivityInfo(void);

ApplyWalRecord(...)
{
    ...
    someActivityInfo();
	someBGWriterInfo();
	someCheckpointerInfo();
}


and somewhere functions themselves


- then 
    ./configure --enable-debug --enable-cassert --prefix $PWD/install && make -j 16 install-world-bin


- vua-la!