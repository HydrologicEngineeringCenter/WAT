**Setting Up a Distributed Compute**

There are a few steps to setting up a distributed compute that both the master and compute nodes need:
1. Download the ignite fabric
The first step is to download the ignite fabric and place it in C:\Programs\ignite.
2. Download the jdk
It is easiest to put the jdk in the same directory as the ignite fabric, I reccomend using C:\Programs\ignite\jdk
A package that is already set up this way and can be extracted into C:\Programs\ignite is available for download here:

3. Next, the computenode.bat file needs to be updated. There are three items that need to be set in the file based on the exact location of your programs

set IGNITE_HOME=C:\Programs\ignite

set JAVA_HOME=C:\Programs\ignite\jdk

set WAT_HOME=C:\Programs\HEC-WAT\HEC-WAT\

(the last one in the set should be the directory that the HEC-WAT.exe exists in, the enclosing HEC-WAT folder is where the Apps directory lives)

4. The default-config.xml file needs to be updated. 
Based on your selected methodology for distributing the compute update the default-config.xml file.
A sample for the LAN distributed compute can be downloaded here:
A sample for the AWS distributed compute can be downloaded here:

Now that those common edits have been completed, the following edits will differ between the compute node and the master node. 

**For the compute node**

**For the master node**

After these have been completed we reccomend you launch the computenode.bat on the compute node. If it runs correctly the command prompt will be visible and no text will be present.

A further test can be to go to the %temp% directory and open the out.log file and scroll to the bottom of the file - you should see the ignite logo printed in charaters...

Finally, launch the HEC-WAT executable on the master node. Go to Tools>Simulation Compute Engine Manager and check to see how many nodes are present. There should be however many compute nodes you have plus the master.
Typically we start with 1 compute node and 1 master, so we expect to see 2. 

We reccomend to compute a single job (either a lifecycle or realization) before proceeding. 

Once the job is complete, ensure the results were copied back to the master node correctly. After that has been confirmed, you can clone the compute nodes to the size you need and start computing.

A few notes regarding best practices.
After a compute we reccomend shutting down the computenode.bat process on each of the compute nodes and cleaning out the %temp% directory. Once this is done you can safely restart all of the computenode.bat processes and run another compute.
Unless it is part of the strategy of your compute we also reccomend deleting the runs directory on the master before starting any distributed compute.
