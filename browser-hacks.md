### show warning before leaving page.
for some reason, when debugging an app, chrome will break on every xhr request except for the last one. so this can be usefull if I want to see everthing that happened before a locaton change 

`jQuery(window).bind('beforeunload', function(){
    return "Do you want to leave this page?";
});`

### Insert utility scripts, such as lodash
This is a deprecated API that has severe impacts on performance, but just for testing, it should be OK 
`document.write('<' + 'script src="' + script + '"' +
                   ' type="text/javascript"><' + '/script>');`

### add box border to every element

    [].forEach.call(document.querySelectorAll("*"),function(a){a.style.outline="1px solid #"+(~~(Math.random()*(1<<24))).toString(16)})
