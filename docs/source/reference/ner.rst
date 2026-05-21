NER Module — Unstructured Text Anonymization
=============================================

MaskMe's NER module detects and replaces personally identifiable information in
**free-form text** using Named Entity Recognition via spaCy. It operates independently
from the structured-data engine and is invoked through the ``maskme ner`` CLI subcommand
or the ``maskme.ner`` Python API.

Installation
------------

.. code-block:: bash

   pip install maskme[ner]
   python -m spacy download en_core_web_lg
   python -m spacy download fr_core_news_lg

Supported languages: ``fr`` (French) and ``en`` (English). Install only the models
you need.

API Reference
-------------

.. automodule:: maskme.ner
   :members:
   :undoc-members:
   :show-inheritance:

CLI Usage
---------

.. code-block:: text

   maskme ner [OPTIONS] [INPUT]

**Arguments:**

- ``INPUT`` — Path to a text file. If omitted, reads from stdin.

**Options:**

.. list-table::
   :header-rows: 1

   * - Option
     - Description
   * - ``-o, --output PATH``
     - Output file path (default: stdout)
   * - ``-l, --language TEXT``
     - Language override (``fr`` or ``en``); auto-detected if omitted
   * - ``--lines``
     - Treat each line as a separate text (batch mode)
   * - ``--verbose``
     - Enable debug logging

Entity Labels
-------------

The following entity types are detected and replaced with bracketed tags:

.. list-table::
   :header-rows: 1

   * - Label
     - Tag
     - Description
   * - ``PERSON``
     - ``[PERSON]``
     - People names
   * - ``LOCATION``
     - ``[LOCATION]``
     - Cities, countries, addresses
   * - ``ORGANISATION``
     - ``[ORGANISATION]``
     - Companies, hospitals, organizations
   * - ``DATE``
     - ``[DATE]``
     - Absolute or relative dates
   * - ``TIME``
     - ``[TIME]``
     - Times of day

Graceful Degradation
--------------------

If spaCy is not installed, the module logs a warning and returns the original text
unchanged. This allows code using the NER module to run without the optional
dependency in environments where text anonymization is not required.
