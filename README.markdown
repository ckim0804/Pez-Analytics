Read more at <a href="http://www.mentalpez.com/2011/08/steal-from-us-presenting-pez-analytics/">mentalpez</a>.

We all know the old-fashioned way of <a href="http://www.google.com/support/analyticshelp/bin/answer.py?hl=en&answer=1008080&topic=1008079">setting up the Google Analytics tracking code</a>:

    <script type="text/javascript">
    	var _gaq = _gaq || [];
    	_gaq.push(['_setAccount', 'UA-XXXXX-Y']);
    	_gaq.push(['_trackPageview']);
    
    	(function() {
    		var ga = document.createElement('script'); ga.type = 'text/javascript'; ga.async = true;
    		ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js';
    		var s = document.getElementsByTagName('script')[0]; s.parentNode.insertBefore(ga, s);
    	})();
    </script>

Pez Analytics simplifies this code a wee bit:

    <head>
    	<meta name="analytics"  data-id="UA-XXXXX-Y" />
    	<script type="text/javascript" src="scripts/jquery-1.6.2.min.js"></script>
    	<script type="text/javascript" src="scripts/pez-analytics-1.0.js"></script>
    </head>

Notice that Pez Analytics is a jQuery plugin and thus requires that jQuery (1.5+) is initially loaded on the page. Notice also that we're using the fun <a href="http://html5doctor.com/html5-custom-data-attributes/">data-* attributes</a> afforded by HTML5. Still super-simple, and requires very little brainspace to set 'er up.

The real magic of this little library (~120 lines, altogether) is the ability to easily handle common page events (the kind of events that marketer-types pine over). For example, if you want to track downloads, outbound links, or user behavior on forms, it's just a matter of flipping a switch. For example:

    <head> 
        <meta name="analytics" 
            data-id="UA-XXXXX-Y" 
            data-debug="true" 
            data-trackDownloads="pdf,doc,docx" 
            data-trackOutboundLinks="true" 
            data-trackForms="true" 
            data-trackPageLoadTime="true"
        /> 
        <script type="text/javascript" src="scripts/jquery-1.6.2.min.js"></script> 
        <script type="text/javascript" src="scripts/pez-analytics-1.0.js"></script> 
    </head> 

Pez Analytics also registers the <strong>ga</strong> variable on the DOM. You can use this variable to fire off custom tracking events whenever you see fit:

    <script type="text/javascript"> 
        $(function() { 
            $('#button').click(function() { 
                ga.track({ 
                    category: 'Buttons', 
                    action: 'Clicked', 
                    label: 'Foo' 
                }); 
            }); 
        }); 
    </script> 

By setting data-debug to true, you can also keep tabs on Pez Analytics in the console. No more digging around in the __utm.gif parameters to figure out WTF just happened. Much better times.

<a href="http://www.mentalpez.com">
<img src="http://www.mentalpez.com/wp-content/uploads/2011/08/mentalpez_logo_black_box.png" alt="mentalpez" />
</a>