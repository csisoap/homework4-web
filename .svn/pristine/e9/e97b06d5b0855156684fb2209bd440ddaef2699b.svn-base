

function validation(event) {
    var emailVal = document.querySelector("#emailtext").value;
    var textVal = document.querySelector(".text").value;
    var error, error2, error3;
    if(emailVal.length == 0) {
        error = "Please enter your email";
        document.querySelector(".emailmessenge").innerHTML = error;
        event.preventDefault();
    }
	else if(textVal.length == 0) {
		error2 = "Please enter your message";
        document.querySelector(".textarea-messenge").innerHTML = error2;
        event.preventDefault();
	}
    else if (textVal.length > 128) {
        error3 = "Your message is too long";
        document.querySelector(".textarea-messenge").innerHTML = error3;
        event.preventDefault();
    }

}

