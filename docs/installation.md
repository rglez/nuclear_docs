# **Setting up the NUCLEAR environment**

You can set up NUCLEAR in your local device by defining a conda[^1] environment. Please ensure you have anaconda/miniconda3 installed in your $HOME and then:

1. Clone the nuclear repo:   
	```
	$ git clone https://github.com/rglez/nuclear.git
	```

1. Change the last line of the *environment.yml* file to suit your local system
1. Create and activate the *nuclear* environment:  

	`$ cd nuclear`  
	`$ conda env create`  
	`$ conda activate nuclear`  

[^1]: Conda is an open-source package management system and environment management system that quickly installs, runs, and updates packages and their dependencies. 
