## Background

Now we have blocked Sneaky Suds from stealing our recipes by exfiltrating data from the Beer Vault Server. We need to figure out how did Sneaky Suds managed to get to the Beer Vault in the first place.

Below is the updated AWS Network Diagram after making the previous changes

<br />
<p><img src="https://aws-jam-challenge-resources.s3.amazonaws.com/panw-vmseries-gwlb/after-task-1.png" alt="Network Diagram2" width="1500" /></p>
<br />
Time to find out how BrewGuardians Webstore became the weak link in our brew chain. In the Firewall logs we only saw the Outbound logs from the Beer Store Data Database. Time to investigate! Let’s  redirect the East-West traffic between our web frontend and the database to the Palo Alto Networks Firewall to see what's going on.
<br />
<br />


## Task
1. First check on the Firewall if you can see any logs between the Beer Store Data Database Server and the Beer Store Frontend Webserver. You can add the following filter into the Firewall Monitor **( zone.src eq internal ) and ( zone.dst eq internal )**
2. After seeing no Logs in the Firewall, you recongize that you have to solve some AWS routing issues. For any help, see Clue 1
3. After solving the AWS routing, you should be able to see the following Monitor Logs inside the Firewall
<p><img src="https://aws-jam-challenge-resources.s3.amazonaws.com/panw-vmseries-gwlb/task2-ssh-new.png" alt="SSH Logs" width="1500" /></p>
<br />

## Task Validation
- Once you made the appropriate changes in AWS check if can see now traffic between the **Beer Store Data Database Server** and the **Beer Store Frontend Webserver** by typing the following filter in the Firewall Monitor **( zone.src eq internal ) and ( zone.dst eq internal )**
- If you can see now the traffic between both EC2 Instances, type the Port number of the ssh application which is used for communication between both EC2 Instances.
<br />
<br />

## Helpful info
**How to see the Traffic Logs inside the Firewall**
- Login into the firewall
- Inside the Firewall, and Navigate to Monitor -> Traffic
- See the following picture as an example <p><img src="https://aws-jam-challenge-resources.s3.amazonaws.com/panw-vmseries-gwlb/example.png" alt="Monitor Logs" width="1500" /></p>
<br />

## Inventory
- Palo Alto Networks NGFW VM-Series
- Amazon EC2
- Amazon VPC
- AWS Systems Manager (SSM)
- AWS Lambda
- AWS Tranist Gateway
- AWS Gateway Load Balancer <br />
<br />

## Services You Should Use
- Palo Alto Networks NGFW VM-Series
- Amazon EC2
- AWS Transit Gateway (TGW route tables) <br />


## Clues
Clue 1:Did you looked into the TGW routing?
1. Login into the AWS console
2. Go to VPC Services and select under Transit Gateways the Transit gateway route tables
