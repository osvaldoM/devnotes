### show ewarning before leaving page.
for some reason, when debugging an app, chrome will break on every xhr request except for the last one. so this can be usefull if I want to see everthing that happened before a locaton change 

`$(window).bind('beforeunload', function(){
    return "Do you want to leave this page?";
});`
