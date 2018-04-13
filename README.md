
This Repo was created in order to test the drag and drop behavior of different data types from different browsers. The browsers tested are  are Chrome, Firefox, Internet Explorer and Edge.
The HTML page provides you with a draggable element(text) and a drop box element. By default the draggable element contains no items in its dataList(ev.dataTransfer.items), therefore the HTML page provides you with buttons to add data items to the data list. The data types that can be added are text/plain, text/uri-list and text/html. The values contained by these data types are unique and constant. The data types selected will be displayed
When the dragged element is dropped into the drop box, the drop box displays the data dragged. You casn attach multiple drag items at the same time. You will need to refresh the page in order to reset your changes.

=======
since different browsers have different behaviors, I have written seperate HTML for different browsers.

