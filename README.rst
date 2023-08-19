
Installation
============
Installing from PyPI is as easy as doing:

.. code-block:: bash

  pip install django-storages

If you'd prefer to install from source (maybe there is a bugfix in master that
hasn't been released yet) then the magic incantation you are looking for is:

.. code-block:: bash

  pip install -e 'git+https://github.com/jschneier/django-storages.git#egg=django-storages'

Once that is done, if using Django 4.1 or earlier, set ``DEFAULT_FILE_STORAGE`` to the backend of your choice.
If, for example, you want to use the boto3 backend you would set:

.. code-block:: python

  DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'

For Django 4.2 or later, set the ``default`` value in ``STORAGES`` to the backend of your choice. For example:

.. code-block:: python

  STORAGES = {
      'default': {
          'BACKEND': 'storages.backends.s3boto3.S3Boto3Storage',
      },
      'staticfiles': {
          # Leave whatever setting you already have here, e.g.:
          'BACKEND': 'django.contrib.staticfiles.storage.StaticFilesStorage',
      }
  }


If you are using the ``FileSystemStorage`` as your storage management class in your models ``FileField`` fields, remove them
and don't specify any storage parameter. That way, the ``DEFAULT_FILE_STORAGE`` class will be used by default in your field.
For example, if you have a `photo` field defined as:

.. code-block:: python

    photo = models.FileField(
        storage=FileSystemStorage(location=settings.MEDIA_ROOT),
        upload_to='photos',
    )

Set it to just:

.. code-block:: python

    photo = models.FileField(
        upload_to='photos',
    )

There are also a number of settings available to control how each storage backend functions,
please consult the documentation for a comprehensive list.

About
=====
django-storages is a project to provide a variety of storage backends in a single library.

This library is usually compatible with the currently supported versions of
Django. Check the Trove classifiers in setup.py to be sure.

django-storages is backed in part by `Tidelift`_. Check them out for all of your enterprise open source
software commercial support needs.

.. _Tidelift: https://tidelift.com/subscription/pkg/pypi-django-storages?utm_source=pypi-django-storages&utm_medium=referral&utm_campaign=enterprise&utm_term=repo
