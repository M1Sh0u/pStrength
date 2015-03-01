pStrength
=========
We have developed a jQuery plugin which can help you adding a password strength feature to your own accounts forms.

Visit the pStrength official page for an working demo @ https://accountspassword.com/password-strength-jquery-plugin

##Plugin defaults##

```
$('#myElement').pStrength({
    'bind': 'keyup change',
    'changeBackground': true,
    'backgrounds'     : [['#cc0000', '#FFF'], ['#cc3333', '#FFF'], ['#cc6666', '#FFF'], ['#ff9999', '#FFF'],
                        ['#e0941c', '#FFF'], ['#e8a53a', '#FFF'], ['#eab259', '#FFF'], ['#efd09e', '#FFF'],
                        ['#ccffcc', '#FFF'], ['#66cc66', '#FFF'], ['#339933', '#FFF'], ['#006600', '#FFF'], ['#105610', '#FFF']],
    'passwordValidFrom': 60, // 60%
    'onValidatePassword': function(percentage) { },
    'onPasswordStrengthChanged' : function(passwordStrength, percentage) { }
});
```

1. **bind** - When bind event is raised, password will be recalculated;
2. **changeBackground** - If true, the background of the element will be changed according with the strength of the password;
3. **backgrounds** - Password strength will get values from 0 to 12. Each color in backgrounds represents the strength color for each value;
4. **passwordValidFrom** - If you define a onValidatePassword function, this will be called only if the passwordStrength is bigger than passwordValidFrom. In that case you can use the percentage argument as you wish;
5. **onValidatePassword** - Define a function which will be called each time the password becomes valid;
6. **onPasswordStrengthChanged** - Define a function which will be called each time the password strength is recalculated. You can use passwordStrength and percentage arguments for designing your own password meter

##How to use pStrength plugin##

```
$(document).ready(function(){
    
    $('#myForm').submit(function(){
        return false;
    });

    $('#myElement1, #myElement2').pStrength({
        'changeBackground'          : false,
        'onPasswordStrengthChanged' : function(passwordStrength, strengthPercentage) {
            if ($(this).val()) {
                $.fn.pStrength('changeBackground', $(this), passwordStrength);
            } else {
                $.fn.pStrength('resetStyle', $(this));
            }
            $('#' + $(this).data('display'))
                .html('Your password strength is ' + strengthPercentage + '%');
        },
        'onValidatePassword': function(strengthPercentage) {
            $('#' + $(this).data('display')).html(
                $('#' + $(this).data('display')).html() + ' Great, now you can continue to register!'
            );

            $('#myForm').submit(function(){
                return true;
            });
        }
    });
});
```
##HTML code for the example above##
```
<form id="myForm">
    <input type="password" id="myElement1" size="40" class="left" data-display="myDisplayElement1" /> <div class="left" id="myDisplayElement1"></div>
    <div class="clear"></div>
    <input type="password" id="myElement2" size="40" class="left" data-display="myDisplayElement2" /> <div class="left" id="myDisplayElement2"></div>
</form>
```
##CSS code for the example above##
```
#myElement1, #myElement2 {
    padding:4px;
    margin:2px;
    border:solid 1px #999;
}

#myElement2 {
    background-color:#036;
}

div {
    margin-left:20px;
    margin-top:6px;
}
.left {
    float:left;
}
.clear {
    clear:both;
}
```
