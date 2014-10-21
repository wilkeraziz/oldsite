#Server-side redirect

Add a file named `.htaccess` with the following instruction


    Redirect /people/W.Aziz/ http://wilkeraziz.github.io/dcs-site/index.html


Or the following, to make it case insensitive


    RedirectMatch permanent (?i)/people/W.Aziz http://wilkeraziz.github.io/dcs-site/index.html
