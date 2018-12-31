# Instruction Set

- RUN
	- The commands passed through `RUN` will be executed at build time
	- After getting the base image we need to do some customizations like installing packages
	- Those executions can be added as `RUN` instructions
	- Every `RUN` instruction will add a new layer to the image
	- To avoid this we can join all the commands through `Logical AND`
- CMD
	- These are run time executions
	- The instructions which need to be executed at runtime of a container can be given as the CMD instructions
	- This is equilent to 
		- `docker run <args> <command>`
		- `docker run <args> /bin/bash`
	- Through out the Dockerfile only one CMD instruction is allowed
	- If we use more CMD instructions then the last one will be executed as everytime it gets overwritten
	- This is possible even if we give one CMD instruction in the Dockerfile and we give the commands at the run time through `docker run` command
	- Commands in CMD instructions can be passed and treated in two forms
		- Shell Form
		- Exec Form

		| Shell Form | Exec Form |
		|------------|-----------|
		| Commands are expressed the way same as the shell commands | JSON array style - ["command","arg1"] |
		| Commands get prepended by "/bin/sh -c" | Containers don't need a shell |
		| Variable expansion etc.. | Avoids string munging |
		| | No shell features - Neither variable expansion nor special characters |

- Below are some differences between `CMD` and `RUN`

| CMD | RUN |
|-----|-----|
| Run-Time | Build-Time |
| Run commands in containers at launch time | Add layers to image |
| Equivalent of `docker run <args> <command>` `docker run <args> /bin/bash` | Used to install apps |
| One per Dockerfile | |