# HPL

linpack: https://software.intel.com/en-us/node/528458

mp_linpack: https://software.intel.com/en-us/node/528462

multi nodes: https://software.intel.com/en-us/node/528467

HPL FAQS: http://www.netlib.org/benchmark/hpl/faqs.html

in HPL.dat, change:

N - size of the problem, which should fill up around 80% of total RAM, as recommended by HPL docs.
	
	-on our bio cluster, peak performance at 64000.

P - number of processes. One caveat - P is less than Q.

Q - number of nodes. 

	- P * Q is the total number of processes you can run on your cluster

NBs - subset of N to distribute across nodes. HPL docs recommend 32 - 256. I used 256.

example run:
N = 64000 (I did multiples of 256, because I noticed huge performance drop off on NBs < the NBs size I set (256). This way it is consistent)
P = 4 (max cores we have on each node)
Q = 5 (number or nodes to use, 6th node didn't have intel libraries at that time)
NBs = 256

to run:
mpirun -n 20 -f /nfs/hosts2 ./xhpl
