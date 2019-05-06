A widget is a bundle consisting of two objects: a definition and a React component. The bundle is typically exported from a file:

const definition = ...;
class TheComponent extends React.Component ...
export default { definition, component: TheComponent };

The definition is a declarative object describing the basic characteristics of a widget, and the inputs that it receives. In the component for the widget, the inputs are made available through a prop named input.

Formal definitions are given below, but we'll start with an example demonstrating the basic idea. Note how the device is set in a single input, which publishes it to a variable that's available to the other inputs.

const definition = {
  type: "MOTOR_CONTROL",
  name: "Motor Control",
  defaultWidth: 10,
  defaultHeight: 20,
  inputs: {
    device: {
      type: "device",
      publish: "$device",
    },
    position: {
      type: "attribute",
      device: "$device",
      attribute: "Position"
    },

    turnRight: {
      type: "command",
      device: "$device",
      command: "TurnRight"
    },

    turnLeft: {
      type: "command",
      device: "$device",
      command: "TurnLeft"
    }
  }
}

The render method of the component implementation may look something like this:

render() {
  const {
    position,
    turnRight,
    turnLeft
  } = this.props.inputs;

  return (
    <div>
      Position: {position.value}
      <button onClick={turnLeft}>Left</button>
      <button onClick={turnRight}>Right</button>
    </div>
  );
}

.. _h4a495e5d56475571221615a3f7c454d:


Widget Definition
=================

+-------------+------------+-----------------------------------------------------------------------------------------------+
|\ |STYLE0|\  |\ |STYLE1|\ |\ |STYLE2|\                                                                                    |
+-------------+------------+-----------------------------------------------------------------------------------------------+
|type         |string      |Type identifier for the widget. Must be unique (e.g. "ATTRIBUTE_PLOT".)                        |
+-------------+------------+-----------------------------------------------------------------------------------------------+
|name         |string      |The name of the widget shown to the user (e.g. "Attribute Plot".)                              |
+-------------+------------+-----------------------------------------------------------------------------------------------+
|defaultWidth |number      |Default width (in number of tiles)                                                             |
+-------------+------------+-----------------------------------------------------------------------------------------------+
|defaultHeight|number      |Default height (in number of tiles)                                                            |
+-------------+------------+-----------------------------------------------------------------------------------------------+
|inputs       |            |An object where the keys are input names and the values are any of the input definitions below.|
+-------------+------------+-----------------------------------------------------------------------------------------------+

.. _h5847556c74124dba303c6b5218556f:

Input Definitions
=================

A question mark (e.g. label?) denotes an optional field.

.. _h7b65175692859261a7f571b7c4f5069:

Base Input Definition
---------------------

All input definitions derive from a base definition, which means that the below fields are available in all input types.

+------------+------------+-------------------------------------------------------------------------------------------------------------------------------+
|\ |STYLE3|\ |\ |STYLE4|\ |\ |STYLE5|\                                                                                                                    |
+------------+------------+-------------------------------------------------------------------------------------------------------------------------------+
|type        |string      |The type of input. Can assume the following values: boolean, number, string, complex, select, attribute, color, device, command|
+------------+------------+-------------------------------------------------------------------------------------------------------------------------------+
|label?      |string      |Label shown to the user in the widget inspector. If it's an empty string, no label is shown.                                   |
+------------+------------+-------------------------------------------------------------------------------------------------------------------------------+
|default?    |-           |Default value of the input. The type depends on the type of input.                                                             |
+------------+------------+-------------------------------------------------------------------------------------------------------------------------------+
|required?   |boolean     |Whether the input is required for the widget to be valid or not. A dashboard cannot start with invalid widgets.                |
+------------+------------+-------------------------------------------------------------------------------------------------------------------------------+

The following input types have no fields in addition to the above:

* "boolean". Manifests itself as a checkbox.

* "string". Manifests itself as a string input field.

* "color". Manifests itself as a color picker.

.. _h2c1d74277104e41780968148427e:



.. _h457f233a4934e164c305644644aa3e:

Number Input Definition
-----------------------

Manifests itself as an input field where the user can enter a numeric value.


+------------+------------+----------------------------------------------+
|\ |STYLE6|\ |\ |STYLE7|\ |\ |STYLE8|\                                   |
+------------+------------+----------------------------------------------+
|nonNumeric? |boolean     |If true, the user can't enter negative values.|
+------------+------------+----------------------------------------------+

.. _h2c1d74277104e41780968148427e:



.. _h6c14a182b6579a6e3425d5043456d:

Select Input Definition
-----------------------

Manifests itself as a drop-down select with a predefined set of options.

+------------+-------------------------------------+---------------------------------------------------------------------------------+
|\ |STYLE9|\ |\ |STYLE10|\                         |\ |STYLE11|\                                                                     |
+------------+-------------------------------------+---------------------------------------------------------------------------------+
|options     |Array of { name: string, value: any }|The available options, where name is the value shown to the user for each option.|
+------------+-------------------------------------+---------------------------------------------------------------------------------+

.. _h2c1d74277104e41780968148427e:



.. _h5b757d5450236f1c2d127974716d21:

Complex Input Definition
------------------------

An input that consists of muliple other inputs.

+-------------+-------------+-------------------------------------------------------------------------------------------------------------------+
|\ |STYLE12|\ |\ |STYLE13|\ |\ |STYLE14|\                                                                                                       |
+-------------+-------------+-------------------------------------------------------------------------------------------------------------------+
|inputs       |-            |Input mapping with the same structure as the top-level widget definition one.                                      |
+-------------+-------------+-------------------------------------------------------------------------------------------------------------------+
|repeat       |boolean      |If true, the complex input becomes an array of complex inputs. The user can add any number of inputs to this array.|
+-------------+-------------+-------------------------------------------------------------------------------------------------------------------+

.. _h2c1d74277104e41780968148427e:



.. _h1968701e591b45416c4b217a5e6e79:

Device Input Definition
-----------------------

Manifests itself as an input where the user can select any of the devices in the database.

+-------------+-------------+--------------------------------------------------------------------------------------------------+
|\ |STYLE15|\ |\ |STYLE16|\ |\ |STYLE17|\                                                                                      |
+-------------+-------------+--------------------------------------------------------------------------------------------------+
|publish      |string       |If true, the device name is made available to other inputs as a variable (see example at the top.)|
+-------------+-------------+--------------------------------------------------------------------------------------------------+

In the component, the input is an object with the following structure:

+-------------+-------------+---------------------------------+
|\ |STYLE18|\ |\ |STYLE19|\ |\ |STYLE20|\                     |
+-------------+-------------+---------------------------------+
|name         |string       |The device name                  |
+-------------+-------------+---------------------------------+
|alias        |string       |The device alias, or null if none|
+-------------+-------------+---------------------------------+

.. _h2c1d74277104e41780968148427e:




.. _h376c32662433e1241334276c543c52:

Attribute Input Definition
--------------------------

An input representing a device attribute. Unless bound to a certain attribute, it manifests itself as an input where the user can select a device attribute.

+-------------+-------------+---------------------------------------------------------------------------------------------------------------+
|\ |STYLE21|\ |\ |STYLE22|\ |\ |STYLE23|\                                                                                                   |
+-------------+-------------+---------------------------------------------------------------------------------------------------------------+
|dataFormat?  |string       |Restricts the attributes shown to the users by data format. Permitted values: "scalar" or "spectrum" or "image"|
+-------------+-------------+---------------------------------------------------------------------------------------------------------------+
|dataType?    |string       |If "numeric", only numeric attributes are shown.                                                               |
+-------------+-------------+---------------------------------------------------------------------------------------------------------------+
|device?      |string       |If set, the input is bound to this device.                                                                     |
+-------------+-------------+---------------------------------------------------------------------------------------------------------------+
|attribute?   |string       |If set, the input is bound to this attribute.                                                                  |
+-------------+-------------+---------------------------------------------------------------------------------------------------------------+

In the component, the input is an object with the following structure:

+-------------+-------------+--------------------------------------------------------------------------+
|\ |STYLE24|\ |\ |STYLE25|\ |\ |STYLE26|\                                                              |
+-------------+-------------+--------------------------------------------------------------------------+
|device       |string       |The device name                                                           |
+-------------+-------------+--------------------------------------------------------------------------+
|attribute    |string       |The attribute name                                                        |
+-------------+-------------+--------------------------------------------------------------------------+
|value        |             |The current value of the attribute                                        |
+-------------+-------------+--------------------------------------------------------------------------+
|write        |function     |A function which writes a value to the attribute when executed. Signature:|
|             |             |                                                                          |
|             |             |(value: any) => Promise<boolean>                                          |
+-------------+-------------+--------------------------------------------------------------------------+

.. _h67292c83572512d6a495d714246b21:

Command Input Definition
------------------------

An input representing a device command. Unless bound to a certain command, it manifests itself as an input where the user can select a device command.

+-------------+-------------+-------------------------------------------------------------+
|\ |STYLE27|\ |\ |STYLE28|\ |\ |STYLE29|\                                                 |
+-------------+-------------+-------------------------------------------------------------+
|device?      |string       |If set, the input is bound to this device.                   |
+-------------+-------------+-------------------------------------------------------------+
|command?     |string       |If set, the input is bound to this command.                  |
+-------------+-------------+-------------------------------------------------------------+
|intype?      |string       |If set, only commands with this intype are shown to the user.|
+-------------+-------------+-------------------------------------------------------------+

In the component, the input is an object with the following structure:


+-------------+-------------+--------------------------------------------------------------------------------------------------------+
|\ |STYLE30|\ |\ |STYLE31|\ |\ |STYLE32|\                                                                                            |
+-------------+-------------+--------------------------------------------------------------------------------------------------------+
|device       |string       |The device name                                                                                         |
+-------------+-------------+--------------------------------------------------------------------------------------------------------+
|command      |string       |The command name                                                                                        |
+-------------+-------------+--------------------------------------------------------------------------------------------------------+
|execute      |function     |A function which executes the command when executed. Currently doesn't take input parameters. Signature:|
|             |             |                                                                                                        |
|             |             |() => Promise<any>                                                                                      |
+-------------+-------------+--------------------------------------------------------------------------------------------------------+


.. bottom of content


.. |STYLE0| replace:: **Key**

.. |STYLE1| replace:: **Type**

.. |STYLE2| replace:: **Description**

.. |STYLE3| replace:: **Key**

.. |STYLE4| replace:: **Type**

.. |STYLE5| replace:: **Description**

.. |STYLE6| replace:: **Key**

.. |STYLE7| replace:: **Type**

.. |STYLE8| replace:: **Description**

.. |STYLE9| replace:: **Key**

.. |STYLE10| replace:: **Type**

.. |STYLE11| replace:: **Description**

.. |STYLE12| replace:: **Key**

.. |STYLE13| replace:: **Type**

.. |STYLE14| replace:: **Description**

.. |STYLE15| replace:: **Key**

.. |STYLE16| replace:: **Type**

.. |STYLE17| replace:: **Description**

.. |STYLE18| replace:: **Key**

.. |STYLE19| replace:: **Type**

.. |STYLE20| replace:: **Description**

.. |STYLE21| replace:: **Key**

.. |STYLE22| replace:: **Type**

.. |STYLE23| replace:: **Description**

.. |STYLE24| replace:: **Key**

.. |STYLE25| replace:: **Type**

.. |STYLE26| replace:: **Description**

.. |STYLE27| replace:: **Key**

.. |STYLE28| replace:: **Type**

.. |STYLE29| replace:: **Description**

.. |STYLE30| replace:: **Key**

.. |STYLE31| replace:: **Type**

.. |STYLE32| replace:: **Description**
