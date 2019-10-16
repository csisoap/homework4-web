var data; 
var parent;
var tr2;
var isCreated = false; //Dùng để đánh dấu nếu đã tạo hoặc chưa tạo thông tin chi tiết về môn học
var isActive = false; // Dùng để đánh dấu nếu nếu đã load hoặc chưa load dữ liệu cho một trang nào đó.
var tbody;
var totalButton;
var tempNum = 1;
var p;
var pagination = document.querySelector(".pagination");
var currentButton;
var next, prev;

function getData() {
    const COURSE_URL = "https://demo6370041.mockable.io/getcourses";
    var promise = fetch(COURSE_URL);

    promise
        .then(function(message) {
            var processedMessage = message.json();
            return processedMessage;
        })
        .then(function(processedMessage) {
            data = processedMessage.data;
            loadPage(1);
            isActive = true;
			createButton(data);
			currentButton = pagination.childNodes[3];
			// console.log(currentButton.nextSibling.childNodes[0].childNodes[0].data);
			currentButton.classList.add("active");
			next = pagination.childNodes[totalButton + 3];
			prev = pagination.childNodes[2];
			prev.classList.add("disabled");
        });
}

function loadPage(page) {
    var table = document.querySelector("table");
    tbody = document.createElement("tbody");
	var count = 0;
    for(let i = 4 * page - 4; i < 4 * page; i++) {     
		if(data[i] !== undefined) {
			var tr = document.createElement("tr");
			var td1 = document.createElement("td");
			var td1word = document.createTextNode(data[i].id);
			td1.appendChild(td1word);
			tr.appendChild(td1);

			var td2 = document.createElement("td");
			var td2word = document.createTextNode(data[i].name);
			td2.appendChild(td2word);
			tr.appendChild(td2);
			tr.addEventListener("click", function(event) {			
				var data2 = event.target.childNodes[0].data;
				parent = event.target.parentNode;
				// console.log(parent);
				var id;
				id = checkData(data2);
				getDetail(id);
						
			});
			tbody.appendChild(tr);
			count++;
		}
	}
	
	p = document.createElement("p");
	var pword = document.createTextNode(`Showing ${4 * page - 3} to ${4 * page} of ${data.length} entries.`);
	if(4 * page > data.length) {
		pword = document.createTextNode(`Showing ${4 * page - 3} to ${4 * page + (count - 4)} of ${data.length} entries.`);
	}
	p.appendChild(pword);
	p.classList.add("flex-grow-1");
	pagination.appendChild(p);
   
    table.appendChild(tbody);
	
}


function createButton(data) {
    var total = data.length;
    totalButton = parseInt(total / 4);
	if(totalButton * 4 < total) {
		totalButton++;
	}
    for(let i = 0; i < totalButton + 2; i++) {
        var li = document.createElement("li");
        li.classList.add("page-item", "order-1");
        var a = document.createElement("a");
        a.classList.add("page-link");
		a.href = "#";
		var aword;
		if(i == 0) {
			aword = document.createTextNode("Previous");
			if(totalButton == 1) {
				li.classList.add("disabled");
			}
			li.addEventListener("click", function(event) {
				// console.log(currentButton.previousSibling.childNodes[0].childNodes[0].data);
				if(currentButton.previousSibling.childNodes[0].childNodes[0].data <= totalButton) {
					if(isActive) {
						tbody.remove();
						p.remove();
						isActive = false;
						currentButton.classList.remove("active");
					}
					else if(!isActive) {
						currentButton = currentButton.previousSibling;
						if(currentButton.childNodes[0].childNodes[0].data == 1) {
							prev.classList.add("disabled");
							event.preventDefault();
						}
						next.classList.remove("disabled");
						loadPage(parseInt(currentButton.childNodes[0].childNodes[0].data));
						isActive = true;
						currentButton.classList.add("active");
					}
					
				}
			});
		} else if(i == totalButton + 1) {
			aword = document.createTextNode("Next");
			if(totalButton == 1) {
				li.classList.add("disabled");
			}
			li.addEventListener("click", function(event) {
				// console.log(currentButton.nextSibling.childNodes[0].childNodes[0].data);
				if(currentButton.nextSibling.childNodes[0].childNodes[0].data <= totalButton) {
					
					if(isActive) {
						tbody.remove();
						p.remove();
						isActive = false;
						currentButton.classList.remove("active");
					}
					else if(!isActive) {
						currentButton = currentButton.nextSibling;
						if(currentButton.childNodes[0].childNodes[0].data == totalButton) {
							next.classList.add("disabled");
							event.preventDefault();
						}
						prev.classList.remove("disabled");
						loadPage(parseInt(currentButton.childNodes[0].childNodes[0].data));
						isActive = true;
						currentButton.classList.add("active");
					}
					
				}
			});
		} else {
			aword = document.createTextNode(i);
			li.addEventListener("click", function(event) {
				if(isActive) {
					tbody.remove();
					p.remove();
					isActive = false;
					currentButton.classList.remove("active");
				}
				else if(!isActive) {
					loadPage(i);
					isActive = true;
					// console.log(event.target);
					currentButton = event.target.parentNode;
					if(currentButton.childNodes[0].childNodes[0].data < totalButton) {
						next.classList.remove("disabled");
					}
					if(currentButton.childNodes[0].childNodes[0].data > 1) {
						prev.classList.remove("disabled")
					} 
					if(currentButton.childNodes[0].childNodes[0].data >= totalButton) {
						next.classList.add("disabled");
					}
					if(currentButton.childNodes[0].childNodes[0].data <= 1) {
						prev.classList.add("disabled");
					}
					currentButton.classList.add("active");
				}
			});
		}
        a.appendChild(aword);
        li.appendChild(a);
        pagination.appendChild(li);
    }
}

function checkData(course) {
    var id;
    for(let i = 0; i < data.length; i++) {
        if(data[i].name == course) {
            id = data[i].id;
        } else if(data[i].id == course) {
            id = data[i].id;
        }
    }
    return id;
}

function getDetail(id) {
    const DETAIL_URL = `https://demo6370041.mockable.io/course/${id}`;
    var promise = fetch(DETAIL_URL);
    promise
        .then(function(message) {
            var processedMessage = message.json();
            return processedMessage;
        })
        .then(function(processedMessage) {
            var data3 = processedMessage;
            if(isCreated) {
                tr2.remove();
                isCreated = false;
            }
            else {
                tr2 = document.createElement("tr");
                var td = document.createElement("td");
                td.colSpan = "2";
                var description = document.createElement("p");
                var descriptionwords = document.createTextNode(`Sơ lược: ${data3.description}`);
                description.appendChild(descriptionwords);
                td.appendChild(description);

                var textbook = document.createElement("p");
                var textbookwords = document.createTextNode(`Sách tham khảo: ${data3.textbook}`);
                textbook.appendChild(textbookwords);
                td.appendChild(textbook);
                tr2.appendChild(td);

                insertAfter(tr2, parent);
                isCreated = true;
            }
        });
        
}

function insertAfter(newNode, referenceNode) {
    referenceNode.parentNode.insertBefore(newNode, referenceNode.nextSibling);
}
getData();