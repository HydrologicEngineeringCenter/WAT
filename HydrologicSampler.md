The Hydrologic Sampler is a plugin that implements the Hydrologic Event Generator interface in the plugin architecture of HEC-WAT.

This means that it is responsible for defining the events that occur in the Flood Risk Compute option. Generally, within HEC-WAT the
event list is one event per year so that we can support annual maximum frequency curves as a primary output. However, there are special cases
where other modeling choices might be appropriate. 

Some users wish to have a continuous simulation within HEC-WAT. In order to allow for this the Hydrologic Sampler (bundled with HEC-WAT 1.1)
has a configurable setting to create a singular time window for the FRA compute for each lifecycle. It also puts the entire flow record into a
single collection member in the lifecycle.dss file.

In order to make this happen the user has to be using the "Bootstrapped Flows" capability in the Hydrologic Sampler and have the events defined
as spanning 365 days.

Close HEC-WAT if it is open and modify the HEC-WAT config file to have the following -d flag:
-DContinuousSimulation=true
