# html

<!--Only contains text/plain-->
<html>
        <head>
            <style>
                div {
                    margin: 0em;
                    padding: 1em;
                }
                #source {
                    color: blue;
                    border: 1px solid black;
                    width:fit-content;
                }
                #target {
                    border: 1px solid black;
                }
            </style>
            <script>
                var clrdata = 'noclear';
                var datatype = [];
                //var datatype = ['text/html','text/uri-list','text/plain'];
                //var datatype = ['text/html'];
                var datatype_value = '';
                uri1 = "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTtQ_NqOyPiB_Xwba8EgziR2cCpQd4zWm05qE33ns7WNynbxflY";
                uri2 = "https://www.bmwjamaica.com/content/dam/bmw/common/all-models/m-series/m4-convertible/2017/images-and-videos/images/BMW-m4-convertible-images-and-videos-1920x1200-06.jpg.asset.1487344406677.jpg";
                img_tag = '<img id="source "src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTtQ_NqOyPiB_Xwba8EgziR2cCpQd4zWm05qE33ns7WNynbxflY" ondragstart="dragstart_handler(event);" ondragend="dragend_handler(event);" draggable="true" />';
                //img_tag = '<img id= "source1" src="https://www.bmwjamaica.com/content/dam/bmw/common/all-models/m-series/m4-convertible/2017/images-and-videos/images/BMW-m4-convertible-images-and-videos-1920x1200-06.jpg.asset.1487344406677.jpg" />';
                
                function cleardata(ev){
                    clrdata = 'clear';
                }

                function setdata(type){
                    if(type == 'text/plain'){
                        if( datatype.indexOf(type) == -1){
                            datatype.push(type);
                            //console.log(datatype);
                            document.getElementById("para2").innerHTML = datatype;
                        }
                        else
                            alert (" Datatype already exists");
                        
                    }
                    else if  (type == 'text/uri-list'){
                        if( datatype.indexOf(type) == -1){
                            datatype.push(type);
                            document.getElementById("para2").innerHTML = datatype;
                        }
                        else
                            alert (" Datatype already exists");
                        
                    }
                    else if (type == 'text/html'){
                        if( datatype.indexOf(type) == -1){
                            datatype.push(type);
                            document.getElementById("para2").innerHTML = datatype;
                        }
                        else
                            alert (" Datatype already exists");
                        
                    }
                }

                function dragstart_handler(ev) {
                    console.log("dragStart");
                    
                    var dataList = ev.dataTransfer.items;
                    
                    console.log('Default dataList',dataList);
                    console.log('types to be added:',datatype.length);
                    
                    if(clrdata == 'clear'){
                        ev.dataTransfer.clearData();
                    }

                    for(var i = 0; i< datatype.length; i++){
                        if(datatype[i] == 'text/plain') 
                            datatype_value=uri1;
                        else if(datatype[i] == 'text/uri-list'){
                            datatype_value = uri2;
                        }
                        else if (datatype[i] ==  'text/html'){
                            datatype_value = img_tag;
                        }
                        else{
                            datatype_value = '';
                        }

                        dataList.add(datatype_value,datatype[i]);
                        console.log('added datatype', datatype[i], dataList);
                    }
                    
                    
                    

                    /*while (dataList.length > 1) {
                        for(var i = 0; i< dataList.length; i++){
                        //if(dataList[i].type != 'text/uri-list') {
                        if(dataList[i].type != 'image/png') {
                        //if(dataList[i].type != 'application/x-moz-nativeimage' ){
                            console.log('removing', dataList[i].type, 'at', i);
                            dataList.remove(i);
                            i=i-1;}}
                    }*/
    
                    /*for(var i = 0; i< 3; i++){
                    console.log('removing',dataList[0].kind,',',dataList[0].type);
                    dataList.remove(0);}
                    for(var i = 0; i< 2; i++){
                    console.log('removing',dataList[1].kind,',',dataList[1].type);
                    dataList.remove(1);}
                    for(var i = 0; i< 3; i++){
                    console.log('removing',dataList[4].kind,',',dataList[4].type);
                    dataList.remove(4);}*/
                    console.log("datalist after adding",ev.dataTransfer.items);
                    
                        
                    //dataList.add(ev.target.id, "text/plain");
                    //The above text/plain data type needs to be added to chrome to support drop into the web page itself, 
                    //needs to be commented in firefox as it adds it by default.
                    for (var i = 0; i < dataList.length; i++) {
                        //console.log('datakind',dataList[i].kind);
                        //console.log('datatype',dataList[i].type);
                        if((dataList[i].kind == 'string')){console.log('datakind', dataList[i].kind);
                        console.log('datatype',dataList[i].type);dataList[i].getAsString(function (s){console.log('elemt', (s))});}
                        else if((dataList[i].kind == 'file' || dataList[i].kind == 'other')){console.log('datakind',dataList[i].kind);
                        console.log('datatype',dataList[i].type);var f = dataList[i].getAsFile(); console.log('File');}
                    }
                }
    
                function drop_handler(ev) {
                    console.log("Drop");
                    console.log("default Drop data", ev.dataTransfer.items);
                    ev.preventDefault();
                    var data = ev.dataTransfer.items;
                    // Loop through the dropped items and log their data
                    for (var i = 0; i < data.length; i++) {
                        console.log('datakind',data[i].kind);
                        console.log('datatype',data[i].type);
                        
                        if ((data[i].kind == 'string') && (data[i].type.match('^text/plain'))) {
                             //This item is the target node
                            data[i].getAsString(function (s){
                            ev.target.appendChild(document.getElementById(s));
                            });
                        } 
                        if ((data[i].kind == 'string') && (data[i].type.match('^text/html'))) {
                            // Drag data item is HTML
                            data[i].getAsString(function (s){
                            console.log("... Drop: HTML = " + s);
                            });
                        } else if ((data[i].kind == 'string') && (data[i].type.match('^text/uri-list'))) {
                            // Drag data item is URI
                            data[i].getAsString(function (s){
                            console.log("... Drop: URI = " + s);
                            //ev.target.appendChild(document.getElementById(s));
                            });
                        }
                    }
                }
    
                function dragover_handler(ev) {
                    console.log("dragOver");
                    ev.preventDefault();
                    // Set the dropEffect to move
                    ev.dataTransfer.dropEffect = "move"
                }
    
                function dragend_handler(ev) {
                    console.log("dragEnd");
                    var dataList = ev.dataTransfer.items;
                    for (var i = 0; i < dataList.length; i++) {
                    dataList.remove(i);
                }
                // Clear any remaining drag data
                dataList.clear();
                }
            </script>
        </head>
        <body>
                <div>
                    <p id= "source" draggable="true" ondragstart="dragstart_handler(event)" ondragend="dragend_handler(event)">Drag data</p>
                </div>
                
                <div>
                    <p>Add Datatypes:</p>
                    <button onclick="setdata('text/plain')">text/plain : url</button>
                    <button onclick="setdata('text/uri-list')">text/uri-list : url</button>
                    <button onclick="setdata('text/html')">text/html : img tag</button>
                </div>
                <br>
                <div><p>Datatypes List: </p><p id="para2"></p></div>
                <br><br><div id="target" ondrop="drop_handler(event)" ondragover="dragover_handler(event)"></div>
        </body>
    </html>
