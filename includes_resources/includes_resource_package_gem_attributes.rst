.. The contents of this file may be included in multiple topics (using the includes directive).
.. The contents of this file should be modified in a way that preserves its ability to appear in multiple topics.

This resource has the following properties:
   
``clear_sources``
   **Ruby Types:** TrueClass, FalseClass

   |clear_sources| Default value: ``false``.
   
``gem_binary``
   **Ruby Type:** String

   |gem_binary resource package| By default, the same version of |ruby| that is used by the |chef client| will be installed.
   
``ignore_failure``
   **Ruby Types:** TrueClass, FalseClass

   |ignore_failure| Default value: ``false``.
   
``notifies``
   **Ruby Type:** Symbol, 'Chef::Resource[String]'

   |notifies|

   .. include:: ../../includes_resources_common/includes_resources_common_notifications_syntax_notifies.rst

   .. include:: ../../includes_resources_common/includes_resources_common_notifications_timers.rst
   
``options``
   **Ruby Type:** String

   |command options|
   
``package_name``
   **Ruby Types:** String, Array

   |name package| |resource_block_default| |see syntax|
   
``provider``
   **Ruby Type:** Chef Class

   Optional. |provider resource_parameter| |see providers|
   
``retries``
   **Ruby Type:** Integer

   |retries| Default value: ``0``.
   
``retry_delay``
   **Ruby Type:** Integer

   |retry_delay| Default value: ``2``.
   
``source``
   **Ruby Type:** String

   Optional. The URL at which the gem package is located.
   
``subscribes``
   **Ruby Type:** Symbol, 'Chef::Resource[String]'

   |subscribes|

   .. include:: ../../includes_resources_common/includes_resources_common_notifications_syntax_subscribes.rst

   |subscribes timers|
   
``timeout``
   **Ruby Types:** String, Integer

   |timeout|
   
``version``
   **Ruby Types:** String, Array

   |version package|
