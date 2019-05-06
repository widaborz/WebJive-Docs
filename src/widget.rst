How to create a widget
===============

A widget is a bundle consisting of two objects: a definition and a React component. The bundle is typically exported from a file:


.. code-block:: console
    const definition = ...;
    class TheComponent extends React.Component ...

    export default { definition, component: TheComponent };

The definition is a declarative object describing the basic characteristics of a widget, and the inputs that it receives. In the component for the widget, the inputs are made available through a prop named `input`.

Formal definitions are given below, but we'll start with an example demonstrating the basic idea. Note how the device is set in a single input, which publishes it to a variable that's available to the other inputs.

.. code-block:: console
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
.. code-block:: console
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


Widget Definition
==


+-----------------+------------------------------------------------+
| Docker service  | Description                                    |
+=================+================================================+
| tangodb         | MariaDB database holding TANGO database tables |
+-----------------+------------------------------------------------+
| databaseds      | TANGO database device server                   |
+-----------------+------------------------------------------------+
| tangogql        | GraphQL interface to Tango control system      |
+-----------------+------------------------------------------------+
| redis           | Redis in-memory key/value database             |
+-----------------+------------------------------------------------+
| webjive         | WebJive container                              |
+-----------------+------------------------------------------------+
| auth            | WebJive authentication service                 |
+-----------------+------------------------------------------------+
| dashboards      | WebJive session persistence service            |
+-----------------+------------------------------------------------+
| mongodb         | Database for WebJive session persistence       |
+-----------------+------------------------------------------------+
| dishmaster      | TMC Dish LMC master Tango device               |
+-----------------+------------------------------------------------+
| dishleafnode    | TMC Dish leaf node Tango device                |
+-----------------+------------------------------------------------+
| subarraynode1   | TMC SubArrayNode Tango device #1               |
+-----------------+------------------------------------------------+
| subarraynode2   | TMC SubArrayNode Tango device #2               |
+-----------------+------------------------------------------------+
| centralnode     | TMC CentralNode Tango device                   |
+-----------------+------------------------------------------------+
| rsyslog-tmc     | rsyslog container for TMC devices              |
+-----------------+------------------------------------------------+
| tangotest       | TANGO test device                              |
+-----------------+------------------------------------------------+
| jive            | Jive - Tango GUI application                   |
+-----------------+------------------------------------------------+
| traefik         | Reverse proxy used for WebJive HTTP routing    |
+-----------------+------------------------------------------------+

