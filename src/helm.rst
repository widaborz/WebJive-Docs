Helm 
====
Helm is a tool for managing Kubernetes charts. Charts are packages of pre-configured Kubernetes resources.

The chart for this integration is composed by:

.. code-block:: console

   Chart.yaml          # A YAML file containing information about the chart
   values.yaml         # The default configuration values for this chart
   chart/              # A directory containing any charts upon which this chart depends.
   chart/templates/    # A directory of templates that, when combined with values,
                       # will generate valid Kubernetes manifest files.

.. code-block:: console

   # Chart.yaml
   apiVersion: v1
   appVersion: "1.0"
   description: A Helm chart for deploying the SKA Integration TMC-WEBUI on Kubernetes
   name: integration-tmc-webui
   version: 0.1.0

.. code-block:: console

   # example of values
   tmcprototype:
    enabled: true
    image:
       registry: nexus.engageska-portugal.pt/tango-example
       image: tmcprototype
       tag: latest
       pullPolicy: Always

More information available `here <https://helm.sh/docs/>`_. 
Helm Glossare here <https://helm.sh/docs/glossary/>`_. 