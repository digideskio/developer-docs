Publisher Web Integration
=========================

**Please Note:** ﻿This documentation references invoca.net in the Web Integration examples below. However, previous installations referencing ringrevenue.com are still valid.

With the publisher web integration code in place, you can dynamically display multiple promo numbers belonging to different campaigns or even different publishers (e.g., sub affiliates). You are also able to specify which promo number(s) to display. Any new numbers can be assigned and displayed on the fly. It's also easy to track SEM performance. With the RingPool feature enabled, set up search campaigns to redirect to your landing page and search promo numbers are automatically displayed on the landing page. You can then view reports that show the calls to a search promo number along with the search engine and the keywords that drove the call.

The following article assumes the web traffic is going to the publisher's landing page and provides instructions on how the publisher can integrate the landing page.


Installation instructions from a Publisher account
--------------------------------------------------

1. Access the Publisher Web Integration Code from the Campaign's Summary tab.

   .. raw:: html

    <p><img src="https://i.embed.ly/1/image?url=http%3A%2F%2Fi40.photobucket.com%2Falbums%2Fe238%2Fnasteele%2FInvoca%2520screenshots%2Fpwic_1_zpsa51b8372.png&key=afea23f29e5a4f63bd166897e3dc72df"></p>

2. Under the Landing Pages and Applications section, click Get Code.

   .. raw:: html

    <p><img src="https://i.embed.ly/1/image?url=http%3A%2F%2Fi40.photobucket.com%2Falbums%2Fe238%2Fnasteele%2FInvoca%2520screenshots%2Fpwic_3_zpsf41ebb00.png&key=afea23f29e5a4f63bd166897e3dc72df"></p>

   Note the ppc_id of your campaign. The ppc_id uniquely identifies the campaign and references the Publisher ID and Advertiser Campaign ID.

   .. raw:: html

    <p><img src="https://i.embed.ly/1/image?url=http%3A%2F%2Fi40.photobucket.com%2Falbums%2Fe238%2Fnasteele%2FInvoca%2520screenshots%2Fpwic_4_zpsf18521d6.png&key=afea23f29e5a4f63bd166897e3dc72df"></p>

   In the example above, the Publisher ID = 170981 and the Advertiser Campaign ID = 50979.

3. Place the publisher web integration code on the campaign landing page by inserting it in the footer just above the </body> tag. This step only has to be done once. See examples below.

4. Flag each HTML element on your page where a number should be inserted. Each instance of this code signals to our code that a promo number should be displayed there. Wrap an HTML element (e.g. a <span> tag) around each number with the following two classes, ppc_integration and ppc_id_xxx_yyy (where xxx = Publisher ID and yyy = Advertiser Campaign ID).

   Inside the container, create a <span> with a CSS class ppc_number, which contains the promo number.

   Example:

   .. code-block:: html

    <span class="ppc_integration ppc_id_xxx_yyy">

          <span class="ppc_number"> YOUR NUMBER </span>

    </span>


   (where xxx = Publisher ID, and yyy =Advertiser Campaign ID)

   (Optional) You can add the class ppc_link which replaces the link with an Invoca enabled link to redirect to the advertiser landing page and display your promo number if the advertiser is web integrated.

   Example:

   .. code-block:: html

    <span class="ppc_integration ppc_id_x_y">

      <a href="http://yourlink.com" class="ppc_link">

        <span class="ppc_number"> YOUR NUMBER </span>

      </a>

    </span>


Mobile phone experience
-----------------------

By default, when your page is visited on a mobile phone browser, your promo numbers are wrapped in a tel link so that when clicked they launch the phone's dialer to place a call.  If you want to launch the dialer and also redirect in the background to the advertiser's landing page, see example 4 below.  If you just want to go to the advertiser's landing page on the click and not launch the dialer, see example 3 below.

To disable the default experience for mobile phones, add a ppc_no_tel class to your DOM element that specified the ppc_number.

Example:

.. code-block:: html

  <span class="ppc_integration ppc_id_xxx_yyy">

    <span class="ppc_number ppc_no_tel"> YOUR NUMBER </span>

  </span>

Example 1: Dynamically Displaying One Promo Number
--------------------------------------------------

This example maps a single number on to a landing page. The ppc_id_xxx_yyy is unique for each campaign and is found on the Campaign's Summary tab.

.. code-block:: html
  :emphasize-lines: 12-14

  <html>
    <head>
      <title>Publisher Landing Page</title>
    </head>

    <body>
     <br><br><br>
     <center>
      <table border=1>
        <tr><td>
          Call Campaign A:
          <span class="ppc_integration ppc_id_xxx_yyy">
             <span class="ppc_number"> 1-800-555-1234 </span>
          </span>
        </td></tr>
      </table>
      <br><br><br>

      <div class="content">
          Here is the content of your website.
      </div>

      </center>
      <!-- Omit http from path to ensure protocol is same as current request -->
      <script src="//js0.invoca.net/0/publisher_integration.js"></script>
      <script>
           Invoca.affiliate_integration( );
      </script>
    </body>
  </html>

.. raw:: html

  <p>You will notice that the number on the webpage is not the same as the highlighted number <span class="hll" style="display: inline; color: black; margin: 0; padding: 0 6px;">1-800-555-1234</span> in the source code. To display the same promo number multiple times on the page, copy and paste the <span class="hll" style="display: inline; color: black; margin: 0; padding: 0 6px;">highlighted code</span> to different areas of the source code.</p>


Example 2: Link to Advertiser Landing Page
------------------------------------------

To insert a tracking link, simply include the additional line of code to example 1:

`:<a href="http://example.com" class="ppc_link">link text here</a>`

With the ppc_link class, the web integration code uses an Invoca link if one is available. Otherwise, it will link to "http://example.com" (a fallback page, perhaps of generic offers, is recommended). The Invoca link takes the user to the advertiser landing page and displays your promo number there. If the class ppc_link is not present, the link always goes to "http://example.com".  The tag must be nested under the ppc_integration DOM element.

﻿The ppc_id_xxx_yyy is unique for each campaign and is found on the Campaign's Summary tab.

.. code-block:: html

  <html>
    <head>
      <title>Publisher Landing Page</title>
    </head>

    <body>
     <br><br><br>
     <center>
      <table border=1>
        <tr><td>
          Campaign A:
          <span class="ppc_integration ppc_id_xxx_yyy">
             <a href="http://example.com" class="ppc_link">Click here</a>
             or Call: <span class="ppc_number">1-800-555-1234</span>
          </span>
        </td></tr>
      </table>
      <br><br><br>

      <div class="content">
          Here is the content of your website.
      </div>

      </center>
      <!-- Omit http from path to ensure protocol is same as current request -->
      <script src="//js0.invoca.net/4/publisher_integration.js"></script>
      <script>
           Invoca.affiliate_integration( );
      </script>
    </body>
  </html>


Example 3: Link a Promo Number to advertiser landing page
---------------------------------------------------------

Building on Example 2, you can nest the ppc_number tag inside the ppc_link tag to make the phone number link to the landing page.  Note: if you want this behavior, you need to disable the default behavior of adding tel links to numbers.

The ppc_id_xxx_yyy is unique for each campaign and is found on the Campaign's Summary tab.

.. code-block:: html

  <html>
    <head>
      <title>Publisher Landing Page</title>
    </head>

    <body>
     <br><br><br>
     <center>
      <table border=1>
        <tr><td>
          Call Campaign A:
          <span class="ppc_integration ppc_id_xxx_yyy">
             <a href="http://example.com" class="ppc_link">
               <span class="ppc_number ppc_no_tel"> 1-800-555-1234 </span>
             </a>
          </span>
        </td></tr>
      </table>
      <br><br><br>

      <div class="content">
          Here is the content of your website.
      </div>

      </center>
      <!-- Omit http from path to ensure protocol is same as current request -->
      <script src="//js0.invoca.net/4/publisher_integration.js"></script>
      <script>
           Invoca.affiliate_integration( );
      </script>
    </body>
  </html>


Example 4: Adding an image to your link
---------------------------------------

﻿This example will allow you to link an image of your choice to an advertiser's landing page.

The ppc_id_xxx_yyy is unique for each campaign and is found on the Campaign's Summary tab.

.. code-block:: html

  <span class="ppc_integration ppc_id_xxx_yyy">

  <a href="http://example.com" class="ppc_link">
       <img src=”http://example.com/example-image.jpg”>
            <span class="ppc_number">xxx-xxx-xxxxx</span>
  </a>

  </span><!-- Omit http from path to ensure protocol is same as current request -->
  <script src="//js15.invoca.net/15/publisher_integration.js"></script>
  <script>
            Invoca.affiliate_integration( );
  </script>


Example 5: Request a Mobile Click-to-Call Link
----------------------------------------------

You can enable links on smartphones to launch the dialer and also redirect to the advertiser landing page in the background.  Enabling this does not alter the user experience on a conventional desktop or tablet computer. You can put this behavior on the number or just a standard text link.

Note: By default, numbers shown as tel links to mobile browsers, meaning they are already enabled for click-to-call, so this feature is only needed for the following actions:

1. Launch the dialer and send the user to the landing page in the background

2. Launch the dialer on a text link, rather than on the number itself:

For example:

`<a href="http://example.com" class="ppc_link ppc_mobile">For great deals, click here to call us now!</a>`


To make this change, add the ppc_mobile class next to the ppc_link class.

﻿﻿The ppc_id_xxx_yyy is unique for each campaign and is found on the Campaign's Summary tab.

.. code-block:: html

  <html>
    <head>
      <title>Publisher Landing Page</title>
    </head>

    <body>
     <br><br><br>
     <center>
      <table border=1>
        <tr><td>
          Call Campaign A:
          <span class="ppc_integration ppc_id_29012_6268">
             <a href="http://example.com" class="ppc_link ppc_mobile">
               <span class="ppc_number ppc_no_tel"> 1-800-555-1234 </span>
             </a>
          </span>
        </td></tr>
      </table>
      <br><br><br>

      <div class="content">
          Here is the content of your website.
      </div>

      </center>
      <!-- Omit http from path to ensure protocol is same as current request -->
      <script src="//js0.invoca.net/4/publisher_integration.js"></script>
      <script>
           Invoca.affiliate_integration( );
      </script>
    </body>
  </html>


Example 6: Display Multiple Promo Numbers
-----------------------------------------

This example shows how to dynamically display promo numbers for multiple campaigns on the same landing page. The different numbers do not have to belong to the same publisher which means users with multiple publisher accounts could use the same landing page for campaigns across different networks.

﻿The ppc_id_xxx_yyy is unique for each campaign and is found on the Campaign's Summary tab.

.. code-block:: html

  <html>
    <head>
      <title>Publisher Landing Page</title>
    </head>

    <body>
     <br><br><br>
     <center>
      <table width=600 border=1>
        <tr><td><br>
          Call Campaign A:
          <span class="ppc_integration ppc_id_xx1_yy1">
             <span class="ppc_number"> xxx-xxx-xxxx </span>
          </span><br>
        </td>

        <td><br>
          Call Campaign B:
          <span class="ppc_integration ppc_id_xx2_yy2">
           <span class="ppc_number"> XXX-XXX-XXXX </span>
          </span><br>
        </td></tr>
      </table>
      <br><br><br>

      <div class="content">
          Here is the content of your website.
      </div>

      </center>
      <!-- Omit http from path to ensure protocol is same as current request -->
      <script src="//js0.invoca.net/4/publisher_integration.js"></script>
      <script>
           Invoca.affiliate_integration( );
      </script>
    </body>
  </html>

The image below is a screenshot of the webpage produced by HTML source code from this example. Notice that the promo number for campaign B is not displayed. This can be caused by a variety of reasons:

1. The ppc_id_xxx_yyy is incorrect.

2. The publisher is not approved to the campaign.

3. The campaign is no longer active.


Example 7: Dynamically Displaying Tel: link
-------------------------------------------

This example demonstrates what an entire webpage could look like, so please note that you may already have jQuery embedded elsewhere on your site.

The example uses jQuery to automatically replace all occurrences of class = ppc_number with a tel: link.
With minor modifications this example can be used to take advantage of jQuery buttons.

The ppc_id_xxx_yyy is unique for each campaign and is found on the Campaign's Summary tab

.. code-block:: html

  <html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
  <head>
  <title>Tel Link</title>
  <style type="text/css"> body { font-family: sans-serif; background: white; }</style>
    <script src="http://code.jquery.com/jquery-1.8.2.min.js"> </script>
    <script>
      function ppcTelLink() {
        $(".ppc_number").each( function(){
          $(this).html("<a href='tel:"+ $(this).html() + "'>" +  $(this).html());
        } );
      }
      setTimeout(ppcTelLink,1000);
    </script>
  </head>

  <body>
    <span class="ppc_integration ppc_id_xxx_yyy_9133">
      <span class="ppc_number"> 888-888-8888 </span>
    </span>
    <script src="//js0.invoca.net/4/publisher_integration.js"></script>
    <script>
      Invoca.affiliate_integration(  );
    </script>
  </body>
  </html>
