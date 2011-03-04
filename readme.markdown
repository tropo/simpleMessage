Simple Message
==============

This is a prepackaged application for Tropo that allows you 
to send text messages simply by requesting a URL. You can also
get replies or other incoming messages sent as form posts to
a URL of your choosing.

If you want to read more about why Simple Message exists, how to 
use it, and see a screencast on how to install it, check out 
[*Simple POST and GET interface to Tropo SMS* on the Tropo blog](http://blog.tropo.com/2010/11/19/simple-post-and-get-interface-to-tropo-sms/).

Adding a Tropo application
--------------------------

After you create or log into your Tropo account, click 
**Create New Application** and choose **Tropo Scripting**.  

For the URL, either upload this code to your web server as 
*simpleMessage.tphp* (note the "t" in the extension) and then
give Tropo the URL to that file, or if you'd like to host the file
on Tropo's server, choose **Hosted File**  and then **Create a 
new hosted file...** and then copy and paste the contents of 
simpleMessage.php into the text box. 

Add a US phone number and make note of your messaging token.

Sending
--------

Load the URL http://api.tropo.com/1.0/sessions with a GET request,
adding the following query string variables 

 * action - set this to "create"
 * token - Your secret messaging token from Tropo
 * to - the phone number (including country code) to send to
 * msg - the message to send
 * network - (optional) the network to send to. Defaults to SMS
 * from - (optional) if you have multiple Tropo numbers, which one to send 
from. **Note** this must be a Tropo number. Carriers reject spoofed SMS messages.

Since this is a URL, all values should be URL encoded. 

** Example **

I want to send "I feel pretty" by SMS 1 (212) 555-1212. My token 
is 1234 (real tokens are much longer). To do this, I'd request 
this url:

http://api.tropo.com/1.0/sessions?action=create&token=1234&to=12125551212&msg=I+feel+pretty

Receiving
----------

Tropo will make a form post to any URL you'd like, using the
following fields:

 * to - the phone number (or IM address) the message was sent to
 * from - the sender's number or IM address
 * msg - the message they sent

You simply need to find the line in simpleMessage.php that says...

  $url = 'http://example.com'; // Tropo will POST incoming messages here
  
... and change http://example.com to the URL you want Tropo to post 
to. You can also add a username and password if your server requires
authentication to access your URL.