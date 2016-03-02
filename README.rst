cartridge-stripe
================

Stripe_ credit card processing integration with Cartridge_.

This should not be used anymore.
Instead, use the following setting to use Cartridge's built in stripe support.
SHOP_HANDLER_PAYMENT = "cartridge.shop.payment.stripe_api.process"

.. _Cartridge: htps://cartridge.jupo.org
.. _Stripe: https://stripe.com/docs

==========
Install
==========

Follow the installation instructions of django-zebra_.

.. _django-zebra: https://github.com/GoodCloud/django-zebra#installation

::

    pip install cartridge-stripe

Update the settings.py to use your shiney new app.
Add it to 'INSTALLED_APPS' above 'cartridge.shop' to override the checkout template
or copy it to the templates dir in your project.

::

    INSTALLED_APPS = (
        # ...
        'cartridge_stripe',
        'cartridge.shop',
        # More stuff...
        'zebra',
        )


    SHOP_HANDLER_PAYMENT = 'cartridge_stripe.payment_handler'

    ZEBRA_ENABLE_APP = True

Update the urls.py.  Add the following line after the other package imports at the top.
::
    # Need to pull in the stripe OrderForm.
    from cartridge_stripe.forms import OrderForm


Add the following line above the r'^shop/'.
::
    # Cartridge-stripe URLs.
    url(r'^shop/checkout/$', 'cartridge.shop.views.checkout_steps', name='checkout_steps',
       kwargs=dict(form_class=OrderForm)),

=======
Optional
=======
cartridge-stripe will by default accept payments in USD. If you need to you can change the currency stripe should accept payment in. Update settings.py with the following line. Replace 'cad' with your currency of choice.
::
    SHOP_CHARGE_CURRENCY = 'cad'

=======
Style
=======

Add some sort of style for 'div.payment-errors' which will display validation
errors from stripe.

::

    div.payment-errors {
        color: #F00;
    }


=====
Done!
=====

Now your checkout flow should have card validation and the Stripe order number
linked to the purchase.

=====
Feedback
=====

I'm open to bugs and pull requests. Just run pep8 first.
Follow me and say hi!  https://twitter.com/readevalprint
