.. . Kicking page rebuild 2014-10-30 17:00:08
.. include:: defs.hrst

.. index:: Contract
.. _Contract:

Contract
========

Schema
------

:id:
    uid, auto-generated

    |ocdsDescription|
    The identifier for this contract.

:awardID:
    string, required

    |ocdsDescription|
    The `Award.id` against which this contract is being issued.

:contractID:
    string, auto-generated, read-only

:contractNumber:
    string

:title:
    string, required

    |ocdsDescription|
    Contract title

:description:
    string

    |ocdsDescription|
    Contract description

:status:
    string, required

    |ocdsDescription|
    The current status of the contract.

    Possible values are:

    * `pending` - this contract has been proposed, but is not yet in force.
      It may be awaiting signature.
    * `active` - this contract has been signed by all the parties, and is
      now legally in force.
    * `cancelled` - this contract has been cancelled prior to being signed.

    Possible values for :ref:`contracting`:

    * `active` - this contract has been signed by all the parties, and is
      now legally in force.
    * `terminated` - this contract was signed and in force, and has now come
      to a close.  This may be due to a successful completion of the contract,
      or may be early termination due to some non-completion issue.

:period:
    :ref:`Period`

    |ocdsDescription|
    The start and end date for the contract.

:items:
    List of :ref:`Item` objects, auto-generated, read-only

    |ocdsDescription|
    The goods, services, and any intangible outcomes in this contract. Note: If the items are the same as the award do not repeat.

:suppliers:
    List of :ref:`Organization` objects, auto-generated, read-only

:value:
    `Value` object, auto-generated, read-only

    |ocdsDescription|
    The total value of this contract.

:dateSigned:
    string, :ref:`date`

    |ocdsDescription|
    The date when the contract was signed. In the case of multiple signatures, the date of the last signature.

    Differences in :ref:`defense`, :ref:`openua` and :ref:`openeu`:

    string, :ref:`date`, auto-generated

    Time frame for `dateSigned`in :ref:`defense`:

    * reporting procedure:
        [24 hours ago - now]

    * negotiation/negotiation.quick procedure:
        [complaint period end - now]

:documents:
    List of :ref:`Document` objects

    |ocdsDescription|
    All documents and attachments related to the contract, including any notices.


:date:
    string, :ref:`date`

    The date when the contract was changed or activated.

    This field is not in :ref:`contracting`

Additional fields for :ref:`contracting`:


:procuringEntity:
   :ref:`ProcuringEntity`

   |ocdsDescription|
   The entity managing the procurement, which may be different from the buyer who is paying / using the items being procured.


:changes:
    List of :ref:`Change` objects.

:amountPaid:

    :amount: float, required
    :currency: string, required, auto-generated
    :valueAddedTaxIncluded: bool, required , auto-generated

    Amount of money actually paid.

:terminationDetails:
    string, required for unsuccessful contract

    Reasons for contract termination. Presence of this field indicates that contract is unsuccessful.


Workflow in :ref:`contracting`
------------------------------

.. graphviz::

    digraph G {
        A [ label="active*" ]
        B [ label="terminated"]
         A -> B;
    }

\* marks initial state


Contract workflow in :ref:`limited`
-----------------------------------

.. graphviz::

    digraph G {
        A [ label="pending*" ]
        B [ label="active"]
        C [ label="cancelled"]
         A -> B;
         A -> C;
    }

\* marks initial state


Workflow in :ref:`openeu`
-------------------------

.. graphviz::

    digraph G {
        A [ label="pending*" ]
        B [ label="active"]
        C [ label="cancelled"]
         A -> B [ headlabel="Broker action"
                  labeldistance=3.7;
                  labelangle=75;
         ];
         A -> C [label="on Award cancellation"];
    }

\* marks initial state

