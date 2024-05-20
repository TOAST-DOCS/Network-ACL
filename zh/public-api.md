## Network > Network ACL > API v2 Guide

To use the API, API endpoint and token are required. Refer to [API usage preparations](/Compute/Compute/ko/identity-api-gov/) to prepare the information required to use the API.

For Security Groups API, the `network` type endpoint is used. For more details, see `serviceCatalog` from the response of token issuance.

| Format | Region | Endpoint |
|---|---|---|
| network | Korea (Pangyo) Region<br>Korea (Pyeongchon) Region | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com |

In each API response, you may find fields that are not specified within this guide. Those fields are for NHN Cloud internal usage, so refrain from using them because they may be changed without prior notice.



## Network ACL
### View an ACL List
```
GET /v2.0/acls
X-Auth-Token: {tokenId}
```

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| sort_dir | Query | Enum | - | Sorting direction of ACL to query<br>Sort by the field specified by `sort_key`<br>Either **asc**, or **desc** |
| sort_key | Query | String | - | Sorting key of ACL to query<br>Sort in the direction as specified by `sort_dir` |
| fields | Query | String | - | Field name of ACL to query<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| acls | Body | Array | ACL list object |
| acls.id | Body | UUID | ACL ID |
| acls.tenant_id | Body | String | Tenant ID |
| acls.description | Body | String | ACL description |
| acls.name | Body | String | ACL name |
| acls.create_at | Body | String | ACL creation time |
| acls.update_at | Body | String | ACL update time |

<details><summary>Example</summary>
<p>

```json
{
  "acls": [
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "description": "Default acl",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "name": "default",
      "created_at":"2020-11-02T06:51:49Z",
      "updated_at":"2020-11-02T06:51:49Z",
      "revision_number":2
    },
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "description": "Default acl2",
      "id": "d3590396-901f-4d90-b8f3-f967831909c2",
      "name": "default2",
      "created_at":"2020-11-05T13:51:43Z",
      "updated_at":"2020-12-10T11:33:12Z",
      "revision_number":2
    }
  ]
}
```
</p>
</details>

---

### View an ACL

```
GET /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| aclId | URL | UUID | O | ACL ID to query |
| fields | Query | String | - | Field name of ACL to query<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| acl | Body | Array | ACL list object |
| acl.id | Body | UUID | ACL ID |
| acl.tenant_id | Body | String | Tenant ID |
| acl.description | Body | String | ACL description |
| acl.name | Body | String | ACL name |
| acl.create_at | Body | String | ACL creation time |
| acl.update_at | Body | String | ACL update time |

<details><summary>Example</summary>
<p>

```json
{
  "acl": 
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "description": "Default acl",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "name": "default",
      "created_at":"2020-11-02T06:51:49Z",
      "updated_at":"2020-11-02T06:51:49Z",
      "revision_number":2
    }
}
```
</p>
</details>

---

### Create an ACL
 
```
POST /v2.0/acls
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| acl | Body | Array | O | ACL list object |
| acl.tenant_id | Body | String | - | Tenant ID |
| acl.name | Body | String | - | ACL name (recommended to put in for identification) |
| acl.description | Body | String | - | ACL description |

<details><summary>Example</summary>
<p>

```json
{
  "acl": 
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "description": "Default acl",
      "name": "default"
    }
}
```
</p>
</details>

#### Response

| Name | Type | Format |  Description |
|---|---|---|---|
| acl | Body | Array | ACL list object |
| acl.id | Body | String | ACL ID |
| acl.tenant_id | Body | String | Tenant ID |
| acl.name | Body | String | ACL name |
| acl.description | Body | String | ACL description |
| acl.create_at | Body | String | ACL creation time |
| acl.update_at | Body | String | ACL update time |

<details><summary>Example</summary>
<p>

```json
{
  "acl": 
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "description": "Default acl",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "name": "default",
      "created_at":"2020-11-02T06:51:49Z",
      "updated_at":"2020-11-02T06:51:49Z",
      "revision_number":2
    }
}
```
</p>
</details>

---

### Delete an ACL

```
DELETE /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| aclId | URL | UUID | O | ACL ID to delete |
| tokenId | Header | String | O | Token ID |

#### Response

This API does not return a response body.

---

### Modify an ACL
Modifies an existing ACL (only name and description can be edited).

```
PUT /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| aclId | URL | String | O | ACL ID |
| acl | Body | Array | O | ACL list object |
| acl.name | Body | String | - | ACL name |
| acl.description | Body | String | - | ACL description |

<details><summary>Example</summary>
<p>

```json
{
  "acl": 
    {
      "description": "Default acl",
      "name": "default"
    }
}
```
</p>
</details>

#### Response

| Name | Type | Format |  Description |
|---|---|---|---|
| acl | Body | Array | ACL list object |
| acl.id | Body | String | ACL ID |
| acl.tenant_id | Body | String | Tenant ID |
| acl.name | Body | String | ACL name |
| acl.description | Body | String | ACL description |
| acl.create_at | Body | String | ACL creation time |
| acl.update_at | Body | String | ACL update time |


<details><summary>Example</summary>
<p>

```json
{
  "acl": 
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "description": "Default acl",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "name": "default",
      "created_at":"2020-11-02T06:51:49Z",
      "updated_at":"2020-11-02T06:51:49Z",
      "revision_number":2
    }
}
```
</p>
</details>

---

### View an ACL Rule List
 
```
GET /v2.0/acl_rules/
X-Auth-Token: {tokenId}
```

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| sort_dir | Query | Enum | - | Sorting direction of ACL Rule to query<br>Sort by the field specified by `sort_key`<br>Either **asc**, or **desc** |
| sort_key | Query | String | - | Sorting key of ACL Rule to query<br>Sort in the direction as specified by `sort_dir` |
| fields | Query | String | - | Field name of ACL Rule to query<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format |  Description |
|---|---|---|---|
| acl_rules | Body | Array | ACL Rule list object |
| acl_rules.id | Body | String | ACL Rule ID |
| acl_rules.tenant_id | Body | String | Tenant ID |
| acl_rules.description | Body | String | ACL Rule description |
| acl_rules.create_at | Body | String | ACL Rule creation time |
| acl_rules.update_at | Body | String | ACL Rule update time |
| acl_rules.acl_id | Body | String | ACL ID |
| acl_rules.protocol | Body | String | protocol(tcp, udp, icmp) |
| acl_rules.ethertype | Body | String | Fixed to IPv4 |
| acl_rules.src_port_range_min | Body | Integer | Minimum value of src port range (1-65535)|
| acl_rules.src_port_range_max | Body | Integer | Maximum value of src port range (1 to 65535)|
| acl_rules.src_ip | Body | String | src ip |
| acl_rules.dst_ip | Body | String | dst ip |
| acl_rules.dst_port_range_max | Body | Integer | Minimum value of dst port range (1-65535)|
| acl_rules.dst_port_range_min | Body | Integer | Maximum value of dst port range (1 to 65535)|
| acl_rules.policy | Body | String | allow or deny  |
| acl_rules.order | Body | Integer | ACL Rule application order, the smaller the number, the earlier it is applied (102~32764 is used).|

<details><summary>Example</summary>
<p>

```json
{
  "acl_rules": [
    {"remote_group_id":null,"protocol":null,"description":"default deny rule","ethertype":"IPv4","created_at":"2022-12-16T06:58:54Z","src_port_range_max":null,"updated_at":"2022-12-16T06:58:54Z","id":"005a5644-4e43-47fc-b3d9-6c1befe12f7b","src_ip":"0.0.0.0/0","dst_port_range_min":null,"dst_port_range_max":null,"revision_number":0,"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce","policy":"deny","dst_ip":"0.0.0.0/0","project_id":"43b53d88b7a54d3aa5472bd800f1cbce","order":32765,"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b","src_port_range_min":null},
{"remote_group_id":null,"protocol":null,"description":"","ethertype":"IPv4","created_at":"2020-11-12T01:23:04Z","src_port_range_max":null,"updated_at":"2020-11-12T01:23:04Z","id":"00817eb7-4a3f-45dc-bc8d-8f792bc5a05c","src_ip":"0.0.0.0/0","dst_port_range_min":null,"dst_port_range_max":null,"revision_number":0,"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce","policy":"allow","dst_ip":"25.0.0.0/0","project_id":"43b53d88b7a54d3aa5472bd800f1cbce","order":125,"acl_id":"f16c042b-a3c6-4bb2-b10a-12b2edb77b01","src_port_range_min":null}
  ]
}
```
</p>
</details>

---

### View an ACL Rule

```
GET /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| aclRuleId | URL | UUID | O | ID of ACL Rule to query |
| fields | Query | String | - | Field name of ACL Rule to query<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format | Description |
|---|---|---|---|
| acl_rule | Body | Array | ACL Rule list object |
| acl_rule.id | Body | String | ACL Rule ID |
| acl_rule.tenant_id | Body | String | Tenant ID |
| acl_rule.description | Body | String | ACL Rule description |
| acl_rule.create_at | Body | String | ACL Rule creation time |
| acl_rule.update_at | Body | String | ACL Rule update time |
| acl_rule.acl_id | Body | String | ACL ID |
| acl_rule.protocol | Body | String | protocol(tcp, udp, icmp) |
| acl_rule.ethertype | Body | String | Fixed to IPv4 |
| acl_rule.src_port_range_min | Body | Integer | Minimum value of src port range (1-65535)|
| acl_rule.src_port_range_max | Body | Integer | Maximum value of src port range (1 to 65535)|
| acl_rule.src_ip | Body | String | src ip |
| acl_rule.dst_ip | Body | String | dst ip |
| acl_rule.dst_port_range_max | Body | Integer | Minimum value of dst port range (1-65535)|
| acl_rule.dst_port_range_min | Body | Integer | Maximum value of dst port range (1 to 65535)|
| acl_rule.policy | Body | String | allow or deny  |
| acl_rule.order | Body | Integer | ACL Rule application order, the smaller the number, the earlier it is applied (102~32764 is used).|


<details><summary>Example</summary>
<p>

```json
{
  "acl_rule": 
    {"remote_group_id":null,"protocol":null,"description":"default deny rule","ethertype":"IPv4","created_at":"2022-12-16T06:58:54Z","src_port_range_max":null,"updated_at":"2022-12-16T06:58:54Z","id":"005a5644-4e43-47fc-b3d9-6c1befe12f7b","src_ip":"0.0.0.0/0","dst_port_range_min":null,"dst_port_range_max":null,"revision_number":0,"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce","policy":"deny","dst_ip":"0.0.0.0/0","project_id":"43b53d88b7a54d3aa5472bd800f1cbce","order":32765,"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b","src_port_range_min":null}
}
```
</p>
</details>

---

### Create an ACL Rule

```
POST /v2.0/acl_rules
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format |  Required |Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| acl_rule | Body | Array | O | ACL Rule list object |
| acl_rule.tenant_id | Body | String | - | Tenant ID |
| acl_rule.description | Body | String | - |ACL Rule description |
| acl_rule.acl_id | Body | String | O |ACL ID |
| acl_rule.protocol | Body | String | -| protocol(tcp, udp, icmp) |
| acl_rule.ethertype | Body | String | -|Fixed to IPv4 |
| acl_rule.src_port_range_min | Body | Integer | -|Minimum value of src port range (1-65535)|
| acl_rule.src_port_range_max | Body | Integer | -|Maximum value of src port range (1 to 65535)|
| acl_rule.src_ip | Body | String | O|src ip |
| acl_rule.dst_ip | Body | String | O|dst ip |
| acl_rule.dst_port_range_max | Body | Integer | -|Minimum value of dst port range (1-65535)|
| acl_rule.dst_port_range_min | Body | Integer | -|Maximum value of dst port range (1 to 65535)|
| acl_rule.policy | Body | String | O| allow or deny  |
| acl_rule.order | Body | Integer | O | ACL Rule application order, the smaller the number, the earlier it is applied (102~32764 is used).|

<details><summary>Example</summary>
<p>

```json
{
  "acl_rule": {"src_ip":"0.0.0.0/0", "tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce",
"policy":"deny","dst_ip":"192.168.0.0/24",
"order":103,"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b"}
}
```
</p>
</details>

#### Response

 
| Name | Type | Format | Description |
|---|---|---|---|
| acl_rule | Body | Array | ACL Rule list object |
| acl_rule.id | Body | String | ACL Rule ID |
| acl_rule.tenant_id | Body | String | Tenant ID |
| acl_rule.description | Body | String | ACL Rule description |
| acl_rule.create_at | Body | String | ACL Rule creation time |
| acl_rule.update_at | Body | String | ACL Rule update time |
| acl_rule.acl_id | Body | String | ACL ID |
| acl_rule.protocol | Body | String | protocol(tcp, udp, icmp) |
| acl_rule.ethertype | Body | String | Fixed to IPv4 |
| acl_rule.src_port_range_min | Body | Integer | Minimum value of src port range (1-65535)|
| acl_rule.src_port_range_max | Body | Integer | Maximum value of src port range (1 to 65535)|
| acl_rule.src_ip | Body | String | src ip |
| acl_rule.dst_ip | Body | String | dst ip |
| acl_rule.dst_port_range_max | Body | Integer | Minimum value of dst port range (1-65535)|
| acl_rule.dst_port_range_min | Body | Integer | Maximum value of dst port range (1 to 65535)|
| acl_rule.policy | Body | String | allow or deny  |
| acl_rule.order | Body | Integer | ACL Rule application order, the smaller the number, the earlier it is applied (102~32764 is used).|

<details><summary>Example</summary>
<p>

```json
{
  "acl_rule": 
    {"remote_group_id":null,"protocol":null,"description":"","ethertype":"IPv4","created_at":"2022-12-16T06:58:54Z","src_port_range_max":null,"updated_at":"2022-12-16T06:58:54Z","id":"005a5644-4e43-47fc-b3d9-6c1befe12f7b","src_ip":"0.0.0.0/0","dst_port_range_min":null,"dst_port_range_max":null,"revision_number":0,"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce","policy":"deny","dst_ip":"192.168.0.0/24","project_id":"43b53d88b7a54d3aa5472bd800f1cbce","order":103,"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b","src_port_range_min":null}
}
```
</p>
</details>

---

### Delete an ACL Rule

```
DELETE /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| aclRuleId | URL | UUID | O | ID of ACL Rule to delete |
| tokenId | Header | String | O | Token ID |

#### Response

This API does not return a response body.

---

### Modify an ACL Rule

Modifies existing ACL Rules (only the description can be modified).

```
PUT /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| aclRuleId | URL | UUID | O | ID of ACL Rule to delete |
| acl_rule | Body | Array | O | ACL Rule list object |
| acl_rule.description | Body | String | O | ACL Rule description |

<details><summary>Example</summary>
<p>

```json
{
  "acl_rule": 
    {
      "description": "acl_rule1"
    }
}
```
</p>
</details>

#### Response

| Name | Type | Format |  Description |
|---|---|---|---|
| acl_rule | Body | Array | ACL Rule list object |
| acl_rule.id | Body | String | ACL Rule ID |
| acl_rule.tenant_id | Body | String | Tenant ID |
| acl_rule.description | Body | String | ACL Rule description |
| acl_rule.create_at | Body | String | ACL Rule creation time |
| acl_rule.update_at | Body | String | ACL Rule update time |
| acl_rule.acl_id | Body | String | ACL ID |
| acl_rule.protocol | Body | String | protocol(tcp, udp, icmp) |
| acl_rule.ethertype | Body | String | Fixed to IPv4 |
| acl_rule.src_port_range_min | Body | Integer | Minimum value of src port range (1-65535)|
| acl_rule.src_port_range_max | Body | Integer | Maximum value of src port range (1 to 65535)|
| acl_rule.src_ip | Body | String | src ip |
| acl_rule.dst_ip | Body | String | dst ip |
| acl_rule.dst_port_range_max | Body | Integer | Minimum value of dst port range (1-65535) |
| acl_rule.dst_port_range_min | Body | Integer | Maximum value of dst port range (1 to 65535)|
| acl_rule.policy | Body | String | allow or deny  |
| acl_rule.order | Body | Integer | ACL Rule application order, the smaller the number, the earlier it is applied (102~32764 is used).|


<details><summary>Example</summary>
<p>

```json
{
  "acl_rule": 
    {"remote_group_id":null,"protocol":null,"description":"default deny rule","ethertype":"IPv4","created_at":"2022-12-16T06:58:54Z","src_port_range_max":null,"updated_at":"2022-12-16T06:58:54Z","id":"005a5644-4e43-47fc-b3d9-6c1befe12f7b","src_ip":"0.0.0.0/0","dst_port_range_min":null,"dst_port_range_max":null,"revision_number":0,"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce","policy":"deny","dst_ip":"0.0.0.0/0","project_id":"43b53d88b7a54d3aa5472bd800f1cbce","order":32765,"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b","src_port_range_min":null}
}
```
</p>
</details>

---

### View an ACL Binding List

```
GET /v2.0/acl_bindings/
X-Auth-Token: {tokenId}
```

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| sort_dir | Query | Enum | - | Sorting direction of ACL biding to query<br>Sort by the field specified by `sort_key`<br>Either **asc**, or **desc** |
| sort_key | Query | String | - | Sorting key of ACL binding to query<br>Sort in the direction as specified by `sort_dir` |
| fields | Query | String | - | Field name of ACL binding to query<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format |  Description |
|---|---|---|---|
| acl_bindings | Body | Array | ACL binding list object |
| acl_bindings.id | Body | String | ACL binding ID |
| acl_bindings.tenant_id | Body | String | Tenant ID |
| acl_bindings.acl_id | Body | String | ACL ID bound to network |
| acl_bindings.network_id | Body | String | Network ID bound to ACL |


<details><summary>Example</summary>
<p>

```json
{
  "acl_bindings": [ 
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "acl_id":"2a61e4ab-b7f7-4323-a399-7e121996f6bb",
      "network_id":"56abace2-98b5-4767-ae5e-a2e2ab44d49a"
    },
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "id": "edb544dc-377d-4bbd-8516-435ad45b47ad",
      "acl_id":"9b0bb5bd-f457-483f-9adb-987bce2bed89",
      "network_id":"0bb5e696-65cf-49d8-a545-d9d814e3c4b2"
    }
   ]
}
```
</p>
</details>

---

### View an ACL Binding

```
GET /v2.0/acl_bindings/{aclBindingId}
X-Auth-Token: {tokenId}
```

#### Request

This API does not require a request body.

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| aclBindingId | URL | UUID | O | ID of ACL binding to query |
| fields | Query | String | - | Field name of ACL binding to query<br>e.g.) `fields=id&fields=name` |

#### Response

| Name | Type | Format |  Description |
|---|---|---|---|
| acl_binding | Body | Array | ACL binding list object |
| acl_binding.id | Body | String | ACL binding ID |
| acl_binding.tenant_id | Body | String | Tenant ID |
| acl_binding.acl_id | Body | String | ACL ID bound to network |
| acl_binding.network_id | Body | String | Network ID bound to ACL |


<details><summary>Example</summary>
<p>

```json
{
  "acl_binding": 
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "acl_id":"2a61e4ab-b7f7-4323-a399-7e121996f6bb",
      "network_id":"56abace2-98b5-4767-ae5e-a2e2ab44d49a"
    }
}
```
</p>
</details>

---
 
### Create an ACL Binding

```
POST /v2.0/acl_bindings
X-Auth-Token: {tokenId}
```

#### Request

| Name | Type | Format |  Required |Description |
|---|---|---|---|---|
| tokenId | Header | String | O | Token ID |
| acl_binding | Body | Array | O | ACL binding list object |
| acl_binding.tenant_id | Body | String | - | Tenant ID |
| acl_binding.network_id | Body | String | O | Network ID |
| acl_binding.acl_id | Body | String | O |ACL ID |

<details><summary>Example</summary>
<p>

```json
{
  "acl_binding": 
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "acl_id":"2a61e4ab-b7f7-4323-a399-7e121996f6bb",
      "network_id":"56abace2-98b5-4767-ae5e-a2e2ab44d49a"
    }
}
```
</p>
</details>


#### Response

| Name | Type | Format |  Description |
|---|---|---|---|
| acl_binding | Body | Array | ACL binding list object |
| acl_binding.id | Body | String | ACL binding ID |
| acl_binding.tenant_id | Body | String | Tenant ID |
| acl_binding.acl_id | Body | String | ACL ID bound to network |
| acl_binding.network_id | Body | String | Network ID bound to ACL |

<details><summary>Example</summary>
<p>

```json
{
  "acl_binding": 
    {
      "tenant_id": "19eeb40d58684543aef29cbb5ebfe8f0",
      "id": "877b092c-2a31-4509-8d23-deeb02d95633",
      "acl_id":"2a61e4ab-b7f7-4323-a399-7e121996f6bb",
      "network_id":"56abace2-98b5-4767-ae5e-a2e2ab44d49a"
    }
}
```
</p>
</details>

---

### Delete an ACL Binding

```
DELETE /v2.0/acl_bindings/{aclBindingId}
X-Auth-Token: {tokenId}
```


#### Request

| Name | Type | Format | Required | Description |
|---|---|---|---|---|
| aclBindingId | URL | UUID | O | ID of ACL binding to delete |
| tokenId | Header | String | O | Token ID |

#### Response

This API does not return a response body.