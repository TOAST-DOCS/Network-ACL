## Network > Network ACL > API v2 가이드

API를 사용하려면 API 엔드포인트와 토큰 등이 필요합니다. [API 사용 준비](/Compute/Compute/ko/identity-api/)를 참고하여 API 사용에 필요한 정보를 준비합니다.

Network ACL API는 `network` 타입 엔드포인트를 이용합니다. 정확한 엔드포인트는 토큰 발급 응답의 `serviceCatalog`를 참조합니다.

| 타입 | 리전 | 엔드포인트 |
|---|---|---|
| network | 한국(판교) 리전<br>한국(평촌) 리전<br>일본 리전 | https://kr1-api-network-infrastructure.nhncloudservice.com<br>https://kr2-api-network-infrastructure.nhncloudservice.com<br>https://jp1-api-network-infrastructure.nhncloudservice.com |

API 응답에 가이드에 명시되지 않은 필드가 나타날 수 있습니다. 이런 필드는 NHN Cloud 내부 용도로 사용되며 사전 공지 없이 변경될 수 있으므로 사용하지 않습니다.

## ACL 목록 보기
```
GET /v2.0/acls
X-Auth-Token: {tokenId}
```

### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 ACL ID |
| tenant_id | Query | String | - | 조회할 ACL의 테넌트 ID |
| sort_dir | Query | Enum | - | 조회할 ACL의 정렬 방향<br>`sort_key`에서 지정한 필드를 기준으로 정렬<br>**asc**, **desc** 중 하나 |
| sort_key | Query | String | - | 조회할 ACL의 정렬 키<br>`sort_dir`에서 지정한 방향대로 정렬 |
| fields | Query | String | - | 조회할 ACL의 필드 이름<br>예) `fields=id&fields=name` |

### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| acls | Body | Array | ACL 목록 객체 |
| acls.id | Body | UUID | ACL ID |
| acls.tenant_id | Body | String | 테넌트 ID |
| acls.description | Body | String | ACL 설명 |
| acls.name | Body | String | ACL 이름 |
| acls.revision_number | Query | String | ACL 개정 번호 |
| acls.create_at | Query | String | ACL 생성시간 |
| acls.update_at | Query | String | ACL 갱신시간 |

<details><summary>예시</summary>
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

## ACL 보기

```
GET /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| aclId | Query | UUID | O | 조회할 ACL ID |
| fields | Query | String | - | 조회할 ACL의 필드 이름<br>예) `fields=id&fields=name` |

### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| acl | Body | Array | ACL 목록 객체 |
| acl.id | Body | UUID | ACL ID |
| acl.tenant_id | Body | String | 테넌트 ID |
| acl.description | Body | String | ACL 설명 |
| acl.name | Body | String | ACL 이름 |
| acl.revision_number | Query | String | ACL 개정 번호 |
| acl.create_at | Query | String | ACL 생성시간 |
| acl.update_at | Query | String | ACL 갱신시간 |

<details><summary>예시</summary>
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

## ACL 생성
 
```
POST /v2.0/acls/
X-Auth-Token: {tokenId}
```

### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| tenant_id | Body | String | O | 테넌트 ID |
| name | Query | String | - | ACL 이름 |
| description | Query | String | - | ACL 설명 |

<details><summary>예시</summary>
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

### 응답

| 이름 | 종류 | 형식 |  설명 |
|---|---|---|---|
| acl | Body | Array | ACL 목록 객체 |
| acl.id | Body | String | acl ID |
| acl.tenant_id | Body | String | 테넌트 ID |
| acl.name | Query | String | ACL 이름 |
| acl.description | Query | String | ACL 설명 |
| acl.revision_number | Query | String | ACL 개정 번호 |
| acl.create_at | Query | String | ACL 생성시간 |
| acl.update_at | Query | String | ACL 갱신시간 |

<details><summary>예시</summary>
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

## ACL 삭제

```
DELETE /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| aclId | Query | UUID | O | 삭제할 ACL ID |
| tokenId | Header | String | O | 토큰 ID |

### 응답

이 API는 응답 본문을 반환하지 않습니다.

## ACL 수정
기존 ACL을 수정합니다. (이름과 설명만 수정 가능 합니다)

```
PUT /v2.0/acls/{aclId}
X-Auth-Token: {tokenId}
```

### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| name | Query | String | - | ACL 이름 |
| description | Query | String | - | ACL 설명 |

<details><summary>예시</summary>
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

### 응답

| 이름 | 종류 | 형식 |  설명 |
|---|---|---|---|
| acl | Body | Array | ACL 목록 객체 |
| acl.id | Body | String | acl ID |
| acl.tenant_id | Body | String | 테넌트 ID |
| acl.name | Query | String | ACL 이름 |
| acl.description | Query | String | ACL 설명 |
| acl.revision_number | Query | String | ACL 개정 번호 |
| acl.create_at | Query | String | ACL 생성시간 |
| acl.update_at | Query | String | ACL 갱신시간 |


<details><summary>예시</summary>
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

## ACL Rule 목록 보기
 
```
GET /v2.0/acl_rules/
X-Auth-Token: {tokenId}
```

### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| id | Query | UUID | - | 조회할 ACL Rule ID |
| tenant_id | Query | String | - | 조회할 ACL Rule의 테넌트 ID |
| sort_dir | Query | Enum | - | 조회할 ACL Rule의 정렬 방향<br>`sort_key`에서 지정한 필드를 기준으로 정렬<br>**asc**, **desc** 중 하나 |
| sort_key | Query | String | - | 조회할 ACL Rule의 정렬 키<br>`sort_dir`에서 지정한 방향대로 정렬 |
| fields | Query | String | - | 조회할 ACL Rule의 필드 이름<br>예) `fields=id&fields=name` |

### 응답

| 이름 | 종류 | 형식 |  설명 |
|---|---|---|---|
| acl_rules | Body | Array | ACL Rule 목록 객체 |
| acl_rules.id | Body | String | ACL Rule ID |
| acl_rules.tenant_id | Body | String | 테넌트 ID |
| acl_rules.name | Query | String | ACL Rule 이름 |
| acl_rules.description | Query | String | ACL Rule 설명 |
| acl_rules.revision_number | Query | String | ACL Rule 개정 번호 |
| acl_rules.create_at | Query | String | ACL Rule 생성시간 |
| acl_rules.update_at | Query | String | ACL Rule 갱신시간 |
| acl_rules.acl_id | Body | String | ACL ID |
| acl_rules.remote_group_id | Body | String | 원격 그룹 id (미사용) |
| acl_rules.protocol | Body | String | protocol (tcp,udp,icmp) |
| acl_rules.ethertype | Body | String | IPv4로 고정 |
| acl_rules.src_port_range_min | Body | String | src 포트 범위의 최소값 |
| acl_rules.src_port_range_max | Body | String | src 포트 범위의 최대값 |
| acl_rules.src_ip | Body | String | src ip |
| acl_rules.dst_ip | Body | String | dst ip |
| acl_rules.dst_port_range_max | Body | String | dst 포트 범위의 최소값 |
| acl_rules.dst_port_range_min | Body | String | dst 포트 범위의 최대값 |
| acl_rules.policy | Body | String | allow or deny  |
| acl_rules.order | Body | Integer | ACL Rule 적용순서, 숫자가 작을수록 먼저 적용됨. (102 ~32764 사용)|

<details><summary>예시</summary>
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

## ACL Rule 보기

```
GET /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| aclRuleId | Query | UUID | O | 조회할 ACL Rule ID |
| fields | Query | String | - | 조회할 ACL Rule의 필드 이름<br>예) `fields=id&fields=name` |

### 응답

| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| acl_rule | Body | Array | ACL Rule 목록 객체 |
| acl_rule.id | Body | String | ACL Rule ID |
| acl_rule.tenant_id | Body | String | 테넌트 ID |
| acl_rule.name | Query | String | ACL Rule 이름 |
| acl_rule.description | Query | String | ACL Rule 설명 |
| acl_rule.revision_number | Query | String | ACL Rule 개정 번호 |
| acl_rule.create_at | Query | String | ACL Rule 생성시간 |
| acl_rule.update_at | Query | String | ACL Rule 갱신시간 |
| acl_rule.acl_id | Body | String | ACL ID |
| acl_rule.remote_group_id | Body | String | 원격 그룹 id (미사용) |
| acl_rule.protocol | Body | String | protocol (tcp,udp,icmp) |
| acl_rule.ethertype | Body | String | IPv4로 고정 |
| acl_rule.src_port_range_min | Body | String | src 포트 범위의 최소값 |
| acl_rule.src_port_range_max | Body | String | src 포트 범위의 최대값 |
| acl_rule.src_ip | Body | String | src ip |
| acl_rule.dst_ip | Body | String | dst ip |
| acl_rule.dst_port_range_max | Body | String | dst 포트 범위의 최소값 |
| acl_rule.dst_port_range_min | Body | String | dst 포트 범위의 최대값 |
| acl_rule.policy | Body | String | allow or deny  |
| acl_rule.order | Body | Integer | ACL Rule 적용순서, 숫자가 작을수록 먼저 적용됨. (102 ~32764 사용)|


<details><summary>예시</summary>
<p>

```json
{
  "acl_rule": 
    {"remote_group_id":null,"protocol":null,"description":"default deny rule","ethertype":"IPv4","created_at":"2022-12-16T06:58:54Z","src_port_range_max":null,"updated_at":"2022-12-16T06:58:54Z","id":"005a5644-4e43-47fc-b3d9-6c1befe12f7b","src_ip":"0.0.0.0/0","dst_port_range_min":null,"dst_port_range_max":null,"revision_number":0,"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce","policy":"deny","dst_ip":"0.0.0.0/0","project_id":"43b53d88b7a54d3aa5472bd800f1cbce","order":32765,"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b","src_port_range_min":null}
}
```
</p>
</details>

## ACL Rule 생성

```
POST /v2.0/acl_rules/
X-Auth-Token: {tokenId}
```

### 요청

| 이름 | 종류 | 형식 |  필수 |설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| tenant_id | Body | String | O | 테넌트 ID |
| name | Query | String | - |ACL Rule 이름 |
| description | Query | String | - |ACL Rule 설명 |
| acl_id | Body | String | O |ACL ID |
| protocol | Body | String | -| protocol (tcp,udp,icmp) |
| ethertype | Body | String | -|IPv4로 고정 |
| src_port_range_min | Body | String | -|src 포트 범위의 최소값 |
| src_port_range_max | Body | String | -|src 포트 범위의 최대값 |
| src_ip | Body | String | O|src ip |
| dst_ip | Body | String | O|dst ip |
| dst_port_range_max | Body | String | -|dst 포트 범위의 최소값 |
| dst_port_range_min | Body | String | -|dst 포트 범위의 최대값 |
| policy | Body | String | O| allow or deny  |
| order | Body | Integer | O | ACL Rule 적용순서, 숫자가 작을수록 먼저 적용됨. (102 ~32764 사용)|

### 응답

 
| 이름 | 종류 | 형식 | 설명 |
|---|---|---|---|
| acl_rule | Body | Array | ACL Rule 목록 객체 |
| acl_rule.id | Body | String | ACL Rule ID |
| acl_rule.tenant_id | Body | String | 테넌트 ID |
| acl_rule.name | Query | String | ACL Rule 이름 |
| acl_rule.description | Query | String | ACL Rule 설명 |
| acl_rule.revision_number | Query | String | ACL Rule 개정 번호 |
| acl_rule.create_at | Query | String | ACL Rule 생성시간 |
| acl_rule.update_at | Query | String | ACL Rule 갱신시간 |
| acl_rule.acl_id | Body | String | ACL ID |
| acl_rule.remote_group_id | Body | String | 원격 그룹 id (미사용) |
| acl_rule.protocol | Body | String | protocol (tcp,udp,icmp) |
| acl_rule.ethertype | Body | String | IPv4로 고정 |
| acl_rule.src_port_range_min | Body | String | src 포트 범위의 최소값 |
| acl_rule.src_port_range_max | Body | String | src 포트 범위의 최대값 |
| acl_rule.src_ip | Body | String | src ip |
| acl_rule.dst_ip | Body | String | dst ip |
| acl_rule.dst_port_range_max | Body | String | dst 포트 범위의 최소값 |
| acl_rule.dst_port_range_min | Body | String | dst 포트 범위의 최대값 |
| acl_rule.policy | Body | String | allow or deny  |
| acl_rule.order | Body | Integer | ACL Rule 적용순서, 숫자가 작을수록 먼저 적용됨. (102 ~32764 사용)|

<details><summary>예시</summary>
<p>

```json
{
  "acl_rule": 
    {"remote_group_id":null,"protocol":null,"description":"default deny rule","ethertype":"IPv4","created_at":"2022-12-16T06:58:54Z","src_port_range_max":null,"updated_at":"2022-12-16T06:58:54Z","id":"005a5644-4e43-47fc-b3d9-6c1befe12f7b","src_ip":"0.0.0.0/0","dst_port_range_min":null,"dst_port_range_max":null,"revision_number":0,"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce","policy":"deny","dst_ip":"0.0.0.0/0","project_id":"43b53d88b7a54d3aa5472bd800f1cbce","order":32765,"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b","src_port_range_min":null}
}
```
</p>
</details>

## ACL Rule 삭제

```
DELETE /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| aclRuleId | Query | UUID | O | 삭제할 ACL Rule ID |
| tokenId | Header | String | O | 토큰 ID |

### 응답

이 API는 응답 본문을 반환하지 않습니다.

## ACL Rule 수정

기존 ACL Rule을 수정합니다. (이름과 설명만 수정 가능 합니다)

```
PUT /v2.0/acl_rules/{aclRuleId}
X-Auth-Token: {tokenId}
```

### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| name | Query | String | - | ACL Rule 이름 |
| description | Query | String | - | ACL Rule 설명 |

<details><summary>예시</summary>
<p>

```json
{
  "acl_rule": 
    {
      "description": "acl_rule1",
      "name": "rule1"
    }
}
```
</p>
</details>

### 응답

| 이름 | 종류 | 형식 |  설명 |
|---|---|---|---|
| acl_rule | Body | Array | ACL Rule 목록 객체 |
| acl_rule.id | Body | String | ACL Rule ID |
| acl_rule.tenant_id | Body | String | 테넌트 ID |
| acl_rule.name | Query | String | ACL Rule 이름 |
| acl_rule.description | Query | String | ACL Rule 설명 |
| acl_rule.revision_number | Query | String | ACL Rule 개정 번호 |
| acl_rule.create_at | Query | String | ACL Rule 생성시간 |
| acl_rule.update_at | Query | String | ACL Rule 갱신시간 |
| acl_rule.acl_id | Body | String | ACL ID |
| acl_rule.remote_group_id | Body | String | 원격 그룹 id (미사용) |
| acl_rule.protocol | Body | String | protocol (tcp,udp,icmp) |
| acl_rule.ethertype | Body | String | IPv4로 고정 |
| acl_rule.src_port_range_min | Body | String | src 포트 범위의 최소값 |
| acl_rule.src_port_range_max | Body | String | src 포트 범위의 최대값 |
| acl_rule.src_ip | Body | String | src ip |
| acl_rule.dst_ip | Body | String | dst ip |
| acl_rule.dst_port_range_max | Body | String | dst 포트 범위의 최소값 |
| acl_rule.dst_port_range_min | Body | String | dst 포트 범위의 최대값 |
| acl_rule.policy | Body | String | allow or deny  |
| acl_rule.order | Body | Integer | ACL Rule 적용순서, 숫자가 작을수록 먼저 적용됨. (102 ~32764 사용)|


<details><summary>예시</summary>
<p>

```json
{
  "acl_rule": 
    {"remote_group_id":null,"protocol":null,"description":"default deny rule","ethertype":"IPv4","created_at":"2022-12-16T06:58:54Z","src_port_range_max":null,"updated_at":"2022-12-16T06:58:54Z","id":"005a5644-4e43-47fc-b3d9-6c1befe12f7b","src_ip":"0.0.0.0/0","dst_port_range_min":null,"dst_port_range_max":null,"revision_number":0,"tenant_id":"43b53d88b7a54d3aa5472bd800f1cbce","policy":"deny","dst_ip":"0.0.0.0/0","project_id":"43b53d88b7a54d3aa5472bd800f1cbce","order":32765,"acl_id":"5efaec75-8f07-4f5f-83b1-8b4c11c07e0b","src_port_range_min":null}
}
```
</p>
</details>

## ACL 바인딩 목록 보기

```
GET /v2.0/acl_bindings/
X-Auth-Token: {tokenId}
```

### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| sort_dir | Query | Enum | - | 조회할 ACL 바인딩의 정렬 방향<br>`sort_key`에서 지정한 필드를 기준으로 정렬<br>**asc**, **desc** 중 하나 |
| sort_key | Query | String | - | 조회할 ACL 바인딩의 정렬 키<br>`sort_dir`에서 지정한 방향대로 정렬 |
| fields | Query | String | - | 조회할 ACL 바인딩의 필드 이름<br>예) `fields=id&fields=name` |

### 응답

| 이름 | 종류 | 형식 |  설명 |
|---|---|---|---|
| acl_bindings | Body | Array | ACL 바인딩 목록 객체 |
| acl_bindings.id | Body | String | ACL 바인딩 ID |
| acl_bindings.tenant_id | Body | String | 테넌트 ID |
| acl_bindings.acl_id | Query | String | Network와 바인딩되는 ACL ID |
| acl_bindings.network_id | Query | String | ACL과 바인딩되는 Network ID |


<details><summary>예시</summary>
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

## ACL 바인딩 보기

```
GET /v2.0/acl_bindings/{aclBindingId}
X-Auth-Token: {tokenId}
```

### 요청

이 API는 요청 본문을 요구하지 않습니다.

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| aclBindingId | Query | UUID | O | 조회할 ACL 바인딩 ID |
| fields | Query | String | - | 조회할 ACL 바인딩의 필드 이름<br>예) `fields=id&fields=name` |

### 응답

| 이름 | 종류 | 형식 |  설명 |
|---|---|---|---|
| acl_binding | Body | Array | ACL 바인딩 목록 객체 |
| acl_binding.id | Body | String | ACL 바인딩 ID |
| acl_binding.tenant_id | Body | String | 테넌트 ID |
| acl_binding.acl_id | Query | String | Network와 바인딩되는 ACL ID |
| acl_binding.network_id | Query | String | ACL과 바인딩되는 Network ID |


<details><summary>예시</summary>
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
 
## ACL 바인딩 생성

### 요청

| 이름 | 종류 | 형식 |  필수 |설명 |
|---|---|---|---|---|
| tokenId | Header | String | O | 토큰 ID |
| tenant_id | Body | String | O | 테넌트 ID |
| network_id | Query | String | O | Network ID |
| acl_id | Body | String | O |ACL ID |

<details><summary>예시</summary>
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


### 응답

| 이름 | 종류 | 형식 |  설명 |
|---|---|---|---|
| acl_binding | Body | Array | ACL 바인딩 목록 객체 |
| acl_binding.id | Body | String | ACL 바인딩 ID |
| acl_binding.tenant_id | Body | String | 테넌트 ID |
| acl_binding.acl_id | Query | String | Network와 바인딩되는 ACL ID |
| acl_binding.network_id | Query | String | ACL과 바인딩되는 Network ID |

<details><summary>예시</summary>
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

## ACL 바인딩 삭제

```
DELETE /v2.0/acl_bindings/{aclBindingId}
X-Auth-Token: {tokenId}
```


### 요청

| 이름 | 종류 | 형식 | 필수 | 설명 |
|---|---|---|---|---|
| aclBindingId | Query | UUID | O | 삭제할 ACL 바인딩 ID |
| tokenId | Header | String | O | 토큰 ID |

### 응답

이 API는 응답 본문을 반환하지 않습니다.

---