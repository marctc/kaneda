.. _queues:

Queues
======

Kaneda provides builtin queues to store metrics and events to perform :ref:`asynchronous reporting <async>`. If you want to use your
custom asynchronous queue system you need to subclass :code:`BaseQueue` and implement your custom :code:`report` method
which is the responsible to pass metrics data to a job queue.

.. _celery:

Celery
~~~~~~

Celery is a simple, flexible and reliable distributed system to process vast amounts of messages. It can be configured
using various broker systems such Redis or RabbitMQ.

.. note::

    Before using Celery as async queue you need to install Celery library::

        pip install celery


.. autoclass:: kaneda.queues.CeleryQueue
    :members:

To run the worker execute this command::

     celery -A kaneda.tasks.celery worker

.. _rq:

RQ
~~

RQ (Redis Queue) is a simple Python library for queueing jobs and processing them in the background with workers. It uses
Redis as main broker system.

.. note::

    Before using RQ as async queue you need to install RQ and Redis library::

        pip install redis
        pip install rq

To run the worker execute this command::

        rqworker [queue]

The default queue is "kaneda".

.. autoclass:: kaneda.queues.RQQueue
    :members:

ZMQ
~~~

ZMQ (or ZeroMQ) is a library which extends the standard socket interfaces with features traditionally provided by
specialised messaging middleware products. ZeroMQ sockets provide an abstraction of asynchronous message queues and much
more.

.. note::

    Before using ZMQ as async queue you need to install ZMQ library::

        pip install pyzmq

To run the worker execute this command::

        zmqworker --connection_url=<zmq_connection_url>

or define :ref:`zmq_settings` settings in :file:`kanedasettings.py` and simply execute the worker command with::

        zmqworker

.. autoclass:: kaneda.queues.ZMQQueue
    :members: