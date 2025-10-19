Routing algorithm that clumps routers into clusters/zones to shorten the size of routing tables to make routing algorithms run faster
- Router stores the path to other routers within a group and path to other groups.
- Multiple zones and clusters are also made when network is huge
![[Pasted image 20250502103845.png]]
>[!important]+ Calculating hierarchy
> Optimal level for N routers → ln(N)
> Minimal size of routing table → try to have equal number of zones, groups, routers in a group
> Ex: 3-level hierarchy for N = 4800. ideally → 16\*16\*16 = 4800. By trial and error, ideal match is 15-16-20 (cluster, region, routers in region)
