### show warning before leaving page.
for some reason, chrome will break on an xhr request if it's followed by a location change. so this can be usefull if I want to see everthing that happened before a locaton change 

`jQuery(window).bind('beforeunload', function(){
    return "Do you want to leave this page?";
});`

### Insert utility scripts, such as lodash
This is a deprecated API that has severe impacts on performance, but just for testing, it should be OK 
`document.write('<' + 'script src="' + script + '"' +
                   ' type="text/javascript"><' + '/script>');`

### add box border to every element

    [].forEach.call(document.querySelectorAll("*"),function(a){a.style.outline="1px solid #"+(~~(Math.random()*(1<<24))).toString(16)})

### start chrome in insecure mode
Many Web APIs(eg. bluetooth, serviceWorker, userMedia) and features are accessible only in a secure context. A context will be considered secure when it's delivered securely(via HTTPS/TLS) or locally(localhost is the only whitelisted domain).

This is very useful if you are using local .test / .dev, etc domains.

        google-chrome --user-data-dir=~/Documents/chrometemp --unsafely-treat-insecure-origin-as-secure=http://www.doomain.test:80 

Although, a warning similar to
 > google-chrome --unsafely-treat-insecure-origin-as-secure command line flag not working
 
might be shown, it still works.

 - [https://stackoverflow.com/questions/34160509/options-for-testing-service-workers-via-http](https://stackoverflow.com/questions/34160509/options-for-testing-service-workers-via-http)
