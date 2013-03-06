pStrength
=========
We have developed a jQuery plugin which can help you adding a password strength feature to your own accounts forms.

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
    	
        $('#myElement').pStrength({
            'changeBackground'          : true,
            'onPasswordStrengthChanged' : function(passwordStrength, percentage) {
                $('#myElement').next('div').html('Your password strength is ' + percentage + '%');
            },
            'onValidatePassword': function(percentage) {
                $('#myElement').next('div').html($('#myElement').next('div').html() + ' Great, now you can continue to register!');
            	
                $('#myForm').submit(function(){
                    return true;
                });
            }
        });
});
```
