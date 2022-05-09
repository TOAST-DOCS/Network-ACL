## Network > Network ACL > Overview

NHN Cloud provides Network ACL function, with which you can control access per protocol, IP, and port.


## ACL 기능

With the ACL function, you can control packets coming into the network. 
This function is different from [Security Group](https://docs.toast.com/ko/Network/VPC/ko/console-guide/#_8), and the differences are as follows:

> [Note] Security Group vs Network ACL
>
> | Classification      | Security Group                      | Network ACL                       | Remark                                                       |
> | ------------------- | ----------------------------------- | --------------------------------- | ------------------------------------------------------------ |
> | Control Target      | Instance                            | Network, Instance                 |                                                              |
> | Setup target        | Protocol, IP, Port Setting          | Protocol, IP, Port Setting        | For ACL, you can choose between blacklist and whitelist to use it |
> | Control Traffic     | Inbound/outbound traffic selectable | src/dst address selectable        |                                                              |
> | Access Control Type | Set only allowed policy             | Allowed/blocked policy selectable |                                                              |

For inbound/outbound traffic, the Network ACL setting takes precedence over the Security Group setting. Even if it is allowed in Network ACL setting, it could be blocked by Security Group, so you should check both settings.

To use the Network ACL function, you need to specify the settings as follows:

### ACL

* Up to 10 ACLs can be created per project.
* Its properties are Name and Memo.

### ACL Rule

* Up to 100 rules can be created per project.
* Their order number determines their priority. Lower number takes higher priority.
* 'Allow': **Allows** access that matches with the rule.
* 'Deny': **Denies** access that matches with the rule.
* An access control target can have an IP address or an IP address list in CIDR format. If you enter an IP address range in CIDR format, the bandwidth entered within the network is included as the target of access control.
* If you specify the protocol, you can have one port or a range of port.
* For src and dst, their rule settings should always be paired.


### ACL Binding

* The number of networks that can be bound to an ACL is equal to the maximum number of VPCs.
* An ACL can be applied to multiple networks.
* One ACL can be applied per network.

> [Note] 
>
> * Network and ACL behaviors 
> * Deleting a network also deletes its ACL binding, but ACL itself remains intact. 
> * If there is any network bound to an ACL, the ACL cannot be deleted. 
> * If an ACL rule is added or deleted, the change is also applied to all networks bound to it.
