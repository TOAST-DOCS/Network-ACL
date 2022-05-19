## Network > Network ACL > Overview

NHN Cloud provides the network access control list (ACL) function.
This function allows you to control access per protocol, IP address, and port.


## ACL Function

You can use the ACL function to control packets coming into the network.
This function is different from the [security group](https://docs.toast.com/en/Network/VPC/en/Security%20Groups/en/overview/), and the differences are as follows:

> [Note] Security Group vs Network ACL
>
> | Classification | Security Group | Network ACL | Remark |
> |--|--|--|--|
> | Control target | Instance | Network, Instance | |
> | Configuration target | Protocol, IP, port setting | Protocol, IP, port setting | For ACL, you can choose between blacklist and whitelist |
> | Controlled traffic | Inbound/outbound traffic<br>selectable | src/dst address selectable |
> | Access control type | Set only the allow policy | Allow/Deny policy selectable |

For inbound/outbound traffic, the network ACL setting takes precedence over the security group setting.
Even if traffic is allowed in the network ACL setting, it can be blocked by the security group, so you should check both settings.

To use the network ACL function, you need to configure the following.

### ACL
* Up to 10 ACLs can be created per project.
* Its properties are name and description.


### ACL Rule
* Up to 100 rules can be created per project.
* Their order number determines their priority. Lower number has higher priority.
* 'Allow': **Allows** access that matches the rule.
* 'Deny': **Denies** access that matches the rule.
* An access control target can have an IP address or an IP address range in CIDR format. If you enter an IP address range in CIDR format, the entered range in the network is included as the target of access control.
* If you specify a protocol, the rule can have one port or a range of ports.
* For source and destination, the rules must always be set as a pair.


### ACL Binding
* The maximum number of networks that can be bound to an ACL is equal to the number of VPCs.
* An ACL can be applied to multiple networks.
* One ACL can be applied per network.

> [Note]
> ### Network and ACL behaviors
> * Deleting a network also deletes its ACL binding, but ACL itself remains intact.
> * If there is any network bound to an ACL, the ACL cannot be deleted.
> * If an ACL rule is added or deleted, the change is also applied to all networks bound to the ACL.
