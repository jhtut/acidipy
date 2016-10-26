# acidipy
Cisco ACI Python API

**ACI** **D**eveloping **I**nterface for **PY**thon

![Relations](./doc/object_relation.png)

## Grammar

### Objects

- Domain
- Tenant
- AppProf
- EndPointGroup
- BridgeDomain
- Subnet

### Methods

!) *Exclude* **Domain** *Object*

#### Class Method
- getList : Retrive Object List

#### Instance Method
- getDetail : Get all attributes on object retrived
- getRefresh : Get lastest attributes
- getParent : Get parent object
- getChildren : Get children objects
- create : Create object to APIC
- update : Update object to APIC
- delete : Delete object from APIC
- relate : Relate between objects
- << : c : as like create
- & : as like relate

## Usages

### Import Source

	from apicipy import *

### Get Domain Session

> **DOMAIN_INSTANCE** = **Domain**(**APIC_IP**, **USER**, **PASSWORD** [,debug(default:False)=True|False])

	domain_instance = Domain('123.123.123.123', 'cisco', 'cisco123')

### Basic C.R.U.D

#### Read Objects

Retrive name-only

> **OBJECT_INSTANCES** = **OBJECT**.getList(dom)

	tenant_instances = Tenant.getList(dom)

Retrive with details

> **OBJECT_INSTANCES** = **OBJECT**.getList(dom, detail=True)

	tenant_instances = Tenant.getList(dom, detail=True)

Retrive details on a instance already read

> **OBJECT_INSTANCE**.getDetail()

	tenant_instance.getDetail()

#### Create Object

Create Object Instance on Local

> **OBJECT_INSTANCE** = **OBJECT**(**PARAMETERS**)

	tenant_instance = Tenant(name='test_tenant')

Register Object to APIC with Object Instance's method create()

> **OBJECT_INSTANCE**.**create**(**PARENT_INSTANCE**)

	tenant_instance.create(domain_instance)
	
Or with "<<" Operator

> **PARENT_INSTANCE** **<<** **OBJECT_INSTANCE**

	domain_instance << tenant_instance

#### Update Object

Set Data to Object Instance

> **OBJECT_INSTANCE**["**OBJECT_ATTRIBUTE**"] = **DATA**

	epg_instance['scope'] = bd_instance['scope']

Update with Object Instance's method update()

> **OBJECT_INSTANCE**.**update**()
	
	epg_instance.update()

##### Relationship

Relate with Object Instance's method relate()

> **BIGGER_RELATION_INSTANCE**.**relate**(**SMALLER_RELATION_INSTANCE**)

	# as like BD(1) : EPG(N)
	epg_instance.relate(bd_instance)

Or with "&" Operator

> **RELATION_INSTANCE_1** **&** **RELATION_INSTANCE_2**

> **RELATION_INSTANCE_2** **&** **RELATION_INSTANCE_1**

	epg_instance & bd_instance
	bd_instance & epg_instance

#### Delete Object

Delete with Object Instance's method delete()

> **OBJECT_INSTANCE**.delete()

	tenant.delete()












