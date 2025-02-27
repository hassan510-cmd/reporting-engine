=======================
Base Comments Templates
=======================

.. 
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
   !! This file is generated by oca-gen-addon-readme !!
   !! changes will be overwritten.                   !!
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
   !! source digest: sha256:7b997157e82302b911ae2417ae973c558527388bcd3e40d34e446c42988d7e10
   !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

.. |badge1| image:: https://img.shields.io/badge/maturity-Beta-yellow.png
    :target: https://odoo-community.org/page/development-status
    :alt: Beta
.. |badge2| image:: https://img.shields.io/badge/licence-AGPL--3-blue.png
    :target: http://www.gnu.org/licenses/agpl-3.0-standalone.html
    :alt: License: AGPL-3
.. |badge3| image:: https://img.shields.io/badge/github-OCA%2Freporting--engine-lightgray.png?logo=github
    :target: https://github.com/OCA/reporting-engine/tree/16.0/base_comment_template
    :alt: OCA/reporting-engine
.. |badge4| image:: https://img.shields.io/badge/weblate-Translate%20me-F47D42.png
    :target: https://translation.odoo-community.org/projects/reporting-engine-16-0/reporting-engine-16-0-base_comment_template
    :alt: Translate me on Weblate
.. |badge5| image:: https://img.shields.io/badge/runboat-Try%20me-875A7B.png
    :target: https://runboat.odoo-community.org/builds?repo=OCA/reporting-engine&target_branch=16.0
    :alt: Try me on Runboat

|badge1| |badge2| |badge3| |badge4| |badge5|

Add a new mixin class to define templates of comments to print on documents.
The comment templates can be defined like make templates, so you can use variables from linked models.

Two positions are available for the comments:

* above document lines (before_lines)
* below document lines (after_lines)

The template are general, and can be attached to any Model and based on some domain defined in the template.
You can define one default template per Model and domain, which can be overwritten for any company and partners.
It has a priority field (smaller number = higher priority)

In existing reports, if you add this line will get the comment template if you created one like

* <span t-raw="o.get_comment_template('position',company_id=o.company_id, partner_id=o.parnter_id )"/> ( or without any parameter)


This module is the base module for following modules:

* sale_comment_template
* purchase_comment_template
* invoice_comment_template
* stock_picking_comment_template

**Table of contents**

.. contents::
   :local:

Configuration
=============

Go to *Settings > Technical > Reporting > Comment Templates* and start designing you comment templates.

This module is the base module for following modules:

* sale_comment_template
* purchase_comment_template
* invoice_comment_template
* stock_picking_comment_template

Usage
=====

#. Go to *Settings* and activate the developer mode.
#. Go to *Settings > Technical > Reporting > Comment Templates*.
#. Create a new record.
#. Define the Company the template is linked or leave default for all companies.
#. Define the Partner the template is linked or leave default for all partners.
#. Define the Model, Domain the template is linked.
#. Define the Position where the template will be printed:

   * above document lines
   * below document lines

You should have at least one template with Default field set, if you choose a Partner the template is deselected as a Default one.
If you create a new template with the same configuration (Model, Domain, Position) and set it as Default, the previous one will be deselected as a default one.

The template is a html field which will be rendered just like a mail template, so you can use variables like {{object}}, {{user}}, {{ctx}} to add dynamic content.

Change the report related to the model from configuration and add a statement like:

<t t-foreach="o.comment_template_ids.filtered(lambda x: x.position == 'before_lines')" t-as="comment_template_top">
  <div t-raw="o.render_comment(comment_template_top)" />

</t>


<t t-foreach="o.comment_template_ids.filtered(lambda x: x.position == 'after_lines')" t-as="comment_template_bottom">
    <div t-raw="o.render_comment(comment_template_bottom)" />

</t>

You should always use t-if since the method returns False if no template is found.

If you want to use Qweb templates, or different context, you can specify it just like in
mail.render.mixin with parameters:

- engine: "inline_template", "qweb" or "qweb_view",
- add_context: dict with your own context,
- post_process: perform a post processing on rendered result

so you could use it :

<t t-foreach="o.comment_template_ids.filtered(lambda x: x.position == 'before_lines')" t-as="comment_template_top">
    <div t-raw="o.render_comment(comment_template_top, engine='qweb', add_context={my dict}, postprocess=True)" />

</t>

Bug Tracker
===========

Bugs are tracked on `GitHub Issues <https://github.com/OCA/reporting-engine/issues>`_.
In case of trouble, please check there if your issue has already been reported.
If you spotted it first, help us to smash it by providing a detailed and welcomed
`feedback <https://github.com/OCA/reporting-engine/issues/new?body=module:%20base_comment_template%0Aversion:%2016.0%0A%0A**Steps%20to%20reproduce**%0A-%20...%0A%0A**Current%20behavior**%0A%0A**Expected%20behavior**>`_.

Do not contact contributors directly about support or help with technical issues.

Credits
=======

Authors
~~~~~~~

* Camptocamp

Contributors
~~~~~~~~~~~~

* Xavier Jimenez <xavier.jimenez@qubiq.es>
* Nicolas Bessi <nicolas.bessi@camptocamp.com>
* Yannick Vaucher <yannick.vaucher@camptocamp.com>
* Guewen Baconnier <guewen.baconnier@camptocamp.com>
* Simone Rubino <simone.rubino@agilebg.com>
* `DynApps <https://www.dynapps.be>`_:

  * Raf Ven <raf.ven@dynapps.be>

* `Druidoo <https://www.druidoo.io>`_:

  * Iván Todorovich <ivan.todorovich@druidoo.io>
* Pierre Verkest <pierreverkest84@gmail.com>

* `NextERP Romania <https://www.nexterp.ro>`_:

  * Fekete Mihai <feketemihai@nexterp.ro>

* `Tecnativa <https://www.tecnativa.com>`_:

  * Carlos Roca
  * Víctor Martínez

* `Jarsa <https://www.jarsa.com>`_:

  * Alan Ramos <alan.ramos@jarsa.com>

* `Bloopark systems <https://www.bloopark.de/>`_:

  * Achraf Mhadhbi <machraf@bloopark.de>

Maintainers
~~~~~~~~~~~

This module is maintained by the OCA.

.. image:: https://odoo-community.org/logo.png
   :alt: Odoo Community Association
   :target: https://odoo-community.org

OCA, or the Odoo Community Association, is a nonprofit organization whose
mission is to support the collaborative development of Odoo features and
promote its widespread use.

This module is part of the `OCA/reporting-engine <https://github.com/OCA/reporting-engine/tree/16.0/base_comment_template>`_ project on GitHub.

You are welcome to contribute. To learn how please visit https://odoo-community.org/page/Contribute.
