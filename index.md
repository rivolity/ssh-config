
# SSH Config
Connect to Hosts using ssh and Tab suggestion Completion, the configuration is for connection to Hosts (using private Keys) and for connection using private key and proxy setup.
### Requirements:
private keys should be deposited in

    ~/.ssh/

Private keys should have permission `rw-------`

if your private keys contain a pattern `private`, you can execute this command to set permission.

    chmod 600 *private*.pem

Public Keys should have permission `rw-r--r--`

if your public keys contain a pattern `pub`, you can execute this command to set permission.


    chmod 644 *pub*.pem
--
> you can use this website to understand permission
> https://chmod-calculator.com/

### Configuration connect with no proxy
Change directory to home/.ssh

    cd ~/.ssh/
Create a new file named `config` with no extension in this repository.
 - The config should look like that

		Host vm-dev-test-1
		    HostName 199.99.33.22
		    StrictHostKeyChecking no
		    User user1
		    IdentityFile ~/.ssh/private1.pem

		Host vm-dev-test-2
		    HostName 200.99.33.33
		    StrictHostKeyChecking no
		    User user2
		    IdentityFile ~/.ssh/private2.pem

 - By following the config file, `user1` will connect to the `vm-dev-test-1` using the `private1.pem` and the `user2` will connect to the `vm-dev-test-2` using `private2.pem`

### Connect  configuration with proxy
You can add a proxy to your Config file, by using the following configuration.

	Host vm-dev-test-3
	    HostName 191.13.31.72
	    StrictHostKeyChecking no
	    User user3
	    IdentityFile ~/.ssh/private3.pem
	    ProxyCommand ssh -W %h:%p proxy-dev

	Host proxy-dev
	  HostName proxy_host.dev.company.com
	  User proxy-user

 - By following this new config, `user3` will connect to the `vm-dev-test-3` using the `private3.pem` and the proxy `proxy-dev` with the user `proxy-user`

### Connection test
	ssh vm-dev-test-1
for the host that requires a proxy

	ssh vm-dev-test-3

To prevent ssh from asking the passphrase everytime, you can just add your private key to the list maintained by ssh-agent

	ssh-add ~/.ssh/your_private_key
