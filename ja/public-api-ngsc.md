## Network > Network ACL > API v2ガイド

APIを使用するにはAPIエンドポイントとトークン などが必要です。 [API使用準備](/Compute/Compute/ko/identity-api-ngsc/)を参照してAPIの使用に必要な情報を準備します。

セキュリティグループAPIは`network`タイプエンドポイントを利用します。正確なエンドポイントはトークン発行レスポンスの`serviceCatalog`を参照します。

| タイプ | リージョン | エンドポイント |
|---|---|---|
| network | 韓国(ピョンチョン)リージョン | https://kr1-api-network-infrastructure.gncloud.go.kr |

APIレスポンスにガイドに明示されていないフィールドが表示される場合があります。このようなフィールドはNHN Cloud内部用途に使用され、予告なしに変更される可能性があるため、使用しないでください。


<a id="1"></a>
## Network ACL

<a id="2"></a>
### ACLリスト表示
```
GET /v2.0/acls
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| sort_dir | Query | Enum | - | 照会するACLのソート方向<br>`sort_key`で指定したフィールドを基準にソート<br>**asc**、**desc**のいずれか |
| sort_key | Query | String | - | 照会するACLのソートキー<br>`sort_dir`で指定した方向でソート |
| fields | Query | String | - | 照会するACLのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acls | Body | Array | ACLリストオブジェクト |
| acls.id | Body | UUID | ACL ID |
| acls.tenant_id | Body | String | テナントID |
| acls.description | Body | String | ACLの説明 |
| acls.name | Body | String | ACLの名前 |
| acls.create_at | Body | String | ACL作成時間 |
| acls.update_at | Body | String | ACL更新時間 |

<details><summary>例</summary>
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

<a id="3"></a>
### ACL表示

```
GET /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| aclId | URL | UUID | O | 照会するACL ID |
| fields | Query | String | - | 照会するACLのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl | Body | Array | ACLリストオブジェクト |
| acl.id | Body | UUID | ACL ID |
| acl.tenant_id | Body | String | テナントID |
| acl.description | Body | String | ACLの説明 |
| acl.name | Body | String | ACLの名前 |
| acl.create_at | Body | String | ACL作成時間 |
| acl.update_at | Body | String | ACL更新時間 |

<details><summary>例</summary>
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

<a id="4"></a>
### ACL作成
 
```
POST /v2.0/acls
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| acl | Body | Array | O | ACLリストオブジェクト |
| acl.tenant_id | Body | String | - | テナントID |
| acl.name | Body | String | - | ACLの名前(区別のために入れることを推奨) |
| acl.description | Body | String | - | ACLの説明 |

<details><summary>例</summary>
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

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl | Body | Array | ACLリストオブジェクト |
| acl.id | Body | String | ACL ID |
| acl.tenant_id | Body | String | テナントID |
| acl.name | Body | String | ACLの名前 |
| acl.description | Body | String | ACLの説明 |
| acl.create_at | Body | String | ACL作成時間 |
| acl.update_at | Body | String | ACL更新時間 |

<details><summary>例</summary>
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

<a id="5"></a>
### ACL削除

```
DELETE /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| aclId | URL | UUID | O | 削除するACL ID |
| tokenId | Header | String | O | トークンID |

#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="6"></a>
### ACL修正
既存のACLを修正します(名前と説明のみ修正可能)。

```
PUT /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| aclId | URL | String | O | ACL ID |
| acl | Body | Array | O | ACLリストオブジェクト |
| acl.name | Body | String | - | ACLの名前 |
| acl.description | Body | String | - | ACLの説明 |

<details><summary>例</summary>
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

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl | Body | Array | ACLリストオブジェクト |
| acl.id | Body | String | ACL ID |
| acl.tenant_id | Body | String | テナントID |
| acl.name | Body | String | ACLの名前 |
| acl.description | Body | String | ACLの説明 |
| acl.create_at | Body | String | ACL作成時間 |
| acl.update_at | Body | String | ACL更新時間 |


<details><summary>例</summary>
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

<a id="7"></a>
### ACL Ruleリスト表示
 
```
GET /v2.0/acl_rules
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| sort_dir | Query | Enum | - | 照会するACL Ruleのソート方向<br>`sort_key`で指定したフィールドを基準にソート<br>**asc**、**desc**のいずれか |
| sort_key | Query | String | - | 照会するACL Ruleのソートキー<br>`sort_dir`で指定した方向でソート |
| fields | Query | String | - | 照会するACL Ruleのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl\_rules | Body | Array | ACL Ruleリストオブジェクト |
| acl\_rules.id | Body | String | ACL Rule ID |
| acl\_rules.tenant_id | Body | String | テナントID |
| acl\_rules.description | Body | String | ACL Ruleの説明 |
| acl\_rules.create_at | Body | String | ACL Rule作成時間 |
| acl\_rules.update_at | Body | String | ACL Rule更新時間 |
| acl\_rules.acl_id | Body | String | ACL ID |
| acl\_rules.protocol | Body | String | protocol(tcp, udp, icmp) |
| acl\_rules.ethertype | Body | String | IPv4で 固定 |
| acl\_rules.src\_port\_range\_min | Body | Integer | srcポート範囲の最小値(1～65535)|
| acl\_rules.src\_port\_range\_max | Body | Integer | srcポート範囲の最大値(1～65535)|
| acl\_rules.src_ip | Body | String | src ip |
| acl\_rules.dst_ip | Body | String | dst ip |
| acl\_rules.dst\_port\_range\_max | Body | Integer | dstポート範囲の最小値(1～65535)|
| acl\_rules.dst\_port\_range\_min | Body | Integer | dstポート範囲の最大値(1～65535)|
| acl\_rules.policy | Body | String | allow or deny  |
| acl\_rules.order | Body | Integer | ACL Rule適用順序、数字が小さいほど先に適用される(102～32764使用).|

<details><summary>例</summary>
<p>

```json
{
  "acl_rules": [
    {
    	"remote_group_id":null,
    	"protocol":null,
    	"description":"default denyrule",
		"ethertype":"IPv4",
		"created_at":"2022-12-16T06:58:54Z",
		"src_port_range_max":null,
		"updated_at":"2022-12-16T06:58:54Z",
		"id":"005a5644-4e43-47fcb3d9-6c1befe12f7b",
		"src_ip":"0.0.0.0/0",
		"dst_port_range_min":null,
		"dst_port_range_max":null,
		"revision_number":0,
		"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce",
		"policy":"deny",
		"dst_ip":"0.0.0.0/0",
		"project_id":"43b53d88b7a54d3aa5472bd800f1cbce",
		"order":32765,
		"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b",
		"src_port_range_min":null
	},
	{
		"remote_group_id":null,
		"protocol":null,
		"description":"",
		"ethertype":"IPv4",
		"created_at":"2020-11-12T01:23:04Z",
		"src_port_range_max":null,
		"updated_at":"2020-11-12T01:23:04Z",
		"id":"00817eb7-4a3f-45dcbc8d-8f792bc5a05c",
		"src_ip":"0.0.0.0/0",
		"dst_port_range_min":null,
		"dst_port_range_max":null,
		"revision_number":0,
		"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce",
		"policy":"allow",
		"dst_ip":"25.0.0.0/0",
		"project_id":"43b53d88b7a54d3aa5472bd800f1cbce",
		"order":125,
		"acl_id":"f16c042b-a3c6-4bb2-b10a-12b2edb77b01",
		"src_port_range_min":null
	}
  ]
}
```
</p>
</details>

---

<a id="8"></a>
### ACL Rule表示

```
GET /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| aclRuleId | URL | UUID | O | 照会するACL Rule ID |
| fields | Query | String | - | 照会するACL Ruleのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl\_rule | Body | Array | ACL Ruleリストオブジェクト |
| acl\_rule.id | Body | String | ACL Rule ID |
| acl\_rule.tenant_id | Body | String | テナントID |
| acl\_rule.description | Body | String | ACL Ruleの説明 |
| acl\_rule.create_at | Body | String | ACL Rule作成時間 |
| acl\_rule.update_at | Body | String | ACL Rule更新時間 |
| acl\_rule.acl_id | Body | String | ACL ID |
| acl\_rule.protocol | Body | String | protocol(tcp, udp, icmp) |
| acl\_rule.ethertype | Body | String | IPv4で固定 |
| acl\_rule.src\_port\_range\_min | Body | Integer | srcポート範囲の最小値(1～65535)|
| acl\_rule.src\_port\_range\_max | Body | Integer | srcポート範囲の最大値(1～65535)|
| acl\_rule.src_ip | Body | String | src ip |
| acl\_rule.dst_ip | Body | String | dst ip |
| acl\_rule.dst\_port\_range\_max | Body | Integer | dstポート範囲の最小値(1～65535)|
| acl\_rule.dst\_port\_range\_min | Body | Integer | dstポート範囲の最大値(1～65535)|
| acl\_rule.policy | Body | String | allow or deny  |
| acl\_rule.order | Body | Integer | ACL Rule適用順序。数字が小さいほど先に適用されます(102～32764使用)。|


<details><summary>例</summary>
<p>

```json
{
  "acl_rule": 
    {
    	"remote_group_id":null,
    	"protocol":null,
    	"description":"default deny rule",
		"ethertype":"IPv4",
		"created_at":"2022-12-16T06:58:54Z",
		"src_port_range_max":null,
		"updated_at":"2022-12-16T06:58:54Z",
		"id":"005a5644-4e43-47fcb3d9-6c1befe12f7b",
		"src_ip":"0.0.0.0/0",
		"dst_port_range_min":null,
		"dst_port_range_max":null,
		"revision_number":0,
		"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce",
		"policy":"deny",
		"dst_ip":"0.0.0.0/0",
		"project_id":"43b53d88b7a54d3aa5472bd800f1cbce",
		"order":32765,
		"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b",
		"src_port_range_min":null
	}
}
```
</p>
</details>

---

<a id="9"></a>
### ACL Rule作成

```
POST /v2.0/acl_rules
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 |説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| acl\_rule | Body | Array | O | ACL Ruleリストオブジェクト |
| acl\_rule.tenant_id | Body | String | - | テナントID |
| acl\_rule.description | Body | String | - |ACL Ruleの説明 |
| acl\_rule.acl_id | Body | String | O |ACL ID |
| acl\_rule.protocol | Body | String | -| protocol(tcp, udp, icmp) |
| acl\_rule.ethertype | Body | String | -|IPv4で固定 |
| acl\_rule.src\_port\_range\_min | Body | Integer | -|srcポート範囲の最小値(1～65535)|
| acl\_rule.src\_port\_range\_max | Body | Integer | -|srcポート範囲の最大値(1～65535)|
| acl\_rule.src_ip | Body | String | O|src ip |
| acl\_rule.dst_ip | Body | String | O|dst ip |
| acl\_rule.dst\_port\_range\_max | Body | Integer | -|dstポート範囲の最小値(1～65535)|
| acl\_rule.dst\_port\_range\_min | Body | Integer | -|dstポート範囲の最大値(1～65535)|
| acl\_rule.policy | Body | String | O| allow or deny  |
| acl\_rule.order | Body | Integer | O | ACL Rule適用順序。数字が小さいほど先に適用されます(102～32764使用)。|

<details><summary>例</summary>
<p>

```json
{
  "acl_rule": 
  	{
  		"src_ip":"0.0.0.0/0", 
  		"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce",
  		"policy":"deny","dst_ip":"192.168.0.0/24",
  		"order":103,
  		"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b"
  	}
}

```
</p>
</details>

#### レスポンス

 
| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl\_rule | Body | Array | ACL Ruleリストオブジェクト |
| acl\_rule.id | Body | String | ACL Rule ID |
| acl\_rule.tenant_id | Body | String | テナントID |
| acl\_rule.description | Body | String | ACL Ruleの説明 |
| acl\_rule.create_at | Body | String | ACL Rule作成時間 |
| acl\_rule.update_at | Body | String | ACL Rule更新時間 |
| acl\_rule.acl_id | Body | String | ACL ID |
| acl\_rule.protocol | Body | String | protocol(tcp, udp, icmp) |
| acl\_rule.ethertype | Body | String | IPv4で固定 |
| acl\_rule.src\_port\_range\_min | Body | Integer | srcポート範囲の最小値(1～65535)|
| acl\_rule.src\_port\_range\_max | Body | Integer | srcポート範囲の最大値(1～65535)|
| acl\_rule.src_ip | Body | String | src ip |
| acl\_rule.dst_ip | Body | String | dst ip |
| acl\_rule.dst\_port\_range\_max | Body | Integer | dstポート範囲の最小値(1～65535)|
| acl\_rule.dst\_port\_range\_min | Body | Integer | dstポート範囲の最大値(1～65535)|
| acl\_rule.policy | Body | String | allow or deny  |
| acl\_rule.order | Body | Integer | ACL Rule適用順序。数字が小さいほど先に適用されます(102～32764使用)。|

<details><summary>例</summary>
<p>

```json
{
  "acl_rule": 
    {
    	"remote_group_id":null,
    	"protocol":null,
    	"description":"",
    	"ethertype":"IPv4",
    	"created_at":"2022-12-16T06:58:54Z",
    	"src_port_range_max":null,
    	"updated_at":"2022-12-16T06:58:54Z",
    	"id":"005a5644-4e43-47fcb3d9-6c1befe12f7b",
    	"src_ip":"0.0.0.0/0",
    	"dst_port_range_min":null,
    	"dst_port_range_max":null,
    	"revision_number":0,
    	"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce",
    	"policy":"deny",
    	"dst_ip":"192.168.0.0/24",
    	"project_id":"43b53d88b7a54d3aa5472bd800f1cbce",
    	"order":103,
    	"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b",
    	"src_port_range_min":null
    }
}
```
</p>
</details>

---

<a id="10"></a>
### ACL Ruleの削除

```
DELETE /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| aclRuleId | URL | UUID | O | 削除するACL Rule ID |
| tokenId | Header | String | O | トークンID |

#### レスポンス

このAPIはレスポンス本文を返しません。

---

<a id="11"></a>
### ACL Ruleの修正

既存ACL Ruleを修正します(説明のみ修正可能です)。

```
PUT /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| aclRuleId | URL | UUID | O | 削除するACL Rule ID |
| acl\_rule | Body | Array | O | ACL Ruleリストオブジェクト |
| acl\_rule.description | Body | String | O | ACL Ruleの説明 |

<details><summary>例</summary>
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

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl\_rule | Body | Array | ACL Ruleリストオブジェクト |
| acl\_rule.id | Body | String | ACL Rule ID |
| acl\_rule.tenant_id | Body | String | テナントID |
| acl\_rule.description | Body | String | ACL Ruleの説明 |
| acl\_rule.create_at | Body | String | ACL Rule作成時間 |
| acl\_rule.update_at | Body | String | ACL Rule更新時間 |
| acl\_rule.acl_id | Body | String | ACL ID |
| acl\_rule.protocol | Body | String | protocol(tcp, udp, icmp) |
| acl\_rule.ethertype | Body | String | IPv4で固定 |
| acl\_rule.src\_port\_range\_min | Body | Integer | srcポート範囲の最小値(1～65535)|
| acl\_rule.src\_port\_range\_max | Body | Integer | srcポート範囲の最大値(1～65535)|
| acl\_rule.src_ip | Body | String | src ip |
| acl\_rule.dst_ip | Body | String | dst ip |
| acl\_rule.dst\_port\_range\_max | Body | Integer | dstポート範囲の最小値(1～65535) |
| acl\_rule.dst\_port\_range\_min | Body | Integer | dstポート範囲の最大値(1～65535)|
| acl\_rule.policy | Body | String | allow or deny  |
| acl\_rule.order | Body | Integer | ACL Rule適用順序。数字が小さいほど先に適用されます(102～32764使用)。|


<details><summary>例</summary>
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

<a id="12"></a>
### ACLバインディングリスト表示

```
GET /v2.0/acl_bindings
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| sort_dir | Query | Enum | - | 照会するACLバインディングのソート方向<br>`sort_key`で指定したフィールドを基準にソート<br>**asc**、**desc**のいずれか |
| sort_key | Query | String | - | 照会するACLバインディングのソートキー<br>`sort_dir`で指定した方向でソート |
| fields | Query | String | - | 照会するACLバインディングのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl\_bindings | Body | Array | ACLバインディングリストオブジェクト |
| acl\_bindings.id | Body | String | ACLバインディングID |
| acl\_bindings.tenant_id | Body | String | テナントID |
| acl\_bindings.acl_id | Body | String | NetworkとバインディングされるACL ID |
| acl\_bindings.network_id | Body | String | ACLとバインディングされるNetwork ID |


<details><summary>例</summary>
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

<a id="13"></a>
### ACLバインディング表示

```
GET /v2.0/acl_bindings/{aclBindingId}
X-Auth-Token: {tokenId}
```

#### リクエスト

このAPIはリクエスト本文を要求しません。

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| aclBindingId | URL | UUID | O | 照会するACLバインディングID |
| fields | Query | String | - | 照会するACLバインディングのフィールド名<br>例) `fields=id&fields=name` |

#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl\_binding | Body | Array | ACLバインディングリストオブジェクト |
| acl\_binding.id | Body | String | ACLバインディングID |
| acl\_binding.tenant_id | Body | String | テナントID |
| acl\_binding.acl_id | Body | String | NetworkとバインディングされるACL ID |
| acl\_binding.network_id | Body | String | ACLとバインディングされるNetwork ID |


<details><summary>例</summary>
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

<a id="14"></a> 
### ACLバインディングの作成

```
POST /v2.0/acl_bindings
X-Auth-Token: {tokenId}
```

#### リクエスト

| 名前 | 種類 | 形式 | 必須 |説明 |
|---|---|---|---|---|
| tokenId | Header | String | O | トークンID |
| acl\_binding | Body | Array | O | ACLバインディングリストオブジェクト |
| acl\_binding.tenant_id | Body | String | - | テナントID |
| acl\_binding.network_id | Body | String | O | Network ID |
| acl\_binding.acl_id | Body | String | O |ACL ID |

<details><summary>例</summary>
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


#### レスポンス

| 名前 | 種類 | 形式 | 説明 |
|---|---|---|---|
| acl\_binding | Body | Array | ACLバインディングリストオブジェクト |
| acl\_binding.id | Body | String | ACLバインディングID |
| acl\_binding.tenant_id | Body | String | テナントID |
| acl\_binding.acl_id | Body | String | NetworkとバインディングされるACL ID |
| acl\_binding.network_id | Body | String | ACLとバインディングされるNetwork ID |

<details><summary>例</summary>
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

<a id="15"></a>
### ACLバインディングの削除

```
DELETE /v2.0/acl_bindings/{aclBindingId}
X-Auth-Token: {tokenId}
```


#### リクエスト

| 名前 | 種類 | 形式 | 必須 | 説明 |
|---|---|---|---|---|
| aclBindingId | URL | UUID | O | 削除するACLバインディングID |
| tokenId | Header | String | O | トークンID |

#### レスポンス

このAPIはレスポンス本文を返しません。
