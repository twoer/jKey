#jKey 1.0 Beta
##The easiest way to add key shortcuts to your web app, period.

###Why
Easy. What key code is the `g` key? What about the `alt`? How do you check if `alt`, `shift`, and `a` are being pressed down at the same time?

If you don't know these off the top of your head, jKey is probably right for you.

###What
jKey is a jQuery plugin written by Oscar Godson and Sebastian Nitu. It allows you to add key shortcuts to your web app _super_ easily.

###Enough already, how?
A simple example would be, if you wanted to add a key command to your app that alerts a user when they press `alt + a` you'd just do:

    $(window).jkey('alt+a',function(){
        alert('You pressed alt+a!');
    });


It also supports multiple key commands that have the same functionality, for example:

    $(window).jkey('s, alt+s',function(){
        alert('You pressed either s, or alt+s!');
    });

It also allows you to get the keys pressed. This is useful if you have a command that fires off an event that is different, but very similar. For example, let's say you have a sliding panel that moves left or right based on the `left` or `right` key. The animation code and events fired are the same, but have an opposite direction. In this case, you could do:

    $(window).jkey('left, right',function(key){
        if(key == 'left') {
            direction = 'left';
        }
        else {
            direction = 'right';
        }
        alert(direction);
    });


###Key Support
jKey doesn't support every possible key as every computer manufacturer and operating system implements keys differently. For example, some computers have a function key (`Fn`) and some of them return a keycode and some don't at all. In any case, here is what we currently support:

- a-z
- 0-9
- F1-F12
- left, up, down, right
- shift, ctrl, control, alt, backspace, enter
- Mac OS X: opt, option, cmd, command, delete _[1]_, return _[2]_
- Not on all OSs: fn, function

If we're missing something, let us know in the bug reporter on our Github page.

_[1]_ - This is the Mac version of the `backspace` button. Calling either should work across OSs. Yes, there is a `delete` key on normal western keyboards as well, we're still trying to figure out how to handle this...

_[2]_ - This is the Mac version of the `enter` key. Calling either should work across OSs.

_[3]_ - This will NOT work in Mac OS X. It does not send a key event to the browser. Silly Apple.

####Note about selectors
You don't have to always select the `window`. If you want to set a key command to an element it's just gotta be in `focus`. So, you could do something such as:

$('input').jkey('^',function(){
   alert('not a valid character!');
});