**Distributed Computing Configurations:**

There are many different configuration considerations when developing a distributed compute.
Managing Multiple Masters with separable compute node grids:
In order to have multiple masters compute on the same network each using a distinct mapping of compute nodes the following settings need to be changed in the default-config.xml file in the ignite directory packaged with WAT on the master node and each compute node. We recommend that the multi-cast options be utilized and that different port numbers be associated with each compute node grid and master pairing.
In order to multi cast multiple distributed computes on the same network you must use these settings in the default-config.xml file on the master and compute nodes:
```
<property name="deploymentMode" value="SHARED"/>
    <property name="discoverySpi">
        <bean class="org.apache.ignite.spi.discovery.tcp.TcpDiscoverySpi">
            <property name="ipFinder">
                <bean class="org.apache.ignite.spi.discovery.tcp.ipfinder.multicast.TcpDiscoveryMulticastIpFinder">
                    <!-- This page has more info about the config options:
                    https://ignite.apache.org/releases/1.5.0.final/javadoc/org/apache/ignite/spi/discovery/tcp/ipfinder/multicast/TcpDiscoveryMulticastIpFinder.html -->
                    <!-- 228.1.2.4 is the default group address, only have to specify if you want to use something different -->
                    <!-- <property name="multicastGroup" value="228.1.2.4"/>-->
                    <!-- 47400 is the default port, only have to specify if you want to use something different -->
                    <property name="multicastPort" value="47801"/>                          
                </bean>
            </property>
        </bean>
    </property>
```

Also the following -D flags will need to be uncommented and properly set (on master and compute nodes) Command to launch compute nodes would also change.

vmparam -DGridGainComputePlugin.configFile="C:\Programs\HEC-WAT\HEC-WAT\ignite\default-config.xml"

#for master node: comment out the following line if this is master node

#vmparam -Djava.rmi.server.hostname=127.0.0.1

#for master node: uncomment (or add) the following line if this is master node
vmparam -Dhec.rmi.server.NoClientSideProxies=true


Another alternative method is to use TcpDiscoverySpi – which allows for a static ip address for the master. In this configuration each compute node will broadcast back to a specified master ip address and port. This would be needed at Amazon to configure a different Discovery mechanism. 
```
  <property name="deploymentMode" value="SHARED"/>
  <property name="discoverySpi">
     <bean class="org.apache.ignite.spi.discovery.tcp.TcpDiscoverySpi">
          <property name="networkTimeout" value="1000000"/>
          <property name="maxMissedClientHeartbeats" value="16"/>
          <property name="maxMissedHeartbeats" value="16"/>
          <property name="ipFinder">
            <bean class="org.apache.ignite.spi.discovery.tcp.ipfinder.vm.TcpDiscoveryVmIpFinder">
              <property name="addresses">
                <list>
                  <!-- replace XXX.XX.XXX.XX:PPPPP with your actual IP:port.-->
                  <value>XXX.XX.XXX.XX:PPPPP</value>
                </list>
              </property>
            </bean>
          </property>
     </bean>
   </property>
   ```
