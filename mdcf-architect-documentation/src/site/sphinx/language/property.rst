.. include:: ../util/substitution.rst
.. default-domain:: aadl
.. _aadl-properties-data:

#############################
*Properties* and *Data* Types
#############################

Two AADL elements -- *properties* and *data* are used throughout the app.

**********
Properties
**********

The MDCF Architect uses a number of properties to configure the real-time (RT) and Quality of Service (QoS) and a small number of other settings.  Most of these properties can be set either as app-wide defaults using the ``default name`` and all can be specified on a per-element basis using the ``override name`` (which will override the default value, if present).

Thread Properties
=================

.. property:: period 

	|prop period|
	
   :default: Default_Thread_Period
   :override: Timing_Properties::Period
   :type: Time
   :context: :construct:`thread`
   :example: ``50 ms``

.. property:: deadline

	|prop deadline|
	
   :default name: Default_Thread_Deadline
   :override: Timing_Properties::Deadline
   :type: Time
   :context: :construct:`thread`
   :example: ``50 ms``
   
.. property:: wcet

	|prop wcet|
	
   :default name: Default_Thread_WCET
   :override: MAP_Properties::Worst_Case_Execution_Time
   :type: Time
   :context: :construct:`thread`
   :example: ``5 ms``  

.. property:: dispatch

	|prop dispatch|
	
   :default name: Default_Thread_Dispatch
   :override: Thread_Properties::Dispatch_Protocol
   :type: ``sporadic`` or ``periodic``
   :context: :construct:`thread`
   :example: ``periodic``


Port Properties
===============

.. property:: output-rate

	|prop output-rate| Note that this is ignored on :construct:`thread` ports  and incoming :construct:`process implementation<processimplementation>` ports.
	
   :default name: Default_Output_Rate
   :override: MAP_Properties::Output_Rate
   :type: Time range
   :context: :construct:`port`
   :example: ``100 ms .. 300 ms``
   
.. property:: exchange-name

	|prop exchange-name| Note that this is ignored on all non-:construct:`device` ports. This property is essentially a tag created by the code generator that produces the device interface to the binding algorithm that operates on the generated Java code. It is not intended to be user-modifiable.
	
   :default name: N/A
   :override: MAP_Properties::Exchange_Name
   :type: AADLString
   :context: :construct:`port`
   :example: ``"spo2_per"``

Port Connection Properties
==========================

.. property:: channel-delay

	|prop channel-delay| Note that this is ignored on port connections which are attached to :construct:`process implementations<processimplementation>`.
	
   :default name: Default_Channel_Delay
   :override: MAP_Properties::Channel_Delay
   :type: Time
   :context: :construct:`port connection<portconnection>`
   :example: ``100 ms``

Process Properties
==================

.. property:: process-type

	|prop process-type|
	
   :default name: N/A
   :override: MAP_Properties::Process_Type
   :type: Either ``logic`` or ``display``
   :context: :construct:`process`
   :example: ``display``
   
Device Properties
==================

.. property:: component-type

	|prop component-type|
	
   :default name: N/A
   :override: MAP_Properties::Component_Type
   :type: one of ``sensor``, ``controller``, ``actuator``, or ``controlled process``
   :context: Any subcomponent of a :construct:`system`: ie, a :construct:`device`, :construct:`process`, or :construct:`abstract`
   :example: ``controller``

Data Properties
==================

Data Subcomponent Properties
----------------------------

.. property:: process-variable

   This variable is used to mark :construct:`data` subcomponents as "process variables," ie part of a component's "process model" (see |SAFE| or |STPA| documentation for a full explanation of this concept). It's optional, and assumed to be false if not present.
	
   :default name: N / A
   :override: MAP_Error_Properties::Process_Variable
   :type: AADLBoolean
   :context: :construct:`data` subcomponent
   :example: ``true``

Data Declaration Properties
---------------------------

.. property:: data-representation

	|prop data-representation|
	
   :default name: N/A
   :override: Data_Model::Data_Representation
   :type: ``Boolean``, ``Integer``, or ``Float``
   :context: :construct:`data`
   :example: ``Integer``

.. note::
	Declaring a data representation of ``Float`` will translate to a ``Double``, as they are "generally the default choice" for decimal values (`source <https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html>`_)
	
.. property:: measurement-unit

   |prop measurement-unit|
	
   :default name: N/A
   :override: Data_Model::Measurement_Unit
   :type: AADLString
   :context: :construct:`data`
   :example: ``"Percent"``

.. property:: real-range

   This is an optional property that lets you specify the range for a data type that has a :property:`data-representation` of ``Float``.
	
   :default name: N/A
   :override: Data_Model::Real_Range
   :type: Range of AADLReal
   :context: :construct:`data`
   :example: ``0.0 .. 100.0``
   
.. property:: integer-range

   This is an optional property that lets you specify the range for a data type that has a :property:`data-representation` of ``Integer``.
	
   :default name: N/A
   :override: Data_Model::Integer_Range
   :type: Range of AADLInteger
   :context: :construct:`data`
   :example: ``0 .. 100``


Example Property Set
====================

.. literalinclude:: snippets/default_properties.aadl
   :language: aadl
   :linenos:
   
**********
Data Types
**********

The MDCF Architect enables developers to name data types and set their data representation.

.. construct:: data

	:property Data_Representation: |prop data-representation|
	:property Real_Range: This is an optional property that lets you specify the range for a data type that has a :property:`data-representation` of ``Float``.
	:property Integer_Range: This is an optional property that lets you specify the range for a data type that has a :property:`data-representation` of ``Integer``.
	:property Measurement_Unit: |prop measurement-unit|
	:type Data_Representation: :property:`Data_Model::Data_Representation<data-representation>`
	:type Real_Range: :property:`Data_Model::Real_Range<real-range>`
	:type Integer_Range: :property:`Data_Model::Integer_Range<integer-range>`
	:type Measurement_Unit: :property:`Data_Model::Measurement_Unit<measurement-unit>`

	
Example Data Type
=================

.. literalinclude:: snippets/data_type.aadl
   :language: aadl
   :linenos:
