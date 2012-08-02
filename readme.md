Discovery Library
=================

Search
------

You can use the #search method to locate a role, optionally
restricted to the environment.

It will fall back to searching the local nodes run_list for roles, so
you can have less logic flow in recipes.

``` ruby
host = Discovery.search("any_role",
                        :node => node,
                        :environment_aware => false)
```

Available options include:

* environment_aware (true or false). Default is false.
* empty_ok (true or false). Default is false.
* remove_self (true or false). Default is true.
* minimum_response_time (true or false). Default is false.

All
---

You can use the #all method to locate all nodes with a role,
optionally restricted to the environment.

Additional options:

``` ruby
hosts = Discovery.all("base",
                      :node => node,
                      :environment_aware => true,
                      :empty_ok => false,
                      :remove_self => true,
                      :minimum_response_time => false
```

ipaddress
---------

You can use the #ipaddress method to automatically grab a prioritised
ipaddress from a node.

The remote node will be compared against the same node, if any are in
any clouds detected by ohai (and they are in the same cloud) the local
ipv4 will be returned.

You can optionally supply a type argument specifying which ipaddress
you would like.

The value of 'host' is returned via the search method.

The :remote_node attribute should contain the node object of the remote node
(search response). The :node attribute should contain the local node object
which is used to compare the remote node to the local node in order to test
if they are in the same cloud, zone, etc.

If you use Discovery.search or all to pass the remote_node, you can omit the
:node attribute as it will already be injected into the DSL.

``` ruby
ipaddress = Discovery.ipaddress(:remote_node => host,
                                :node => node)
```

``` ruby
local_ipv4 = Discovery.ipaddress(:remote_node => host,
                                 :node => node,
                                 :type => :local)
```                                 

``` ruby
public_ipv4 = Discovery.ipaddress(:remote_node => host,
                                 :node => node,
                                 :type => :public)
```
