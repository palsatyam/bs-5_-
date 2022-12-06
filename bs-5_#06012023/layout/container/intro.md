```Containers
Containers are a fundamental building block of Bootstrap that contain, pad, and align your content within a given device or viewport.


```How they work
Containers are the most basic layout element in Bootstrap and are required when using our default grid system. Containers are used to contain, pad, and (sometimes) center the content within them. While containers can be nested, most layouts do not require a nested container.

Bootstrap comes with three different containers:

.container, which sets a max-width at each responsive breakpoint
.container-fluid, which is width: 100% at all breakpoints
.container-{breakpoint}, which is width: 100% until the specified breakpoint
The table below illustrates how each container’s max-width compares to the original .container and .container-fluid across each breakpoint.





        Extra-small    Small     px-Medium   Large    Large    XX-Large 
.container	100%	   540px      720px	     960px    1140px   	1320px
.container-sm	100%	540px   	720px	960px	1140px	1320px
.container-md	100%	100%	   720px	960px	1140px	1320px
.container-lg	100%	100%	    100%	960px	1140px	1320px
.container-xl	100%	100%	    100%	100%	1140px	1320px
.container-xxl	100%	100%	    100%	100%	100%	1320px
.container-fluid100%	100%	100%	100%	100%	100%